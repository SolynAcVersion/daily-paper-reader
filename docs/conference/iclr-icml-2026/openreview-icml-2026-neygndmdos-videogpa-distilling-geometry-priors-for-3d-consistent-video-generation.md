---
title: "VideoGPA: Distilling Geometry Priors for 3D-Consistent Video Generation"
title_zh: VideoGPA：蒸馏几何先验以实现3D一致的视频生成
authors: "Hongyang Du, Junjie Ye, Xiaoyan Cong, Runhao Li, Jingcheng Ni, Aman Agarwal, Zeqi Zhou, Zekun Li, Randall Balestriero, Yue Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6959df1a6955fcefb233d586ca70a1513418d6b1.pdf"
tags: ["query:phys-video"]
score: 8.0
evidence: 通过DPO蒸馏几何先验，实现3D一致的视频生成
tldr: 视频扩散模型虽视觉惊艳，却难以维持3D结构一致性，常出现物体变形或空间漂移，根源在于标准去噪目标缺乏几何一致性激励。本文提出VideoGPA，一种数据高效的自监督框架，利用几何基础模型自动生成稠密偏好信号，并通过直接偏好优化DPO引导模型分布趋向内在3D一致性，无需人工标注。实验表明其显著提升了生成视频的几何一致性与结构合理性，为物理一致的视频生成提供了偏好对齐新路径。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频扩散模型缺乏几何一致性激励，常出现物体变形与空间漂移等3D不一致问题。
method: 提出自监督框架VideoGPA，用几何基础模型生成稠密偏好信号，经DPO引导模型趋向3D一致分布。
result: 方法无需人工标注即显著提升了生成视频的3D结构一致性与合理性。
conclusion: 偏好对齐为物理与几何一致的视频生成提供了数据高效的新路径。
---

## Abstract
While recent video diffusion models (VDMs) produce visually impressive results, they fundamentally struggle to maintain 3D structural consistency, often resulting in object deformation or spatial drift. We hypothesize that these failures arise because standard denoising objectives lack explicit incentives for geometric coherence. To address this, we introduce VideoGPA (Video Geometric Preference Alignment), a data-efficient self-supervised framework that leverages a geometry foundation model to automatically derive dense preference signals that guide VDMs via Direct Preference Optimization (DPO). This approach effectively steers the generative distribution toward inherent 3D consistency without requiring human annotations. VideoGPA significantly enhances temporal stability, geometric plausibility, and motion coherence using minimal preference pairs, consistently outperforming state-of-the-art baselines in extensive experiments.

---

## 论文详细总结（自动生成）

## 论文总结：VideoGPA：蒸馏几何先验以实现 3D 一致的视频生成

> 说明：提供的 PDF 正文提取失败（HTTP 503，内容为 “no healthy upstream”），因此以下总结主要依据论文标题、摘要与 Markdown 元数据。凡摘要未覆盖的细节，均标注为“未说明/无法核实”，不做推测性补全。

### 1. 核心问题与整体含义

- **研究背景**：近期视频扩散模型（VDMs）能生成视觉上令人印象深刻的视频，但在维持 **3D 结构一致性** 方面存在根本困难，常出现物体变形、空间漂移等问题。
- **核心假设**：这些失败源于标准去噪目标 **缺乏对几何一致性的显式激励**，模型只被训练去拟合像素/视觉分布，而没有被引导去保持 3D 结构合理。
- **整体含义**：论文提出 **VideoGPA（Video Geometric Preference Alignment）**，试图通过偏好对齐，将视频扩散模型的生成分布引导向内在 3D 一致性。其意义在于：不依赖人工标注，利用几何基础模型自动构造偏好信号，为物理/几何一致的视频生成提供数据高效的新路径。
- **元数据信息**：该论文标注为 ICML-2026 Accepted，评分 8.0，标签涉及 `query:phys-video`。

### 2. 方法论

- **核心思想**：VideoGPA 是一个 **数据高效的自监督框架**。它利用 **几何基础模型** 自动导出 **稠密偏好信号**，再通过 **直接偏好优化（DPO）** 引导视频扩散模型，使其生成结果趋向 3D 一致。
- **关键技术点**：
  - 使用几何基础模型自动生成偏好信号，而非依赖人工标注。
  - 通过 DPO 将偏好信号转化为对视频扩散模型的优化信号。
  - 目标是提升生成视频的时间稳定性、几何合理性和运动一致性。
  - 强调“数据高效”，摘要称仅需 **minimal preference pairs** 即可取得效果。
- **算法流程（摘要层面可概括为）**：
  1. 视频扩散模型生成候选视频或去噪轨迹；
  2. 几何基础模型对候选结果提供几何一致性相关的稠密偏好信号；
  3. 基于这些偏好信号，用 DPO 更新视频扩散模型；
  4. 使模型分布逐步偏向内在 3D 一致、结构合理的视频生成结果。
- **未说明内容**：具体使用哪个几何基础模型、偏好对如何构造、DPO 损失形式、训练目标公式、是否涉及奖励模型或正则项等，摘要中均未给出。

### 3. 实验设计

- **数据集/场景**：未说明。摘要和元数据中未列出具体数据集、视频场景或任务类型。
- **Benchmark**：未说明。没有给出具体 benchmark 名称或评测协议。
- **对比方法**：摘要仅称与 **state-of-the-art baselines** 对比，但未列出具体基线方法名称。
- **评价维度**：摘要提到主要提升维度包括：
  - temporal stability，时间稳定性；
  - geometric plausibility，几何合理性；
  - motion coherence，运动一致性。
- **实验规模描述**：摘要称进行了 **extensive experiments**，并持续优于 SOTA 基线，但未给出实验组数、数据集数量或消融设置。

### 4. 资源与算力

- 论文摘要与元数据中 **未提及** GPU 型号、GPU 数量、训练时长、训练数据规模、推理成本等算力信息。
- 因此无法总结具体资源消耗，也无法判断其训练成本是否与“数据高效”一致。

### 5. 实验数量与充分性

- **实验数量**：无法确定。仅有“extensive experiments”的概括性表述，未说明做了多少组实验、覆盖多少数据集或多少消融实验。
- **充分性**：由于缺少数据集、benchmark、baseline、评价指标、消融实验和统计显著性信息，无法客观判断实验是否充分。
- **客观性与公平性**：摘要声称“consistently outperforming state-of-the-art baselines”，但未提供对比设置、公平性控制、相同训练/推理预算等信息，因此无法核实比较是否公平。
- **可验证性**：当前提供的文本不足以复现或验证实验结论。

### 6. 论文的主要结论与发现

- VideoGPA 能显著增强生成视频的：
  - 时间稳定性；
  - 几何合理性；
  - 运动一致性。
- 方法只需 **极少量偏好对**，即可取得明显效果，体现数据高效性。
- 在广泛实验中，VideoGPA **持续优于现有 SOTA 基线**。
- 偏好对齐被证明是提升视频生成几何/物理一致性的有效路径，且无需人工标注。

### 7. 优点

- **问题切入准确**：指出视频扩散模型 3D 不一致的根源可能在于标准去噪目标缺少几何一致性激励。
- **自监督与数据高效**：利用几何基础模型自动生成偏好信号，避免昂贵的人工标注。
- **方法路径新颖**：将 DPO 引入视频扩散模型的 3D 一致性对齐，结合几何先验与偏好优化。
- **目标明确**：不仅追求视觉质量，还关注时间稳定性、几何合理性和运动一致性。
- **潜在通用性**：若偏好信号可自动生成，方法可能较容易扩展到不同视频生成模型或任务中。
- **元数据评价较高**：ICML-2026 Accepted，评分 8.0，说明同行评审对其动机和方法有较高认可。

### 8. 不足与局限

- **全文不可获取导致的信息局限**：由于 PDF 提取失败，无法核实方法细节、公式、实验设置和附录内容。
- **实验覆盖不明确**：未说明数据集、场景、benchmark、baseline、指标定义和消融实验，难以判断泛化能力。
- **公平性风险**：未报告与基线是否在相同数据、算力、训练步数或评价协议下比较。
- **偏差风险**：偏好信号来自几何基础模型，若该模型本身存在偏差或误差，可能将错误几何先验蒸馏进视频模型。
- **应用限制未知**：对复杂动态、遮挡、多物体交互、物理接触等困难场景的表现未说明。
- **计算开销未知**：虽然声称数据高效，但未报告训练和推理成本，实际部署代价不明确。
- **多样性与保真度权衡未知**：DPO 对齐可能提升一致性，但也可能影响生成多样性，摘要未讨论。

（完）
