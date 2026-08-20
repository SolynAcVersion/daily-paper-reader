---
title: "Zero-to-Interaction: Generating Dynamic Videos from Synthetic State Transitions"
title_zh: 从零到交互：从合成状态转换生成动态视频
authors: "Jiho Jang, Jin-Young Kim, Nojun Kwak, Kyungjune Baek"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=fej4EppPMZ"
tags: ["query:phys-video"]
score: 9.0
evidence: 从合成状态转换生成具有合理物理交互的动态视频，并提供数据集
tldr: 视频生成模型难以描绘合理的物理交互与状态转换，为此提出从合成状态转换生成动态视频的框架。通过结构化分类与图像编辑模型构造明确的起止状态锚点，并设计状态引导采样减少伪影，生成可扩展的高质量交互视频数据集，为机器人等领域提供训练数据。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频模型虽能合成高保真视频，但物理交互与状态转换的合理性不足，限制机器人与VR/AR应用。
method: 利用结构化分类法和图像编辑模型生成显式起止状态图，并采用状态引导采样技术生成无缝视频。
result: 构建可扩展的合成交互视频数据集，缓解朴素条件生成的伪影，支持交互视频生成训练。
conclusion: 为可控物理交互视频的生成与数据集构建提供了有效范本。
---

## Abstract
While recent video generative models can synthesize high-fidelity videos, they struggle to portray plausible physical interactions and the resulting state transitions, a critical bottleneck for applications in robotics and VR/AR. To address this, we introduce a framework to generate a scalable synthetic dataset of controllable interactions. Our pipeline leverages a structured taxonomy and state-of-the-art image editing models to create explicit 'start' and 'end' state images, which serve as visual anchors for the interaction. To generate a seamless video utilizing these anchors, we propose State-Guided Sampling (SGS), a novel sampling technique that mitigates artifacts common in naive conditional generation. Furthermore, we develop and validate a new automated evaluation system that aligns with human judgments to ensure data quality. Experiments show that fine-tuning a base model on our dataset significantly enhances its ability to generate plausible interactions. The dataset, code, and evaluation tools will be released.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：尽管现有视频生成模型能够合成高保真度视频，但在描绘**合理的物理交互**及由交互引发的**状态转换**方面表现不佳。这一问题成为机器人和 VR/AR 应用中的关键瓶颈。
- **核心问题**：如何生成具有可信物理交互（如物体被推动、碰撞、变形等）且状态转换自然连贯的视频，同时保证数据规模可扩展性和可控性。
- **整体含义**：提出一套从“合成状态转换”出发生成动态视频的框架，不仅用于直接生成视频，更重要的是**构建高质量、可扩展的交互视频数据集**，用于训练下游视频生成模型，提升其在物理交互场景中的表现。

## 2. 论文提出的方法论

- **核心思想**：利用显式的“起始状态”和“结束状态”图像作为视觉锚点，引导视频生成模型演绎完整的物理交互过程。
- **关键技术细节**：
  - **结构化分类法（structured taxonomy）**：对物理交互进行系统分类，覆盖不同类型的状态转换，确保数据生成的覆盖面和规范性。
  - **图像编辑模型**：利用 SOTA 图像编辑模型，根据分类法生成明确的起始状态图像和结束状态图像，两者构成交互的“锚点”。
  - **状态引导采样（State-Guided Sampling, SGS）**：一种全新的采样技术，用于在给定两个锚点图像的情况下生成无缝视频，缓解朴素条件生成中常见的伪影（如跳变、闪烁、不连续）。
- **算法流程（文字描述）**：
  1. 定义交互分类体系，枚举各类状态转换。
  2. 对每个交互类别，使用图像编辑模型生成配对的起始图像和结束图像。
  3. 将这两个图像作为条件输入视频生成模型，并使用 SGS 采样方法生成中间帧，形成完整视频。
  4. 通过自动化评估系统筛选高质量样本，构建训练数据集。

## 3. 实验设计

- **数据集**：论文构建了一个**可扩展的合成交互视频数据集**（具体规模、类别数量未在摘要中给出）。
- **场景**：主要覆盖物理交互场景，包括但不限于推、拉、碰撞、变形等；具体场景细节未在文本中详述。
- **Benchmark**：未明确说明具体基准数据集，但提出了一套**新的自动化评估系统**，该系统与人类判断对齐，用于评估生成视频的质量和物理合理性。
- **对比方法**：主要与“朴素条件生成”（即直接以起止状态为条件但不使用 SGS）进行对比，未提及与其他既有视频生成方法的对比细节。

## 4. 资源与算力

- 论文摘要中**未明确说明** GPU 型号、数量、训练时长或计算资源规模。
- 仅提及对基础模型进行微调（fine-tuning），但具体硬件配置和成本未知。

## 5. 实验数量与充分性

- **实验组数**：摘要中仅提及两类实验：
  1. 微调基础模型后的效果提升实验；
  2. 自动化评估系统与人类判断的对齐验证。
- **消融实验**：提到了 SGS 对伪影的缓解作用，但未详细列出消融组。
- **充分性评估**：从摘要信息看，实验规模描述较为简略，缺乏量化指标（如 FVD、SSIM 等）和更多基线对比，因此**充分性和客观性无法完整判断**。不过论文提出自动化评估系统对齐人类判断，这在一定程度上增强了结果的可信度。

## 6. 论文的主要结论与发现

- 利用“起止状态锚点 + SGS 采样”能够生成更平滑、合理的交互视频，减少伪影。
- 在所构建数据集上微调基础模型，能**显著增强**模型生成合理物理交互的能力。
- 提出的自动化评估系统可以有效筛选高质量数据，并与人类主观判断一致性较高。
- 数据集、代码和评估工具将开源，有利于后续研究。

## 7. 优点

- **问题定位精准**：直击视频生成中“物理交互合理性”这一重要但困难的问题。
- **方法新颖**：用结构化分类 + 图像编辑生成显式状态锚点，将复杂交互生成转化为状态条件生成，思路清晰。
- **采样技术创新**：SGS 针对条件生成的伪影问题提出专门解决方案，具有通用潜力。
- **数据与评估闭环**：不仅生成数据，还构建了自动化评估系统，保证数据集质量，形成“生成-评估-训练”的完整流程。
- **应用价值高**：为机器人、VR/AR 等领域提供可交互视频训练数据，实用性强。

## 8. 不足与局限

- **实验细节缺失**：论文摘要未给出量化结果、数据集规模、类别数量、基线对比详情，难以全面评估性能增益水平。
- **评估偏差风险**：自动化评估系统虽然与人类判断对齐，但可能仍存在领域偏置，且未说明评估指标的具体形式和局限性。
- **合成数据固有局限**：由图像编辑模型生成的起止状态可能无法覆盖真实世界的全部物理规律，合成数据与真实数据之间存在分布差异。
- **应用限制**：物理交互的合理性依赖于分类法和图像编辑模型的能力，复杂、非刚性或细粒度交互可能未被充分覆盖。
- **算力未知**：未披露训练资源，无法评估方法的可复现成本。
- **对比公平性存疑**：仅与朴素条件生成对比，未与其他可控视频生成方法进行同等条件下的比较。

（完）
