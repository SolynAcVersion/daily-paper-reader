---
title: Temporal-aware Flow Matching for Video Generation with Temporally Coherent Motion
title_zh: 面向时序连贯运动的视频生成时序感知流匹配
authors: "Zirui Pan, Xin Wang, Yipeng Zhang, Yuwei Zhou, Wenwu Zhu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/2353dd72ba2db602d82f7e1a530e20640cd45ad5.pdf"
tags: ["query:video-gen-rl"]
score: 9.0
evidence: 时序感知流匹配嵌入帧间约束实现连贯运动
tldr: 当前文本到视频生成模型常产生时序不连贯、不真实的运动，根源在于将视频视为帧序列并直接套用为图像设计的流匹配目标，未显式建模运动先验与时间依赖。本文提出时序感知流匹配TFM，将帧间约束嵌入流匹配目标，实现视频生成中时间连贯的运动建模。实验表明该方法改善了运动动力学的一致性与真实性，为帧间分布关系建模提供了有效训练范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频生成把视频当作帧序列直接套用为图像设计的流匹配目标，导致运动时序不连贯。
method: 提出时序感知流匹配TFM，将帧间约束嵌入流匹配目标，显式建模运动先验与时间依赖。
result: 方法生成的运动在时间上更连贯、更真实，改善了动力学建模质量。
conclusion: 帧间约束建模为连贯视频生成提供了有效训练范式。
---

## Abstract
Despite rapid advances in text-to-video generation, state-of-the-art generative models still suffer from producing temporally incoherent and unrealistic motion for videos. The key weakness of existing works is that they commonly treat videos as frame sequences and directly adopt Flow Matching (FM) objectives, which are originally designed for images. This practice fails to explicitly model motion priors or temporal dependencies, resulting in suboptimal dynamics that may appear incoherent and unrealistic. To solve this problem, we propose Temporal-aware Flow Matching (TFM), a novel training paradigm that embeds inter-frame constraints into the flow objective, leading to temporally coherent motion modeling in video generation. More specifically, the proposed TFM enforces temporal correlations across frames while retaining the desirable properties of FM, and further introduces a residual-type loss that aligns naturally with this new flow. We theoretically prove that models trained with TFM are able to exhibit remarkably enhanced temporal perception ability. Notably, TFM imposes no additional cost during inference and is applicable to any model using FM. Extensive experiments demonstrate that our TFM can significantly improve motion realism across diverse motion types. Generated videos are presented at https://pzrain.github.io/tfm.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
时序感知流匹配嵌入帧间约束实现连贯运动。

### 2. 核心内容
当前文本到视频生成模型常产生时序不连贯、不真实的运动，根源在于将视频视为帧序列并直接套用为图像设计的流匹配目标，未显式建模运动先验与时间依赖。本文提出时序感知流匹配TFM，将帧间约束嵌入流匹配目标，实现视频生成中时间连贯的运动建模。实验表明该方法改善了运动动力学的一致性与真实性，为帧间分布关系建模提供了有效训练范式。

### 3. 对应检索需求
maintaining inter-frame coherence in video generation。

### 4. 来源与原文
- Source：ICML-2026-Accepted
- OpenReview：[https://openreview.net/forum?id=hPIOKm727h](https://openreview.net/forum?id=hPIOKm727h)
