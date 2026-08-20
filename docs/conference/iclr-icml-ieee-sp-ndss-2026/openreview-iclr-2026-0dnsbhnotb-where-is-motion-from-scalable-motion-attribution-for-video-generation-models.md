---
title: Where is Motion From? Scalable Motion Attribution for Video Generation Models
title_zh: 运动从何而来？视频生成模型的可扩展运动归因
authors: "Xindi Wu, Despoina Paschalidou, Jun Gao, Antonio Torralba, Laura Leal-Taixé, Olga Russakovsky, Sanja Fidler, Jonathan Lorraine"
date: 2025-09-14
pdf: "https://openreview.net/pdf?id=0dnSbhNoTB"
tags: ["query:phys-video"]
score: 8.0
evidence: 通过数据归因提升视频模型运动质量与物理合理性的框架
tldr: 视频生成中运动质量受数据影响的作用机制尚不明确。本文提出MOTIVE，一种基于梯度的、可扩展的运动归因方法，通过光流加权损失将时间动态与静态外观解耦，为现代大规模视频数据集和模型计算运动影响分数。在文生视频模型上，该方法可识别对运动至关重要的片段，并指导数据筛选，从而提升时间一致性与物理合理性。这项工作为通过数据归因增强视频生成物理可信度提供了新途径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视频生成模型质量快速提升，但数据如何影响运动质量与物理合理性尚未被充分理解。
method: 提出MOTIVE框架，利用梯度归因和光流加权损失掩码，对大规模视频数据中的运动影响进行可扩展评分与数据筛选。
result: 识别出影响运动的关键片段，指导数据筛选后显著提升时间一致性和物理合理性。
conclusion: 数据归因可有效指导数据策展，从而改善视频生成的运动真实感与物理合理性。
---

## Abstract
Despite the rapid progress of video generative models, the role of data in shaping motion quality is poorly understood. We present MOTIVE (MOtion Training Influence for Video gEneration), a motion-centric, gradient-based data attribution framework that scales to modern, large, high-quality video datasets and models. We use this to study which finetuning clips improve or degrade temporal dynamics. MOTIVE isolates temporal dynamics from static appearance via flow-weighted loss masks, yielding scalable influence scores practical for modern, large, and high-quality datasets and models. On text-to-video models, MOTIVE identifies clips that strongly affect motion and guides data curation that improves temporal consistency and physical plausibility. With MOTIVE selected high-influence data, our method improves both motion smoothness and dynamic degree on VBench, achieving a 74.1% human preference win rate compared with the pretrained base model. To our knowledge, this is the first framework that attributes motion (not just appearance) in video generative models and uses it to curate finetuning data.

---

## 论文详细总结（自动生成）

# 《运动从何而来？视频生成模型的可扩展运动归因》论文总结

## 1. 核心问题与研究动机
- **背景**：视频生成模型质量进步迅速，但数据在塑造"运动质量"方面的作用仍缺乏清晰理解。
- **核心问题**：现有数据归因研究大多聚焦于静态外观（appearance），缺少面向"运动/时间动态"的可扩展归因方法。
- **研究意义**：厘清数据对运动质量的影响机制，可指导数据策展（data curation），进而提升视频生成的时间一致性与物理合理性。
- **整体含义**：本文首次尝试为视频生成模型建立"运动归因"框架，将数据归因从外观扩展到运动维度。

## 2. 方法论
- **核心思想**：提出 MOTIVE（MOtion Training Influence for Video gEneration），一个以运动为中心（motion-centric）、基于梯度（gradient-based）的数据归因框架。
- **关键技术**：
  - **可扩展性**：设计上适配现代大规模、高质量视频数据集与生成模型。
  - **运动与外观解耦**：通过光流加权损失掩码（flow-weighted loss masks）将时序动态从静态外观中分离出来，使损失信号聚焦于运动信息。
  - **影响分数**：为每个微调片段（clip）计算可扩展的运动影响力分数，用于衡量该片段对运动质量的正面或负面贡献。
- **算法流程（文字说明）**：对候选训练片段计算模型损失 → 使用光流对损失进行加权（抑制外观干扰）→ 基于梯度计算影响力分数 → 按分数排序识别对运动影响最强的片段 → 用于数据筛选与微调数据策展。

## 3. 实验设计
- **应用场景**：文生视频模型（text-to-video models）上的微调数据研究。
- **Benchmark**：VBench，重点评估运动平滑度（motion smoothness）与动态程度（dynamic degree）。
- **对比与评估**：与预训练基座模型（pretrained base model）对比，并额外进行人类偏好评估（human preference），报告胜率。
- **说明**：论文摘要未明确列出具体数据集名称（如 WebVid、UCF101 等）及更多基线方法，细节需查阅全文。

## 4. 资源与算力
- 所提供的论文内容中**未提及** GPU 型号、数量、训练时长等算力细节，因此无法对本方法的资源成本做出确认。

## 5. 实验数量与充分性
- **可见实验**：VBench 双指标评估（运动平滑度、动态程度）、人类偏好测试（74.1% 胜率）、高影响力数据策展效果验证。
- **充分性评估**：摘要层面证据链基本完整，但由于全文不可见，难以判断是否包含充分的消融实验、多数据集验证及统计显著性检验；值得注意的是，该论文在 ICLR 2026 评审中被拒（source 标注），说明审稿人视角下实验或论证可能仍存在不足。

## 6. 主要结论与发现
- MOTIVE 能够有效识别对运动质量影响显著的训练片段，并区分正向与负向影响。
- 基于高影响力数据筛选进行微调后，VBench 上的运动平滑度与动态程度均有提升。
- 相对预训练基座模型，人类偏好胜率达到 **74.1%**。
- 作者声称这是**首个**将视频生成模型的数据归因聚焦于"运动"（而非仅外观）、并用于指导微调数据策展的框架。

## 7. 优点
- **问题新颖**：首次将数据归因拓展到运动/时间动态维度，弥补了以往只归因外观的空白。
- **实用性强**：方法可扩展到现代大规模高质量视频数据集和模型，具有实际部署价值。
- **形成闭环**：不只提出归因方法，还落实为数据策展策略，带来 VBench 指标与人类偏好的可量化提升。
- **思路简洁**：光流加权损失掩码实现外观–运动解耦，概念直观、实现成本低。

## 8. 不足与局限
- **信息局限性**：当前仅有摘要，缺少网络结构、超参数、数据预处理、代码可用性等细节，难以完整复现。
- **算力未披露**：无法评估方法在真实大规模数据集上的资源开销与可复现性。
- **评估范围有限**：仅报告 VBench 与人类偏好，缺少多数据集、多任务或更多针对性基线的系统比较。
- **潜在偏差风险**：光流加权可能对特定运动类型（如大位移、遮挡、复杂相机运动）敏感，其泛化性需进一步验证；人类偏好测试的样本规模与评审者构成未知，可能存在主观偏差。
- **审稿状态**：该论文为 ICLR 2026 被拒稿，提示方法或实验设计在学术评审层面仍存在薄弱环节，读者应谨慎参考其结论强度。

（完）
