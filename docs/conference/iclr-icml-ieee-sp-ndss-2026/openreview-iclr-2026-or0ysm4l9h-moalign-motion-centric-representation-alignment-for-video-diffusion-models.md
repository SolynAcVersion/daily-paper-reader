---
title: "MoAlign: Motion-Centric Representation Alignment for Video Diffusion Models"
title_zh: MoAlign：面向视频扩散模型的以运动为中心的表示对齐
authors: "Aritra Bhowmik, Denis Korzhenkov, Cees G. M. Snoek, Amir Habibian, Mohsen Ghafoorian"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=OR0ySm4l9h"
tags: ["query:phys-video"]
score: 8.0
evidence: 以光流监督的运动中心对齐提升生成视频的物理合理性
tldr: 文本到视频扩散模型常因对复杂运动理解不足而生成时间不连贯、物理上不合理的运动。MoAlign从预训练视频编码器中学习一个与外观解耦的运动子空间，并用真实光流预测来监督该子空间，使其捕捉真实运动动态。训练时将该运动子空间与扩散模型特征对齐，从而显著提升视频生成的运动一致性和物理合理性。这表明解耦运动表示是对齐视频生成与物理规律的有效途径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 视频扩散模型对复杂运动理解不足，导致物理不合理的运动。
method: 学习解耦运动子空间并用光流预测监督，与扩散特征对齐。
result: 有效提升生成视频的时间一致性和物理合理性。
conclusion: 验证了解耦运动表示在物理合理视频生成中的关键作用。
---

## Abstract
Text-to-video diffusion models have enabled high-quality video synthesis, yet often fail to generate temporally coherent and physically plausible motion. A key reason is the models' insufficient understanding of complex motions that natural videos often entail. Recent works tackle this problem by aligning diffusion model features with those from pretrained video encoders. However, these encoders mix video appearance and dynamics into entangled features, limiting the benefit  of such alignment. In this paper, we propose a motion-centric alignment framework that learns a disentangled motion subspace from a pretrained video encoder. This subspace is optimized to predict ground-truth optical flow, ensuring it captures true motion dynamics. We then align the latent features of a text-to-video diffusion model to this new subspace, enabling the generative model to internalize motion knowledge and generate more plausible videos. Our method improves the physical commonsense in a state-of-the-art video diffusion model, while preserving adherence to textual prompts, as evidenced by empirical evaluations on VideoPhy, VideoPhy2, VBench, and VBench-2.0, along with a user study.

---

## 论文详细总结（自动生成）

# 论文总结：MoAlign：面向视频扩散模型的以运动为中心的表示对齐

## 1. 论文的核心问题与整体含义（研究动机和背景）
- 文本到视频扩散模型已能生成高质量视频，但在生成**时间连贯、物理合理**的运动方面仍存在明显不足，常出现不符合物理常识的运动。
- 核心原因是模型对自然视频中固有的**复杂运动理解不足**。
- 近年已有方法尝试将扩散模型特征与预训练视频编码器特征对齐，以注入运动知识；但这类编码器往往将**外观与运动动态纠缠在特征中**，导致对齐效果受限。
- 本文提出一种**以运动为中心的对齐框架（MoAlign）**，旨在显式解耦运动与外观，使扩散模型更好地内化真实运动动态，从而提升物理合理性。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：学习一个与外观解耦的**运动子空间**，并用真实光流进行监督，使该子空间准确捕捉真实运动动态；随后将扩散模型的潜在特征与该运动子空间对齐，使生成模型吸收运动知识。
- **关键技术步骤**（根据摘要提取）：
  1. 从预训练视频编码器中学习一个**解耦的运动子空间**。
  2. 以**预测真实光流**为优化目标，确保该子空间表征的是真实运动动态而非外观信息。
  3. 将**文本到视频扩散模型的潜在特征**对齐到该运动子空间上，使扩散模型在生成时能够利用该运动表示。
- **未提供的细节**：摘要和元数据中未给出具体网络结构、损失函数形式、训练流程或公式，需参考完整论文。

## 3. 实验设计：数据集、基准与对比方法
- **评估基准**：在 **VideoPhy、VideoPhy2、VBench、VBench-2.0** 四个视频生成基准上进行了实证评估，并额外进行了**用户研究**。
- **评估维度**：主要考察生成视频的**物理常识（physical commonsense）**以及**对文本提示的遵循程度（adherence）**。
- **对比方法**：文中仅提到改进了“一个最先进的视频扩散模型（state-of-the-art video diffusion model）”，但未在提供的摘要中列出具体的对比方法或基线名称。

## 4. 资源与算力
- 提供的文本（元数据、摘要）中**未说明**使用的 GPU 型号、数量、训练时长、参数量等具体资源信息。
- 需要查阅完整论文才能获得计算资源相关细节。

## 5. 实验数量与充分性
- **从提供内容来看**：实验覆盖了 4 个公开基准和一个用户研究，说明作者进行了多场景验证，包括自动指标和主观评价。
- **充分性判断**：
  - 支持了方法的有效性和泛化性，但**无法确认是否包含消融实验**（如解耦子空间的作用、光流监督的贡献、不同对齐策略的对比等）。
  - 由于缺少具体数值、基线比较细节和设置说明，**无法充分评估实验的客观性和公平性**。

## 6. 论文的主要结论与发现
- 所提 MoAlign 方法能**有效提升生成视频的时间一致性和物理合理性**。
- 在提升物理常识的同时，**保持了模型对文本提示的遵循能力**。
- 验证了**解耦运动表示**是促进视频生成符合物理规律的有效途径。

## 7. 优点
- **问题针对性强**：直接针对视频扩散模型对运动理解不足的痛点，并指出已有特征对齐方法中外观/运动纠缠的缺陷。
- **思路清晰且有新意**：通过光流监督学习解耦运动子空间，再与扩散特征对齐，是解决该问题的合理且可操作的设计。
- **评估较全面**：在多个 VideoPhy 和 VBench 系列基准上验证，并辅以用户研究，兼顾客观指标与主观感受。

## 8. 不足与局限
- **信息不完整**：当前提供的文本缺乏方法细节、消融实验、量化结果与算力配置，无法深入评估技术实现和实验严谨性。
- **潜在局限（基于现有信息推断）**：方法依赖于光流作为真实运动动态的监督信号，但光流本身可能难以覆盖所有复杂的物理运动（如遮挡、光照变化、非刚性运动等）。
- **应用限制**：摘要未讨论该方法在不同视频生成任务或不同扩散模型架构上的泛化能力，也未提到潜在失败案例。

（完）
