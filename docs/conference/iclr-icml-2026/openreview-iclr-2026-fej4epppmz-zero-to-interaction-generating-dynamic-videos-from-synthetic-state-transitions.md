---
title: "Zero-to-Interaction: Generating Dynamic Videos from Synthetic State Transitions"
title_zh: 从合成状态转换生成动态视频：从零到交互
authors: "Jiho Jang, Jin-Young Kim, Nojun Kwak, Kyungjune Baek"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=fej4EppPMZ"
tags: ["query:phys-video"]
score: 8.0
evidence: 为物理合理视频生成构建可控交互的合成数据集
tldr: 该论文针对视频生成模型难以呈现合理物理交互的问题，提出一套生成可控交互合成视频数据的框架。通过结构化分类和图像编辑模型创建起始与结束状态锚点，并设计状态引导采样技术来生成连贯动态视频。实验表明该方法能有效减少生成伪影、提升物理交互合理性，为训练机器人、VR/AR等应用所需的物理感知视频模型提供了可扩展的数据基础。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频生成模型难以生成合理的物理交互及状态转换，制约了机器人、VR/AR等应用。
method: 提出一个可扩展的合成交互数据集生成框架，利用结构化分类法和图像编辑模型构建起始与结束状态锚点，并用状态引导采样(SGS)生成连续视频。
result: 通过SGS缓解了朴素条件生成的伪影，并验证了生成视频在物理交互合理性上的提升。
conclusion: 该工作为训练物理可解释的视频生成模型提供了一种可扩展的合成数据生成途径。
---

## Abstract
While recent video generative models can synthesize high-fidelity videos, they struggle to portray plausible physical interactions and the resulting state transitions, a critical bottleneck for applications in robotics and VR/AR. To address this, we introduce a framework to generate a scalable synthetic dataset of controllable interactions. Our pipeline leverages a structured taxonomy and state-of-the-art image editing models to create explicit 'start' and 'end' state images, which serve as visual anchors for the interaction. To generate a seamless video utilizing these anchors, we propose State-Guided Sampling (SGS), a novel sampling technique that mitigates artifacts common in naive conditional generation. Furthermore, we develop and validate a new automated evaluation system that aligns with human judgments to ensure data quality. Experiments show that fine-tuning a base model on our dataset significantly enhances its ability to generate plausible interactions. The dataset, code, and evaluation tools will be released.

---

## 论文详细总结（自动生成）

# 论文总结：Zero-to-Interaction: Generating Dynamic Videos from Synthetic State Transitions

> 注：本总结仅基于提供的论文摘要与元数据信息，正文细节未一并给出，因此部分内容基于合理推断，并会明确标注“未提及”。

## 1. 核心问题与整体含义

- **研究动机**：现有视频生成模型能够生成高保真画质，但难以刻画**合理的物理交互**以及由交互导致的**状态转换**（如物体被推动、翻转、破裂等）。这一瓶颈严重制约了视频生成在**机器人、VR/AR**等需要物理可理解性的领域中的应用。
- **整体含义**：论文提出了一套**可扩展的合成数据生成框架**，通过可控的方式构造交互视频数据，从而引导视频生成模型学会更符合物理规律的状态演化。该工作为“物理感知”视频生成模型提供了低成本、大规模的数据来源。

## 2. 方法论

- **核心思想**：利用**结构化分类法（structured taxonomy）** 定义一类交互及其状态转换关系；然后借助**图像编辑模型**生成交互过程的**起始状态图像**和**结束状态图像**，这两个图像作为视觉锚点；最后通过一种新的采样策略——**状态引导采样（State-Guided Sampling, SGS）**，生成连接这两个锚点的连贯动态视频。
- **关键技术细节**：
  - **结构化分类法**：对物理交互类型进行系统归纳，确保合成数据覆盖多样化的状态转换。
  - **图像编辑模型**：从起始状态图像出发，编辑生成对应的结束状态图像，例如改变物体位置、朝向或形状，从而显式定义交互目标。
  - **状态引导采样（SGS）**：在扩散模型的采样过程中引入状态引导，强制视频帧在时间轴上与起始/结束状态图像保持一致，避免朴素条件生成中常见的伪影（如跳变、断裂、状态不连续）。
  - **自动评估系统**：构建了一个与人类主观判断高度对齐的自动评分系统，用来筛选和验证生成视频的状态转换质量。
- **算法流程（文字描述）**：
  1. 按分类法选择交互类型；
  2. 生成/选择起始状态图像；
  3. 用图像编辑模型生成结束状态图像；
  4. 将两个状态图像作为条件输入视频生成模型；
  5. 在采样阶段应用 SGS，逐步去噪并约束中间帧状态；
  6. 输出完整视频，并用自动评估系统进行质量验证。

> 注：论文摘要未给出具体公式或网络结构细节，此处仅为流程归纳。

## 3. 实验设计

- **数据集**：论文构建的是**合成交互数据集**，但具体规模、交互类别数量、图像分辨率等未在摘要中给出。
- **场景**：涉及物理状态转换的可控交互场景，例如物体运动、形态变化等（具体示例未提及）。
- **Benchmark**：未明确说明使用了现有基准数据集；论文提出了**新的自动评估系统**，并验证该系统与人类判断的一致性。
- **对比方法**：
  - 以**朴素条件生成**（naive conditional generation）作为基线，用于验证 SGS 的增益；
  - 另外，通过**微调基础视频生成模型**的方式，对比微调前后模型在物理交互合理性上的表现。

> 注：由于正文缺失，无法得知是否对比了其他 SOTA 方法，或者是否在多个基准上测试。

## 4. 资源与算力

- 论文摘要与元数据中**未提及任何算力信息**，包括 GPU 型号、数量、训练时长、参数量等。
- 因此无法评估该方法的计算开销和可复现性成本。

## 5. 实验数量与充分性

- 从现有信息可以看出至少包含两类关键实验：
  1. **SGS 消融**：对比 SGS 与朴素条件生成的伪影情况；
  2. **模型微调验证**：在合成数据集上微调基础模型后，验证其生成合理交互的能力提升。
- 但**具体实验数量、消融维度、评估指标数值、统计显著性**均未提供。
- 总体来看，论文声称有实验支撑，但在当前信息下无法判断实验是否充分、客观、公平，尤其是缺乏对基准选择、评估协议和误差分析的描述。

## 6. 主要结论与发现

- **SGS 有效缓解了伪影**：相比朴素条件生成，SGS 能生成更连贯、状态转换更平滑的视频。
- **微调带来显著收益**：在生成的数据集上微调基础模型，能显著增强其生成合理物理交互的能力。
- **自动评估系统可靠**：提出的评估系统与人类判断高度一致，可用于大规模数据筛选和质量控制。
- 整体结论是：该合成数据生成框架为训练物理感知视频模型提供了一条可扩展且可控制的有效路径。

## 7. 优点

- **可扩展性**：不依赖真实交互视频数据，可以大规模合成，成本低。
- **可控性**：通过结构化的分类法和显式的状态锚点，能精确控制视频的交互类型和状态转换。
- **方法简洁**：SGS 是一种采样阶段的技术，可方便地迁移到不同的扩散式视频生成模型中。
- **评估体系完备**：专门设计了与人类判断一致的评价工具，解决了生成视频质量难以自动衡量的痛点。
- **开源计划**：论文承诺释放数据集、代码和评估工具，有利于领域后续研究。

## 8. 不足与局限

- **信息不完整**：摘要和元数据中缺少详细的实验设置、数据统计和计算资源描述，难以全面评估方法的真实效能。
- **合成数据现实差距**：由图像编辑模型生成的合成交互可能无法覆盖真实世界的复杂物理规律（如弹性、摩擦、流体力学），存在 **sim-to-real 泛化风险**。
- **交互类型受限**：分类法界定的交互种类可能有限，对开放世界的物理交互建模仍需扩展。
- **评估系统可能偏见**：自动评估系统是否在不同视频生成模型、不同交互类别下都能保持一致，尚未有充分证据。
- **未提及失败案例与边界条件**：缺乏对 SGS 失效场景或伪影残留情况的讨论。
- **算力成本未知**：没有提供训练和推理的资源需求，这对于可复现性和实用化是一个劣势。

---

（完）
