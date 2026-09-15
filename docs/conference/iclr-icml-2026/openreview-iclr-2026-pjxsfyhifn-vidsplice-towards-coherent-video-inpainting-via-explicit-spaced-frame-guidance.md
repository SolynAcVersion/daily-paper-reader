---
title: "VidSplice: Towards Coherent Video Inpainting via Explicit Spaced Frame Guidance"
title_zh: VidSplice：通过显式间隔帧引导实现连贯视频修复
authors: "Ming Xie, Junqiu Yu, Qiaole Dong, Xiangyang Xue, Yanwei Fu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=pjXSfyhifn"
tags: ["query:video-gen-rl"]
score: 5.0
evidence: 利用间隔帧引导实现连贯视频修复与时间一致性
tldr: 现有视频修复方法借助图像到视频先验建模帧间一致性，但在严重内容退化下难以兼顾时空稳定性，对视频后段控制不足。本文提出VidSplice，将修复解耦为多帧一致的图像修复与掩膜区域运动传播，并引入间隔帧先验提供时空线索。该框架提升了修复视频的时空连贯性，其帧间一致性建模思路对视频生成有借鉴意义。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频修复在严重退化下忽视时空稳定性，后段视频控制不足。
method: 将修复解耦为一致图像修复与运动传播，并引入间隔帧先验提供时空线索。
result: 方法在复杂退化场景下提升了修复视频的时空连贯性与稳定性。
conclusion: 为视频修复的帧间一致性建模提供了新框架。
---

## Abstract
Recent video inpainting methods often employ image-to-video (I2V) priors to model temporal consistency across masked frames. While effective in moderate cases, these methods struggle under severe content degradation and tend to overlook spatiotemporal stability, resulting in insufficient control over the latter parts of the video. To address these limitations, we decouple video inpainting into two sub-tasks: multi-frame consistent image inpainting and masked area motion propagation. We propose VidSplice, a novel framework that introduces spaced-frame priors to guide the inpainting process with spatiotemporal cues. To enhance spatial coherence, we design a CoSpliced Module to perform first-frame propagation strategy that diffuses the initial frame content into subsequent reference frames through a splicing mechanism. Additionally, we introduce a delicate context controller module that encodes coherent priors after frame duplication and injects the spliced video into the I2V generative backbone, effectively constraining content distortion during generation. Extensive evaluations demonstrate that VidSplice achieves competitive performance across diverse video inpainting scenarios. Moreover, its design significantly improves both foreground alignment and motion stability, outperforming existing approaches.

---

## 论文详细总结（自动生成）

# VidSplice 论文总结

> 说明：提供的 PDF 正文提取失败，仅有摘要与元数据可用。以下总结主要基于摘要和元数据，凡未提供的实验、算力、数据集等细节均如实标注为“未说明”，避免臆测。

## 1. 核心问题与整体含义

- **研究背景**：近期视频修复方法常借助图像到视频（I2V）先验，对掩膜帧之间的时间一致性进行建模。
- **核心问题**：这类方法在中等退化场景下有效，但在严重内容退化时表现受限，且容易忽视时空稳定性，导致对视频后段内容的控制不足。
- **整体含义**：论文提出 VidSplice，将视频修复解耦为两个子任务：
  - 多帧一致的图像修复；
  - 掩膜区域运动传播。
- **核心思路**：引入“间隔帧先验”为修复过程提供时空线索，从而提升修复视频的时空连贯性，并为视频生成中的帧间一致性建模提供新框架。

## 2. 方法论

- **核心思想**：
  - 不直接将视频修复作为单一端到端任务，而是解耦为“多帧一致图像修复”和“掩膜区域运动传播”。
  - 使用显式间隔帧作为先验，为后续帧修复提供时空参考。
- **关键技术细节**：
  - **CoSpliced Module**：
    - 执行首帧传播策略；
    - 通过拼接机制将初始帧内容扩散到后续参考帧；
    - 目的是增强空间连贯性。
  - **Context Controller Module**：
    - 在帧复制之后编码连贯先验；
    - 将拼接后的视频注入 I2V 生成骨干；
    - 用于约束生成过程中的内容失真。
- **算法流程文字说明**：
  1. 输入待修复视频及掩膜区域；
  2. 将视频修复解耦为多帧一致图像修复与掩膜区域运动传播；
  3. 引入间隔帧作为时空线索；
  4. 通过 CoSpliced Module 将首帧内容传播到后续参考帧；
  5. 通过 Context Controller 编码连贯先验，并注入 I2V 生成骨干；
  6. 在生成过程中约束内容失真；
  7. 结合运动传播保持掩膜区域运动稳定性，输出修复视频。
- **公式/伪代码**：提供的文本中未给出具体公式或算法伪代码。

## 3. 实验设计

- **数据集/场景**：
  - 摘要仅称在“diverse video inpainting scenarios”上进行广泛评估；
  - 未列出具体数据集名称、视频类型或场景划分。
- **Benchmark**：
  - 未说明使用了哪些 benchmark 或评价指标。
- **对比方法**：
  - 摘要称“outperforming existing approaches”，但未列出具体对比方法。
- **可确认的实验结论表述**：
  - 在复杂退化场景下提升修复视频的时空连贯性与稳定性；
  - 显著改善前景对齐和运动稳定性；
  - 在多种视频修复场景中取得有竞争力的性能。

## 4. 资源与算力

- 提供的文本中未提及：
  - GPU 型号；
  - GPU 数量；
  - 训练时长；
  - 参数量、训练数据规模、推理成本等。
- 因此无法总结其算力资源与训练开销。

## 5. 实验数量与充分性

- 摘要仅使用“Extensive evaluations”描述实验规模。
- 未提供：
  - 具体实验组数；
  - 不同数据集上的定量结果；
  - 消融实验设置；
  - 用户研究或主观评价细节。
- 因此无法判断实验是否充分、客观、公平。
- 基于现有材料，只能确认作者声称方法在多种视频修复场景中有效，但无法验证其对比公平性和统计显著性。

## 6. 主要结论与发现

- VidSplice 通过显式间隔帧引导，能够提升视频修复的时空连贯性。
- 将视频修复解耦为“多帧一致图像修复”和“掩膜区域运动传播”是有效思路。
- CoSpliced Module 与 Context Controller 有助于增强空间连贯性并约束生成失真。
- 方法在复杂退化场景下改善了前景对齐和运动稳定性。
- 论文为视频修复中的帧间一致性建模提供了新框架，对视频生成任务也有借鉴意义。

## 7. 优点

- **问题拆解清晰**：将视频修复分解为图像修复与运动传播两个子任务，降低建模难度。
- **显式时空引导**：引入间隔帧先验，为后续帧提供更明确的时空线索。
- **模块设计有针对性**：
  - CoSpliced Module 通过首帧传播和拼接机制增强空间一致性；
  - Context Controller 将连贯先验注入 I2V 生成骨干，约束内容失真。
- **关注后段控制**：针对现有方法对视频后段控制不足的问题进行改进。
- **跨任务启发**：帧间一致性建模思路可迁移到更广泛的视频生成任务。

## 8. 不足与局限

- **材料限制**：
  - 提供的 PDF 正文未成功提取，无法全面评估论文的实验、公式、实现细节和附录。
- **实验信息缺失**：
  - 未说明具体数据集、benchmark、对比方法和评价指标；
  - 无法判断实验覆盖是否充分、是否存在选择性报告；
  - 无法验证公平性和可复现性。
- **资源与效率未知**：
  - 未说明训练算力、推理速度、显存占用等实际部署成本。
- **潜在应用限制**：
  - 方法依赖 I2V 先验，可能继承其偏差或生成伪影；
  - 间隔帧选择、拼接机制和上下文控制对复杂运动的鲁棒性尚无法确认；
  - 对长视频、严重遮挡、快速运动、真实场景泛化等问题的表现未在提供材料中说明。
- **偏差风险**：
  - 仅有摘要和元数据，结论主要来自作者自述，缺少独立验证。

（完）
