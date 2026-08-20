---
title: Can Your Model Separate Yolks with a Water Bottle? Benchmarking Physical Commonsense Understanding in Video Generation Models
title_zh: 你的模型能用矿泉水瓶分离蛋黄吗？视频生成模型物理常识理解基准
authors: "Baris Sarper Tezcan, Enes Sanli, Erkut Erdem, Aykut Erdem"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=RsletK8757"
tags: ["query:phys-video"]
score: 9.0
evidence: T2V模型物理常识与推理基准
tldr: 当前文本生成视频模型常违反物理常识，例如因果、物体行为和使用工具等方面的直觉预期。针对这一问题，作者提出PhysVidBench基准，包含覆盖七个物理交互维度的人工验证提示，并用三阶段流程评估多个SOTA模型的物理推理能力。实验显示现有模型在物理合理性上仍明显不足。该基准为衡量和改善视频生成物理正确性提供了评测工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: T2V模型常违反物理常识，缺乏系统性评测基准。
method: 构建PhysVidBench基准，含七个物理交互维度的提示集和三阶段评测流程。
result: 评测显示现有SOTA模型在物理合理性上明显不足。
conclusion: 为视频生成物理正确性提供标准评测工具。
---

## Abstract
Recent advances in text-to-video (T2V) generation have enabled visually compelling outputs, but models still struggle with everyday physical commonsense, often producing videos that violate intuitive expectations of causality, object behavior, and tool use. We introduce PhysVidBench, a human-validated benchmark for assessing physical reasoning in T2V models. It comprises carefully curated prompts spanning seven dimensions of physical interaction, from material transformation to temporal dynamics, offering broad, multi-faceted coverage of scenarios where physical plausibility is critical. For each prompt, we generate videos using diverse state-of-the-art models, and evaluate them through a three-stage pipeline: grounded physics questions are derived from each prompt, generated videos are captioned with a vision–language model, and a language model answers the questions using only the captions. This strategy mitigates hallucination and produces scores that align closely with human judgments. Beyond evaluation, PhysVidBench also serves as a diagnostic tool, enabling feedback-driven refinement of model outputs. By emphasizing affordances and tool-mediated actions, areas often overlooked in existing benchmarks, PhysVidBench provides a structured, interpretable framework for assessing and improving everyday physical commonsense in T2V models.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义

- **研究动机**：文本生成视频（Text-to-Video, T2V）模型近年来在生成视觉效果上取得了显著进展，输出画面日益精美。然而，这些模型在**日常物理常识（everyday physical commonsense）** 的理解上仍存在系统性缺陷，经常生成违反因果直觉、物体行为规律和工具使用逻辑的视频片段。
- **核心研究问题**：当前 T2V 模型在物理合理性方面究竟表现如何？是否存在系统性的评测方法，能够客观、可解释地衡量模型的物理推理能力？
- **整体意义**：论文指出，现有视频生成评测基准大多关注视觉质量、文本对齐或动作多样性，**鲜有专门针对物理常识的系统性评测**，尤其是"功能可供性（affordance）"与"工具中介行为（tool-mediated actions）"这两类物理交互维度长期被忽视。该工作填补了这一空白，为视频生成模型的物理常识能力提供了结构化的评测与诊断框架。

### 2. 论文提出的方法论

- **核心思想**：构建一个人工验证的基准数据集 PhysVidBench，配合一条"生成—转述—推理"的三阶段评测流水线，以**纯文本推理的方式**评估视频生成模型的物理合理性，从而规避视觉语言模型（VLM）直接理解视频时可能产生的幻觉问题。
- **基准构建（PhysVidBench）**：
  - 提示词（prompts）经过人工验证，覆盖**七个物理交互维度**：材料转化（material transformation）、时间动态（temporal dynamics）等，从多角度考察物理合理性关键场景。
- **三阶段评测流水线**：
  1. **问题生成**：针对每个 prompt 派生出一个以物理常识为基础的接地问题（grounded physics question），问题具有明确答案，便于客观评分。
  2. **视频转述**：将生成的视频交给视觉语言模型（VLM），生成对应的文本描述（caption）。
  3. **文本推理与回答**：语言模型（LM）仅基于上一步的 caption 来回答物理问题，不与视频直接交互，从而隔离 VLM 的视觉理解误差，提升评分与人类判断的一致性。
- **诊断功能**：该评测管线不仅用于打分，还可以定位失败原因，支持对模型输出的**反馈驱动优化（feedback-driven refinement）**，即根据物理错误类型提供可操作的改进方向。

### 3. 实验设计

- **数据集/基准**：论文的核心评测工具为自建的 **PhysVidBench 基准**，提示词覆盖七个物理交互维度，强调传统基准忽略的功能可供性和工具使用场景。
- **被测模型**：研究使用多个**当前最先进（state-of-the-art）的 T2V 模型**生成视频作为评测对象，但摘要中未逐一点名具体模型。
- **对比方法**：论文未在摘要中列出传统对比方法或消融模型，但从方法论看，实验的核心对比是**模型自动评分 vs. 人类判断**，以验证评测分数与人类感知的一致性。
- **评估方式**：采用上述三阶段流水线进行自动化评估，并以人类判断作为对齐基准。

### 4. 资源与算力

- 论文摘要中**未明确说明**所使用的 GPU 型号、数量、训练时长或推理计算开销等具体资源信息。
- 需要注意的是：视频生成模型推理、VLM 转述和 LM 推理均涉及较大的计算量，但作者未在摘要中披露相关算力细节，如需完整了解，应查阅论文正文的实验设置部分。

### 5. 实验数量与充分性

- **实验数量**：摘要中未给出具体的实验组数或消融数量。根据描述可推断，实验至少涵盖：
  - 多个 SOTA T2V 模型在 PhysVidBench 全部七个维度上的视频生成；
  - 自动化三阶段评测与人类判断的一致性对比；
  - 基准作为诊断工具的应用性验证。
- **充分性与公平性评估**：
  - **优势**：采用人工验证的提示词和人类判断作为对齐基准，有助于保证评测的客观性和公平性。
  - **潜在不足**：摘要中未提及实验的具体规模、模型覆盖面、帧数设置、视频长度控制等细节，因而难以从摘要层面完全判断实验的充分程度。同时，"仅基于 VLM 转述文本"的评测方式虽然规避了视频直接理解的幻觉，但也可能引入转述信息丢失的偏差，需要正文中的对比实验加以佐证。

### 6. 论文的主要结论与发现

- 当前主流的 T2V 模型虽然能生成视觉上吸引人的视频，但在**物理常识推理方面仍有显著缺陷**，尤其在涉及因果链条、物体行为规律和工具使用等场景中，输出往往不符合物理直觉。
- 通过 PhysVidBench 的系统评测，能够**稳定地暴露这些物理常识缺陷**，且自动评测得分与人类判断高度一致，说明该基准具有较高的可信度和实用价值。
- 论文还发现，将评测管线用作**诊断工具**时，可以为模型输出的物理合理性改进提供明确的反馈信号，而不只是提供一个粗粒度的评分。

### 7. 优点

- **填补空白**：首次系统性地将物理常识评测覆盖到功能可供性和工具中介行为，拓展了既有视频评测基准的维度。
- **多维度覆盖**：七个物理交互维度设计较为全面，能多角度考察模型的物理推理能力。
- **评测方法创新**：三阶段流水线通过"视频→文本→问答"的转化，将复杂的视频物理判断问题降解为文本推理问题，有效降低 VLM 幻觉干扰，提高了评测的可靠性。
- **人类对齐**：基准提示词经过人工验证，评测结果与人类判断对齐良好，增强了评估结果的可信度。
- **可解释性与工具价值**：不仅是评分基准，还能作为诊断工具辅助模型改进，应用价值更高。

### 8. 不足与局限

- **信息缺失**：作为摘要，未披露具体模型名单、实验规模、消融设计、数据集大小、算力配置等细节，难以全面评估实验的完备性。
- **依赖文本转述**：三阶段评估依赖 VLM 对视频的转述质量，如果 VLM 遗漏关键物理细节，评测结果可能出现偏差；尽管该方法旨在缓解幻觉，但并未完全消除信息损耗问题。
- **二元正确性刻画**：基于"问答—判分"的方式可能不足以刻画视频物理合理性的连续性或部分合理性（如物体先正确后错误的行为），存在评分粒度较粗的风险。
- **覆盖范围限制**：物理常识维度虽然多，但仍无法覆盖全部物理交互类型（如流体力学、热传导等复杂物理现象），且提示词规模是否足够大以保证统计稳健性，摘要中未给出。
- **模型时效性**：评测所用 SOTA 模型会随技术发展快速过时，基准本身的长期适用性需要后续持续迭代与扩展。

（完）
