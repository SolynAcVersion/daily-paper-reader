---
title: "SpeedVFI: One-step Diffusion for Efficient Video Frame Interpolation"
title_zh: SpeedVFI：高效视频帧插值的单步扩散
authors: "Ganggui Ding, Xiaogang Xu, Hao Chen, Chunhua Shen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b3a60e2acb30ede9ae0f90d8997a046925385a9e.pdf"
tags: ["query:frame-dist"]
score: 5.0
evidence: 统一序列插值捕捉帧间关系
tldr: 视频帧插值中生成式扩散模型虽对大运动和遮挡鲁棒，但成对推理与多步去噪导致效率低下。本文提出SpeedVFI，将生成式帧插值重构为统一序列插值，通过一次前向传播插值整段视频消除成对开销，并将生成轨迹蒸馏为单步去噪以规避迭代延迟。方法在保持插值质量的同时大幅提升推理效率，为高效视频帧插值提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 生成式帧插值受成对推理与多步去噪拖累，推理效率低。
method: 将帧插值重构为统一序列插值，并把多步去噪蒸馏为单步生成。
result: 在保持插值质量的同时显著降低推理开销。
conclusion: 为高效生成式视频帧插值提供了单步序列化方案。
---

## Abstract
Generative video diffusion models have shown strong robustness to large motion and occlusions for video frame interpolation (VFI). However, their inference efficiency lags significantly behind learning-based methods due to the structural redundancy of pairwise inference and the procedural latency of multi-step iterative denoising. To address these limitations, we propose SpeedVFI, a task-specific one-step diffusion formulation that recasts generative VFI as unified sequence interpolation. SpeedVFI achieves dual efficiency improvements by interpolating the entire video sequence in a single forward pass to eliminate pairwise overhead, and by distilling the generation trajectory into a one-step denoising process to bypass iterative latency. To make this formulation effective for VFI, we introduce temporal RoPE alignment for temporally consistent conditioning and noise-centric partial attention to reduce computational overhead while preserving global context. Extensive experiments demonstrate that SpeedVFI accelerates diffusion-based VFI by orders of magnitude while maintaining competitive quantitative and visual quality.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 文本实际为 OpenReview 人机验证页面，未包含论文正文。以下总结主要基于论文元数据与 Abstract；凡涉及数据集、算力、实验组数等正文细节，均只能标注“未提供/无法判断”，不能据此编造。

## 1. 核心问题与整体含义

- **研究背景**：生成式视频扩散模型在视频帧插值（VFI）中，对大幅度运动和遮挡表现出较强鲁棒性，优于部分传统学习型方法。
- **核心问题**：扩散式 VFI 的推理效率显著落后，主要来自两个结构性瓶颈：
  - **成对推理冗余**：通常需要逐对帧进行插值，带来重复计算与结构冗余。
  - **多步迭代去噪延迟**：扩散模型需要多步去噪，推理过程缓慢。
- **整体含义**：论文提出 **SpeedVFI**，将生成式 VFI 重构为 **统一序列插值**，并设计为任务特定的 **单步扩散** 形式，目标是在保持插值质量的同时大幅提升推理效率。
- **一句话概括**：SpeedVFI 试图同时消除“成对推理”与“多步去噪”两大效率瓶颈，为高效生成式视频帧插值提供新范式。

## 2. 方法论：核心思想与关键技术

- **核心思想**：
  - 将生成式 VFI 从“逐对帧插值”重构为“统一序列插值”。
  - 将多步扩散生成轨迹蒸馏为单步去噪，从而规避迭代延迟。

- **关键技术细节**：
  - **统一序列插值**：在单次前向传播中插值整段视频序列，而不是逐对帧独立推理，以消除成对推理开销。
  - **单步去噪蒸馏**：把原本多步迭代的生成轨迹蒸馏到一个单步去噪过程中，避免多步扩散带来的程序性延迟。
  - **Temporal RoPE Alignment**：引入时间 RoPE 对齐，用于构造时间一致的条件信息，提升序列插值中的时间一致性。
  - **Noise-centric Partial Attention**：采用以噪声为中心的部分注意力机制，在降低计算开销的同时尽量保留全局上下文。

- **算法流程（文字说明）**：
  1. 输入低帧率视频序列或相关条件信息。
  2. 通过时间 RoPE 对齐建立时间一致的条件表示。
  3. 使用带 noise-centric partial attention 的扩散/去噪网络。
  4. 以单步去噪方式一次性生成整段视频的中间帧，而非逐对帧多次去噪。
  5. 训练阶段将多步教师扩散轨迹蒸馏为单步学生模型。
  6. 推理阶段只需一次前向传播，即可输出整段插值序列。

- **注意**：摘要未给出显式公式、损失函数、网络结构细节或蒸馏目标，因此无法进一步还原具体数学形式。

## 3. 实验设计：数据集、Benchmark 与对比方法

- **摘要中的描述**：论文声称进行了 “Extensive experiments”，并表明 SpeedVFI 相比扩散式 VFI 可实现数量级加速，同时保持有竞争力的定量和视觉质量。
- **具体数据集**：未提供。无法确认使用了哪些 VFI 常用数据集或场景。
- **Benchmark / 评价指标**：未提供。无法确认采用 PSNR、SSIM、LPIPS、FID 等哪些指标。
- **对比方法**：未提供。无法确认与哪些学习型 VFI 方法、生成式 VFI 方法或扩散基线进行了比较。
- **元数据信息**：
  - 来源标注为 **ICML-2026-Accepted**。
  - 元数据 score 为 **5.0**。
  - tags 为 **query:frame-dist**。
  - evidence 为“统一序列插值捕捉帧间关系”。

## 4. 资源与算力

- **未明确说明**：当前可用文本中没有提到 GPU 型号、GPU 数量、训练时长、显存占用、蒸馏成本或推理硬件环境。
- **无法判断**：
  - 训练总计算量。
  - 单步蒸馏所需额外训练开销。
  - 推理阶段的实际延迟、吞吐量或实时性。
- 因此，关于算力与效率优势的结论只能依赖摘要中的“数量级加速”表述，具体数值无法从现有材料核实。

## 5. 实验数量与充分性

- **实验组数**：未提供。无法确认包含多少数据集、多少基线、多少消融实验。
- **消融实验**：摘要未列出。无法判断是否验证了 temporal RoPE alignment、noise-centric partial attention、单步蒸馏、统一序列插值等各模块贡献。
- **充分性评估**：
  - 从摘要看，论文声称有广泛实验，并强调加速与质量保持。
  - 但缺少具体数据、指标、基线、统计显著性和用户研究信息。
  - 因此基于现有文本，**无法认定实验充分、客观或公平**。
- **公平性风险**：
  - 是否在相同训练数据、相同计算预算、相同评价协议下比较，未说明。
  - 是否只选择有利基线，未说明。
  - “竞争性质量”是否包含主观视觉质量评估，未说明。

## 6. 主要结论与发现

- SpeedVFI 将生成式 VFI 重构为 **统一序列插值**，并采用 **单步扩散** 公式。
- 通过一次前向传播插值整段视频，消除成对推理开销。
- 通过将生成轨迹蒸馏为单步去噪，规避多步迭代延迟。
- 引入 temporal RoPE alignment 和 noise-centric partial attention，以支持时间一致条件并降低计算量。
- 实验结论声称：SpeedVFI 可将基于扩散的 VFI 加速 **数量级**，同时保持有竞争力的定量和视觉质量。
- 总体贡献：为高效生成式视频帧插值提供了单步、序列化的新方案。

## 7. 优点

- **问题定位准确**：直接针对扩散式 VFI 的两个核心效率瓶颈：成对推理和多步去噪。
- **方法针对性强**：统一序列插值消除成对冗余，单步蒸馏规避迭代延迟，二者形成双重效率改进。
- **技术组件合理**：
  - temporal RoPE alignment 有助于时间一致的条件建模。
  - noise-centric partial attention 试图在降低计算的同时保留全局上下文。
- **应用潜力**：若结果成立，对长视频、高帧率插值和实时/近实时 VFI 场景有实际价值。
- **任务特定设计**：相比通用扩散模型，任务特定的单步扩散形式更可能兼顾效率与质量。

## 8. 不足与局限

- **文本不完整**：提供的 PDF 实际为 OpenReview 验证页，无法获取论文正文，因此总结存在信息缺失风险。
- **实验细节缺失**：
  - 未提供数据集、benchmark、评价指标、对比方法。
  - 未提供消融实验、定量结果表、视觉对比或用户研究。
- **算力信息缺失**：未说明 GPU 型号、数量、训练时长和推理成本，难以评估实际效率优势。
- **公平性无法验证**：无法确认基线选择、训练预算、评价协议是否公平。
- **潜在质量风险**：单步蒸馏可能限制复杂运动、遮挡或极端场景下的生成质量，需原文实验验证。
- **潜在扩展性限制**：统一序列插值可能受长序列内存或注意力复杂度影响，需原文说明其可扩展性。
- **应用限制**：蒸馏依赖教师轨迹，训练成本可能不低；实际部署时的延迟、显存和长视频稳定性仍需验证。

（完）
