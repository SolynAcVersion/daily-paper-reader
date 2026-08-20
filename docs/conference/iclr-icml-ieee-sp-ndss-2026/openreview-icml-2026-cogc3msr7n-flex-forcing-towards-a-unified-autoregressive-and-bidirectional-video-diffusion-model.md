---
title: "Flex-Forcing: Towards a Unified Autoregressive and Bidirectional Video Diffusion Model"
title_zh: Flex-Forcing：迈向自回归与双向视频扩散模型的统一
authors: "Xinyin Ma, Julius Berner, Chao Liu, Arash Vahdat, Weili Nie, Xinchao Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/fb09bc662aa5fe48966115b38afe6de5901f4cc7.pdf"
tags: ["query:phys-video"]
score: 4.0
evidence: 统一双向与自回归视频扩散框架，改善全局一致性与长程一致性
tldr: 现有视频扩散模型在双向生成时全局一致性好但推理慢，而自回归模型生成高效却长程一致性有限。Flex-Forcing通过统一的训练与推理框架，在时间轴与去噪步骤上联合定义灵活的分块机制，使模型能够同时支持双向与自回归生成。该方法在保持全局连贯性的同时提升推理效率并缓解曝光偏差。尽管未显式强调物理规律，但其长程一致性改进对跨帧物理一致性具有潜在帮助。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 双向扩散模型与自回归视频生成各有优缺点，现有推理范式僵硬，难以兼顾效率与一致性。
method: 提出Flex-Forcing框架，在时间轴与去噪步上联合定义灵活分块，统一双向与自回归视频扩散。
result: 模型可无缝切换两种生成模式，在全局连贯性与推理效率之间取得更好平衡，并改善长程一致性。
conclusion: 该架构为视频生成提供统一范式，对实现跨帧物理一致性有一定启发，但并非专门针对物理约束。
---

## Abstract
Recent progress in large-scale generative models has substantially advanced video generation, yet existing methods remain constrained by a rigid inference paradigm. Bidirectional diffusion models excel at global coherence and visual fidelity but suffer from slow inference, while autoregressive models offer efficient and streaming generation at the cost of long-range consistency and exposure bias. We introduce Flex-Forcing, a unified training and inference framework that enables a video diffusion model to seamlessly operate under both bidirectional and autoregressive generation regimes. The core idea is a flexible chunking mechanism jointly defined over the temporal axis and denoising steps. This design allows the model to (1) perform flexible chunking according to different device budgets, (2) perform bidirectional inference across chunks for global structure planning, while generating frames autoregressively within each chunk for efficient and fine-grained synthesis, and (3) perform any-order, any-timestep autoregressive generation without the strict causal constraint. Extensive experiments on multiple video generation benchmarks demonstrate that Flex-Forcing achieves consistently better video quality, long-video stability than strong baselines with a rigid inference schedule, while offering faster inference.

---

## 论文详细总结（自动生成）

# Flex-Forcing：迈向自回归与双向视频扩散模型的统一（中文总结）

## 1. 论文的核心问题与整体含义

- **研究动机**：大规模生成模型推动了视频生成的显著进展，然而现有方法受限于**僵化的推理范式**，难以在效率与质量之间取得平衡。
- **双向扩散模型的困境**：擅长全局连贯性与视觉保真度，但推理速度慢，难以满足实时或流式生成需求。
- **自回归模型的困境**：生成高效、支持流式输出，但存在**长程一致性不足**与**曝光偏差**（exposure bias）问题。
- **核心研究问题**：如何设计一个统一的训练与推理框架，使视频扩散模型能够**无缝切换**双向与自回归两种生成模式，兼顾全局结构规划与高效细粒度合成。
- **整体含义**：该工作试图打破当前视频生成中"全局质量"与"推理效率"不可兼得的僵局，为视频生成提供一种更灵活、更统一的范式基础。

## 2. 论文提出的方法论

- **核心思想**：提出 **Flex-Forcing**，一种统一的训练与推理框架，核心是**在时间轴与去噪步骤上联合定义灵活的分块机制（flexible chunking）**。
- **分块机制的三个关键能力**：
  1. **设备自适应**：可根据不同设备的计算预算灵活调整分块大小，适应从边缘设备到高性能集群的部署需求。
  2. **跨块双向、块内自回归**：在块与块之间执行**双向推理**，用于全局结构规划；在每个块内部执行**自回归生成**，实现高效且细粒度的合成。
  3. **任意顺序、任意时间步自回归**：突破严格因果约束，支持任意顺序、任意去噪时间步的自回归生成，增强模型的灵活性与泛化能力。
- **算法流程（文字描述）**：
  1. 将视频序列在时间维度划分为多个块，同时在去噪过程中将扩散步划分为多个阶段。
  2. 训练时，模型学习在不同分块配置下同时完成双向与自回归生成任务。
  3. 推理时，根据设备预算选择合适的分块策略——先跨块双向规划全局结构，再在块内逐步自回归生成细节。
- **与传统方法的本质区别**：传统方法在生成模式上是二选一（要么纯双向、要么纯自回归），Flex-Forcing 则将其统一在同一模型框架内，消除了推理范式的人为割裂。

## 3. 实验设计

- **数据集 / 场景**：论文在**多个视频生成基准**上进行实验，但提供的材料中**未明确列出具体数据集名称**（如 UCF-101、Kinetics 等），仅以"multiple video generation benchmarks"概括。
- **Benchmark**：标准视频生成基准，评估指标涵盖**视频质量、长视频稳定性、推理速度**。
- **对比方法**：与具有**刚性推理调度**（rigid inference schedule）的强基线方法进行对比，具体基线名称未在提供材料中列出。
- **实验重点**：验证 Flex-Forcing 在视频质量、长视频稳定性上的持续优势，以及在推理速度上的提升。

## 4. 资源与算力

- **未明确说明**：论文提供的材料中**没有**提及使用的 GPU 型号、数量、训练时长等算力信息。
- **无法评估训练成本**：因此无法判断该方法的训练开销与可复现性门槛，这是一个信息缺口。

## 5. 实验数量与充分性

- **实验数量**：从摘要来看，实验覆盖了**多个基准**，但具体实验组数、消融实验的详细设置无法从当前材料中获知。
- **充分性评估**：
  - **优点**：跨多基准的验证为方法的普适性提供了一定支撑。
  - **不足**：缺少消融实验的细节描述（如分块大小的影响、双向/自回归比例的影响、不同设备预算下的表现等），也缺少与更多最新方法的全面对比，使得实验**充分性难以完全判定**。
- **客观性与公平性**：材料中虽声称"consistently better"，但未给出误差棒、统计显著性检验等细节，**公平性需依赖完整论文的实验部分进一步核实**。

## 6. 论文的主要结论与发现

- **统一范式可行**：Flex-Forcing 成功让同一视频扩散模型在双向与自回归两种生成模式间无缝切换，验证了统一框架的可行性。
- **质量与稳定性提升**：在多个视频生成基准上，Flex-Forcing 相较刚性推理调度的强基线，**持续获得更好的视频质量与长视频稳定性**。
- **推理加速**：在保持或提升质量的同时，实现了**更快的推理速度**，有效缓解了双向扩散慢推理的瓶颈。
- **曝光偏差缓解**：灵活的任意顺序、任意时间步的自回归生成机制有助于缓解传统自回归模型中的曝光偏差问题。

## 7. 优点

- **范式创新性强**：首次在统一框架内同时支持双向与自回归视频扩散生成，打破了此前范式对立的局面，具有较大学术价值。
- **灵活性与适配性**：分块机制可随设备算力动态调整，兼顾了不同硬件条件下的可用性，工程实用性较强。
- **针对性解决问题**：同时瞄准双向扩散的推理慢和自回归的长程一致性差两个痛点，研究问题定义清晰、击中要害。
- **架构简洁统一**：用统一的分块机制同时解决训练和推理的灵活性问题，设计优雅而不引入复杂的辅助模块。

## 8. 不足与局限

- **实验信息不足**：提供的材料中缺少具体数据集、基线模型、实验组数等关键信息，无法从当前文本中全面评估实验的完整性与公平性。
- **算力成本未知**：未报告训练资源与算力消耗，影响方法的可复现性和实用性判断。
- **物理一致性未显式建模**：论文标签含 "phys-video"，但方法并未显式引入物理规律约束，对跨帧物理一致性的帮助仅来自长程一致性的间接改善，非专门设计。
- **评分与接受情况**：ICML 2026 接收，但评分仅 4.0 分（满分 10），暗示审稿人可能对方法的新颖性贡献或实验说服力存在一定分歧。
- **应用边界未说明**：未讨论该方法在极端长视频、高分辨率、多模态输入等更复杂场景下的表现与限制，适用边界有待进一步明确。

（完）
