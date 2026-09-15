---
title: Fast Block Attention Computation via Dynamic Algorithm
title_zh: 基于动态算法的快速块注意力计算
authors: "Yang Cao, Xuyang Guo, Zhao Song"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=iPCgCxmSR4"
tags: ["query:video-gen-rl"]
score: 4.0
evidence: 视频建模中时序帧依赖的注意力计算
tldr: 视频建模因token数量庞大，注意力机制成为主要计算瓶颈，朴素方法展平f帧n个token会产生O(n^2f^2)复杂度。本文提出一种动态算法计算块注意力，突破了以往方法仅在某一个维度较小时才能达到次二次复杂度、且依赖固定块划分的限制。该方法可加速视频Transformer中跨空间块与时序帧的依赖建模，为长视频建模提供更高效的计算基础。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频建模token量庞大，注意力机制成为主要计算瓶颈，现有次二次方法适用范围受限。
method: 提出一种动态算法高效计算块注意力，突破单一维度较小的限制。
result: 方法降低了跨空间块与时序帧注意力的计算成本。
conclusion: 为长视频建模提供了更高效的注意力计算基础。
---

## Abstract
Recent progress in video modeling has been largely driven by Transformer architectures, which simulate dependency relationships across spatial patches and temporal frames. However, compared to text or image modeling, video modeling involves orders of magnitude more tokens, resulting in an input sequence several orders of magnitude longer than typical NLP or image tasks, and makes the attention mechanism the primary computational bottleneck. The naive method flattens $f$ frames of $n$ tokens each into length $N = nf$, incurring total $O(n^2f^2)$ attention cost.
Prior work (e.g., radial/axial variants) attains subquadratic time only when either the spatial or temporal dimension is small. We present a dynamic algorithm that computes block attention in $O(\mathcal{T}_\mathrm{mat}
(n,n,n^a) \frac{f}{n^{a}})$ amortized running time, where $a \in [0,1)$.

---

## 论文详细总结（自动生成）

## 说明

- 当前可获取的论文内容仅为标题、元数据与摘要；PDF 正文抓取失败（503 / no healthy upstream）。
- 因此，实验设计、数据集、算力、对比方法、实验数量等正文信息无法确认。以下总结严格区分“摘要/元数据明确信息”与“未提供/无法判断”。

## 1. 论文的核心问题与整体含义

- **研究背景**：视频建模近年主要由 Transformer 架构推动，需要建模空间 patch 与时序帧之间的依赖关系。
- **核心问题**：视频 token 数量远大于文本或图像任务，输入序列长度可达数量级增长，导致注意力机制成为主要计算瓶颈。
- **朴素做法**：将 \(f\) 帧、每帧 \(n\) 个 token 展平为长度 \(N = nf\)，注意力计算成本为 \(O(n^2 f^2)\)。
- **现有方法局限**：已有径向/轴向变体等次二次方法，通常只在空间维度或时间维度之一较小时才有效，且依赖固定块划分。
- **整体含义**：论文试图提出一种动态算法，高效计算跨空间块与时序帧的块注意力，为长视频建模提供更高效的注意力计算基础。

## 2. 论文提出的方法论

- **核心思想**：提出一种动态算法来计算块注意力，突破以往方法“仅某一维度较小才能次二次”以及“固定块划分”的限制。
- **问题设定**：
  - 输入可视为 \(f\) 帧，每帧 \(n\) 个 token。
  - 朴素展平后序列长度为 \(N = nf\)。
  - 注意力总成本为 \(O(n^2 f^2)\)。
- **目标场景**：加速视频 Transformer 中跨空间块与时序帧的依赖建模。
- **复杂度声明**：
  - 论文提出 amortized running time 为  
    \[
    O\left(\mathcal{T}_{\mathrm{mat}}(n,n,n^a)\frac{f}{n^a}\right),\quad a \in [0,1)
    \]
  - 其中 \(\mathcal{T}_{\mathrm{mat}}\) 应表示矩阵乘法相关时间复杂度。
  - \(a\) 为可调参数，暗示算法可根据块规模或维度动态调整。
  - 该复杂度试图避免朴素方法的 \(O(n^2 f^2)\)。
- **技术细节限制**：摘要未给出具体算法流程、块划分策略、动态规划/分治过程、数据结构或伪代码，因此无法进一步还原实现步骤。

## 3. 实验设计

- **数据集 / 场景**：
  - 摘要与元数据未列出任何具体数据集。
  - 元数据 tags 为 `video-gen-rl`，evidence 提到“视频建模中时序帧依赖的注意力计算”，因此可推测任务场景与视频建模、视频生成或强化学习相关，但这不是正文实验证据。
- **Benchmark**：
  - 未提及。
- **对比方法**：
  - 摘要仅将 radial/axial variants 作为已有工作进行理论背景描述。
  - 未说明实验中是否对比这些方法，也未列出任何 baseline。
- **评价指标**：
  - 未提及准确率、吞吐量、显存、实际加速比、FLOPs 或长视频生成质量等指标。
- **结论**：当前可获取内容不足以总结实验设计。

## 4. 资源与算力

- 未提及 GPU 型号、GPU 数量、训练时长、参数量、推理成本或实验集群规模。
- 若论文偏理论/算法复杂度分析，可能没有大规模训练实验；但当前信息无法确认。
- 因此，算力资源无法总结。

## 5. 实验数量与充分性

- 摘要和元数据未给出任何实验组数、消融实验、数据集数量或对比实验数量。
- 无法判断实验是否充分、是否客观、是否公平。
- 目前仅能确认论文给出了理论复杂度声明；但该复杂度是否在真实视频 Transformer 中带来实际加速，缺少可验证信息。
- 若正文没有实验，则实证充分性不足；若正文有实验但未被抓取，则当前无法评估。

## 6. 论文的主要结论与发现

- 提出一种动态算法，用于高效计算块注意力。
- 该算法在均摊意义下达到  
  \[
  O\left(\mathcal{T}_{\mathrm{mat}}(n,n,n^a)\frac{f}{n^a}\right)
  \]
  的复杂度，其中 \(a \in [0,1)\)。
- 相比朴素方法的 \(O(n^2 f^2)\)，该复杂度有望降低跨空间块与时序帧注意力的计算成本。
- 方法突破以往次二次注意力方法对“某一维度必须较小”和“固定块划分”的依赖。
- 最终目标是为长视频建模提供更高效的注意力计算基础。

## 7. 优点

- **理论动机清晰**：直接针对视频建模中 token 数量爆炸、注意力成为瓶颈的问题。
- **复杂度改进有针对性**：从朴素 \(O(n^2 f^2)\) 出发，提出均摊次二次/更优的块注意力计算。
- **突破现有局限**：不要求空间或时间维度之一很小，也不依赖固定块划分。
- **面向长视频建模**：若理论结果可落地，将对长视频 Transformer 的计算效率有实际意义。
- **参数化设计**：复杂度含可调参数 \(a \in [0,1)\)，可能提供灵活性。

## 8. 不足与局限

- **正文不可获取**：PDF 返回 503，当前总结主要依赖摘要和元数据，信息严重受限。
- **缺少实验验证**：未提供数据集、benchmark、baseline、评价指标和实验结果，无法判断实际加速效果。
- **算法细节不足**：摘要未说明动态块划分如何实现、如何选择 \(a\)、常数因子和内存开销如何。
- **理论复杂度需条件**：复杂度依赖 \(\mathcal{T}_{\mathrm{mat}}\) 的假设，实际性能可能受矩阵乘法实现、块大小和硬件影响。
- **应用限制**：主要面向视频 Transformer 的块注意力；对非规则视频、不同帧率、长时序依赖的泛化能力未知。
- **公平性无法判断**：没有对比方法和实验设置，无法评估与 radial/axial 等方法的公平比较。
- **偏差风险**：元数据来源为 ICLR-2026-Public，且 score 为 4.0，但该评分含义未说明，不能作为论文质量结论。

（完）
