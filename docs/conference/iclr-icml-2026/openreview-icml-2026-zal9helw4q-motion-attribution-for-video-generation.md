---
title: Motion Attribution for Video Generation
title_zh: 用于视频生成的运动归因
authors: "Xindi Wu, Despoina Paschalidou, Jun Gao, Antonio Torralba, Laura Leal-Taixé, Olga Russakovsky, Sanja Fidler, Jonathan Lorraine"
date: 2026-04-30
pdf: "https://openreview.net/pdf/24ac3b41f32abbf79a5ef7b5aae0f217024883e6.pdf"
tags: ["query:psd"]
score: 9.0
evidence: 以运动为中心的数据归因提升时间一致性与物理合理性；支持物理感知的数据筛选
tldr: 视频生成模型中数据对运动的影响机制尚不清楚。Motive提出可扩展的以运动为中心的数据归因框架，利用运动加权损失掩码将时间动态与静态外观分离，高效计算各微调片段的影响。在文本到视频模型上，Motive识别出对运动影响大的片段，并据此筛选数据，改善了时间一致性与物理合理性。该方法为物理感知视频生成的数据处理提供了系统性工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频生成中数据对运动质量的影响尚未明确，缺乏可扩展的数据归因方法。
method: 提出Motive框架，用运动加权损失掩码分离运动与外观，基于梯度计算运动影响分数。
result: 在文本生成视频模型上，Motive筛选高影响数据后提升了时间一致性与物理合理性。
conclusion: 该工作为运动感知的数据筛选提供了高效框架，有助于提升视频生成的物理合理性。
---

## Abstract
Despite the rapid progress of video generation models, the role of data in influencing motion is poorly understood. We present Motive (MOTIon attribution for Video gEneration), a motion-centric, gradient-based data attribution framework that scales to modern, large, high-quality video datasets and models. We use this to study which fine-tuning clips improve or degrade temporal dynamics. Motive isolates temporal dynamics from static appearance via motion-weighted loss masks, yielding efficient and scalable motion-specific influence computation. On text-to-video models, Motive identifies clips that strongly affect motion and guides data curation that improves temporal consistency and physical plausibility. With Motive-selected high-influence data, we improve both motion smoothness and dynamic degree on VBench, achieving a 74.1% human preference win rate compared with the pretrained base model. To our knowledge, this is the first framework to attribute motion rather than visual appearance in video generative models and to use it to curate fine-tuning data.

---

## 论文详细总结（自动生成）

## 论文总结：Motive — 用于视频生成的运动归因（Motion Attribution for Video Generation）

### 1. 核心问题与整体含义（研究动机与背景）
- 视频生成模型（如文本到视频模型）近年来取得了快速进展，但**数据对视频中“运动”的影响机制**仍不清晰。
- 现有的数据归因研究主要聚焦于静态外观（如图像分类、图像生成），缺乏从**运动（temporal dynamics）**角度对训练数据进行归因的框架。
- 该论文填补了上述空白，提出**Motive**——一个以运动为中心、基于梯度的数据归因框架，能够扩展到现代大规模视频数据集和模型规模，用于判断哪些微调视频片段对运动质量的提升或退化具有显著影响。
- 整体意义：通过识别高影响的运动样本，指导视频生成模型的微调数据筛选，从而提升生成视频的时间一致性、物理合理性和动态表现，是首个面向“运动”而非“外观”的视频生成数据归因工作。

### 2. 方法论：核心思想与技术细节
- **核心思想**：将视频中的**时间动态（运动）**与**静态外观**通过**运动加权损失掩码（motion-weighted loss masks）**分离，从而仅针对运动相关特征计算数据影响。
- **影响计算**：基于梯度计算每个微调样本对模型运动相关输出的影响分数（类似于影响函数或基于梯度的归因），实现高效、可扩展的运动特定影响评估。
- **算法流程**（文字描述）：
  1. 对视频样本生成运动权重掩码，弱化静态区域对损失的贡献；
  2. 在微调过程中，利用运动加权后的损失计算该样本的梯度；
  3. 基于梯度内积或类似度量，计算样本对模型运动输出的影响分数；
  4. 筛选出影响分数高（定义为改善运动质量）或较低（定义为损害运动质量）的样本，用于后续的数据筛选实验。
- 参数更新上，论文采用微调（fine-tuning）方案，而非从零训练，以保证计算可行性。

### 3. 实验设计
- **数据集 / 场景**：实验基于**文本到视频（text-to-video）生成模型**，使用大规模高质量视频数据集中的微调片段。
- **Benchmark**：使用 **VBench** 进行定量评估（包括运动平滑度、动态程度等维度），并进行**人类偏好评估**（win rate）。
- **对比方法**：主要比较基线为**预训练基础模型**（pretrained base model），未提及与其他数据归因方法的直接对比（因该方向此前缺乏运动归因的先例）。

### 4. 资源与算力
- 论文提供的文本（Abstract及元数据）中**未明确说明**使用的 GPU 型号、数量、训练时长、显存占用等算力信息。
- 仅能确定实验涉及现代大规模视频生成模型的微调计算，所提框架强调“可扩展性（scalable）”，但具体硬件资源不明。

### 5. 实验数量与充分性
- 从摘要可见的实验组数有限，主要包括：
  - 在文本到视频模型上验证 Motive 识别高/低运动影响片段的能力；
  - 使用 Motive 筛选的高影响数据进行微调后，与基础模型的对比（VBench 指标 + 人类偏好）；
  - 人类偏好评价（74.1% 胜率）。
- 未提及多数据集交叉验证、多模型架构对比、与不同数据筛选策略（如随机采样、外观归因）的消融实验，因此**实验覆盖相对有限**。
- 实验在已公开的 VBench 上评估，具有一定客观性；但由于缺少对更多基线和变量控制的详细说明，其公平性验证尚不充分。

### 6. 主要结论与发现
- Motive 能够有效识别对运动影响显著的视频片段，区分改善与损害运动质量的样本。
- 使用 Motive 筛选的高影响数据进行微调后，模型在 VBench 上**运动平滑度（motion smoothness）和动态程度（dynamic degree）**均获得提升。
- 人类偏好评估中，Motive 筛选数据微调后的模型以 **74.1% 的胜率**优于预训练基础模型。
- 该工作首次实现视频生成模型中的**运动归因**（而非外观归因），并验证了其用于数据筛选的实际价值。

### 7. 优点
- **新颖性强**：首次提出运动特定的数据归因方法，切入角度独特。
- **可扩展性设计**：采用基于梯度的方法，避免昂贵的逐样本重训练，能适配大规模现代视频数据集。
- **实用价值高**：直接将归因结果用于数据筛选，提升了视频生成的运动质量与物理合理性，为物理感知数据筛选提供了系统性工具。
- **评估维度全面**：同时考量运动平滑度、动态程度与人类偏好，兼顾客观指标与主观感受。

### 8. 不足与局限
- **算力信息缺失**：未公布 GPU 型号、数量、训练时长等，复现成本难以估计。
- **实验覆盖有限**：仅评估了文本到视频模型，未涉及其他视频生成范式；未提供多数据集、多模型、多筛选策略的广泛消融。
- **对比基线较少**：未与其他数据归因或数据筛选方法（如随机采样、基于外观的归因）进行系统性比较，难以判断优势来源。
- **潜在偏差风险**：运动加权掩码的设计可能对某些运动类型（如细微运动、复杂物理交互）不敏感，存在偏差；此外，人类偏好评价的评委规模与多样性未说明。
- **实际应用限制**：运动加权损失掩码需要额外的运动估计计算；对超长视频或低质量数据的适用性有待验证。

（完）
