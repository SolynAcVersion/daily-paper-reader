---
title: Learning Adaptive and Temporally Causal Video Tokenization in a 1D Latent Space
title_zh: 在一维隐空间中学习自适应且时序因果的视频分词
authors: "Yan Li, Changyao Tian, Renqiu Xia, Ning Liao, Weiwei Guo, Junchi Yan, Hongsheng Li, Jifeng Dai, Hao Li, Xue Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=dkLto1KNFV"
tags: ["query:video-gen-rl"]
score: 6.0
evidence: 面向重建与生成的自适应时序因果视频分词
tldr: 视频分词通常在帧间统一分配令牌，难以适应内容差异。本文提出AdapTok，一种自适应时序因果视频分词器，训练时用块状掩码随机丢弃尾部令牌，并用块因果评分器预测不同令牌数下的重建质量，推理时用整数线性规划动态分配令牌。实验在视频重建与生成上验证了其在可控预算下的内容自适应分配能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频分词对不同帧统一分配令牌，无法适应内容差异。
method: 提出AdapTok自适应时序因果分词器，结合块掩码、因果评分器与整数线性规划分配令牌。
result: 在UCF-101与Kinetics-600上验证了重建与生成中的内容自适应令牌分配效果。
conclusion: 为视频生成提供了可控预算下的自适应时序分词方案。
---

## Abstract
We propose AdapTok, an adaptive temporal causal video tokenizer that can flexibly allocate tokens for different frames based on video content. AdapTok is equipped with a block-wise masking strategy that randomly drops tail tokens of each block during training, and a block causal scorer to predict the reconstruction quality of video frames using different numbers of tokens. During inference, an adaptive token allocation strategy based on integer linear programming is further proposed to adjust token usage given predicted scores. Such design allows for sample-wise, content-aware, and temporally dynamic token allocation under a controllable overall budget. Extensive experiments for video reconstruction and generation on UCF-101 and Kinetics-600 demonstrate the effectiveness of our approach. Without additional image data, AdapTok consistently improves reconstruction quality and generation performance under different token budgets, allowing for more scalable and token-efficient generative video modeling.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本实际为 “no healthy upstream”，未能获取论文正文；以下总结主要依据论文元数据、TLDR 与摘要信息。因此，方法公式、实验细节、算力资源等内容只能基于已有信息概括，未明确处将标注为“未提供/无法确认”。

# 论文总结：Learning Adaptive and Temporally Causal Video Tokenization in a 1D Latent Space

## 1. 核心问题与整体含义
- **研究背景**：视频分词/视频 tokenization 是生成式视频建模的关键环节，目标是将视频压缩为 latent token 序列，以便后续重建或生成。
- **核心问题**：现有视频分词方法通常在不同帧之间**统一分配令牌数量**，无法适应视频内容的时序差异与复杂度变化，导致 token 预算利用效率不高。
- **整体含义**：论文提出 **AdapTok**，一种自适应、时序因果的视频分词器，能够在一维隐空间中根据视频内容为不同帧灵活分配 token，从而在可控总预算下提升视频重建与生成效果。
- **目标价值**：实现 sample-wise、content-aware、temporally dynamic 的 token 分配，使生成式视频建模更可扩展、更 token-efficient。

## 2. 方法论
- **核心思想**：
  - 不同视频帧或片段对重建/生成的贡献不同，因此不应统一分配 token。
  - 在总 token 预算约束下，动态决定每帧或每块使用多少 token。
  - 保持时序因果性，并在一维 latent space 中完成视频分词。
- **关键技术细节**：
  - **Block-wise masking**：训练时对每个块随机丢弃尾部 token，模拟不同 token 数量下的输入条件，使 tokenizer 适应可变 token 预算。
  - **Block causal scorer**：预测视频帧在使用不同数量 token 时的重建质量，为后续 token 分配提供依据。
  - **整数线性规划分配**：推理时，根据 scorer 预测分数，用整数线性规划在整体预算约束下调整各块/帧的 token 使用量。
- **算法流程文字说明**：
  1. 将视频按块进行时序因果分词。
  2. 训练阶段通过块状掩码随机丢弃尾部 token，让模型见到不同 token 预算下的重建任务。
  3. 训练块因果评分器，预测不同 token 数对应的重建质量。
  4. 推理阶段，评分器给出各块在不同 token 数下的质量预测。
  5. 整数线性规划在总预算约束下选择每块 token 数，实现内容自适应、时序动态分配。
- **未提供信息**：具体网络结构、损失函数、评分器形式、ILP 目标函数与约束、训练细节等，因正文缺失无法确认。

## 3. 实验设计
- **数据集/场景**：
  - **UCF-101**
  - **Kinetics-600**
- **任务**：
  - 视频重建
  - 视频生成
- **Benchmark**：元数据表明在 UCF-101 与 Kinetics-600 上验证重建与生成中的内容自适应 token 分配效果；但具体评价指标、实验协议未提供。
- **对比方法**：摘要提到在不同 token budget 下，AdapTok 均能提升重建质量与生成性能，且无需额外图像数据；但具体 baseline 名称、对比设置未在现有材料中列出。
- **可能对比方向**：可推测与固定 token 分配或统一帧级分配方法比较，但无法从现有信息确认。

## 4. 资源与算力
- 提供的材料中**未提及 GPU 型号、数量、训练时长、参数量、训练成本或推理开销**。
- 因此无法总结算力资源；需要查阅原文或附录。
- 仅可确认：论文强调 token 效率与可控预算，但未给出实际计算资源数据。

## 5. 实验数量与充分性
- 从现有信息看，实验至少覆盖：
  - 2 个数据集：UCF-101、Kinetics-600。
  - 2 类任务：视频重建、视频生成。
  - 多个 token budget 设置。
- **消融实验**：是否对 block-wise masking、block causal scorer、ILP 分配策略分别做消融，现有材料未说明。
- **充分性判断**：
  - 在给定信息下，实验覆盖了常用视频重建/生成数据集和不同预算条件，具有一定针对性。
  - 但缺少具体实验组数、对比方法、指标数值、统计显著性和公平性设置，无法完全判断实验是否充分、客观、公平。
  - 由于正文抓取失败，不能验证是否存在数据泄漏、预训练依赖或计算资源不对等等问题。

## 6. 主要结论与发现
- AdapTok 能在**可控总 token 预算**下，实现样本级、内容感知、时序动态的 token 分配。
- 在 UCF-101 与 Kinetics-600 上，视频重建质量和生成性能均有提升。
- 无需额外图像数据即可在不同 token budget 下持续改进，说明方法具有较好的 token 效率与可扩展性。
- 验证了自适应、时序因果视频分词在生成式视频建模中的有效性。

## 7. 优点
- **问题切入准确**：打破帧间统一 token 分配，利用视频内容差异进行自适应分配。
- **方法设计闭环**：训练时块掩码模拟可变预算，评分器预测重建质量，推理时 ILP 做预算约束分配。
- **可控预算**：适合实际生成场景中对计算、带宽或 token 数的限制。
- **时序因果 + 1D latent**：与自回归视频生成、时序建模方向兼容。
- **实验方向合理**：覆盖 UCF-101 与 Kinetics-600 的重建和生成任务，并强调不同 token budget。
- **无需额外图像数据**：摘要明确这一点，有利于公平比较与扩展应用。

## 8. 不足与局限
- **全文缺失导致信息不完整**：无法核实具体公式、网络结构、训练损失、ILP 细节和实验配置。
- **实验覆盖有限**：仅提及 UCF-101 与 Kinetics-600，未涉及更复杂、长视频、高分辨率或开放域场景。
- **公平性无法判断**：未列出具体 baseline、评价指标、训练资源与预训练依赖。
- **推理开销未知**：ILP 可能带来额外优化成本，是否满足实时或大规模生成需求尚不明确。
- **评分器依赖风险**：自适应分配依赖 block causal scorer 的质量预测，若预测偏差可能影响 token 分配效果。
- **应用限制未知**：是否适用于不同压缩率、不同视频长度、不同生成模型架构，现有材料无法确认。
- **元数据评分 6.0**：说明论文在评审中获得中等偏上评价，但具体争议点需结合全文与审稿意见判断。

（完）
