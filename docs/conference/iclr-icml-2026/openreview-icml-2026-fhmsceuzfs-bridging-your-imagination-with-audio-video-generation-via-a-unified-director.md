---
title: Bridging Your Imagination with Audio-Video Generation via a Unified Director
title_zh: 通过统一导演模型连接想象与音视频生成
authors: "Jiaxu Zhang, Tianshu Hu, Yuan Zhang, Zenan Li, Linjie Luo, Mingyuan Gao, Guosheng Lin, Xin Chen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f9d8b0b486c87eaf70c11c7b44c4c40f10295db7.pdf"
tags: ["query:manga-drama"]
score: 9.0
evidence: 统一导演模型将用户提示与结构化剧本连接，生成多镜头长影片，直接支持自动化短剧创作。
tldr: 本文指出现有AI视频创作将剧本和关键镜头设计分离，导致流程割裂。提出UniMAGE统一导演模型，基于混合Transformer架构统一文本和图像生成，将用户提示转换为结构化脚本与镜头设计，并驱动现成的音视频生成模型。实验表明，非专业用户能够借助UniMAGE生成连贯的多镜头长影片，为自动化的短剧/微剧创作提供了统一的提示到成片的实现路径。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有AI视频创作把剧本起草和关键镜头设计分开处理，缺乏整体性，非专业用户难以制作多镜头长视频。
method: 提出UniMAGE统一导演模型，使用混合Transformer架构统一文本与图像生成，从而将用户提示转化为结构化的脚本和关键镜头，供音视频生成模型使用。
result: 实验表明UniMAGE能有效帮助非专业用户生成连贯的长镜头多镜头影片，桥接脚本与视频生成。
conclusion: 为自动化短片/短剧创作提供了一个从提示到多镜头成片的统一解决方案。
---

## Abstract
Existing AI-driven video creation systems typically treat script drafting and key-shot design as two disjoint tasks: the former relies on large language models, while the latter depends on image generation models. We argue that these two tasks should be unified within a single framework, as logical reasoning and imaginative thinking are both fundamental qualities of a film director. In this work, we propose **UniMAGE**, a unified director model that bridges user prompts with well-structured scripts, thereby empowering non-experts to produce long-context, multi-shot films by leveraging existing audio–video generation models. To achieve this, we employ the Mixture-of-Transformers architecture that unifies text and image generation. To further enhance narrative logic and keyframe consistency, we introduce a ``first interleaving, then disentangling" training paradigm. Specifically, we first perform **Interleaved Concept Learning**, which utilizes interleaved text–image data to foster the model’s deeper understanding and imaginative interpretation of scripts. We then conduct **Disentangled Expert Learning**, which decouples script writing from keyframe generation, enabling greater flexibility and creativity in storytelling. Extensive experiments demonstrate that UniMAGE achieves state-of-the-art performance among open-source models, generating logically coherent scripts and visually consistent keyframe images.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- 现有 AI 驱动视频创作系统通常将**剧本起草**与**关键镜头设计**视为两个互不关联的独立任务：
  - 剧本起草依赖大语言模型（LLM）；
  - 关键镜头设计依赖图像生成模型。
- 作者认为，这种分离不符合电影导演的实际工作方式——导演同时需要**逻辑推理**（叙事逻辑）与**想象思维**（视觉构想），两者应统一在同一框架内。
- 现有流程割裂导致非专业用户难以制作结构连贯、多镜头、长上下文的视频内容，尤其限制了自动化短剧/微剧的创作效率。  
- 因此，本文旨在构建一个“统一导演模型”，将用户提示直接转化为结构化剧本和一致的关键帧，再借助现成的音视频生成模型生成完整影片。

### 2. 方法论：核心思想、关键技术细节与算法流程

- **模型名称**：UniMAGE（统一导演模型）。
- **核心思想**：在一个统一框架内同时完成剧本写作与关键帧生成，桥接用户提示与视频生成模型。
- **技术架构**：
  - 采用 **Mixture-of-Transformers（MoT）** 架构，统一文本生成与图像生成任务。
  - MoT 通过混合专家机制，在共享 Transformer 骨架下对不同模态（文本/图像）进行专业化处理，既保持跨模态知识共享，又允许模态特有能力。
- **训练范式**：提出“先交织、后解耦”的两阶段训练策略：
  1. **交织概念学习（Interleaved Concept Learning）**：
     - 使用文本–图像交错排列的数据进行训练；
     - 使模型学习剧本中的概念与视觉表现之间的深层对应关系，提升对剧本的想象性解读能力。
  2. **解耦专家学习（Disentangled Expert Learning）**：
     - 将剧本写作与关键帧生成解耦为相对独立的专家模块；
     - 允许两种能力分别优化，从而增强叙事灵活性和创造性。
- **算法流程（文字描述）**：
  1. 输入：用户自然语言提示（例如短剧剧情梗概）。
  2. UniMAGE 将提示解析为结构化的完整剧本（含分场景、分镜头、对白、动作描述等）。
  3. 同时生成与剧本逻辑一致的关键帧图像（keyframes）。
  4. 将生成的剧本与关键帧作为条件输入，驱动现成的音频–视频生成模型（audio-video generation models），最终输出多镜头长影片。

### 3. 实验设计：数据集 / 场景 / benchmark / 对比方法

- **提及的数据与基准**：摘要中未明确列出具体数据集名称、评价基准或对比基准的细节。
- **实验场景**：主要围绕“非专业用户使用 UniMAGE 从提示生成多镜头长影片”的整体能力进行评估，包括：
  - 剧本逻辑连贯性；
  - 关键帧图像视觉一致性；
  - 生成影片的整体可用性。
- **对比方法**：摘要仅说明“在开源模型中达到 state-of-the-art 性能”，但未列出具体的对比基线模型名称。
- **评估方式**：推测包含自动指标与用户研究（因强调“非专业用户”），但具体指标未在摘要中给出。

### 4. 资源与算力

- 论文摘要及提供的元数据中**未明确说明**使用的 GPU 型号、数量、训练时长或总计算量。
- 仅能推断训练规模较大（因涉及多模态、多阶段训练），但具体算力信息缺失。

### 5. 实验数量与充分性

- **实验组数量**：摘要中未给出具体实验数量（如不同数据集上的实验组数、消融实验数量等）。
- **提及的实验类型**：
  - 整体性能评估（剧本逻辑与关键帧一致性）；
  - 两阶段训练范式的效果（隐含对比，但未明确列出消融细节）；
  - “非专业用户”使用效果的实验（可能为用户研究）。
- **充分性与客观性评价**：
  - **不充分**：缺少公开数据集细节、具体对比方法、定量指标和完整消融实验描述，难以独立复现或严格验证。
  - **客观性存疑**：未展示失败案例、局限性分析或与商业模型（如闭源模型）的对比；仅称“开源模型中 SOTA”，范围有限。

### 6. 主要结论与发现

- UniMAGE 能够在一个统一框架内生成逻辑连贯的剧本和视觉一致的关键帧。
- 通过“交织概念学习 + 解耦专家学习”，模型同时具备了叙事逻辑与视觉想象力，优于现有的开源模型。
- 非专业用户能够借助 UniMAGE 直接生成连贯的多镜头长影片，验证了“提示到成片”的自动化路径的可行性。
- 该工作为自动化短剧/微剧创作提供了一种端到端的统一解决方案。

### 7. 优点

- **任务统一创新**：首次明确将剧本写作与关键帧设计合并在一个模型中，符合创作直觉，减少流程割裂。
- **架构设计合理**：Mixture-of-Transformers 能够兼顾模态共享与模态特有能力，适合多模态生成。
- **训练范式有启发性**：“先交织、后解耦”策略既鼓励跨模态深层理解，又保留各任务的灵活性，思路清晰。
- **应用价值明确**：直接服务于自动化短剧/微剧创作，对非专业用户友好，落地潜力大。

### 8. 不足与局限

- **实验细节缺失**：未提供数据集、基准、指标、对比方法等关键信息，证据强度不足。
- **算力资源未披露**：无法评估训练成本与可复现性。
- **评估范围有限**：
  - 仅声明“开源模型中 SOTA”，未与闭源商业系统或更强基线对比；
  - 未讨论生成视频的音频质量、运动自然度、长视频中的跨镜头一致性等更复杂的维度；
  - 未包含消融实验的量化结果和失败模式分析。
- **潜在偏差风险**：若评价主要依赖用户主观评分，可能存在引导性偏差；缺乏第三方盲评说明。
- **应用限制**：对于超长剧本、复杂叙事或专业级电影制作需求，仍可能存在逻辑漏洞和视觉不一致；模型生成的“关键帧”能否完全驱动高质量视频生成未被证明。

（完）
