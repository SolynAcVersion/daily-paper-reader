---
title: Temporal-aware Flow Matching for Video Generation with Temporally Coherent Motion
title_zh: 面向时序连贯运动视频生成的时间感知流匹配
authors: "Zirui Pan, Xin Wang, Yipeng Zhang, Yuwei Zhou, Wenwu Zhu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/2353dd72ba2db602d82f7e1a530e20640cd45ad5.pdf"
tags: ["query:frame-dist"]
score: 8.0
evidence: 将帧间约束嵌入流目标以建模时间依赖
tldr: 针对现有文本到视频生成模型常把视频视为帧序列、直接套用为图像设计的流匹配目标，导致无法显式建模运动先验与帧间时间依赖、产生时序不一致和不真实运动的问题，本文提出时间感知流匹配TFM。该方法将帧间约束嵌入流匹配目标，从而在视频生成中实现时序连贯的运动建模。研究显式建模了帧与帧之间的分布与依赖关系，为提升生成视频的运动合理性与时间一致性提供了有效训练范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频生成直接套用图像流匹配目标，未显式建模帧间时间依赖。
method: 提出时间感知流匹配TFM，将帧间约束嵌入流匹配目标。
result: 实现时序连贯的运动建模，提升生成视频的运动合理性。
conclusion: 为显式建模视频帧间分布关系提供了有效训练范式。
---

## Abstract
Despite rapid advances in text-to-video generation, state-of-the-art generative models still suffer from producing temporally incoherent and unrealistic motion for videos. The key weakness of existing works is that they commonly treat videos as frame sequences and directly adopt Flow Matching (FM) objectives, which are originally designed for images. This practice fails to explicitly model motion priors or temporal dependencies, resulting in suboptimal dynamics that may appear incoherent and unrealistic. To solve this problem, we propose Temporal-aware Flow Matching (TFM), a novel training paradigm that embeds inter-frame constraints into the flow objective, leading to temporally coherent motion modeling in video generation. More specifically, the proposed TFM enforces temporal correlations across frames while retaining the desirable properties of FM, and further introduces a residual-type loss that aligns naturally with this new flow. We theoretically prove that models trained with TFM are able to exhibit remarkably enhanced temporal perception ability. Notably, TFM imposes no additional cost during inference and is applicable to any model using FM. Extensive experiments demonstrate that our TFM can significantly improve motion realism across diverse motion types. Generated videos are presented at https://pzrain.github.io/tfm.

---

## 论文详细总结（自动生成）

# 论文总结：面向时序连贯运动视频生成的时间感知流匹配（TFM）

## 0. 材料说明
- 提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页面，并未包含论文正文。
- 可获取的论文信息主要来自元数据与摘要：标题、作者、来源、摘要、TLDR 等。
- 因此，下文关于实验数据集、benchmark、对比方法、算力、实验组数等细节，只能标注为“未提供/无法确认”，不能从给定材料中可靠推断。

## 1. 核心问题与整体含义
- **研究背景**：文本到视频生成发展迅速，但当前先进生成模型仍常产生时序不一致、不真实的运动。
- **核心问题**：现有工作通常把视频视为帧序列，并直接套用原本为图像设计的 Flow Matching 目标。
- **关键缺陷**：这种直接套用没有显式建模运动先验或帧间时间依赖，导致生成视频的动态效果次优，表现为不连贯、不真实。
- **整体含义**：论文主张应从训练目标层面引入时间感知能力，而不是仅在架构或后处理上处理视频时序问题。
- **研究目标**：通过显式建模帧与帧之间的分布和依赖关系，提升生成视频的运动合理性与时间一致性。

## 2. 方法论：时间感知流匹配 TFM
- **核心思想**：提出 Temporal-aware Flow Matching（TFM），将帧间约束嵌入流匹配目标中，使视频生成在训练阶段就学习时序连贯的运动建模。
- **关键设计**：
  - 在 Flow Matching 目标中加入跨帧时间约束，强制模型建模帧间相关性。
  - 在引入帧间约束的同时，尽量保留 Flow Matching 原有的优良性质。
  - 引入一种**残差型损失**，使其与新的流目标自然对齐。
- **理论部分**：论文声称从理论上证明，使用 TFM 训练的模型能够表现出显著增强的时间感知能力。
- **推理特性**：TFM 在推理阶段不引入额外成本。
- **适用范围**：TFM 可应用于任何使用 Flow Matching 的模型，具有较强通用性。
- **算法流程文字说明**：训练时，模型不再只学习图像式的单帧流匹配目标，而是在流匹配框架中额外施加帧间一致性/相关性约束，并用残差型损失优化；推理时仍按原 Flow Matching 方式采样，不增加额外模块或计算步骤。具体公式、约束形式与损失细节未在提供文本中给出。

## 3. 实验设计
- 提供文本中**没有给出具体数据集名称、场景设置、benchmark、评价指标或对比方法**。
- 摘要仅称进行了“extensive experiments”，并表明 TFM 能显著改善多种运动类型下的运动真实性。
- 生成视频展示在项目页：https://pzrain.github.io/tfm。
- 因此，无法从给定材料确认：
  - 使用了哪些视频生成数据集；
  - benchmark 是什么；
  - 与哪些基线方法进行了比较；
  - 采用了哪些定量指标或用户研究。

## 4. 资源与算力
- 提供文本中**未提及 GPU 型号、数量、训练时长、参数量、训练数据规模等算力信息**。
- 因此无法总结该论文的资源消耗与训练成本。
- 仅能从摘要得知：TFM 在推理阶段无额外成本，但训练阶段是否增加成本未说明。

## 5. 实验数量与充分性
- 摘要声称进行了大量实验，但给定材料中**没有实验组数、消融实验、数据集数量、统计显著性、公平性设置等细节**。
- 因此无法客观评估实验是否充分、是否公平、是否存在偏差风险。
- 从可获取信息看，只能确认作者报告了运动真实性提升，但缺少可验证的实验协议与结果细节。

## 6. 主要结论与发现
- TFM 能够显著提升多种运动类型下的运动真实性。
- 将帧间约束嵌入 Flow Matching 目标，有助于实现时序连贯的运动建模。
- 显式建模视频帧间分布与依赖关系，是改善视频生成时间一致性的有效训练范式。
- 理论上，TFM 训练后的模型具有更强的时间感知能力。
- TFM 推理无额外成本，并可适用于任何使用 Flow Matching 的模型。

## 7. 优点
- **问题定位清晰**：明确指出直接套用图像 Flow Matching 目标会忽略视频特有的时间依赖。
- **方法通用性强**：不绑定特定模型结构，可应用于任何 Flow Matching 模型。
- **推理友好**：推理阶段无额外成本，便于实际部署。
- **训练范式创新**：从目标函数层面嵌入帧间约束，而非仅依赖架构修改或后处理。
- **理论结合实验**：摘要称有理论证明，并辅以实验验证运动真实性提升。
- **残差型损失设计**：使损失形式与新流目标自然对齐，具有一定方法美感。

## 8. 不足与局限
- **材料限制导致的不足**：
  - 给定 PDF 文本不是论文正文，无法核实实验、公式、理论证明与实现细节。
  - 无法评估数据集覆盖、baseline 公平性、指标客观性与消融充分性。
  - 无法确认算力消耗与训练成本。
- **基于摘要可推测的潜在局限**：
  - 帧间约束的引入可能增加训练复杂度或超参数调优难度。
  - 对长视频、复杂运动、物理合理性、文本-视频对齐等关键问题的影响未在给定材料中说明。
  - “适用于任何 FM 模型”仍需实际兼容性与稳定性验证。
  - 若评估主要依赖展示页面或有限运动类型，可能存在选择偏差与泛化性风险。
  - 应用层面未讨论计算资源、版权、深度伪造等伦理与社会影响。

（完）
