---
title: Self-Refining Video Sampling
title_zh: 自修正视频采样
authors: "Sangwon Jang, Taekyung Ki, Jaehyeong Jo, Saining Xie, Jaehong Yoon, Sung Ju Hwang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/7247a3a140d0d6053ef9efb55873879757557b3a.pdf"
tags: ["query:phys-video"]
score: 8.0
evidence: 视频采样中提升物理真实感的自修正
tldr: 现代视频生成器在复杂物理动态上仍缺乏物理真实感，现有方案依赖外部验证器或额外训练，成本高昂且难以把握细粒度运动。本文提出自修正视频采样方法，将预训练生成器解释为去噪自编码器，在推理时进行迭代内循环修正，无需外部验证器或额外训练，并引入基于自一致性的不确定性感知修正以避免过度修整伪影。该方法提升了复杂动态视频的物理合理性，且即插即用。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频生成器在复杂物理动态上缺乏真实感，现有方法依赖额外训练或外部验证器。
method: 将预训练生成器解释为去噪自编码器，在推理时自修正，并引入不确定性感知策略。
result: 无需外部验证器和额外训练即可提升物理动态合理性。
conclusion: 为视频生成物理真实感提供即插即用方案。
---

## Abstract
Modern video generators still struggle with complex physical dynamics, often falling short of physical realism. Existing approaches address this using external verifiers or additional training on augmented data, which is computationally expensive and still limited in capturing fine-grained motion. In this work, we present self-refining video sampling, a simple method that uses a pre-trained video generator trained on large-scale datasets as its own self-refiner. By interpreting the generator as a denoising autoencoder, we enable iterative inner-loop refinement at inference time without any external verifier or additional training. We further introduce an uncertainty-aware refinement strategy that selectively refines regions based on self-consistency, which prevents artifacts caused by over-refinement. Experiments on state-of-the-art video generators demonstrate significant improvements in motion coherence and physics alignment, achieving over 70% human preference compared to the default sampler and guidance-based sampler.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与整体含义（研究动机和背景）
- 当前视频生成模型在**复杂物理动态**（如碰撞、重力、流体等）的建模上仍缺乏**物理真实感**，生成结果常常违背物理规律。
- 已有改进方案通常依赖**外部验证器**（如物理引擎或判别器）或基于增强数据**额外训练**，这些方法计算开销大，且对**细粒度运动**的捕捉能力有限。
- 本文提出一种**自修正视频采样**方法，无需外部验证器或额外训练，仅利用预训练生成器自身作为“自修正器”，在推理时迭代优化生成过程的物理合理性，从而为视频生成提供即插即用、低成本的真实感增强方案。

### 2. 提出方法论
- **核心思想**：将预训练视频生成器**解释为去噪自编码器（denoising autoencoder）**，从而在不改变模型参数的前提下，于推理阶段执行**迭代内循环（inner-loop）修正**。
- **关键步骤**：
  1. 使用默认采样器生成初始视频潜变量（或采样轨迹）。
  2. 将该潜变量视为带噪声的数据，通过生成器的去噪解码能力获得一个“自重建”结果。
  3. 比较原始潜变量与重建结果，计算**自一致性（self-consistency）**信号。
  4. 利用**不确定性感知（uncertainty-aware）**策略，仅选择性修正自一致性较低的区域，而非全图修改，以避免过度修正导致的伪影。
  5. 重复上述步骤若干轮，直至输出满足物理一致性的视频。
- **技术优势**：所有修正过程都在推理时进行，无需额外训练、无需外部物理引擎或判别器，且即插即用。

### 3. 实验设计
- **数据集 / 场景**：论文仅提及在“state-of-the-art video generators”上评估，未明确列出具体数据集或场景（如机器人交互、物体掉落、流体模拟等）。
- **Benchmark**：未提供标准 benchmark 名称；评估指标包括**运动连贯性（motion coherence）**和**物理对齐（physics alignment）**，以及**人类偏好（human preference）**。
- **对比方法**：与**默认采样器（default sampler）**和**基于引导的采样器（guidance-based sampler）**进行对比。
- **实验覆盖范围**：由于信息来源有限（仅摘要），未给出具体实验数量、消融设置、基线细节或量化表格。

### 4. 资源与算力
- 论文提供的信息中**未明确提及**GPU 型号、数量、训练时长或推理成本等算力细节。
- 仅能推断该方法无需额外训练，因此训练算力成本较低；推理阶段因增加内循环迭代，会有额外计算开销，但具体数值未给出。

### 5. 实验数量与充分性
- 从摘要看，实验仅涉及两两对比（默认采样器、引导采样器）以及人类偏好评估，但**缺乏具体实验数量、数据集多样性、消融研究（如不同迭代轮数、不确定性阈值的影响）等细节**。
- 由于论文全文信息不足，无法判断实验是否充分、客观或公平。摘要中未报告方差、显著性检验或跨不同生成器架构的全面评测，因此科学严谨性存疑，需要阅读完整论文才能评估。

### 6. 主要结论与发现
- 所提出的自修正视频采样方法，在无需外部验证器和额外训练的情况下，能显著提升复杂动态视频的**运动连贯性**和**物理对齐**。
- 在人类偏好上，相比默认采样器和基于引导的采样器，该方法获得**超过 70% 的偏好率**，表明用户更认可其生成结果。
- 不确定性感知的修正策略可有效避免过度修正造成的伪影，从而提高整体生成质量。

### 7. 优点
- **即插即用**：不修改生成器参数，直接应用于任何预训练视频扩散模型，部署成本低。
- **自监督机制**：利用模型自身的去噪能力生成修正信号，摆脱对外部物理模拟器或判别网络的依赖。
- **细粒度修正**：不确定性感知策略按区域选择性修正，避免全局过度平滑，保留原始生成细节。
- **简单有效**：方法核心思想简洁，对现有 SOTA 生成器均有增益，且人类偏好提升显著。

### 8. 不足与局限
- **实验细节匮乏**：摘要未提供具体数据集、生成器型号、可视化样例、消融实验等，难以全面评估方法的普适性和稳健性。
- **潜在偏差风险**：人类偏好评估可能存在主观偏差，未报告评估者数量、多样性、评分标准等，客观性不足。
- **计算开销未量化**：虽然无需训练，但推理时迭代内循环可能显著增加采样时间，文中未与基线进行耗时对比。
- **适用范围未知**：是否适用于所有视频扩散模型、是否对极复杂物理场景（如流体、软体）有效，尚未在摘要中给出明确证据。
- **信息完整性受限**：当前仅基于论文摘要与元数据，无法深入分析公式细节、算法伪代码、理论保证等。

---

（完）
