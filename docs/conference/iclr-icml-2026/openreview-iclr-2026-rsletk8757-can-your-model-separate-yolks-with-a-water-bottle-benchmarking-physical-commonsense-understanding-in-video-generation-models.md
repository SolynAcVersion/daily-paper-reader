---
title: Can Your Model Separate Yolks with a Water Bottle? Benchmarking Physical Commonsense Understanding in Video Generation Models
title_zh: 你的模型能用矿泉水瓶分离蛋黄吗？视频生成模型物理常识理解基准测试
authors: "Baris Sarper Tezcan, Enes Sanli, Erkut Erdem, Aykut Erdem"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=RsletK8757"
tags: ["query:phys-video"]
score: 9.0
evidence: 提出PhysVidBench，评估文本生成视频的物理常识
tldr: 文本到视频模型常生成违反日常物理常识的视频。为此提出PhysVidBench，一个经人类验证的基准，涵盖七个物理交互维度的精心设计提示，覆盖材料变化、时间动态等场景。通过三阶段流程对多个模型进行评测，该基准能有效揭示模型在因果推理、物体行为与工具使用等方面的物理常识缺陷。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 文本到视频模型虽能生成视觉吸引人的内容，但常违反日常物理常识。
method: 构建PhysVidBench基准，包含七个物理交互维度的精心设计提示，并用三阶段流程评测多个模型。
result: 人类验证表明该基准能有效揭示模型在因果、物体行为与工具使用等物理推理上的缺陷。
conclusion: PhysVidBench为衡量视频生成模型的物理常识推理提供了多维度评测工具。
---

## Abstract
Recent advances in text-to-video (T2V) generation have enabled visually compelling outputs, but models still struggle with everyday physical commonsense, often producing videos that violate intuitive expectations of causality, object behavior, and tool use. We introduce PhysVidBench, a human-validated benchmark for assessing physical reasoning in T2V models. It comprises carefully curated prompts spanning seven dimensions of physical interaction, from material transformation to temporal dynamics, offering broad, multi-faceted coverage of scenarios where physical plausibility is critical. For each prompt, we generate videos using diverse state-of-the-art models, and evaluate them through a three-stage pipeline: grounded physics questions are derived from each prompt, generated videos are captioned with a vision–language model, and a language model answers the questions using only the captions. This strategy mitigates hallucination and produces scores that align closely with human judgments. Beyond evaluation, PhysVidBench also serves as a diagnostic tool, enabling feedback-driven refinement of model outputs. By emphasizing affordances and tool-mediated actions, areas often overlooked in existing benchmarks, PhysVidBench provides a structured, interpretable framework for assessing and improving everyday physical commonsense in T2V models.

---

## 论文详细总结（自动生成）

# 论文总结：PhysVidBench——视频生成模型的物理常识理解基准

> 说明：本文档基于所给的论文摘要与元数据信息生成。原文全文不可见，因此部分细节（如具体模型列表、实验配置、算力信息）在摘要中未披露。

## 1. 核心问题与研究动机

- **问题背景**：文本到视频（Text-to-Video, T2V）生成模型近年来取得了显著进展，能够生成视觉上吸引人的视频内容。
- **核心痛点**：这些模型仍然缺乏对日常物理常识（everyday physical commonsense）的理解，生成的视频经常违反人类对**因果性、物体行为、工具使用**的直观预期。
- **研究意义**：物理常识是视频表现真实性和可用性的关键，现有基准很少专门关注“可供性（affordances）”和“工具中介行为（tool-mediated actions）”，导致这类缺陷未被系统评估。

## 2. 方法论：PhysVidBench 的构建与评估流程

- **核心思想**：构建一个人类验证的基准，从多个物理交互维度出发，系统评估 T2V 模型的物理常识推理能力。
- **基准内容**：
  - 包含精心设计的提示（prompts），覆盖**七个物理交互维度**。
  - 范围从**材料转变（material transformation）** 到**时间动态（temporal dynamics）** 等，强调物理合理性至关重要的场景。
- **三阶段评估流程（pipeline）**：
  1. **问题生成**：为每个提示（prompt）派生出基于物理事实的问答对（grounded physics questions）。
  2. **视频描述**：用视觉-语言模型（VLM）为生成的视频生成字幕（captions）。
  3. **答案推理**：让语言模型（LM）仅根据字幕回答问题。
- **设计优势**：这种“只依赖字幕”的方法可缓解视觉模型幻觉问题，且得到的评分与人类判断高度一致。
- **额外功能**：该基准不仅用于评估，还可作为**诊断工具**，通过反馈驱动的方式改进模型输出。

## 3. 实验设计

- **数据集/场景**：PhysVidBench 本身是评估基准，其场景涵盖七个物理交互维度（摘要中未逐一列举）。
- **评估对象**：使用多种**最先进的 T2V 模型**分别生成视频，具体模型名称未在摘要中给出。
- **对比方法**：未明确提及与其他基准或方法的定量对比，仅说明该基准的评分与人类判断对齐。
- **人类验证**：基准经过人类验证（human-validated），说明其提示和评估指标具有合理性。

## 4. 资源与算力

- **文本中未提及**：摘要和元数据中未说明使用的 GPU 型号、数量、训练/推理时长、计算规模等信息。
- 因此无法评估该工作所需的计算资源。

## 5. 实验数量与充分性

- **实验信息有限**：摘要只说了“在多种模型上生成视频”并给出“三阶段评估”，但没有报告具体实验数量、模型数量、消融实验或详细统计分析。
- **充分性**：
  - 从摘要看，人类验证和与人类判断的一致性提供了较强的可信度；
  - 但缺少具体数值（如一致性相关系数、误差界限）和全面的消融实验，难以在公开信息层面判断其充分性和公平性。

## 6. 主要结论与发现

- T2V 模型在物理常识方面存在明显缺陷，尤其在**因果推理、物体行为、工具使用**等维度表现不佳。
- 提出的 PhysVidBench 能够有效揭示这些不足，并且提供了一个**结构化、可解释**的评估框架。
- 该基准可作为诊断工具，为模型输出的迭代优化提供反馈。

## 7. 主要优点

- **人类验证</strong>：基准内容经过人类确认，增强了提示与问题的生态有效性。
- **多维覆盖**：涵盖七个物理交互维度，比单一场景评测更全面。
- **关注盲区**：强调了可供性和工具中介行为，补充了现有基准较少触及的方面。
- **幻觉缓解**：用 VLM 生成字幕、再用 LLM 回答，避免了直接依赖视频像素的视觉误导，且能保持与人类评价一致。
- **可解释性**：三阶段流程让错误可以追溯到具体问题，有助于定位模型失败原因。

## 8. 不足与局限

- **信息不完整**：由于仅提供摘要，具体模型、数据规模、评估指标和统计细节缺失，无法全面评估实验严谨性。
- **依赖字幕的局限性**：字幕可能丢失视频中的视觉细节，导致部分物理错误被忽略或被错误归因。
- **维度覆盖有限**：尽管包含七个维度，但仍无法穷尽所有物理常识场景（如流体动力学、弹性碰撞等可能未覆盖）。
- **潜在偏差风险**：提示和问题设计可能受作者主观选择影响；人类验证的具体人数、协议和一致性统计未披露。
- **应用限制**：基准主要面向文本到视频生成模型，对于其他模态或音频提示的视频生成可能不适用。

---

（完）
