---
title: "From Frames to Sequences: Temporally Consistent Human-Centric Dense Prediction"
title_zh: 从帧到序列：时序一致的人体中心稠密预测
authors: "Xingyu Miao, Junting Dong, Qin Zhao, Yuhang Yang, Junhao Chen, Yang Long"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=2xaNU3lgKC"
tags: ["query:frame-dist"]
score: 5.0
evidence: 跨视频序列的时序一致稠密预测
tldr: 该文针对视频序列中人体中心稠密预测的时序一致性问题，指出逐帧的深度、法线与分割预测在运动、遮挡与光照变化下难以稳定。作者设计合成数据管线，生成大规模逼真人像与运动对齐视频序列并提供帧级与序列级监督，进而提出融合人体先验与时序模块的模型。方法同时学习空间精度与时序稳定性。结果改善了运动与遮挡下的预测稳定性。其贡献在于时序一致性建模，与帧间分布关系建模有一定关联。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 逐帧的人体中心稠密预测在运动、遮挡与光照变化下难以保持时序稳定。
method: 设计提供帧级与序列级监督的合成数据管线，并提出融合人体先验与时序模块的模型。
result: 在运动与遮挡场景下提升了深度、法线与分割预测的时序稳定性。
conclusion: 贡献在于视频序列的时序一致性建模，与帧间分布建模部分相关。
---

## Abstract
In this work, we focus on the challenge of temporally consistent human-centric dense prediction across video sequences. While progress has been made in per-frame predictions of depth, surface normals, and segmentation, achieving stability under motion, occlusion, and illumination changes remains difficult. For this, we design a synthetic data pipeline that produces large-scale photorealistic human images and motion-aligned video sequences with high-fidelity annotations. Unlike prior static data synthetic pipelines, our pipeline provides both frame-level and sequence-level supervision, supporting the learning of spatial accuracy and temporal stability. Building on this, we introduce a model that integrates human-centric priors and temporal modules to jointly estimate temporally consistent segmentation, depth, and surface normals within a single framework. Our two-stage training strategy, combining static pretraining with dynamic sequence supervision, enables the model to first acquire robust spatial representations and then refine temporal consistency across motion-aligned sequences. Extensive experiments show that we achieve state-of-the-art performance on THuman2.1 and Hi4D and generalize effectively to in-the-wild videos.

---

## 论文详细总结（自动生成）

# 论文总结：从帧到序列——时序一致的人体中心稠密预测

> 说明：提供的 PDF 提取文本为 OpenReview 验证页面，未包含论文正文；以下总结主要依据论文元数据、摘要与条目信息。未明确给出的公式、对比方法、算力与消融细节不作臆造。

## 1. 核心问题与整体含义
- **研究问题**：视频序列中的人体中心稠密预测，包括深度、表面法线和人体分割，如何在运动、遮挡与光照变化下保持**时序一致性**。
- **背景动机**：逐帧预测方法虽在单帧深度、法线、分割上已有进展，但在视频中容易产生帧间抖动、闪烁和不稳定结果。
- **整体含义**：论文试图把人体中心稠密预测从“单帧估计”推进到“序列级稳定估计”，通过合成数据、人体先验与时序建模，联合学习空间精度和时序稳定性。
- **任务定位**：属于视频人体理解、数字人、AR/VR、人像编辑与动作分析等方向的底层感知问题。
- **元数据信息**：该文题为 *From Frames to Sequences: Temporally Consistent Human-Centric Dense Prediction*，来源标注为 ICLR-2026-Rejected-Public，评分 5.0。

## 2. 方法论
- **核心思想**：构建大规模、逼真、运动对齐的人体视频合成数据管线，并提供帧级与序列级监督；再设计融合人体先验与时序模块的统一模型，在单框架内联合估计时序一致的分割、深度和表面法线。
- **数据管线关键点**：
  - 生成大规模照片级真实感人像与运动对齐视频序列。
  - 提供高保真标注。
  - 不同于以往静态合成数据管线，同时提供**帧级监督**和**序列级监督**。
  - 帧级监督用于空间精度，序列级监督用于跨帧时序稳定性。
- **模型设计**：
  - 集成**人体中心先验**，以利用人体结构、部位或姿态等相关信息。
  - 引入**时序模块**，在视频序列中传播、对齐或聚合跨帧信息。
  - 单一框架联合输出分割、深度和表面法线，追求多任务间的一致性。
- **训练策略**：
  - 采用**两阶段训练**。
  - 第一阶段：静态预训练，学习稳健的空间表征。
  - 第二阶段：动态序列监督，在运动对齐序列上优化时序一致性。
- **算法流程文字说明**：合成数据构建 → 静态预训练获取单帧空间能力 → 序列微调引入时序模块与人体先验 → 多任务联合输出 → 在运动/遮挡/光照变化下提升稳定性。
- **公式与细节**：摘要未给出具体损失函数、网络结构、时序模块形式或公式，因此无法进一步总结技术实现。

## 3. 实验设计
- **数据集**：
  - THuman2.1：人体相关数据集。
  - Hi4D：人体/多人交互相关视频数据集。
  - in-the-wild videos：用于验证真实野外视频泛化能力。
- **Benchmark**：论文声称在 THuman2.1 和 Hi4D 上达到 state-of-the-art 性能，并有效泛化到野外视频。
- **场景**：重点涉及运动、遮挡与光照变化下的时序稳定性。
- **对比方法**：摘要未列出具体对比方法名称，仅说明达到 SOTA。
- **评价指标**：摘要未明确说明深度、法线、分割及时间一致性的具体指标。
- **实验任务**：人体中心稠密预测，包括分割、深度和表面法线。

## 4. 资源与算力
- 提供的摘要与元数据中**未提及** GPU 型号、数量、训练时长、参数量或计算开销。
- PDF 正文未能提取，因此无法从正文确认算力资源。
- 结论：该论文的算力与训练资源信息在现有材料中缺失。

## 5. 实验数量与充分性
- 从摘要可推断至少包含：
  - THuman2.1 主实验。
  - Hi4D 主实验。
  - in-the-wild 视频泛化实验。
  - 可能包含两阶段训练、时序模块、人体先验、序列级监督等消融，但摘要未披露具体组数。
- **充分性**：若仅按摘要描述，实验覆盖两个基准数据集和野外泛化，具备一定充分性；但缺少对比方法、指标、消融数量和失败案例分析，无法完全判断。
- **客观与公平性**：论文声称 SOTA，但未提供对比协议、评价指标与统计显著性，现有信息不足以评估公平性。
- **可复现性**：由于正文不可访问，数据管线、模型结构、训练细节和超参数均不明确，可复现性难以判断。

## 6. 主要结论与发现
- 逐帧人体中心稠密预测在运动、遮挡和光照变化下难以保持稳定。
- 同时使用帧级与序列级监督的合成数据管线，有助于学习空间精度和时序稳定性。
- 融合人体先验与时序模块的统一模型，可以在一个框架内联合估计时序一致的分割、深度和表面法线。
- 两阶段训练策略有效：先静态预训练学习空间表示，再动态序列监督提升时序一致性。
- 方法在 THuman2.1 和 Hi4D 上达到 SOTA，并能泛化到真实野外视频。
- 论文主要贡献在于视频序列的时序一致性建模，与帧间分布关系建模部分相关。

## 7. 优点
- **问题选择有意义**：聚焦视频人体稠密预测中的时序稳定性，而非仅追求单帧精度。
- **数据管线创新**：同时提供帧级和序列级监督，弥补静态合成数据在时序学习上的不足。
- **统一多任务框架**：在单模型中联合处理分割、深度和表面法线，有利于任务间一致性。
- **训练策略合理**：静态预训练加动态序列微调，符合从空间表征到时序稳定的学习逻辑。
- **泛化验证**：除标准数据集外，还报告 in-the-wild 视频泛化，增强应用潜力。
- **人体先验引入**：利用人体中心先验，符合人体稠密预测的结构化特点。

## 8. 不足与局限
- **正文不可获取**：当前 PDF 提取为验证页，无法核实方法细节、公式、实验设置与附录。
- **算力信息缺失**：未说明 GPU 型号、数量与训练时长，难以评估计算成本与可复现性。
- **实验细节不足**：未列出具体对比方法、评价指标、消融实验数量和统计结果。
- **公平性存疑**：仅声称 SOTA，缺少与各方法的完整对比协议和误差分析。
- **合成到真实域差距**：依赖合成数据管线，可能存在域偏差，真实场景泛化仍可能受限。
- **应用限制**：方法面向人体中心稠密预测，对非人体、通用场景或极端遮挡的适用性未知。
- **时序一致性评估风险**：若评价指标偏重某些序列或场景，可能高估稳定性；需要更多跨数据集与失败案例分析。
- **评审信息**：元数据标注为 ICLR-2026-Rejected-Public，评分 5.0，提示该方法在评审中可能存在争议或未被接收。

（完）
