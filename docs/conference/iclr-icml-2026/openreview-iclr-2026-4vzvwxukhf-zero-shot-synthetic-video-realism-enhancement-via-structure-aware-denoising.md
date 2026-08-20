---
title: Zero-shot Synthetic Video Realism Enhancement via Structure-aware Denoising
title_zh: 基于结构感知去噪的合成视频零样本真实感增强
authors: "Yifan Wang, Liya Ji, Zhanghan Ke, Harry Yang, Ser-Nam Lim, Qifeng Chen"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=4VzVWXUkhf"
tags: ["query:phys-video"]
score: 5.0
evidence: 提升合成视频真实感并保持跨帧结构
tldr: 论文针对合成视频真实感不足的问题，提出一种零样本结构感知去噪增强方法。该方法利用预训练扩散视频基础模型，并通过辅助模型估计合成视频的深度、语义和边缘图等结构信息来引导去噪，而非依赖模拟器参数。实验显示该方法在保持时空结构的同时显著提升合成视频的逼真度，无需额外微调，可广泛用于仿真视频的真实化处理。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 合成视频与真实视频视觉差异大，直接使用会影响下游任务性能，需要提升其真实感。
method: 提出零样本框架，利用扩散视频基础模型，以合成视频的深度、语义和边缘图作为结构感知条件引导去噪增强。
result: 无需微调即可保持合成视频的多级结构并进行真实感重渲染，提升了时空一致性。
conclusion: 该方法可有效缩小合成与真实视频之间的视觉差距，适用于数据增强与仿真到真实的转换。
---

## Abstract
We propose an approach to enhancing synthetic video realism, which can re-render synthetic videos from a simulator in photorealistic fashion. 
Our realism enhancement approach is a zero-shot framework that focuses on preserving the multi-level structures from synthetic videos into the enhanced one in both spatial and temporal domains, built upon a diffusion video foundational model without further fine-tuning. Specifically, we incorporate an effective modification to have the generation/denoising process conditioned on estimated structure-aware information from the synthetic video, such as depth maps, semantic maps, and edge maps, by an auxiliary model, rather than extracting the information from a simulator. This guidance ensures that the enhanced videos are consistent with the original synthetic video at both the structural and semantic levels. Our approach is a simple yet general and powerful approach to enhancing synthetic video realism: we show that our approach outperforms existing  baselines in structural consistency with the original video while maintaining state-of-the-art photorealism quality in our experiments.

---

## 论文详细总结（自动生成）

## 论文总结：基于结构感知去噪的合成视频零样本真实感增强

### 1. 核心问题与整体含义
- **研究动机**：合成视频（例如来自仿真器的渲染结果）与真实视频在视觉外观上存在明显差异，直接将合成数据用于下游任务（如视觉感知、自动驾驶等）会损害模型性能。因此，需要一种能够将合成视频“真实化”的方法，缩小合成与真实之间的视觉差距。
- **核心问题**：如何在保持合成视频原有空间与时间结构（如深度、语义、边缘）的前提下，将其重渲染为高逼真度的视频，同时避免依赖仿真器内部的参数或额外的训练/微调。
- **整体含义**：论文提出一种零样本、结构感知的合成视频真实感增强框架，有望作为通用的数据增强工具，服务于仿真到真实（sim-to-real）迁移等场景。

### 2. 方法论
- **核心思想**：基于预训练的扩散视频基础模型，在不进行微调的情况下，利用合成视频本身的结构信息（深度图、语义图、边缘图）作为条件，引导视频生成/去噪过程，使增强后的视频在保持多级结构一致性的同时获得真实感外观。
- **关键细节**：
  - 使用辅助模型（auxiliary model）从合成视频中估计结构信息，而非从仿真器中直接提取，从而保证方法适用于任意来源的合成视频。
  - 去噪/生成过程被条件化为“结构感知”的，增强后的视频在空间维度和时间维度上都与原始合成视频保持对齐。
  - 该方法属于零样本框架，无需针对特定仿真器或视频内容进行微调。
- **公式或算法流程**：原文仅提供概述，未给出具体公式。整体流程可概括为：输入合成视频 → 辅助模型提取深度/语义/边缘图 → 将这些结构图作为条件输入扩散视频模型 → 生成/去噪得到与原始结构一致的写实视频。

### 3. 实验设计
- **数据集/场景**：摘要中未明确列出具体数据集或仿真环境。仅笼统提及“来自仿真器的合成视频”，未说明是何种仿真器（如自动驾驶模拟器、游戏引擎渲染等）或视频类别。
- **Benchmark**：没有给出具体基准测试集或评估指标细节。
- **对比方法**：称“优于现有基线（existing baselines）”，但未列出基线方法名称。
- **评估维度**：同时评估了结构一致性（与原始合成视频的保持程度）和照片级真实感质量，并声称在结构一致性上超过基线，同时保持领先的真实感水平。
- **总体情况**：由于仅提供摘要，实验的定量结果、可视化对比和具体指标均未披露。

### 4. 资源与算力
- 原文摘要和元数据中**未提及**任何算力信息，包括 GPU 型号、数量、训练或推理时长、显存消耗等。
- 由于该方法是零样本且无需微调，推测主要算力开销来自预训练扩散模型和辅助模型的推理过程，但论文未给出相关量化说明。

### 5. 实验数量与充分性
- **实验数量**：从现有信息无法判断做了多少组实验；没有列出数据集、消融实验、时序一致性分析或不同合成域测试。
- **充分性**：当前提供的抽象内容不足以支撑全面评估。缺乏：
  - 定量指标（如 FVD、LPIPS、结构相似度、语义分割准确率等）。
  - 与不同扩散模型或结构信息组合的消融实验。
  - 对不同仿真器/合成内容泛化能力的系统测试。
  - 用户研究或下游任务验证。
- **客观性与公平性**：摘要声称“优于现有基线”，但因未披露实验细节，难以判断比较是否公平、充分。

### 6. 主要结论与发现
- 所提出的零样本结构感知去噪方法能够有效提升合成视频的真实感，同时保留原始合成视频的空间与时间结构。
- 方法具有简单、通用、强大的特点，无需微调即可使用，适合作为仿真到真实转换或数据增强工具。
- 实验表明该方法在结构一致性方面优于现有基线，并具备业界领先的照片级真实感生成质量。

### 7. 优点
- **零样本与免微调**：直接利用预训练扩散基础模型，降低了应用成本和训练难度，便于推广。
- **结构感知保持**：通过深度、语义、边缘等多级结构信息联合引导，兼顾空间与时间一致性，避免仅“换风格”导致的结构失真。
- **不依赖仿真器参数**：使用辅助模型估计结构信息，使方法对合成视频来源具有更广泛的适用性。
- **通用性强**：适用于多种合成视频输入，无需针对特定仿真器定制。

### 8. 不足与局限
- **实验细节缺失**：未提供数据集、基线、指标、消融实验等关键信息，难以评估方法的真实有效性和可复现性。
- **结构信息质量依赖**：方法效果高度依赖于辅助模型估计深度/语义/边缘图的准确性；若合成视频中存在遮挡、复杂动态或罕见类别，结构估计可能出错，进而影响增强结果。
- **时间一致性风险**：尽管强调时空一致性，但视频扩散模型在长序列或大运动场景下仍可能出现闪烁、漂移等不稳定问题，摘要未对此进行分析。
- **真实感与结构保持的权衡**：更高强度的去噪可能提升视觉真实感，但可能牺牲精细结构，摘要未讨论这一权衡及其调控方式。
- **下游任务验证不足**：没有展示增强后的视频在目标下游任务（如识别、跟踪）上的增益，其实用价值尚需更多证据。
- **应用范围限制**：主要针对合成视频，对真实视频或其他域的视频是否有效未作说明。
- **资源消耗不透明**：零样本方法虽不需训练，但扩散模型推理仍可能较昂贵，论文未给出计算开销分析。

（完）
