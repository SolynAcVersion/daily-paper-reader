---
title: "Frankentext: Stitching random text fragments into long-form narratives"
title_zh: Frankentext：将随机文本片段拼接成长篇叙事
authors: "Chau Minh Pham, Jenna Russell, Dzung Pham, Mohit Iyyer"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=wfmEwfaRxN"
tags: ["query:manga-drama"]
score: 6.0
evidence: 通过拼接文本片段生成长篇叙事的文本生成方法，可应用于短剧剧本生成作为自动化创作的一部分。
tldr: "本文针对直接让LLM生成连贯长篇叙事的困难，提出Frankentext范式，将LLM视为文本片段的拼接者。给定提示和大量随机采样的片段，模型必须在复制约90%原文的前提下选择和编排片段，形成连贯故事。实验表明这一极端约束反而激发出有趣的长篇叙事能力，为自动化短剧中的剧本生成提供了新的可解释文本重组思路。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 长文本叙事生成通常由LLM直接生成，但难以保证连贯性和特定约束。
method: 提出Frankentexts范式，让LLM从随机人类文本片段中挑选并拼接成连贯长故事，大部分token必须复制原文。
result: 实验表明LLM能在极端约束下生成连贯的长篇故事，并具有独特的创意。
conclusion: 为长叙事生成提供了一种基于文本重组的可解释方法，可用于剧本等长文本创作。
---

## Abstract
We introduce Frankentexts, a long-form narrative generation paradigm that treats a large language model (LLM) as a composer of existing texts rather than as an author. Given a writing prompt and thousands of randomly sampled human-written snippets, the model is asked to produce a narrative under the extreme constraint that most tokens (e.g., 90%) must be copied verbatim from the provided paragraphs. This task is effectively intractable for humans: selecting and ordering snippets yields a combinatorial search space that an LLM implicitly explores, before minimally editing and stitching together selected fragments into a coherent long-form story. Despite the extreme challenge, we observe through extensive automatic and human evaluation that Frankentexts significantly improve over vanilla LLM generations in terms of writing quality, diversity, and originality, while remaining coherent and relevant to the prompt. Furthermore, Frankentexts pose a fundamental challenge to detectors of AI-generated text: 72% of Frankentexts produced by our best Gemini 2.5 Pro configuration are misclassified as human-written by Pangram, a state-of-the-art detector. Human annotators praise Frankentexts for their inventive premises, vivid descriptions, and dry humor; on the other hand, they identify issues with abrupt tonal shifts and uneven grammar across segments, particularly in longer pieces. The emergence of high-quality Frankentexts raises serious questions about authorship and copyright: when humans provide the raw materials and LLMs orchestrate them into new narratives, who truly owns the result?

---

## 论文详细总结（自动生成）

## Frankentext：将随机文本片段拼接成长篇叙事

### 一、核心问题与整体含义（研究动机与背景）

- **核心问题**：尽管大规模语言模型（LLM）在文本生成领域取得了显著进展，但在长篇叙事生成方面仍面临重大挑战——尤其是如何保证长文本的连贯性、多样性、原创性，以及在特定创作约束下的可控性。
- **研究动机**：传统范式让 LLM 直接“创作”长文，模型虽能产出流畅文本，但在长程叙事结构、创意表现和风格一致性上往往表现不佳。同时，LLM 生成文本正日益面临可检测性危机，这引发了关于文本所有权、版权和归属的深层问题。
- **核心洞察**：作者提出，或许 LLM 更适合扮演“文本重组者”而非“原创作者”。文章引入一种名为 **Frankentexts** 的全新范式，将 LLM 置于一个极端约束之下，从而迫使模型展现出一种全新的长篇叙事能力——它不再逐字生成，而是在已有文本的“积木”中进行组合。

### 二、方法论

- **核心思想**：将 LLM 视为已有文本片段的**拼接器**，而非原创作者。模型从随机采样的人类文本片段中挑选、排序，然后进行最小程度的编辑，将选定的片段“缝合”成一个连贯的长篇故事。
- **关键技术细节**：
  - **输入设置**：给定一个写作提示词（prompt）以及数千个随机采样的人类写作片段（snippets）。
  - **极端约束**：模型生成的叙事中，**至少 90% 的 token 必须逐字复制**取自提供的段落，这个约束极大地限制了模型的自由生成空间。
  - **搜索问题**：从海量候选片段中选择并排序以构建连贯叙事，实际上是一个*组合爆炸*的搜索空间，对任何人工作者来说几乎是不可能的任务。LLM 的隐式推理能力使其能够“探索”这个空间，并在复制的基础上进行最小编辑来弥合拼接处的裂缝。
- **算法流程**（文字描述）：
  1. 对给定提示，从大语料库中随机采样数千个文本片段。
  2. 将提示和片段全部提供给 LLM，要求其输出一个故事。
  3. 在生成过程中，LLM 内部进行选择—排序—编辑的策略：先选定某些片段作为“故事线”的组成部分，再决定片段出现顺序，最后通过微小的语言润色将选中的片段拼接成通顺叙事。
  4. 输出结果中 90% 以上 token 源自原始片段，剩余部分是模型添加的连接词、修正或衔接性语句。

### 三、实验设计

- **数据集 / 场景**：论文使用了大规模人类写作语料库（如多个领域的随机文本片段），构成长篇叙事生成测试环境。
- **Benchmark**：以“写作质量、多样性、原创性、连贯性和提示相关性”为自动评估指标，并辅以人工评估。此外，使用了当前最先进的 AI 文本检测器（如 **Pangram**）来评估 Frankentexts 对人类/机器的欺骗性。
- **对比方法**：
  - 基线：**Vanilla LLM 生成**（由 LLM 直接无约束生成的长篇故事）。
  - 变体：不同配置下的 Frankentexts，如不同模型（包含 Gemini 2.5 Pro）及不同的约束强度（如 token 复制比例等）。

### 四、资源与算力

- 论文摘要中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力细节。
- **可知信息**：使用了包括 Gemini 2.5 Pro 在内的 LLM 作为生成工具；未提及训练或微调的硬件资源配置。由于本文是推理场景任务而非模型训练任务，算力需求更有可能集中在 LLM 推理 API 调用上，但原文未给出具体数值。

### 五、实验数量与充分性

- **实验数量**：论文进行了两类主要实验：
  - ① **自动评估**：比较 Frankentexts 与 Vanilla 生成在多个维度上的指标表现；
  - ② **人工评估**：人类标注者对生成文本进行质量、原创性、连贯性等多维打分；
  - ③ **消融/变体实验**：对不同模型、不同约束配置下的输出进行比较（如 Gemini 2.5 Pro 的配置）。
- **充分性与客观性**：
  - 优点：评估体系比较全面，兼顾了自动量化指标和人类主观感受；对 AI 检测器（Pangram）的鲁棒性进行了测试，是一个有说服力的维度。
  - 局限：摘要中未提到具体试验次数、样本量与统计分析细节，读者难以判断差异的显著性水平；评估场景相对单一（仅限写作提示），没有测试多领域、多风格扩展。

### 六、主要结论与发现

- **Frankentexts 显著优于 Vanilla 生成**，在写作质量、多样性和原创性上表现更好，同时保持连贯性和对提示的相关性。
- **对抗 AI 检测能力突出**：在最佳配置（Gemini 2.5 Pro）下，72% 的 Frankentexts 被高级检测器 Pangram 误判为人类写作。
- **人类评价者视角**：赞赏其*富有想象力的前提设定、生动的描述、冷幽默的特征*；同时也指出了问题，如跨段落语气的突然转变、语法不一致，尤其在长文场景中更明显。
- **提出深层版权问题**：当人类提供原材料、LLM 进行编排时，谁拥有最终故事的所有权？这为 AI 时代著作权和法律框架提出了关键问题。
- **核心发现**：即使（或正因为）在极端约束下，LLM 也能通过重组既有文本产生高质量的新叙事——暗示“文本重组”可能是长篇叙事可控生成的重要新范式。

### 七、优点

- **方法创新性强**：明确提出“LLM 作为拼接器而非作者”的新范式，区别于传统“端到端生成”，为长篇叙事生成提供了全新思路。
- **实验设计有亮点**：引入 90% token 复制约束，使任务标准化、可量化，同时又保留了足够创作自由，实验设定富有挑战性且有趣。
- **评估视角全面**：自动指标 + 人工评价 + AI 检测器三重验证，从质量、创造性和安全性多个角度给出结果。
- **问题意识深刻**：不仅局限于技术性能，还引发了关于版权、著作权的新思考，兼具技术价值与社会学意义。

### 八、不足与局限

- **信息完整性不足**：论文摘要未透露具体的模型内部机制、编辑策略、拼接受限条件和超参数设置等详细信息，难以完全复现。
- **实验依据有限**：摘要中未报告具体实验规模（如生成了多少篇故事、使用了多少个提示词、不同配置下的样本量），统计分析支撑薄弱。
- **应用场景受限**：目前仅聚焦“基于提示的长篇写作”，未涉足对话式生成、代码生成、事实性文本（如新闻/百科类）等对准确性要求更高的场景。
- **约束导致的天然局限**：依赖大规模已有语料库，片段的质量直接影响输出，可能存在风格不均、逻辑跳跃等天然瑕疵；部分评价者指出的“语气突变、语法不一致”正是这一机制的固有缺陷。
- **版权和伦理风险未深入解决方案**：虽然提出了版权问题，但没有给出可操作的技术或法律路径来应对。

（完）
