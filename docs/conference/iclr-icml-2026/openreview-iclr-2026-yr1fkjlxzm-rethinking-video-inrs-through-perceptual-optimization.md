---
title: Rethinking Video-INRs through Perceptual Optimization
title_zh: 通过感知优化重新思考视频隐式神经表示
authors: "Junqi Shi, Wuyang Cong, Ming Lu, Bowei Xu, Zhan Ma"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=yR1fKjlxzm"
tags: ["query:frame-dist"]
score: 7.0
evidence: 视频误差高度结构化且时间相关
tldr: 视频隐式神经表示大多沿用像素级损失，隐含假设高斯或拉普拉斯误差分布。本文借助变分推断，从理论与实验两方面表明这些假设与视频中高度结构化、时间相关的误差分布并不匹配。为此作者提出把监督从像素域转移到感知特征空间。结果表明感知优化更契合视频帧间误差的统计特性，为视频建模提供更合理的分布假设。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频INR多用像素级损失，隐含高斯或拉普拉斯误差分布假设。
method: 借助变分推断分析误差分布，转而用感知特征空间监督。
result: 理论与实验表明像素级目标与视频时间相关误差结构不匹配。
conclusion: 感知优化更契合视频帧间结构化、时间相关的误差分布。
---

## Abstract
Implicit neural representations (INRs) have recently emerged as a powerful paradigm for video modeling, representing videos as continuous functions parameterized by network weights, rather than storing raw pixels or latent codes. Despite architectural progress, most video-INR methods largely persist with pixel-wise (MSE or $\ell_1$) losses.
Through the lens of variational inference, we show—both theoretically and empirically—that these pixel-wise objectives implicitly assume Gaussian or Laplacian error distributions, which are statistically misaligned with per-video characteristics, where errors are highly structured and temporally correlated. To address this limitation, we propose shifting supervision from the pixel domain to perceptual feature spaces, which provide stable transformation spaces that relax restrictive distributional assumptions and align optimization with perceptual semantics. Specifically, we introduce two feature-domain objectives: Multi-Vision Feature Similarity (MVFS) for intra-frame fidelity and Vision Subject Similarity (VSS) for inter-frame temporal consistency. Even with a lightweight INR backbone using simple cascaded upsampling, our method surpasses state-of-the-art VAE- and diffusion-based codecs in perceptual quality while maintaining real-time decoding at an average of $\sim$125 FPS on 1080p resolution. Our results demonstrate that perceptual supervision provides a principled and promising direction for advancing video-INRs.

---

## 论文详细总结（自动生成）

> 说明：给定 PDF 正文提取被 CAPTCHA 拦截，以下总结主要依据论文摘要与元数据；未在提供内容中出现的细节，我会明确标注为“未说明”或“无法确认”。

## 1. 核心问题与整体含义

- **研究背景**：隐式神经表示（INRs）将视频建模为由网络权重参数化的连续函数，而不是直接存储原始像素或潜码。尽管视频 INR 的架构不断进步，大多数方法仍沿用像素级损失，如 MSE 或 \(\ell_1\)。
- **核心问题**：论文通过变分推断指出，像素级目标隐含假设误差服从高斯或拉普拉斯分布。但视频中的误差往往是**高度结构化且时间相关**的，这种分布假设与真实视频特性不匹配。
- **整体含义**：视频 INR 的优化目标不应局限于像素域；将监督转移到感知特征空间，可能提供更合理的分布假设和更符合感知语义的优化方向。

## 2. 方法论

- **核心思想**：把监督从像素域转移到感知特征空间，利用稳定变换空间放宽限制性分布假设，并使优化与感知语义对齐。
- **理论视角**：借助变分推断，从理论和实验两方面说明像素级损失隐含的误差分布假设与视频误差结构不一致。
- **关键技术细节**：
  - 提出两个特征域目标：
    - **MVFS（Multi-Vision Feature Similarity）**：用于帧内保真，约束单帧的感知特征相似性。
    - **VSS（Vision Subject Similarity）**：用于帧间时间一致性，约束视频帧之间的视觉主体/时序一致性。
  - 使用轻量级 INR 骨干网络，并采用简单的级联上采样结构。
- **算法流程概述**：视频仍由 INR 网络权重参数化；优化时不在像素域计算 MSE/\(\ell_1\)，而是在感知特征空间中计算 MVFS 与 VSS；MVFS 负责帧内感知质量，VSS 负责帧间时间一致性，从而替代传统像素级监督。

## 3. 实验设计

- **数据集/场景**：提供的摘要与元数据未明确列出具体数据集名称；仅提到在 **1080p 分辨率**下评估解码速度。
- **Benchmark**：主要围绕**感知质量**与**实时解码速度**进行评估。
- **对比方法**：与基于 VAE 和基于扩散模型的 codecs 进行对比。
- **主要实验结论**：即使使用轻量 INR 骨干和简单级联上采样，方法在感知质量上超过当前先进的 VAE 与 diffusion-based codecs，并在 1080p 下保持平均约 **125 FPS** 的实时解码。
- **未说明内容**：具体评测指标、码率/压缩率、训练配置、数据集规模、对比方法完整列表等，在提供文本中均未给出。

## 4. 资源与算力

- 论文提供内容中**未明确说明**训练所用 GPU 型号、数量、训练时长、显存或总计算量。
- 仅提到推理阶段在 1080p 分辨率下平均约 **125 FPS**，这是解码速度，不等同于训练算力。
- 因此，无法根据现有信息评估其训练成本、能耗或可复现性。

## 5. 实验数量与充分性

- 从摘要可确认至少包含：
  - 变分推断角度的理论分析；
  - 对像素级目标分布假设的实证验证；
  - 与 VAE/diffusion-based codecs 的感知质量对比；
  - 1080p 下的解码速度评估。
- **无法确认**具体实验组数，例如不同数据集、不同分辨率、不同码率、消融实验、跨视频类型泛化等。
- **充分性与公平性**：由于缺少实验协议、评测指标、训练细节和对比设置，无法客观判断实验是否充分、公平。若仅报告感知指标而缺少像素保真、码率或下游任务指标，则评估可能不全面。

## 6. 主要结论与发现

- 视频 INR 中常用的像素级损失隐含高斯/拉普拉斯误差假设，这与视频中高度结构化、时间相关的误差分布不匹配。
- 感知特征空间监督比像素域监督更契合视频帧间误差的统计特性。
- 提出的 MVFS 与 VSS 分别改善帧内保真和帧间时间一致性。
- 即使使用轻量 INR 骨干，也能在感知质量上超过先进 VAE/diffusion codecs，并保持 1080p 实时解码。
- 总体结论：感知优化为视频 INR 提供了更合理、更有前景的优化方向。

## 7. 优点

- **理论驱动**：从变分推断角度重新审视像素级损失，指出其分布假设问题，而非仅做架构改进。
- **目标设计针对性强**：MVFS 关注帧内保真，VSS 关注帧间时间一致性，覆盖视频建模的两个关键维度。
- **轻量高效**：使用简单级联上采样和轻量 INR 骨干即可实现实时解码，具备实际应用潜力。
- **挑战主流范式**：将监督从像素域迁移到感知特征空间，为视频 INR 提供新思路。
- **对比对象有代表性**：与 VAE 和 diffusion-based codecs 对比，说明方法在感知质量上的竞争力。

## 8. 不足与局限

- **正文信息缺失**：给定 PDF 文本被 CAPTCHA 拦截，无法获取完整实验、公式和实现细节，因此上述总结受限于摘要与元数据。
- **实验覆盖不明确**：未说明使用了哪些数据集、视频类型、分辨率范围和评测指标，难以判断泛化能力。
- **公平性无法验证**：缺少训练配置、码率控制、对比方法复现细节，无法确认对比是否完全公平。
- **感知指标依赖风险**：感知特征空间监督可能依赖预训练视觉模型，其偏差会影响优化结果。
- **应用限制**：若任务需要像素级精确重建或下游任务对像素保真敏感，感知优化可能不足。
- **资源成本未知**：训练算力、训练时长和显存需求未报告，难以评估实际部署与复现成本。
- **实时速度依赖硬件**：125 FPS 的具体硬件平台未说明，实际速度可能随设备变化。

（完）
