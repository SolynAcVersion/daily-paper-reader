---
title: "Captain Cinema: Towards Short Movie Generation"
title_zh: Captain Cinema：面向短片生成
authors: "Junfei Xiao, Ceyuan Yang, Lvmin Zhang, Shengqu Cai, Yang Zhao, Yuwei Guo, Gordon Wetzstein, Maneesh Agrawala, Alan Yuille, Lu Jiang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=zlNZBxQZIC"
tags: ["query:manga-drama"]
score: 9.0
evidence: 直接从文本剧情生成关键帧序列并进行视频合成，实现短电影生成。
tldr: 该文提出Captain Cinema短片生成框架，先在细粒度文本剧情描述上生成关键帧序列以规划完整叙事，确保场景与角色等视觉元素的长程一致性，再以关键帧为条件用支持长上下文的视频合成模型生成中间时空动态。通过多模态扩散Transformer的交错训练策略，框架能稳定高效地生成多场景长叙事电影短片，为短剧的自动化视觉化提供了直接路径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频生成缺乏从剧情到多场景短片的长程一致性与规划机制。
method: 采用自顶向下关键帧规划与自底向上视频合成，结合交错训练的多模态扩散Transformer。
result: 在短片生成上实现了叙事与外观的长程一致性，并提高多场景生成的稳定性与效率。
conclusion: 证明了关键帧规划对短片生成的有效性，为短剧自动化制作提供端到端方案。
---

## Abstract
We present **Captain Cinema**, a generation framework for short movie generation.
Given a detailed textual description of a movie storyline, our approach firstly generates a sequence of keyframes that outline the entire narrative, which ensures long-range coherence in both the storyline and visual appearance (e.g., scenes and characters). We refer to this step as top-down keyframe planning. These keyframes then serve as conditioning signals for a video synthesis model, which supports long context learning, to produce the spatio-temporal dynamics between them. This step is referred to as bottom-up video synthesis. To support stable and efficient generation of multi-scene long narrative cinematic works, we introduce an interleaved training strategy for Multimodal Diffusion Transformers (MM-DiT), specifically adapted for long-context video data. Our model is trained on a curated cinematic dataset consisting of interleaved samples for video generation. Our experiments demonstrate that Captain Cinema performs favorably in the automated creation of visually coherent and narratively consistent short films.

---

## 论文详细总结（自动生成）

# Captain Cinema：面向短片生成——论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：现有视频生成模型虽然能生成高质量短视频片段，但面对**多场景、长叙事**的短片（short movie）时，普遍缺乏**长程一致性**——包括剧情逻辑的统一性，以及角色外貌、场景风格等视觉元素在时间上的连贯性。
- **研究动机**：长篇影视作品通常涉及多个场景的切换和复杂叙事的推进，直接让生成模型从头到尾生成完整视频不仅在计算上不可行，也无法保证画面中人物、环境等要素在异地多场景间保持一致。因此，需要一种**规划与生成分离**的策略，先“想清楚再画出来”。
- **整体含义**：该论文提出一个名为 **Captain Cinema** 的端到端短片生成框架，尝试将“叙事规划”与“视频合成”解耦，为短剧、短电影的自动化制作提供一条全新路径。

## 2. 方法论：核心思想、关键技术细节与流程

- **总体架构**：自顶向下的关键帧规划（Top-down Keyframe Planning）+ 自底向上的视频合成（Bottom-up Video Synthesis）。
- **第一步：关键帧规划**：给定完整的文本剧情描述，模型首先生成一串**关键帧（keyframes）**，这些关键帧勾勒出整个叙事的骨架，从而在故事线和视觉外观（场景、角色）两个层面上确保长程一致性。
- **第二步：视频合成**：将关键帧作为条件信号，输入到支持**长上下文学习**的视频合成模型中，生成关键帧之间的时空动态，最终形成完整的短片。
- **模型基础**：采用**多模态扩散 Transformer（Multimodal Diffusion Transformers, MM-DiT）**，并专门设计了一种**交错训练策略（interleaved training strategy）**，以适应长上下文视频数据的稳定、高效训练。
- **训练数据**：模型在一个精心策划的电影数据集上训练，该数据集包含用于视频生成的交错样本（interleaved samples）。
- **流程要点**：通过“关键帧规划→视频填充”的两阶段流水线，将长视频生成任务分解为“全局叙事设计”和“局部动态生成”两个可控子问题，提高生成的可控性和一致性。

## 3. 实验设计

- **数据集**：论文提到使用了**自建的精选电影数据集（curated cinematic dataset）**，包含交错样本用于视频生成训练。数据集的具体规模、来源、标注方式等在摘要中未展开说明。
- **Benchmark**：文中未明确列出具体的基准测试名称（如 VBench、EvalCrafter 等），仅表示实验证明了框架“在自动创建视觉连贯、叙事一致的短片方面表现良好”。
- **对比方法**：摘要中未提及具体对比了哪些基线方法（如其他视频生成模型或关键帧引导方法），需要查阅全文才能获知详细对比设置。

## 4. 资源与算力

- 摘要和元数据中**未提及**使用的 GPU 型号、数量、训练时长、参数量等具体算力信息。
- 由于长上下文视频数据训练的复杂度较高，推测需要大规模并行 GPU 集群，但缺乏实际数据佐证，需查阅论文全文的实验设置部分。

## 5. 实验数量与充分性

- 从摘要层面来看，实验描述**较为概括**：仅提到在精选电影数据集上训练并验证了整体效果，未列出具体的消融实验数量、指标对比表或用户研究。
- 实验的**充分性和客观性**在当前信息下难以全面评估。关键问题包括：
  - 是否对不同数量的关键帧、不同视频长度进行了消融？
  - 长程一致性如何量化评估（如角色身份保持指标）？
  - 是否有与逐帧生成或无规划生成方法的直接对比？
- 这些细节需要通过完整论文来确认。就摘要而言，实验证据的数量和维度较为有限。

## 6. 主要结论与发现

- **关键帧规划行之有效**：先规划关键帧再合成视频的两阶段方法，能有效保证短片在叙事和视觉外观上的**长程一致性**。
- **交错训练策略可行**：针对 MM-DiT 设计的交错训练策略，能够支持**多场景长叙事**视频的稳定、高效生成。
- **端到端自动化**：从纯文本剧情直接生成短片成为可能，为短剧、电影预告片等内容的自动化制作提供了实用方案。

## 7. 优点

- **问题定位准确**：直击长视频生成中“多场景一致性”这一关键痛点，而非只关注单镜头视频质量。
- **方法设计优雅**：采用“先规划、后合成”的层次化分解，将难题拆解为可控子任务，符合影视制作的实际流程（分镜→拍摄）。
- **模型创新性**：针对长上下文视频交错训练 MM-DiT，是扩散 Transformer 在长视频领域的有效延伸。
- **应用价值高**：为短剧自动生成提供了一条直接、端到端的落地路径，具有明确的产业价值。

## 8. 不足与局限

- **实验细节不透明**：数据集规模、评价指标、基线对比等关键信息未在摘要中体现，难以判断方法在量化指标上的实际优势。
- **算力开销未披露**：长上下文视频训练的计算资源需求未知，可能影响方法的可复现性和推广性。
- **潜在偏差风险**：精选电影数据集可能存在题材、风格偏差，生成结果是否具有通用性尚需验证。
- **用户评估缺失**：叙事质量最终需人工评判，摘要中未提及用户研究或主观评估结果。
- **需要全文验证**：关键帧数量的选择、规划与合成的衔接方式、失败案例分析等，均需通过完整论文来进一步考察。

（完）
