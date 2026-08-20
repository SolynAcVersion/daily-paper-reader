---
title: Motion Attribution for Video Generation
title_zh: 视频生成的运动归因
authors: "Xindi Wu, Despoina Paschalidou, Jun Gao, Antonio Torralba, Laura Leal-Taixé, Olga Russakovsky, Sanja Fidler, Jonathan Lorraine"
date: 2026-04-30
pdf: "https://openreview.net/pdf/24ac3b41f32abbf79a5ef7b5aae0f217024883e6.pdf"
tags: ["query:phys-video"]
score: 8.0
evidence: 通过运动数据归因提升时间一致性与物理合理性
tldr: 视频生成中数据对运动的影响尚不清楚，Motive 提出可扩展的梯度式运动归因方法，用运动加权损失掩码区分动态与外观。在文生视频上，它能识别显著影响运动的片段，指导数据策展以提升时间一致性和物理合理性，并可扩展到大模型与大数据集。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频生成模型受训练数据影响显著，但数据如何影响运动质量仍缺乏系统理解。
method: 提出 Motive，一种基于梯度的运动中心数据归因框架，通过运动加权损失掩码分离时间动态与静态外观，实现高效可扩展的运动归因。
result: 在文生视频模型上，Motive 可识别高影响力片段并指导数据筛选，改善时间一致性和物理合理性。
conclusion: 该工作为通过数据归因改善视频运动质量提供了可扩展工具，有助于数据策展与模型微调。
---

## Abstract
Despite the rapid progress of video generation models, the role of data in influencing motion is poorly understood. We present Motive (MOTIon attribution for Video gEneration), a motion-centric, gradient-based data attribution framework that scales to modern, large, high-quality video datasets and models. We use this to study which fine-tuning clips improve or degrade temporal dynamics. Motive isolates temporal dynamics from static appearance via motion-weighted loss masks, yielding efficient and scalable motion-specific influence computation. On text-to-video models, Motive identifies clips that strongly affect motion and guides data curation that improves temporal consistency and physical plausibility. With Motive-selected high-influence data, we improve both motion smoothness and dynamic degree on VBench, achieving a 74.1% human preference win rate compared with the pretrained base model. To our knowledge, this is the first framework to attribute motion rather than visual appearance in video generative models and to use it to curate fine-tuning data.

---

## 论文详细总结（自动生成）

## 视频生成的运动归因（Motive）论文总结

### 1. 核心问题与整体含义（研究动机和背景）
- **背景**：视频生成模型发展迅速，但训练数据如何影响生成视频的“运动”质量，仍然缺乏系统性理解。现有研究多关注数据对视觉外观的影响，极少关注对时间动态（运动）的影响。
- **核心问题**：哪些训练片段会改善或损害视频生成模型的时间动态？如何在大规模、高质量的视频数据集上高效地归因运动层面的数据影响？
- **整体含义**：该论文首次将数据归因对象从“视觉外观”扩展到“运动”，为视频生成模型的运动质量提升提供了数据驱动的新工具，填补了运动层面数据归因的空白。

### 2. 方法论：核心思想、关键技术细节
- **提出框架**：Motive（MOTIon attribution for Video gEneration），一种以运动为中心、基于梯度的数据归因框架。
- **核心思想**：将“时间动态”与“静态外观”分离，从而单独计算每个训练片段对运动的影响。
- **关键技术细节**：
  - 使用**运动加权损失掩码（motion-weighted loss masks）**，在计算损失时对运动相关区域赋予更高权重，对静态外观区域降低权重，从而隔离运动信号。
  - 基于梯度计算数据影响力（influence），衡量每个训练样本对模型时间动态的影响方向（正面或负面）和强度。
  - 支持**可扩展**归因：可适用于现代大规模视频数据集和参数量较大的视频生成模型。
- **算法流程（文字说明）**：
  1. 对每个候选训练视频片段，计算其在模型训练中的损失，并使用运动掩码仅保留运动相关部分；
  2. 计算该损失对模型参数的梯度，并通过梯度内积或其他影响函数近似，衡量该样本对模型运动生成能力的影响；
  3. 根据影响分值对样本排序，识别高影响（正面）和低影响/负面样本；
  4. 使用高影响样本进行数据策展，用于模型微调。

### 3. 实验设计
- **基准模型**：文生视频（text-to-video）模型。
- **数据集**：使用了较大规模的视频数据集进行数据策展和微调，但论文摘要未给出具体数据集名称（如 WebVid、HDVILA 等），需以正文为准。
- **评估指标**：
  - **VBench** 上的 **motion smoothness（运动平滑度）** 和 **dynamic degree（动态程度）**；
  - **人类偏好评估**：与预训练基座模型对比，报告胜率（win rate）。
- **对比方法**：摘要中未提及与其他归因方法的对比，主要展示了 Motive 自身的效果以及数据筛选带来的增益。

### 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提到 GPU 型号、数量、训练时长等算力信息。
- **推测**：由于面向“现代大型视频数据集和模型”，估计需要多卡 GPU 集群（如 A100/H100），但具体细节需查阅正文。

### 5. 实验数量与充分性
- **实验数量**：摘要仅报告了一组主要结果（VBench 指标 + 74.1% 人类偏好胜率），未列出消融实验数量。
- **充分性评价**：
  - **相对有限**：摘要层面未展示多数据集、多基座模型的泛化验证，也没有与现有数据筛选或归因方法的对比；
  - **存在潜在偏差**：仅以文生视频模型为例，未覆盖视频生成其他范式（如图文视频编辑、无条件生成）的适用性；
  - **主观指标**：人类偏好评估的规模、人数、协议未在摘要中说明，公平性与可复现性信息不足。
  - **结论方向正确**：从数据归因角度提升运动质量具有新意，但实验充分性还需正文补充。

### 6. 主要结论与发现
- Motive 能有效识别对视频生成运动质量有显著影响的训练片段。
- 使用 Motive 筛选出的高影响数据对模型进行微调，可以：
  - 改善 VBench 上的运动平滑度与动态程度；
  - 获得 74.1% 的人类偏好胜率（对比预训练基座模型）。
- 该框架是首个将运动与外观分离进行归因的视频生成数据归因方法，并成功应用于大规模数据策展。

### 7. 优点
- **视角新颖**：首次关注视频生成中的“运动归因”，而非传统的外观/内容归因。
- **技术有效**：通过运动加权损失掩码巧妙地分离时间动态与静态外观，具有较高可解释性。
- **可扩展性强**：设计上支持现代大型视频数据集和模型，具备实际应用潜力。
- **应用价值明确**：可直接用于数据策展、数据筛选、模型微调，提升视频生成质量。

### 8. 不足与局限
- **实验验证面窄**：仅展示在文生视频模型上的结果，未验证其他类型的视频模型或生成框架。
- **缺乏对比基线**：未在摘要中说明与随机数据筛选、其他影响函数或数据选择方法的对比，难以体现实质性优势。
- **算力细节缺失**：未报告计算成本，无法评估该方法的资源门槛。
- **主观评估信息不足**：人类偏好评估的具体流程、样本数量、评分者一致性等未交代，可能影响结论的可靠性。
- **潜在假设限制**：方法依赖运动掩码的准确性，若视频中运动与外观耦合较强或有复杂遮挡，归因质量可能下降。
- **应用范围有限**：目前主要针对微调数据策展，未涉及训练过程动态调整或模型架构优化。

（完）
