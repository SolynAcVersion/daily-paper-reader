---
title: "AudioChat: Unified Audio Storytelling, Editing, and Understanding with Transfusion Forcing"
title_zh: AudioChat：利用透射强制实现统一音频故事生成、编辑与理解
authors: "William Chen, Prem Seetharaman, Rithesh Kumar, Oriol Nieto, Shinji Watanabe, Justin Salamon, Zeyu Jin"
date: 2026-04-30
pdf: "https://openreview.net/pdf/ed67262e8f56128e324f28433319c023b0d461df.pdf"
tags: ["query:manga-drama"]
score: 6.0
evidence: 统一音频故事生成框架，支持多说话人与音效，可服务于短剧配音与音频制作。
tldr: 该文提出AudioChat框架，面向多说话人、前景/背景音效等复杂音频故事，实现生成、编辑与理解三类任务的统一。核心思想是利用LLM工具调用智能体模拟用户与系统交互的对话作为训练数据，并引入新型Transfusion Forcing范式和音频分词方法。该方法为短剧视频的音轨创作提供了可复用的基础模型技术。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有音频基础模型难以处理多音源叠加的复杂音频故事场景。
method: 通过LLM工具调用智能体模拟交互对话生成训练数据，并采用Transfusion Forcing统一生成、编辑与理解。
result: 在音频故事相关任务上验证了统一框架及模拟对话数据的有效性。
conclusion: 为多说话人、多音效的音频生成提供新范式，可支持短剧配音与音效制作。
---

## Abstract
Despite recent breakthroughs, audio foundation models struggle in processing complex multi-source acoustic scenes. We refer to this challenging domain as audio stories, which can have multiple speakers and background/foreground sound effects. Compared to traditional audio processing tasks, audio stories introduce new layers of semantic, temporal, and physical complexity. To address this challenge, we propose AudioChat, a framework for developing audio foundation models that can generate, edit, and understand audio stories. AudioChat introduces a new paradigm in which LLM-based toolcalling agents simulate interactions between users and the system, and these simulated dialogues are used as training data. We also introduce a novel Audio Transfusion Forcing objective to train the AudioChat model, allowing it to simultaneously decompose high-level instructions via structured chain-of-thought reasoning and perform interactive multi-turn audio understanding/generation. To evaluate generation and editing performance, we develop three new metrics that directly measure task performance instead of relying upon distribution-based scoring. We highly encourage readers to visit our demo to better understand the capabilities of AudioChat: https://audiochat-icml-2026.github.io/.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有音频基础模型在处理复杂多源声学场景时存在明显局限。论文将这类场景定义为“音频故事”（audio stories），其特点是包含**多个说话人**以及**前景/背景音效**的叠加，在语义、时间和物理层面引入了新的复杂性。
- **研究动机**：传统的音频处理任务（如语音识别、声音事件检测等）多聚焦于单一或简单源场景，难以胜任音频故事这种多音源、高交互、时序依赖强的场景。
- **整体含义**：论文提出 AudioChat 框架，旨在构建统一的音频基础模型，使得**生成、编辑与理解**三类任务在同一个框架下完成。这为短剧配音、音效制作等创造性音频内容生产提供了新的基础技术路径。

## 2. 论文提出的方法论

- **核心思想**：将音频故事建模为多轮交互过程，通过模拟用户与系统之间的对话来生成训练数据，从而让模型学会在动态交互中完成复杂的音频任务。
- **关键技术与流程**：
  - **LLM 工具调用智能体模拟交互**：使用基于大语言模型（LLM）的工具调用智能体，模拟用户与音频系统之间的自然交互对话，并将这些模拟对话作为训练数据。这种方式可以低成本地生成大规模、多样化的交互式训练样本。
  - **Audio Transfusion Forcing 训练目标**：一种新的训练范式，允许模型在训练时**同时进行结构化的链式思维推理（chain-of-thought）**，以逐层分解高级指令，并完成**交互式的多轮音频理解与生成**。该目标将理解与生成统一在同一训练进程中，而非分离的模块。
  - **整体流程（文字说明）**：输入高级指令 → 模型通过链式思维将其分解为子任务 → 调用相应工具或生成音频 → 在下一轮交互中根据用户反馈进行编辑或再理解，形成闭环。

## 3. 实验设计

- **数据集与场景**：摘要中未明确列出具体数据集的名称与规模，仅表明实验聚焦于“音频故事”相关任务，即多说话人和多音效的复杂声学场景。
- **Benchmark**：论文提出开发了**三个新指标**，用于直接衡量生成与编辑的任务表现，而非依赖基于分布的打分（如 FID 等）。这体现了对任务导向评估的重视，但具体指标名称与计算方式未在摘要中详述。
- **对比方法**：未在摘要中明确提及与哪些基线方法进行了对比。

## 4. 资源与算力

- 论文摘要与元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长、参数量等算力资源细节。因此，无法对该方法的训练成本进行量化评估。

## 5. 实验数量与充分性

- **实验数量**：摘要中提到在“音频故事相关任务”上验证了统一框架及模拟对话数据的有效性，并且开发了三个新的评估指标。
- **充分性评估**：由于未提供具体的实验组数、数据集列表、消融实验细节和与基线方法的量化对比，当前信息**不足以全面判断实验的客观性与公平性**。特别是缺少对“模拟对话数据有效性”这一核心贡献的消融验证细节。

## 6. 论文的主要结论与发现

- **统一框架的可行性**：AudioChat 成功地将生成、编辑与理解三类任务统一到一个模型框架中，并验证了其在音频故事场景中的有效性。
- **模拟对话数据的有效性**：通过 LLM 工具调用智能体生成模拟交互对话作为训练数据，这一数据策略被实验证明是有效的。
- **新训练范式的价值**：引入的 Audio Transfusion Forcing 目标可以同时支持结构化推理与多轮交互式处理，为复杂音频任务提供了一种新的训练思路。
- **应用前景**：该方法为多说话人、多音效场景下的音频生成提供了新范式，尤其可服务于短剧配音、音效制作等实际应用。

## 7. 优点

- **任务统一性**：将生成、编辑、理解三大任务融合在一个框架中，避免了传统方法中任务分离带来的工程与性能损失。
- **数据生成新范式**：利用 LLM 工具调用智能体模拟用户交互，是一种低成本、可扩展的训练数据生产方法，且更贴近真实使用场景。
- **推理与生成结合**：通过 Transfusion Forcing 同时进行结构化推理和多轮生成，有助于处理复杂高级指令的分解与执行。
- **任务导向评估**：提出直接衡量任务表现的三个新指标，相比分布相似性评估更能反映真实应用中的模型能力。

## 8. 不足与局限

- **实验细节缺失**：摘要中未提供数据集规模、具体实验设置、基线方法列表及定量结果，难以对方法的有效性和相对优势做出准确判断。
- **评估指标未展开描述**：三个新指标的具体定义、计算方式、与既有指标的相关性及其可靠性尚不明确，需在全文或附录中进一步验证。
- **模拟数据与真实用户偏差风险**：LLM 模拟的用户交互可能与真实用户行为存在分布差异，可能导致模型在真实场景中的泛化性不足。
- **应用范围限制**：方法明确针对“音频故事”场景，对于更通用的音频理解或简单音频处理任务，其优势是否依然成立未得到说明。
- **算力成本不透明**：缺乏训练所需的资源和时间信息，限制了从工程角度评估其实用性。

（完）
