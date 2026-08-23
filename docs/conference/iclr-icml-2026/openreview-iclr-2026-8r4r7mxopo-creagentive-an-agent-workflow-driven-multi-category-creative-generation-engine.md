---
title: "CreAgentive: An Agent Workflow Driven Multi-Category Creative Generation Engine"
title_zh: CreAgentive：智能体工作流驱动的多类别创意生成引擎
authors: "Yuyang Cheng, Linyue Cai, Changwei Peng, Yumiao xu, Rongfang Bie, Yong Zhao"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=8R4r7MXOpo"
tags: ["query:manga-drama"]
score: 8.0
evidence: 用于故事与剧本生成的智能体工作流，能生成具备叙事连贯性和结构约束的戏剧内容，是短剧剧本生成的核心技术。
tldr: 该文提出由智能体工作流驱动的多类别创意生成引擎，利用基于知识图谱的故事原型将叙事逻辑与风格实现解耦，并通过初始化、构建、润色三阶段工作流生成故事与剧本。它能解决大模型在生成戏剧等长创意内容时类型多样性不足、长度受限、叙事连贯性弱及结构约束难以落实的问题。该工作为短剧自动化生产中的剧本生成与情节规划提供直接可用的技术方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有大模型生成戏剧等长创意内容时存在类型单一、长度不足、叙事弱和结构约束难实现等问题。
method: 基于知识图谱的故事原型解耦故事逻辑与风格，采用三阶段智能体工作流生成多类别创意文本。
result: 提升了生成内容的类型多样性、长度、叙事连贯性与结构复杂度，适用于戏剧与故事创作。
conclusion: 为短剧剧本的自动化创作提供了一套可复用的智能体工作流与叙事表示方法。
---

## Abstract
We present CreAgentive, an agent workflow driven multi-category creative generation engine that addresses four key limitations of contemporary large language models in writing stories, drama and other categories of creatives: restricted genre diversity, insufficient output length, weak narrative coherence, and inability to enforce complex structural constructs. At its core, CreAgentive employs a Story Prototype, which is a genre-agnostic, knowledge graph-based narrative representation that decouples story logic from stylistic realization by encoding characters, events, and environments as semantic triples. CreAgentive engages a three‑stage agent workflow that comprises: an Initialization Stage that constructs a user‑specified narrative skeleton; a Generation Stage in which long‑ and short‑term objectives guide multi‑agent dialogues to instantiate the Story Prototype; a Writing Stage that leverages this prototype to produce multi‑genre text with advanced structures such as retrospection and foreshadowing. This architecture reduces storage redundancy and overcomes the typical bottlenecks of long‑form generation. In extensive experiments, CreAgentive generates thousands of chapters with stable quality and low cost (less than \$1 per 100 chapters) using a general-purpose backbone model. To evaluate performance, we define a two-dimensional framework with 10 narrative indicators measuring both quality and length. Results show that CreAgentive consistently outperforms strong baselines and achieves robust performance across diverse genres, approaching the quality of human-authored novels.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机

- 当代大语言模型（LLM）在生成故事、戏剧等多类创意文本时存在四大关键局限：
  - **类型多样性不足**：难以稳定覆盖多种文学/戏剧体裁；
  - **输出长度受限**：长文本生成容易出现质量衰减或提前终止；
  - **叙事连贯性弱**：长故事/剧本中情节主线、角色动机容易失焦；
  - **结构约束难以落实**：无法可靠地强制实现倒叙、伏笔、多线叙事等复杂叙事结构。

- 论文提出 **CreAgentive**——一个由智能体工作流驱动的多类别创意生成引擎，旨在解决上述问题，为短剧剧本自动化生产等场景提供可复用的技术方案。

## 2. 方法论

### 核心思想
- 将**故事逻辑**与**风格实现**解耦，通过一种与类型无关的叙事表示——**Story Prototype（故事原型）**——来统一承载故事的结构性信息。
- Story Prototype 基于**知识图谱**构建，将角色、事件、环境编码为**语义三元组**，从而以结构化形式表达叙事骨架，降低后续生成阶段的存储冗余，并缓解长文本生成的瓶颈。

### 三阶段智能体工作流
- **初始化阶段（Initialization Stage）**：
  - 根据用户需求构建一个明确的叙事骨架（narrative skeleton），确定故事的人物、事件脉络与环境。
- **生成阶段（Generation Stage）**：
  - 由**长期目标**与**短期目标**共同引导多个智能体进行对话式协作，逐步将故事原型实例化，确保叙事目标在长生成过程中持续对齐。
- **写作阶段（Writing Stage）**：
  - 利用已完成实例化的故事原型，生成多类型（multi-genre）文本；
  - 支持**倒叙**（retrospection）、**伏笔**（foreshadowing）等高级结构的落实。

> 论文未提供公式化算法伪代码。整体流程可概括为：*构建骨架 → 多智能体实例化 → 原型驱动的风格化写作*。

## 3. 实验设计

- **数据集/场景**：论文摘要未明确列出具体公开数据集，但声称在**多种不同体裁**（diverse genres）上进行了广泛实验，且实验规模达到**数千章节**（thousands of chapters）。
- **Benchmark**：作者定义了一个**二维评估框架**，包含 **10 个叙事指标**，分别衡量生成内容的**质量**与**长度**。
- **对比方法**：摘要中提到与**强基线（strong baselines）**进行对比，但未给出具体基线模型名称。
- **骨干模型**：使用**通用型大模型**（general-purpose backbone model）作为基础生成器，而非专用大模型。

## 4. 资源与算力

- 论文摘要中**没有明确说明**使用的 GPU 型号、数量、训练时长或训练步数。
- 已知信息包括：
  - 使用“通用型骨干模型”（未指出具体参数量或厂商）；
  - 推理/生成成本极低：**低于 1 美元 / 100 章**；
  - 能在低成本下生成**数千章节**且保持稳定质量。

## 5. 实验数量与充分性

- 实验覆盖面较广：包括多类型创意文本生成、长文本稳定性测试、成本评估，以及与传统强基线的性能对比。
- 评估指标体系完备（10 个指标、质量与长度两维度），具有一定方法论意义。
- **不足之处**：由于本文仅提供摘要而未展示完整实验章节，无法获知：
  - 具体实验组数与每组的重复次数；
  - 是否进行了系统的消融实验（例如移除 Story Prototype 或拆分三阶段流程）；
  - 基线模型的选取标准与参数设置；
  - 人工评估的评分者数量与一致性检验。
- 因此，**实验充分性无法从现有材料中完全判断**。从摘要看设计完整，但客观公平性需要更多细节支撑。

## 6. 主要结论

- CreAgentive 在 **类型多样性、输出长度、叙事连贯性、结构复杂度** 四个方面均优于强基线；
- 在多种体裁上表现稳健，生成质量**接近人类作者撰写的小说**水平；
- 可以在极低经济成本（< \$1/100 章）的前提下实现大规模长文本生成，且质量稳定。

## 7. 优点

- **叙事逻辑与风格解耦**：基于知识图谱的 Story Prototype 是一种高可复用、低冗余的中间表征，避免了直接端到端生成的不可控性。
- **三阶段工作流设计清晰**：将“骨架构建→实例化→文本化”拆分，使长目标与短目标分别得到管理，逻辑上能够有效应对长文本生成中的连贯性与结构约束问题。
- **低成本高效率**：在通用骨干模型上实现了极低生成成本，具有工程可用性。
- **评估框架具有启发性**：提出的二维 10 指标框架可服务于创意生成任务的标准化评测，且同时考虑质量与长度，比单一指标更全面。

## 8. 不足与局限

- **实验细节缺失**：论文抽提内容仅包含摘要，未提供完整实验设置、具体基线和消融结果，难以全面验证结论的稳健性。
- **可能存在的偏差风险**：叙事质量指标往往是主观的，若缺乏人工评估的一致性验证与盲测设计，结论可能受到评测偏差影响。
- **类型覆盖的未知边界**：虽然宣称支持多类别，但对极端风格、跨模态或互动式叙事（如游戏剧本）的适用范围未在摘要中说明。
- **应用限制**：故事原型的构建与实例化依赖知识图谱设计，如何自动构造高质量图谱、如何处理用户定制约束的冲突，仍有待深入探讨。
- **与人类创作差距的表述**：“接近人类作者”是一个相对模糊的表述，缺少具体量化标准或读者调研支持。

---

（完）
