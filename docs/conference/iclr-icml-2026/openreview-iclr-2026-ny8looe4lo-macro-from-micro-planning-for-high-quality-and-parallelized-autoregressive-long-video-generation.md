---
title: Macro-from-Micro Planning for High-Quality and Parallelized Autoregressive Long Video Generation
title_zh: 面向高质量与并行化自回归长视频生成的宏观来自微观规划
authors: "Xunzhi Xiang, Yabo Chen, Guiyu Zhang, Zhongyu Wang, Zhe Gao, Quanming Xiang, Gonghu Shang, Junqi Liu, Haibin Huang, Yang Gao, Chi Zhang, Qi Fan, Xuelong Li"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=nY8looE4lO"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 自回归长视频生成预测未来关键帧
tldr: 自回归扩散模型擅长视频生成但通常局限于较短时长，理论分析表明其受误差累积导致的时间漂移影响，且难以并行化。本文提出以宏观来自微观规划（MMPL）为核心的先规划后填充框架，通过微观规划与宏观规划两个层级阶段为整段视频勾勒全局故事线，微观规划预测各短片段的稀疏关键帧提供运动与外观先验。该框架提升了长视频生成的画质并实现并行化。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 自回归扩散视频模型受误差累积导致的时间漂移影响，时长受限且难以并行化。
method: 提出先规划后填充框架MMPL，以微观规划预测关键帧先验、宏观规划勾勒全局故事线。
result: 该方法提升了长视频生成质量并实现了并行化生成。
conclusion: 为高质量长视频合成提供了分层规划的新思路。
---

## Abstract
Current autoregressive diffusion models excel at video generation but are generally limited to short temporal durations. Our theoretical analysis indicates that the autoregressive modeling typically suffers from temporal drift caused by error accumulation and hinders parallelization in long video synthesis. To address these limitations, we propose a novel planning-then-populating framework centered on Macro-from-Micro Planning (MMPL) for long video generation. MMPL sketches a global storyline for the entire video through two hierarchical stages: Micro Planning and Macro Planning. Specifically, Micro Planning predicts a sparse set of future keyframes within each short video segment, offering motion and appearance priors to guide high-quality video segment generation. Macro Planning extends the in-segment keyframes planning across the entire video through an autoregressive chain of micro plans, ensuring long-term consistency across video segments. Subsequently, MMPL-based Content Populating generates all intermediate frames in parallel across segments, enabling efficient parallelization of autoregressive generation. The parallelization is further optimized by Adaptive Workload Scheduling for balanced GPU execution and accelerated autoregressive video generation. Extensive experiments confirm that our method outperforms existing long video generation models in quality and stability. Generated videos and comparison results are in the Anonymous Demo page.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本仅包含标题、作者、元数据、TLDR 与 Abstract，正文、实验细节、公式和算力信息均未出现。以下总结主要基于这些有限信息，未提供的内容将明确标注为“未说明/无法判断”。

## 1. 核心问题与整体含义

- **研究背景**：当前自回归扩散模型在视频生成方面表现优秀，但通常只能生成较短时长的视频，难以直接扩展到长视频合成。
- **核心问题**：
  - 自回归建模存在**误差累积**，导致长视频生成中的**时间漂移**，影响长期一致性。
  - 自回归逐帧/逐段生成模式天然偏串行，**难以并行化**，限制长视频生成效率。
- **整体含义**：论文试图同时解决长视频生成的“质量/稳定性”与“并行化效率”问题，提出一种“先规划后填充”的框架，为高质量、可并行化的自回归长视频生成提供新思路。
- **元数据信息**：该论文被标注为 ICLR-2026-Rejected-Public，score 为 7.0；具体审稿意见与拒稿原因未提供。

## 2. 方法论

- **核心思想**：提出 **Macro-from-Micro Planning（MMPL）**，即“宏观来自微观规划”，采用 **planning-then-populating** 框架：先为整段视频规划全局故事线，再并行填充中间帧。
- **两个层级规划阶段**：
  - **Micro Planning（微观规划）**：在每个短视频片段内部预测一组稀疏的未来关键帧，为后续高质量视频片段生成提供**运动先验**和**外观先验**。
  - **Macro Planning（宏观规划）**：通过微观规划的自回归链，将片段内的关键帧规划扩展到整个视频，形成全局故事线，以保证跨视频片段的**长期一致性**。
- **内容填充**：
  - 基于 MMPL 的 **Content Populating** 阶段，跨片段并行生成所有中间帧。
  - 这样可在保持自回归规划能力的同时，实现自回归视频生成的并行化。
- **并行优化**：
  - 使用 **Adaptive Workload Scheduling** 平衡 GPU 执行负载，加速自回归视频生成。
- **文字化算法流程**：
  1. 对每个短片段进行微观规划，预测稀疏关键帧；
  2. 通过自回归链串联各片段微观规划，形成宏观全局规划；
  3. 依据关键帧先验，并行填充各片段中间帧；
  4. 通过自适应负载调度优化 GPU 并行执行。
- **注意**：提取文本未给出具体公式、网络结构、损失函数或训练细节。

## 3. 实验设计

- **数据集/场景**：未说明。提取文本未列出任何数据集名称、视频领域或评测场景。
- **Benchmark**：未说明。摘要仅称“extensive experiments”，但没有给出具体 benchmark 或评价指标。
- **对比方法**：摘要称与“existing long video generation models”比较，但未列出具体基线模型名称。
- **结果展示**：提到生成视频和对比结果位于匿名 Demo 页面，但当前提取文本无法访问该页面。

## 4. 资源与算力

- 提取文本与元数据中**未提及** GPU 型号、GPU 数量、训练时长、参数量、推理成本或显存开销等算力信息。
- 因此无法总结其资源消耗与训练/推理规模。

## 5. 实验数量与充分性

- 仅能从摘要确认作者声称进行了“Extensive experiments”，但**无法确定具体实验组数**。
- 未提供：
  - 数据集数量与规模；
  - 消融实验设置；
  - 与基线的定量对比表；
  - 人工评估或用户研究细节；
  - 并行化加速比、稳定性指标等。
- 因此，实验是否充分、客观、公平，**无法基于现有文本判断**。需要全文、附录和审稿意见才能评估。

## 6. 主要结论与发现

- 自回归扩散视频生成受误差累积影响，会产生时间漂移，并阻碍长视频合成中的并行化。
- 通过 MMPL 的微观规划与宏观规划，可以为整段视频勾勒全局故事线，并利用稀疏关键帧先验提升片段生成质量。
- 基于 MMPL 的内容填充可实现跨片段并行生成，结合自适应负载调度可加速自回归视频生成。
- 作者声称该方法在长视频生成的**质量**和**稳定性**上优于现有长视频生成模型。
- 该框架为高质量长视频合成提供了**分层规划**的新思路。

## 7. 优点

- **问题定位清晰**：直接指出自回归长视频生成的两个关键瓶颈：误差累积导致的时间漂移，以及并行化困难。
- **分层规划思路新颖**：Micro Planning 负责局部关键帧先验，Macro Planning 负责全局一致性，兼顾局部质量与长期连贯。
- **先规划后填充**：将规划与生成解耦，有助于跨片段并行填充，缓解自回归串行瓶颈。
- **工程优化意识**：引入 Adaptive Workload Scheduling，关注 GPU 负载平衡与实际加速。
- **有理论分析动机**：摘要提到理论分析支持其对时间漂移和并行化问题的判断，增强动机说服力。

## 8. 不足与局限

- **信息严重不足**：当前提取文本只有摘要和元数据，无法核验方法细节、公式、网络设计、训练策略与实验数据。
- **实验透明度不足**：未提供数据集、指标、基线、消融、定量结果和失败案例，难以判断泛化性与公平性。
- **算力与效率未说明**：没有 GPU 型号、数量、训练时长、推理开销或加速比，无法评估实际部署成本。
- **元数据提示被拒**：标注为 ICLR-2026-Rejected-Public，score 7.0；若准确，说明论文曾获中等偏上评分但最终未接收，具体原因未知。
- **潜在应用限制**：长视频生成本身计算昂贵；MMPL 增加规划阶段可能带来额外开销，且关键帧规划质量可能直接影响最终生成效果，但文本未讨论这些风险。
- **可复现性未知**：未说明代码、模型或 Demo 是否公开，匿名 Demo 页面在当前提取文本中无法访问。

（完）
