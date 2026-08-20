---
title: Where is Motion From? Scalable Motion Attribution for Video Generation Models
title_zh: 运动从何而来？视频生成模型的可扩展运动归因
authors: "Xindi Wu, Despoina Paschalidou, Jun Gao, Antonio Torralba, Laura Leal-Taixé, Olga Russakovsky, Sanja Fidler, Jonathan Lorraine"
date: 2025-09-14
pdf: "https://openreview.net/pdf?id=0dnSbhNoTB"
tags: ["query:psd"]
score: 9.0
evidence: 数据归因识别提升时间一致性与物理合理性的微调片段，指导物理感知的数据筛选
tldr: 视频生成模型中数据对运动质量的影响尚不明确。MOTIVE提出一种可扩展的梯度基数据归因框架，通过光流加权损失掩码将时间动态与静态外观分离，计算视频片段对训练的影响分数。该方法能够识别改善或损害时间动态的微调片段，指导数据筛选，从而提升生成视频的时间一致性和物理合理性。该框架适用于现代大规模视频数据集与模型，为物理感知的数据选择提供了实用工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视频生成模型的数据对运动质量的影响尚未被充分理解，需要可扩展的方法分析微调数据对时间动态的作用。
method: 提出MOTIVE运动归因框架，用光流加权损失掩码分离运动与外观，基于梯度计算数据影响分数。
result: 在文本生成视频模型上，MOTIVE识别出影响运动的片段，指导数据筛选后提升时间一致性和物理合理性。
conclusion: 该工作提供了可扩展的数据归因工具，有助于理解并优化视频生成中的运动与物理合理性。
---

## Abstract
Despite the rapid progress of video generative models, the role of data in shaping motion quality is poorly understood. We present MOTIVE (MOtion Training Influence for Video gEneration), a motion-centric, gradient-based data attribution framework that scales to modern, large, high-quality video datasets and models. We use this to study which finetuning clips improve or degrade temporal dynamics. MOTIVE isolates temporal dynamics from static appearance via flow-weighted loss masks, yielding scalable influence scores practical for modern, large, and high-quality datasets and models. On text-to-video models, MOTIVE identifies clips that strongly affect motion and guides data curation that improves temporal consistency and physical plausibility. With MOTIVE selected high-influence data, our method improves both motion smoothness and dynamic degree on VBench, achieving a 74.1% human preference win rate compared with the pretrained base model. To our knowledge, this is the first framework that attributes motion (not just appearance) in video generative models and uses it to curate finetuning data.

---

## 论文详细总结（自动生成）

# 论文总结：Where is Motion From? Scalable Motion Attribution for Video Generation Models

## 1. 核心问题与研究动机
- 视频生成模型发展迅速，但**数据在塑造运动质量方面的具体作用仍未被充分理解**——即“运动从何而来”这一根本问题缺少系统性分析工具。
- 现有数据归因（data attribution）方法主要关注静态外观（appearance），很少针对时间动态（temporal dynamics）或运动属性进行归因。
- 论文提出 MOTIVE（MOtion Training Influence for Video gEneration），旨在**以运动为中心、基于梯度**的可扩展数据归因框架，用于回答“哪些微调片段改善或损害了生成视频的时间动态”。

## 2. 方法论
- **核心思想**：将视频片段对模型运动质量的影响分离出来，通过计算训练数据对模型的“影响分数”（influence score）来识别对运动有显著影响的样本。
- **关键技术创新**：
  - 使用**光流加权损失掩码（flow-weighted loss masks）** 来将时间动态与静态外观分离，使归因聚焦于运动而非外观。
  - 采用**梯度基（gradient-based）** 的影响计算，从而能够扩展到现代大规模、高质量视频数据集和模型。
- **算法流程（文字描述）**：
  1. 对每个微调视频片段，计算模型在带运动掩码下的损失（光流权重突出运动区域）。
  2. 利用梯度信息评估该片段对模型参数（或输出）的影响方向与幅度。
  3. 汇总得到每个片段的正/负影响分数，用于排序或筛选数据。
- 该方法不是针对具体模型架构定制的，因此可用于通用文本生成视频模型。

## 3. 实验设计
- **任务场景**：文本生成视频（text-to-video）模型。
- **评估基准**：使用 VBench，测量生成视频的**运动平滑度（motion smoothness）** 和**动态程度（dynamic degree）** 等指标。
- **对比方式**：将使用 MOTIVE 筛选的高影响数据微调后的模型，与**预训练基础模型（pretrained base model）** 进行对比。
- **主要结果**：MOTIVE 选择的数据使 VBench 上的运动平滑度和动态程度均有所提升；在人类偏好评估中，**胜率达到 74.1%**。
- 原文未给出具体数据集名称，也未列出与其他数据归因或数据筛选方法的直接对比。

## 4. 资源与算力
- 原文（提供的摘要部分）**未明确说明**使用的 GPU 型号、数量、训练时长或计算成本。
- 论文强调方法“可扩展（scalable）”，但没有给出具体的算力开销数据。

## 5. 实验数量与充分性
- 从摘要可见的实验结果包括：
  - VBench 运动平滑度和动态程度指标；
  - 74.1% 的人类偏好胜率（对比基础模型）；
  - 数据筛选后的提效结果。
- **充分性评估**：
  - 由于仅提供了摘要级信息，**缺少对基线方法（如随机数据选择、其他归因方法）的系统比较**，也未见消融实验（如光流掩码的作用验证）。
  - 没有报告不同数据规模、不同模型架构或不同视频领域的泛化结果。
  - 因此，**实验覆盖面相对有限**，尚不足以全面验证方法的稳健性与公平性；但如果论文正文包含更多消融，则另当别论。就当前提供文本而言，实验数量与充分性不足。

## 6. 主要结论与发现
- MOTIVE 能有效识别对运动质量有强烈影响的微调片段，并区分“有益”与“有害”数据。
- 使用高影响数据微调后，生成视频的**时间一致性（temporal consistency）** 和**物理合理性（physical plausibility）** 得到提升。
- 这是**第一个针对视频生成模型进行运动（而非仅外观）归因**的框架，并成功将其用于微调数据筛选。

## 7. 优点
- **运动与外观解耦**：通过光流加权损失掩码，将分析焦点从静态外观转移到运动，具有较强的可解释性。
- **可扩展性**：梯度基方法可在现代大规模视频数据集和模型上实际应用，具有实用性。
- **直接用于数据筛选**：不仅给出归因分数，还能指导数据 curation，形成闭环，对训练视频生成模型有现实价值。
- **评估信号明确**：VBench 指标和人类偏好胜率提供了量化证据，初步验证方法有效性。

## 8. 不足与局限
- **信息受限**：当前提供文本仅为摘要，缺少方法细节、公式推导和完整实验设计，难以深入验证。
- **依赖于光流质量**：光流加权掩码的效果可能受光流估计误差影响，尤其在复杂动态或遮挡场景中。
- **仅关注微调场景**：论文主要分析微调数据的影响，未探讨大规模预训练阶段的归因。
- **缺乏对比基线**：未与其他数据归因或数据选择方法（如随机采样、基于外观的归因、影响函数等）进行比较，公平性存疑。
- **泛化性问题**：仅在文本生成视频模型上验证，未涉及其他视频生成范式；数据集多样性未知。
- **算力与可复现性**：未报告计算资源，可能增加复现难度。

（完）
