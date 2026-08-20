---
title: Real-Time Motion-Controllable Autoregressive Video Diffusion
title_zh: 实时运动可控的自回归视频扩散
authors: "Kesen Zhao, Jiaxin Shi, Beier Zhu, Junbao Zhou, Xiaolong Shen, Yuan Zhou, Qianru Sun, Hanwang Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=4Q55RwYte9"
tags: ["query:phys-video"]
score: 7.0
evidence: 用强化学习增强自回归视频扩散的运动控制，基于轨迹奖励；可用于物理合理性RL微调
tldr: 实时运动可控视频生成仍受限于双向扩散模型延迟和自回归模型运动伪影。AR-Drag提出首个RL增强的少步自回归视频扩散模型，首先微调基础I2V模型支持基本运动控制，再利用基于轨迹的奖励模型通过强化学习进一步提升运动可控性。Self-Rollout设计保持了马尔可夫性质，实现高质量实时生成。该方法为通过RL改善视频运动物理合理性提供了可行范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 双向扩散模型延迟高，自回归视频扩散模型在少步生成中出现质量退化和运动伪影。
method: 提出AR-Drag，先用微调支持运动控制，再通过基于轨迹奖励的强化学习改进，并用Self-Rollout保持马尔可夫性。
result: 实现实时图像到视频生成，支持多样运动控制并提升生成质量。
conclusion: RL增强的自回归扩散为实时运动可控视频生成提供了新方案，可扩展到物理合理性优化。
---

## Abstract
Real-time motion-controllable video generation remains challenging due to the inherent latency of bidirectional diffusion models and the lack of effective autoregressive (AR) approaches. Existing AR video diffusion models are limited to simple control signals or text-to-video generation, and often suffer from quality degradation and motion artifacts in few-step generation. To address these challenges, we propose AR-Drag, the first RL-enhanced few-step AR video diffusion model for real-time image-to-video generation with diverse motion control. We first fine-tune a base I2V model to support basic motion control, then further improve it via reinforcement learning with a trajectory-based reward model. Our design preserves the Markov property through a Self-Rollout mechanism and accelerates training by selectively introducing stochasticity in denoising steps. Extensive experiments demonstrate that AR-Drag achieves high visual fidelity and precise motion alignment, significantly reducing latency compared with state-of-the-art motion-controllable VDMs, while using only 1.3B parameters.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）

- **领域背景**：实时运动可控视频生成（real-time motion-controllable video generation）是视频扩散模型（VDM）的重要方向之一，但面临两难困境：
  - **双向扩散模型（bidirectional diffusion）**：生成质量高但推理延迟大，难以满足实时交互式生成的需求；
  - **自回归视频扩散模型（AR video diffusion）**：虽然具有并行/逐帧生成的低延迟潜力，但现有方法局限于简单控制信号或文本到视频（T2V）生成，且在少步生成（few-step generation）场景下容易出现**质量退化（quality degradation）**和**运动伪影（motion artifacts）**。
- **核心问题**：如何在保持自回归模型实时生成优势的同时，实现**多样化的运动控制（如拖拽式控制）** 并保证生成质量与运动对齐精度。
- **研究含义**：作者试图填补“AR视频扩散模型 + 运动控制 + 少步实时生成”这一空白，并将强化学习引入运动控制优化，为后续物理合理性视频生成提供新范式。

---

### 2. 论文提出的方法论（核心思想、关键技术细节）

- **总体框架**：提出 **AR-Drag**，据作者称是**首个RL增强的少步自回归视频扩散模型**，面向实时图像到视频（I2V）生成，支持多样化运动控制。
- **两阶段训练策略**：
  1. **第一阶段：基础运动控制微调**——对基础I2V模型进行微调（fine-tune），使其具备基本的运动控制能力（如拖拽/轨迹控制）；
  2. **第二阶段：强化学习优化**——引入**基于轨迹的奖励模型（trajectory-based reward model）**，通过强化学习（RL）进一步提升运动可控性和运动对齐精度。
- **关键技术：Self-Rollout 机制**：
  - 设计目的是**保持马尔可夫性质（Markov property）**，使自回归生成过程在训练和推理中保持一致，避免因长期依赖引入的分布偏移。
- **训练加速技巧**：
  - 在去噪（denoising）步骤中**选择性引入随机性（selectively introducing stochasticity）**，在不牺牲生成质量的前提下加速RL训练。
- **模型规模**：仅 **1.3B 参数**，强调轻量高效。

---

### 3. 实验设计（数据集 / 场景 / Benchmark / 对比方法）

> ⚠️ 注意：当前可获取的内容仅为摘要级信息（来自OpenReview验证页），未包含论文全文的实验章节。以下只能基于摘要推断，无法给出具体数据集名称。

- **场景**：实时图像到视频（I2V）生成，支持**多样化运动控制**（据方法名“AR-Drag”可推断以拖拽式/轨迹式控制为主）。
- **Benchmark**：摘要未明确列出标准benchmark名称，仅说明与**state-of-the-art motion-controllable VDMs**（最先进的运动可控视频扩散模型）进行对比。
- **对比方法**：与现有运动可控VDM进行对比，但具体方法名称、指标细节、参数量对比未在摘要中展示。
- **评估指标**：摘要提到两个核心维度——**视觉保真度（visual fidelity）** 和**运动对齐精度（motion alignment）**，具体量化指标（如FVD、LPIPS、运动轨迹误差等）未披露。

---

### 4. 资源与算力（GPU 型号、数量、训练时长等）

- **文中明确信息**：摘要中**未提及**任何关于算力的具体信息：
  - 未说明GPU型号（如A100/H100等）；
  - 未说明GPU数量；
  - 未说明训练总时长或推理时延的具体数值（仅定性地提到“显著降低延迟”）。
- **唯一相关数据**：模型参数量为 **1.3B**，暗示其训练资源需求相对可控，但无法据此推断具体算力开销。

---

### 5. 实验数量与充分性（是否充分、客观、公平）

- **实验数量**：摘要仅笼统提到“大量实验”（Extensive experiments），但没有给出具体实验组数、消融实验清单或数据集数量。
- **潜在充分性分析**：
  - **优势**：设计了两阶段训练（微调 + RL），从方法论上看存在多个可消融的组件（如Self-Rollout机制、选择性随机性、轨迹奖励模型），有较强的消融空间；
  - **不足**：由于无法访问全文，无法确认是否进行了完整的消融实验、跨数据集泛化测试、用户研究等；
  - **客观性/公平性风险**：对比方法仅模糊表述为“SOTA运动可控VDM”，未说明是否统一了推理步数、是否控制相同计算预算等公平对比条件，存在潜在的选择性对比风险。

---

### 6. 论文的主要结论与发现

1. **实时性达标**：AR-Drag实现了**实时（real-time）** 图像到视频生成，延迟显著低于现有运动可控VDM。
2. **质量与可控性兼顾**：在**视觉保真度**和**运动对齐精度**两个维度上同时达到高水平——这一组合在AR视频扩散模型中是此前未实现的。
3. **RL有效性验证**：通过基于轨迹奖励的强化学习，可以有效弥补AR模型在少步生成中的运动伪影问题，提升运动控制精度。
4. **轻量高效**：仅用 **1.3B参数** 即可达到上述效果，展示了AR架构在运动可控视频生成中的潜力。
5. **可扩展性**：作者在元数据中指出，该方法**可扩展到物理合理性RL微调**，为后续研究（如物理规律嵌入视频生成）提供范式参考。

---

### 7. 优点（方法/实验设计亮点）

- **首创性**：第一个将强化学习引入**少步自回归视频扩散**用于运动控制的工作，填补了AR视频模型在多样化运动控制上的空白。
- **两阶段训练设计清晰**：先“学会控制”（微调），再“擅长控制”（RL），分解了学习难度，逻辑清晰。
- **Self-Rollout机制具有理论价值**：在自回归视频生成中保持马尔可夫性是一个重要且往往被忽视的细节，该设计有助于缓解训练-推理不一致。
- **训练效率考量**：选择性引入随机性来加速RL训练，体现了方法在工程实用性和理论严谨性之间的平衡。
- **轻量模型**：1.3B参数在当前动辄数十亿参数的视频模型背景下具有部署优势，利于实时应用。

---

### 8. 不足与局限

- **实验细节缺失（从当前可获得信息判断）**：
  - 具体数据集、benchmark、评估指标、对比方法的量化结果均未在摘要中体现，无法独立验证其声明；
  - 未报告消融实验的完整结构与结果；
  - 未报告失败案例或控制失败率。
- **公平性风险**：对“SOTA方法”的对比描述过于笼统，未说明是否在相同计算资源、相同推理步数下进行比较，存在对比偏差可能。
- **应用限制**：
  - 运动控制能力是否限于拖拽式/轨迹式，对其他类型控制（如文本控制、区域控制）的泛化能力未知；
  - 1.3B参数虽轻量，但在更长视频生成、复杂场景下是否仍保持质量与实时性未可知；
  - 对物理合理性（如重力、碰撞）的直接保证并未在摘要中明确，作者仅暗示未来可拓展到物理合理性RL。
- **未提及算力成本**：训练该两阶段框架（微调+RL）的实际GPU消耗未知，可能影响可复现性。
- **可复现性**：论文细节（奖励函数具体形式、RL算法选择、Self-Rollout的具体实现）无法从摘要获取，需要全文确认。

---

**说明**：以上总结基于OpenReview提供的论文元数据与摘要。由于原始链接显示为“浏览器验证”页面，无法访问PDF全文，因此实验数据集、量化结果、算法细节（奖励函数公式、RL损失函数）等深层内容无法获取。建议在访问完整论文后补充验证。

（完）
