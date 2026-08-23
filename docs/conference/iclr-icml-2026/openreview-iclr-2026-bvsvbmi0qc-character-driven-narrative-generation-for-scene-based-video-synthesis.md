---
title: Character-Driven Narrative Generation for Scene-Based Video Synthesis
title_zh: 面向基于场景的视频合成的角色驱动叙事生成
authors: "Taewon Kang, Ming Lin"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=bVsVbmI0qC"
tags: ["query:manga-drama"]
score: 8.0
evidence: 面向场景视频合成的角色驱动叙事对白生成直接支持漫剧自动化创作
tldr: 针对基于场景的视频合成缺乏角色驱动对白和语音表达的问题，该论文提出一个模块化流水线，将动作级提示转换为视觉和听觉上落地的人物对话，从而丰富视觉叙事的角色魅力。方法支持角色一致性表达，并可与现有故事生成模型搭配使用，为自动化漫剧和微短剧中的对白生成提供了关键模块，显著提升生成剧情的自然度和表现力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 场景级视频生成缺乏角色驱动的对白和语音，导致角色表达不足和视觉叙事不够生动。
method: 构建模块化流水线，将动作级提示转化为与场景视觉和听觉相一致的、具有角色一致性的对话语音。
result: 生成的对白自然且角色一致，有效增强叙事视频中的角色表现力与内容吸引力。
conclusion: 为自动化短剧和漫剧制作提供角色驱动对白生成方法，可集成到视频合成系统中。
---

## Abstract
Recent advances in scene-based video generation have enabled systems to synthesize coherent visual narratives from structured prompts. However, a crucial dimension of storytelling—character-driven dialogue and speech—remains underexplored. In this paper, we present a modular pipeline that transforms action-level prompts into visually and auditorily grounded narrative dialogue, enriching visual storytelling with natural voice and character expression. Our method takes as input a pair of prompts per scene, where the first defines the setting and the second specifies a character’s behavior. While a story generation model such as Text2Story produces the corresponding visual scene, we focus on generating expressive, character-consistent utterances grounded in both the prompts and the scene image. A pretrained vision-language encoder extracts high-level semantic features from a representative frame, capturing salient visual context. These features are then integrated with structured prompts to guide a large language model in synthesizing natural dialogue. To ensure contextual and emotional consistency across scenes, we introduce a \textit{Recursive Narrative Bank}—a speaker-aware, temporally structured memory that recursively accumulates each character’s dialogue history. Inspired by Script Theory in cognitive psychology, this design enables characters to speak in ways that reflect their evolving goals, social context, and narrative roles throughout the story. Finally, we render each utterance as expressive, character-conditioned speech, resulting in fully-voiced, multimodal video narratives. Our training-free framework generalizes across diverse story settings—from fantasy adventures to slice-of-life episodes—offering a scalable solution for coherent, character-grounded audiovisual storytelling.

---

## 论文详细总结（自动生成）

## 详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）
- 当前基于场景的视频生成技术已能从结构化提示（prompts）合成连贯的视觉叙事，例如使用故事生成模型（如 Text2Story）生成对应视觉场景。
- 然而，叙事中一个关键维度——**角色驱动的对白与语音**——仍未被充分探索。缺少角色表达、对话和语音，使得生成视频的视觉叙事不够生动，角色魅力不足。
- 该论文旨在填补这一空白，将动作级提示（action-level prompts）转化为**视觉和听觉上落地**的叙事对话，让角色在视频中用自然、连贯、具有个性特征的语言“说话”，从而提升整体视频叙事的吸引力和表现力。
- 从产业角度看，这一研究直接支持**自动化漫剧、微短剧等场景视频创作**中对白生成需求，具有应用潜力。

### 2. 方法论：核心思想、关键技术细节与流程
- **整体框架**：提出一个**模块化、无需训练（training-free）**的流水线，可灵活搭配现有故事生成模型（如 Text2Story）使用。
- **输入格式**：每个场景接受两个提示——第一个定义场景设置（setting），第二个指定角色行为（behavior）。
- **视觉上下文提取**：利用预训练的视觉-语言编码器（vision-language encoder）从代表性视频帧中提取高层语义特征，捕获关键视觉上下文。
- **对话生成**：将视觉特征与结构化提示融合，输入大语言模型（LLM），引导其生成自然、符合场景的对白。
- **跨场景一致性机制**：提出 **递归叙事库（Recursive Narrative Bank）**，这是一个**说话者感知、时间结构化**的记忆模块，递归累积每个角色的对话历史。其设计灵感来自认知心理学中的**脚本理论（Script Theory）**，使角色的说话方式反映其不断演进的目标、社会背景和叙事角色。
- **语音合成**：将生成的每句对白渲染为**具有角色条件（character-conditioned）的语音**，最终输出完整带声的多模态视频叙事。
- **关键特点**：无需训练、泛化性强、可即插即用。

### 3. 实验设计
- **数据集 / 场景**：论文摘要中提到方法可适用于“从奇幻冒险到日常生活片段”等多种故事类型，但**未提供具体数据集名称、规模或基准（benchmark）**。
- **对比方法**：未在摘要中说明与哪些基线方法进行了比较，也未说明评测指标（如自然度、一致性、角色相似度等的量化方式）。
- **整体评价**：由于原始提供内容仅是摘要加元数据，无法获知完整的实验设置、消融实验设计及用户研究等细节。

### 4. 资源与算力
- 论文摘要中**未提及任何关于 GPU 型号、数量、训练时长或推理资源**的信息。
- 由于该方法声称是“training-free”（无需训练），可能仅需推理阶段的算力，但具体规模并未说明。
- 如果读者需要了解算力需求，必须查阅论文全文的实验章节；当前文本无法提供更多信息。

### 5. 实验数量与充分性
- 从摘要来看，论文展示了一定程度的泛化能力（多种故事类型），但**缺乏明确的实验数量、消融组数、定量指标及对比实验结果**。
- 摘要中未提及用户调研、人类评估或与现有对话生成/视频叙事方法进行对比的细节。
- 因此，基于现有信息无法判断实验是否充分、客观、公平。需要结合全文审阅才能评估。

### 6. 主要结论与发现
- 生成的对话**自然且角色一致**，能有效增强叙事视频中的角色表现力与内容吸引力。
- 所提出的框架**无需训练**，可推广至不同故事设定，提供一种可扩展的、连贯的、角色本位的视听故事生成方案。
- 该方法可作为**关键模块**集成到现有视频合成系统中，为自动化短剧、漫剧制作提供角色驱动对白生成能力。

### 7. 优点
- **模块化设计**：可灵活搭配不同故事生成模型，即插即用。
- **无需训练**：降低使用门槛，便于快速部署和迁移。
- **多模态一致性**：同时考虑视觉语义、对话内容与语音表达，使叙事更丰富立体。
- **角色记忆机制**：通过递归叙事库实现跨场景的对话历史和情感一致性，避免了情节脱节。
- **理论支撑**：借鉴认知心理学脚本理论，具有一定理论深度。
- **应用前景明确**：直指自动化短剧、漫剧等实际场景，实用价值高。

### 8. 不足与局限
- **实验细节缺失**：摘要中未给出具体评测数据、基准、对比方法或用户研究，难以全面评估方法的有效性和相对优势。
- **依赖上游模型**：需要先由故事生成模型生成视觉场景，且依赖预训练视觉-语言编码器和 LLM 的能力，如果上游模型有偏差或错误，会对最终对话质量产生连锁影响。
- **视觉信息利用有限**：仅从代表帧提取高层语义特征，可能忽略时间动态、镜头变化和复杂动作细节，导致对话与视频细微内容不够贴合。
- **多角色与长序列支持**：虽然提及递归叙事库，但未详细说明其对极长叙事、大规模角色交互时的记忆容量和效率问题。
- **应用限制**：对需要精确事实、文化语境或细腻情感演绎的复杂剧本，可能仍存在自动化生成的固有局限，仍需人工审校。

（完）
