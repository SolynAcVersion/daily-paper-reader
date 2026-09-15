---
title: Arbitrary Generative Video Interpolation
title_zh: 任意生成式视频插帧
authors: "Guozhen Zhang, Haiguang Wang, Chunyu Wang, Yuan Zhou, Qinglin Lu, Limin Wang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=eKGkb4cFRe"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 生成式视频插帧合成起止帧之间的中间帧
tldr: 现有生成式视频插帧方法只能生成固定数量的中间帧，限制了帧率与时长调节的灵活性。本文提出ArbInterp框架，通过时间戳感知旋转位置编码TaRoPE将生成帧对齐到目标归一化时间戳，从而实现任意时间戳、任意长度的插帧。实验表明该方法在保持高质量的同时提升了插帧的灵活性，为视频创作中的帧率与时长控制提供了新方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有生成式视频插帧只能生成固定数量的中间帧，难以灵活调整帧率或时长。
method: 提出ArbInterp框架与时间戳感知旋转位置编码TaRoPE，将生成帧对齐到目标归一化时间戳。
result: 实现任意时间戳、任意长度的高效插帧，提升视频创作中帧率与时长调节的灵活性。
conclusion: 为生成式视频插帧提供了灵活可控的时间建模方案。
---

## Abstract
Generative Video Frame Interpolation (VFI), which synthesizes intermediate frames from a given pair of start and end frames, plays a pivotal role in video creation. However, existing generative VFI methods are constrained to producing a fixed number of intermediate frames, which significantly limits the flexibility in adjusting the frame rate or duration of videos during the creation process. In this work, we present \textbf{ArbInterp}, a novel generative VFI framework that enables efficient interpolation at any timestamp and of any length. Specifically, to support interpolation at any timestamp, we propose the Timestamp-aware Rotary Position Embedding (TaRoPE), which modulates positions in temporal RoPE to align generated frames with target normalized timestamps. This design enables fine-grained control over frame timestamps, addressing the inflexibility of fixed-position paradigms in prior work. For any-length interpolation, we decompose long-sequence generation into segment-wise frame synthesis. We further design a novel appearance-motion decoupled conditioning strategy: it leverages prior segment endpoints to enforce appearance consistency and temporal semantics to maintain motion coherence, ensuring seamless spatiotemporal transitions across segments. Experimentally, we build comprehensive benchmarks for multi-scale frame interpolation (2× to 32×) to assess generalizability across arbitrary interpolation factors. Results show that ArbInterp outperforms prior methods across all scenarios with higher fidelity and more seamless spatiotemporal continuity. Video demos are provided on the website: https://mcg-nju.github.io/ArbInterp-Web.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 正文抓取失败（URL 返回 503，内容为 “no healthy upstream”），因此以下总结主要依据论文摘要与元数据，无法覆盖正文中的数据集名称、具体对比方法、训练算力、消融实验数量等细节。

## 1. 核心问题与整体含义
- **研究背景**：生成式视频插帧（Generative Video Frame Interpolation, VFI）旨在根据给定的起始帧和结束帧，合成中间帧，在视频创作中具有重要作用。
- **核心问题**：现有生成式 VFI 方法通常只能生成**固定数量**的中间帧，导致在视频创作过程中难以灵活调整帧率或视频时长。
- **整体含义**：论文提出 **ArbInterp**，希望突破固定帧数限制，实现“任意时间戳、任意长度”的生成式视频插帧，为视频帧率与时长控制提供更灵活的时间建模方案。

## 2. 方法论
### 核心思想
- 将插帧从“固定倍率/固定位置”扩展为“目标时间戳驱动”的生成问题。
- 支持两类灵活性：
  - **任意时间戳**：生成帧可对齐到任意归一化时间戳。
  - **任意长度**：可生成长序列中间帧，而不局限于固定数量。

### 关键技术细节
- **TaRoPE（Timestamp-aware Rotary Position Embedding）**：
  - 在时间旋转位置编码（temporal RoPE）中调制位置。
  - 使生成帧与目标归一化时间戳对齐。
  - 相比固定位置范式，可对帧时间戳进行细粒度控制。
- **任意长度插帧策略**：
  - 将长序列生成分解为**分段式帧合成**（segment-wise frame synthesis）。
  - 避免一次性生成长序列，降低建模难度。
- **外观-运动解耦条件策略**：
  - 利用前一段的端点帧作为条件，增强**外观一致性**。
  - 利用时间语义作为条件，维持**运动连贯性**。
  - 目标是保证跨段之间的时空过渡无缝。
- **文字化算法流程**：
  1. 输入起始帧、结束帧以及目标时间戳/目标长度。
  2. 对每个目标时间戳，使用 TaRoPE 调制时间位置，使生成帧对齐目标时间。
  3. 若需长序列插帧，则划分为多个片段，逐段生成。
  4. 每段生成时，结合前段端点保持外观一致，并结合时间语义保持运动连贯。
  5. 拼接各段结果，输出任意时间戳、任意长度的中间帧序列。

## 3. 实验设计
- **基准构建**：论文构建了面向**多尺度帧插帧**的综合基准，插帧倍率范围为 **2× 到 32×**。
- **评估目标**：评估方法在不同任意插帧因子下的泛化能力。
- **对比方法**：摘要称与先前方法进行比较，并在所有场景中取得更优结果；但未列出具体对比方法名称。
- **评价维度**：提到更高保真度（fidelity）和更无缝的时空连续性（seamless spatiotemporal continuity）。
- **数据集/场景**：摘要与元数据未明确说明使用了哪些数据集或具体视频场景。
- **定量指标**：未说明是否使用 PSNR、SSIM、LPIPS、FVD 等具体指标。

## 4. 资源与算力
- 提供的摘要与元数据中**未提及** GPU 型号、GPU 数量、训练时长、训练轮数或推理成本。
- 因此无法总结其算力资源使用情况，也无法判断训练与推理开销是否适合实际应用。

## 5. 实验数量与充分性
- 从摘要看，实验至少覆盖 **2× 到 32× 的多尺度插帧设置**，并声称在所有场景中优于先前方法。
- 但无法确认具体做了多少组实验，例如：
  - 使用了多少个数据集；
  - 有多少个基线方法；
  - 是否包含消融实验；
  - 是否报告不同时间戳、不同长度、不同分辨率下的细分结果。
- **充分性与公平性**：由于正文缺失，无法验证实验是否充分、客观、公平。摘要中的“所有场景均优于先前方法”需要具体数值、协议和统计结果支撑。

## 6. 主要结论与发现
- ArbInterp 能够实现**任意时间戳、任意长度**的高效生成式视频插帧。
- 通过 TaRoPE，模型可细粒度控制生成帧的时间位置。
- 通过分段生成与外观-运动解耦条件，长序列插帧在跨段时能保持较好的外观一致性和运动连贯性。
- 在多尺度插帧基准上，ArbInterp 相比先前方法取得更高保真度和更无缝的时空连续性。
- 整体上，为视频创作中的帧率与时长调节提供了灵活可控的新方案。

## 7. 优点
- **问题定义有价值**：突破传统生成式 VFI 只能生成固定数量中间帧的限制。
- **时间建模思路清晰**：TaRoPE 将时间位置编码与目标时间戳对齐，直接支持任意时间戳插帧。
- **长序列处理有针对性**：分段生成降低长序列建模难度，并通过外观-运动解耦条件缓解跨段不一致。
- **基准覆盖较广**：构建 2× 到 32× 的多尺度插帧基准，有利于评估任意插帧因子的泛化性。
- **论文状态较好**：元数据表明该工作为 ICLR 2026 接收论文，OpenReview 评分 7.0。

## 8. 不足与局限
- **正文信息缺失导致可验证性不足**：当前材料未提供数据集、对比方法、指标、算力、消融等关键细节。
- **“任意长度”可能带来累积误差**：分段生成虽可扩展长度，但跨段边界是否出现闪烁、漂移、身份变化，需要正文实验验证。
- **计算成本未说明**：长序列、高分辨率或实时场景下的推理效率、显存占用未知。
- **应用限制未讨论**：对极端运动、遮挡、新内容出现、复杂光照变化等困难场景的表现尚未说明。
- **实验公平性无法判断**：缺少基线实现细节、训练预算、评价协议和统计显著性分析。
- **宣传性结论需谨慎看待**：摘要称“所有场景优于先前方法”，但未给出具体数值，需结合正文与复现实验判断。

（完）
