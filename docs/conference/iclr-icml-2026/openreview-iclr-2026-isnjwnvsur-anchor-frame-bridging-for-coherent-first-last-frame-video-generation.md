---
title: Anchor Frame Bridging for Coherent First-Last Frame Video Generation
title_zh: 面向连贯首尾帧视频生成的锚帧桥接
authors: "Xuehan Hou, Meng Fan, Pengchong Qiao, Zesen Cheng, Yian Zhao, Lei Zhu, Kaiwen Cheng, Chang Liu, Jie Chen"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=isNjWnVsUR"
tags: ["query:frame-dist"]
score: 6.0
evidence: 将语义连续性桥接到中间帧以保持时序一致
tldr: 针对首尾帧视频生成中中间帧语义退化、场景扭曲和主体变形破坏时序一致性的问题，本文提出即插即用的锚帧桥接方法AFB。该方法在语义不连续性最大的时间关键位置自适应地插入锚帧，显式地将边界帧的语义连续性桥接到中间帧，无需训练即可通用。研究有效缓解了中间帧的语义漂移，为帧间语义与分布连续性的建模提供了思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 首尾帧视频生成的中间帧易出现语义退化，破坏时序一致性。
method: 提出即插即用AFB，在语义不连续关键位置自适应插入锚帧。
result: 有效缓解中间帧语义漂移，提升帧间语义连续性。
conclusion: 为帧间语义与分布连续性的建模提供了免训练思路。
---

## Abstract
First-last frame video generation has recently gained significant attention. It enables coherent motion generation between specified first and last frames. However, this approach suffers from semantic degradation in intermediate frames, causing scene distortion and subject deformation that undermine temporal consistency.
 To address this issue, we introduce Anchor Frame Bridging (AFB), a novel plug-and-play method that explicitly bridges semantic continuity from boundary frames to intermediate frames, offering training-free adaptability and generalizability. By adaptively interpolating anchor frames at temporally critical locations exhibiting maximal semantic discontinuities, our approach effectively mitigates semantic drift in intermediate frames. Specifically, we propose an adaptive anchor frame selection module, which generates text-aligned candidate frames via frame order reversal and selects anchors based on semantic continuity. Subsequently, we develop anchor frame guided generation, which leverages the selected anchor frames to guide semantic propagation across intermediate frames, ensuring consistent boundary semantics and preserving temporal coherence throughout the video sequence. The final video is synthesized using the first frame, last frame, selected anchor frames, and the text prompt.
 The results demonstrate that our method significantly enhances the temporal consistency and overall quality of generated videos. Specifically, when applied to the Wan2.1-I2V model, it yields improvements of 16.58\% in FVD and 10.21\% in PSNR. The codes are provided in the supplementary material.

---

## 论文详细总结（自动生成）

# 论文总结：Anchor Frame Bridging for Coherent First-Last Frame Video Generation

> 说明：当前可获取的论文文本仅为标题、元数据与摘要，正文、实验设置、公式和附录未提供。以下总结主要依据摘要与元数据，未提及之处会明确标注为“未说明”。

## 1. 核心问题与整体含义
- **研究任务**：首尾帧视频生成，即在给定首帧和尾帧的条件下，生成二者之间连贯、合理的运动视频。
- **核心问题**：现有方法在中间帧容易出现**语义退化/语义漂移**，导致场景扭曲、主体变形，破坏视频时序一致性。
- **整体含义**：论文提出一种通用、免训练、即插即用的方案，将边界帧语义显式桥接到中间帧，以缓解首尾帧视频生成中的不一致问题，提升生成视频的整体质量与泛化性。

## 2. 方法论：Anchor Frame Bridging（AFB）
- **核心思想**：在语义不连续最大的时间关键位置自适应插入“锚帧”，显式桥接首尾边界帧的语义连续性，从而约束中间帧生成，减少语义漂移。
- **关键模块与流程**：
  - **自适应锚帧选择**：通过帧顺序反转生成与文本对齐的候选帧，并基于语义连续性选择锚帧。
  - **锚帧引导生成**：利用选中的锚帧引导中间帧的语义传播，使边界语义保持一致，并维持全视频的时序连贯性。
  - **最终合成**：使用首帧、尾帧、所选锚帧以及文本提示共同合成最终视频。
- **公式/算法**：给定文本未提供显式公式或伪代码；可概括为“检测语义不连续关键位置 → 反转帧序生成候选锚帧 → 按语义连续性筛选锚帧 → 以锚帧引导中间帧生成 → 融合首尾帧、锚帧与文本提示输出视频”。

## 3. 实验设计
- **数据集/场景**：未说明具体数据集；任务场景明确为首尾帧视频生成。
- **Benchmark**：未说明。
- **对比方法**：未说明具体基线或对比方法。
- **模型与指标**：摘要提到应用于 **Wan2.1-I2V** 模型，报告 **FVD 提升 16.58%**、**PSNR 提升 10.21%**。
- **代码**：摘要称代码在补充材料中。

## 4. 资源与算力
- 给定文本**未明确说明**使用的 GPU 型号、数量、训练时长或推理算力。
- 由于方法被描述为“免训练”，可能不涉及训练阶段算力；但其推理成本、实验运行资源仍未披露。

## 5. 实验数量与充分性
- 从可获取文本看，**无法确定实验组数**，也未列出不同数据集、消融实验、用户研究或统计显著性分析。
- 目前仅知在一个模型 **Wan2.1-I2V** 上报告了两个指标的相对提升。
- 因此，实验是否充分、对比是否客观公平，**无法仅凭摘要判断**；需要正文与附录验证。

## 6. 主要结论与发现
- AFB 能有效缓解中间帧语义漂移，提升帧间一致性与视频整体质量。
- 在 Wan2.1-I2V 上，FVD 改善 **16.58%**，PSNR 改善 **10.21%**。
- 方法具有免训练、即插即用和较强泛化性的特点，可作为首尾帧视频生成的通用增强方案。

## 7. 优点
- **免训练、即插即用**：易于集成到现有首尾帧视频生成模型中。
- **显式语义桥接**：直接在关键位置插入锚帧，针对中间帧语义漂移问题。
- **自适应锚帧选择**：通过帧序反转与文本对齐候选帧，按语义连续性筛选锚帧。
- **指标提升明显**：在摘要报告的两个指标上均有正向收益。
- **通用性潜力**：不依赖特定模型重训练，理论上可适配多种生成框架。

## 8. 不足与局限
- **信息不完整**：正文不可得，方法细节、公式、实验配置均缺失，难以复现或深入验证。
- **实验覆盖未知**：未说明数据集、benchmark、对比方法、消融实验数量，充分性与公平性无法评估。
- **算力与开销未披露**：未说明推理成本、锚帧选择开销、是否显著增加生成时间。
- **偏差风险**：仅报告相对提升，未提供绝对值、方差、显著性检验或失败案例。
- **应用限制**：效果可能依赖首尾帧质量与文本提示；对长视频、复杂运动、多主体场景的鲁棒性未知。
- **评估指标局限**：FVD、PSNR 不能完全代表人类感知质量，缺少主观评价或更全面的一致性指标。

（完）
