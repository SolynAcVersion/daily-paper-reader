---
title: Streaming Autoregressive Video Generation via Diagonal Distillation
title_zh: 基于对角蒸馏的流式自回归视频生成
authors: "Jinxiu Liu, Xuanming Liu, Kangfu Mei, Yandong Wen, Ming-Hsuan Yang, Weiyang Liu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=X7YW6STzeL"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 自回归流式视频生成，强调时序依赖与运动连贯性
tldr: 大扩散模型提升了视频质量，但实时流式生成仍受限。自回归模型适合顺序合成帧，却需大量计算；现有视频蒸馏多沿用图像方法而忽视时序依赖，导致运动连贯性下降与误差累积。本文提出对角线蒸馏方法，针对时序依赖进行压缩。实验表明该方法在保持高保真度的同时提升流式生成效率与运动连贯性，为实时视频生成提供了方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频蒸馏多沿用图像方法忽视时序依赖，导致运动连贯性下降与误差累积。
method: 提出对角线蒸馏方法，针对时序依赖压缩扩散模型以实现流式自回归生成。
result: 在保持高保真度的同时提升流式生成效率与运动连贯性。
conclusion: 为实时流式视频生成提供了高效蒸馏方案。
---

## Abstract
Large pretrained diffusion models have significantly enhanced the quality of generated videos, and yet their use in real-time streaming remains limited. Autoregressive models offer a natural framework for sequential frame synthesis but require heavy computation to achieve high fidelity. Diffusion distillation can compress these models into efficient few-step variants, but existing video distillation approaches largely adapt image-specific methods that neglect temporal dependencies. These techniques often excel in image generation but underperform in video synthesis, exhibiting reduced motion coherence, error accumulation over long sequences, and a latency-quality trade-off. We identify two factors that result in these limitations: insufficient utilization of temporal context during step reduction and implicit prediction of subsequent noise levels in next-chunk prediction (i.e., exposure bias). To address these issues, we propose Diagonal Distillation, which operates orthogonally to existing approaches and better exploits temporal information across both video chunks and denoising steps. Central to our approach is an asymmetric generation strategy: more steps early, fewer steps later. This design allows later chunks to inherit rich appearance information from thoroughly processed early chunks, while using partially denoised chunks as conditional inputs for subsequent synthesis. By aligning the implicit prediction of subsequent noise levels during chunk generation with the actual inference conditions, our approach mitigates error propagation and reduces oversaturation in long-range sequences. We further incorporate implicit optical flow modeling to preserve motion quality under strict step constraints. Our method generates a 5-second video in 2.61 seconds (up to 31 FPS), achieving a 277.3× speedup over the undistilled model.

---

## 论文详细总结（自动生成）

# 论文总结：基于对角蒸馏的流式自回归视频生成

> 说明：提供的 PDF 提取失败（503 Service Unavailable），因此以下总结主要依据论文摘要与 OpenReview 元数据；正文中的公式、完整实验设置、数据集、算力等细节无法从当前材料确认。

## 1. 核心问题与整体含义

- **背景**：大型预训练扩散模型显著提升了视频生成质量，但难以用于实时流式生成。
- **矛盾**：自回归模型天然适合逐帧/逐块顺序合成视频，但高保真生成需要大量计算，实时性受限。
- **现有蒸馏的不足**：视频扩散蒸馏多沿用图像领域的少步蒸馏方法，忽视视频中的时序依赖，导致：
  - 运动连贯性下降；
  - 长序列误差累积；
  - 延迟与质量之间难以平衡。
- **作者识别的两个关键原因**：
  - 在减少去噪步数时，没有充分利用时序上下文；
  - 在下一视频块预测中，模型隐式预测后续噪声水平，产生 **exposure bias**，即训练与推理条件不一致。
- **整体含义**：论文提出 **Diagonal Distillation（对角蒸馏）**，与现有方法正交，旨在更好利用跨视频块和跨去噪步的时序信息，为实时流式自回归视频生成提供高效蒸馏方案。

## 2. 方法论：核心思想与关键技术

- **核心思想**：对角蒸馏不简单套用图像蒸馏，而是同时利用“视频块之间”和“去噪步骤之间”的时序信息，压缩扩散模型以实现少步流式生成。
- **非对称生成策略**：
  - 早期视频块使用较多去噪步；
  - 后续视频块使用较少去噪步；
  - 后续块可继承早期充分处理块中的丰富外观信息；
  - 部分去噪的视频块被用作后续合成的条件输入。
- **缓解 exposure bias**：
  - 对齐视频块生成过程中“后续噪声水平的隐式预测”与“实际推理条件”；
  - 从而减少误差传播，并缓解长序列中的过饱和问题。
- **隐式光流建模**：
  - 在严格限制去噪步数的情况下，引入隐式光流建模以保持运动质量。
- **算法流程概述**：
  - 将视频按块自回归生成；
  - 对早期块进行较充分去噪，对后期块减少步数；
  - 后续块以早期高质量块和当前部分去噪块为条件；
  - 训练时使模型预测的噪声水平与真实推理条件一致；
  - 联合光流约束，保持运动连贯性。
- **注意**：当前材料未给出具体公式、损失函数或伪代码，无法进一步展开数学细节。

## 3. 实验设计

- 当前摘要与元数据 **未列出具体数据集、场景或 benchmark**。
- **未说明对比了哪些方法**，也未说明是否与图像蒸馏迁移方法、其他视频蒸馏方法或未蒸馏模型进行系统比较。
- 摘要中报告的核心结果：
  - 生成 5 秒视频仅需 **2.61 秒**；
  - 最高达到 **31 FPS**；
  - 相比未蒸馏模型实现 **277.3× 加速**。
- 元数据称方法在保持高保真度的同时，提升了流式生成效率与运动连贯性，但缺少定量指标、评测协议和基线细节。

## 4. 资源与算力

- 当前材料 **未提及** GPU 型号、数量、训练时长、显存占用或推理硬件。
- 因此无法总结训练与推理的算力成本，也无法判断 31 FPS 和 277.3× 加速是在何种硬件条件下取得。

## 5. 实验数量与充分性

- 当前材料无法确认实验组数，包括：
  - 使用了多少数据集；
  - 是否进行了消融实验；
  - 是否评估长序列、复杂运动、不同分辨率或不同视频长度；
  - 是否有人类主观评价或用户研究。
- 摘要仅报告了一个端到端效率结果和若干定性结论。
- 因此，从现有材料看，**实验充分性、客观性与公平性无法评估**；缺少基线设置、评价指标、统计显著性和消融证据。

## 6. 主要结论与发现

- 对角蒸馏能够针对视频时序依赖进行压缩，支持流式自回归视频生成。
- 非对称步数分配有助于后续视频块继承早期块的外观信息，并缓解误差累积与过饱和。
- 对齐后续噪声水平预测可减轻 exposure bias。
- 隐式光流建模有助于在严格步数限制下保持运动质量。
- 方法实现了 5 秒视频 2.61 秒生成、最高 31 FPS、277.3× 加速，为实时流式视频生成提供了可行方案。

## 7. 优点

- **问题定位清晰**：明确指出视频蒸馏不能简单照搬图像蒸馏，时序依赖是关键。
- **方法有针对性**：非对称生成、跨块条件、噪声水平对齐、隐式光流建模均直接回应运动连贯性与误差累积问题。
- **效率提升显著**：277.3× 加速和 31 FPS 表明其接近实时生成目标。
- **与现有方法正交**：对角蒸馏可能可与已有蒸馏或自回归生成框架结合。
- **关注实际痛点**：长序列误差传播、过饱和、延迟-质量权衡都是流式视频生成中的核心难题。

## 8. 不足与局限

- **材料严重不足**：PDF 提取失败，无法验证方法公式、训练目标和实现细节。
- **实验信息缺失**：数据集、benchmark、对比方法、评价指标、消融实验均未在现有材料中说明。
- **算力未报告**：无法评估训练成本、推理硬件依赖和复现难度。
- **公平性未知**：无法确认加速比是否在同等模型规模、同等硬件和同等质量条件下取得。
- **应用限制未知**：长视频漂移、复杂运动、多物体交互、不同分辨率下的表现尚不可知。
- **偏差风险**：当前总结仅基于摘要与元数据，可能存在选择性报告；31 FPS 与 277.3× 加速的具体条件需完整论文确认。
- **总体判断**：论文思路有吸引力，但需完整正文与实验细节才能客观评估其有效性、泛化性和可复现性。

（完）
