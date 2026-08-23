---
title: "Narrative Knowledge Weaver: A Multi-Agent Framework for Knowledge Graph Construction and Analysis from Complex Narratives"
title_zh: 叙事知识编织者：面向复杂叙事的知识图谱构建与分析多智能体框架
authors: "Qiuyu Tian, Fengyi Chen, Youyong Kong, Fan Guo, Xin Zhang, Zhijing Xie, Yuyao Li, Jinjing Shen"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=P7KtWPDhRz"
tags: ["query:manga-drama"]
score: 4.0
evidence: 从剧本构建知识图谱可支持长剧叙事一致性与连续性检查，对自动化短剧生成有辅助作用
tldr: 针对长剧情叙事中知识图谱缺乏连贯性和可解释性的问题，该论文提出多智能体框架Narrative Knowledge Weaver，结合自适应模式归纳、反思增强抽取和归一化技术，从剧本等复杂文本中构建高质量人类可读的知识图谱。该系统能够支持连续性检查与角色时间线分析，为自动化短剧生成中的剧情一致性与角色管理提供辅助工具，具有较好的跨场景应用潜力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 基于LLM的叙事抽取生成的知识图谱缺乏连贯性和可解释性，难以支持连续性检查和角色时间线分析等下游任务。
method: 提出多智能体框架，结合自适应模式归纳、反思增强抽取和归一化技术，从复杂叙事中构建高质量人类可读的知识图谱。
result: 系统能够产出连贯且可解释的知识图谱，有效支持叙事理解相关的连续性检查和角色时间线分析任务。
conclusion: 该框架为自动叙事分析和长剧生成中的剧情一致性维护提供了结构化知识支撑。
---

## Abstract
Long-form narratives such as screenplays and novels require reasoning over evolving characters,
multi-stage events, and long-range temporal and causal structure.
Although recent LLM-based methods can extract surface entities and relations, automatically
induced knowledge graphs often lack the coherence and interpretability needed for narrative
understanding and downstream tasks such as continuity checking or character timeline analysis.
We introduce $\textbf{Narrative Knowledge Weaver}$, a multi-agent framework for constructing
high-quality, human-readable knowledge graphs from complex narratives.
The system combines adaptive schema induction, reflection-augmented extraction, and a
normalization-before-merge pipeline that performs type refinement, scope convergence, and
LLM-guided disambiguation.
A dedicated module conducts $\textbf{adaptive attribute enrichment}$ for narrative entities, aggregating
multi-granular evidence and reflection-guided feedback to incrementally refine and expand
schema-defined properties.
An $\textbf{event-centric refinement}$ stage further transforms raw event mentions into structured event
cards and causally organized Event Plot Graphs (EPGs).
All outputs are stored with fine-grained provenance and leveraged by a $\textbf{tool-augmented reasoning
agent}$ for temporal, causal, and structural queries.
Evaluations on Re-DocRED, a NarrativeQA-derived benchmark, and a Practitioner Screenplay QA
dataset show substantial improvements in entity normalization, relation accuracy, and event-level
reasoning over strong baselines including EDC, Hybrid Retrieval, and GraphRAG.
Beyond quantitative gains, the resulting graphs provide interpretable, application-ready
representations of story worlds, supporting detailed analyses of narrative dynamics—from
character states to causal chains and scene-level progression.

---

## 论文详细总结（自动生成）

## 论文总结：《叙事知识编织者：面向复杂叙事的知识图谱构建与分析多智能体框架》

> 说明：以下总结基于提供的论文元数据和摘要，正文细节（如完整公式、实验配置、消融表等）未在材料中直接给出，因此在相应部分会明确指出信息缺失。

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：长形式叙事（如剧本、小说）涉及动态演化的角色、多阶段事件以及长程时间与因果结构，需要系统化的语义表示才能支持深层理解。
- **核心问题**：当前基于大语言模型（LLM）的抽取方法虽然能提取表面实体和关系，但自动构建的知识图谱往往缺乏连贯性和可解释性，难以支撑连续性检查、角色时间线分析等下游任务。
- **总体含义**：论文提出一个多智能体框架，旨在从复杂叙事中构建**高质量、人类可读**的知识图谱，从而为叙事理解、剧情一致性维护和以剧本为代表的自动化创作提供结构化知识支撑。

### 2. 论文提出的方法论

- **整体架构**：提出名为 **Narrative Knowledge Weaver** 的多智能体框架，采用模块化、流水线式协作。
- **关键技术细节**：
  - **自适应模式归纳（Adaptive Schema Induction）**：根据输入叙事动态生成知识图谱模式，而不是使用固定模板，增强对不同文本风格的适应性。
  - **反思增强抽取（Reflection-Augmented Extraction）**：在抽取过程中引入反思机制，对已抽取结果进行验证与修正，提高抽取质量。
  - **归一化-合并流水线（Normalization-before-Merge Pipeline）**：包含三种操作：
    - 类型细化（Type Refinement）
    - 范围收敛（Scope Convergence）
    - LLM引导的消歧（LLM-guided Disambiguation）
    该流程旨在先规范化实体/关系，再执行合并，以提升图谱一致性。
  - **自适应属性丰富（Adaptive Attribute Enrichment）**：针对叙事实体，聚合多粒度证据，并使用反思引导的反馈，逐步完善和扩展模式定义的属性。
  - **事件中心细化（Event-Centric Refinement）**：将原始事件提及转换为结构化事件卡片，并进一步构建具有因果组织的事件图（Event Plot Graphs, EPGs）。
  - **工具增强推理代理（Tool-Augmented Reasoning Agent）**：所有图谱输出均带有细粒度来源（provenance），并由该代理支持时间、因果和结构类查询。
- **公式/算法流程**：所提供材料未给出具体数学公式；在文字层面，方法遵循“模式归纳 → 抽取 → 归一化与合并 → 属性丰富 → 事件细化 → 图谱存储与查询”的流程。

### 3. 实验设计

- **数据集与基准（Benchmark）**：
  - **Re-DocRED**（关系抽取基准）
  - **NarrativeQA 派生基准**（面向叙事理解）
  - **Practitioner Screenplay QA 数据集**（剧本问答场景）
- **对比方法**：
  - EDC
  - Hybrid Retrieval
  - GraphRAG
- **评估维度**：
  - 实体归一化（Entity Normalization）
  - 关系准确率（Relation Accuracy）
  - 事件级推理（Event-Level Reasoning）

### 4. 资源与算力

- 材料中**未明确说明**所使用的 GPU 型号、数量、训练/推理时长等算力资源。
- 推测需要一定规模的 LLM 调用，但具体硬件与成本不得而知。

### 5. 实验数量与充分性

- 摘要报告了在**三个不同数据集**上的实验，并对比了三种强基线方法，覆盖实体、关系和事件三个层面的指标。
- 但受限于可获取信息：
  - 没有提供消融实验的具体数量与结果。
  - 未展示每个数据集上的详细指标数值。
  - 未提及统计显著性检验或多次运行方差。
- 因此，**实验覆盖度可观，但充分性与公平性难以完全判断**；至少需要在论文全文中查看消融研究和详细数值才能做出更准确评价。

### 6. 论文的主要结论与发现

- 该框架能够在实体归一化、关系准确率和事件级推理等方面显著优于现有基线（EDC、Hybrid Retrieval、GraphRAG）。
- 输出的知识图谱具有可解释性和应用即用性，能够刻画故事世界，支持从角色状态、因果链到场景级推进的精细叙事分析。
- 可以为自动化短剧生成中的**剧情一致性与角色管理**提供辅助工具。

### 7. 优点

- **方法设计系统性强**：将模式归纳、抽取、归一化、属性丰富、事件细化组织为完整流水线，思路清晰。
- **强调可解释性与人类可读性**：不同于一般黑箱图谱，其输出便于人工审阅和下游分析。
- **多智能体协作**：不同模块各司其职，结合反思机制，有助于提升抽取鲁棒性。
- **支持多类型查询**：通过工具增强代理，支持时间、因果和结构查询，应用面广。
- **跨场景验证**：在通用关系抽取（Re-DocRED）、叙事问答（NarrativeQA派生）和剧本问答上均验证，表明一定泛化能力。

### 8. 不足与局限

- **信息可得性限制**：基于提供的摘要，无法获取算法细节、提示词设计、智能体交互方式等关键内容。
- **算力与效率未报告**：没有关于推理成本、运行时间和资源消耗的说明，实际部署可行性未知。
- **消融实验缺失/不明**：摘要未提及消融研究，无法判断各模块的独立贡献。
- **基线覆盖有限**：仅与少量基线对比，缺少与更多最新知识图谱构建方法（如基于图神经网络或其它检索增强方法）的比较。
- **数据集偏斜风险**：三个数据集中有两个偏向文档/剧本领域，对于更广泛的叙事类型（如口头故事、新闻叙事、游戏剧情）的泛化性尚未验证。
- **潜在偏差与错误分析缺乏**：未讨论抽取失败类型、错误传播、归一化丢失信息等局限。

（完）
