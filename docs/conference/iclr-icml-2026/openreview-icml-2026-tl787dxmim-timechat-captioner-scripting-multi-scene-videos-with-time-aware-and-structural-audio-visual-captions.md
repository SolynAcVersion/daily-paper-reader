---
title: "TimeChat-Captioner: Scripting Multi-Scene Videos with Time-Aware and Structural Audio-Visual Captions"
title_zh: 时间聊天字幕器：基于时间感知与结构化视听字幕的多场景视频脚本编写
authors: "Linli Yao, Yuancheng Wei, Yaojie Zhang, Lei Li, Xinlong Chen, Feifan Song, Ziyue Wang, Kun Ouyang, Yuanxin Liu, Lingpeng Kong, Qi Liu, Pengfei Wan, Kun Gai, Yuanxing Zhang, Xu Sun"
date: 2026-04-30
pdf: "https://openreview.net/pdf/163efa63e293136bf17fe821ace93b8a8261298e.pdf"
tags: ["query:manga-drama"]
score: 4.0
evidence: 为多场景视频生成类脚本的密集字幕，可能辅助短剧剧本制作。
tldr: 该文提出全模态密集字幕任务，通过六维结构模式生成带时间戳的音频-视觉连续叙述，实现类似电影剧本的场景化视频描述。作者构建了OmniDCBench基准、SodaM评估指标以及TimeChatCap-42K训练集，并训练了TimeChat-Captioner-7B基线模型。该工作可用于多场景视频的脚本化理解与制作辅助，对短剧自动化生产中的内容策划有潜在价值。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频描述缺乏时间感知与结构化的连续叙述，难以支撑场景级脚本化理解。
method: 提出六维结构模式生成带时间戳的视听字幕，构建基准与训练集并训练基线模型。
result: 构建了OmniDCBench基准和TimeChatCap-42K数据集，SodaM指标验证了时间感知详细描述的有效性。
conclusion: 该工作为多场景视频的脚本化描述提供了数据、指标和基线，可辅助短剧内容制作。
---

## Abstract
This paper proposes Omni Dense Captioning, a novel task designed to generate continuous, fine-grained, and structured audio-visual narratives with explicit timestamps. To ensure dense semantic coverage, we introduce a six-dimensional structural schema to create "script-like" captions, enabling readers to vividly imagine the video content scene by scene, akin to a cinematographic screenplay. To facilitate research, we construct OmniDCBench, a high-quality, human-annotated benchmark, and propose SodaM, a unified metric that evaluates time-aware detailed descriptions while mitigating scene boundary ambiguity. Furthermore, we construct a training dataset, TimeChatCap-42K, and present TimeChat-Captioner-7B, a strong baseline trained via SFT and GRPO with task-specific rewards. Extensive experiments demonstrate that TimeChat-Captioner achieves state-of-the-art performance, surpassing Gemini-2.5-Pro, while its generated dense descriptions significantly boost downstream capabilities in audio-visual reasoning (DailyOmni and WorldSense) and temporal grounding (Charades-STA). All datasets, models, and code are publicly available at https://github.com/yaolinli/TimeChat-Captioner.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

> 说明：以下总结基于论文标题、摘要及提供的元数据信息，论文正文未完整提供，因此部分细节（如六维结构具体定义、训练超参数等）无法展开，已在相应部分明确指出。

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现有视频描述任务（video captioning / dense captioning）通常只生成概括性描述或局部片段字幕，缺乏**时间感知**和**结构化连续叙述**，难以支撑“逐场景脚本化理解”需求。
- **核心问题**：如何为多场景视频生成**细粒度、连续、带时间戳的音频-视觉字幕**，使得读者仅凭文字即可像阅读电影剧本一样在脑海中重现视频内容。
- **整体含义**：论文提出 **Omni Dense Captioning（全模态密集字幕）** 这一新任务，将视频理解从“描述内容”推进到“生成可拍摄/可编排的脚本级叙述”，对多场景视频的内容策划、短剧自动化制作、视频检索与推理等下游应用具有潜在价值。

## 2. 方法论

- **核心思想**：利用**结构化模式（structural schema）** 生成“脚本式”连续叙述，并嵌入**显式时间戳**，使描述既覆盖密集语义又具备场景边界可区分性。
- **六维结构模式**：摘要提到“six-dimensional structural schema”，但未具体展开六个维度。其设计目标是为保证密集语义覆盖，使字幕呈现类似电影剧本的分场效果（如场景、动作、对话、音频事件等维度的组合）。
- **训练数据构建**：构建了 **TimeChatCap-42K** 训练集，用于训练基线模型。
- **模型训练**：提出 **TimeChat-Captioner-7B**，采用两阶段训练：
  - **SFT（监督微调）**：让模型学习生成结构化、时间感知的字幕。
  - **GRPO（带群体相对策略优化的强化学习）**：使用任务特定奖励（task-specific rewards）进一步优化，提升时间戳准确性和语义密度。
- **评估指标**：提出 **SodaM** 统一指标，用于评价“时间感知的详细描述”，并缓解**场景边界模糊（scene boundary ambiguity）** 问题。
- **备注**：摘要中未提供具体的公式、网络架构细节或算法伪代码。

## 3. 实验设计

- **基准（Benchmark）**：构建了 **OmniDCBench**，这是一个人工标注的高质量基准，用于评测全模态密集字幕任务。
- **训练集**：**TimeChatCap-42K**（42K规模的时间感知结构化视听字幕数据）。
- **对比方法**：摘要明确提到的对比模型是 **Gemini-2.5-Pro**，并宣称达到超越效果；但未列出其他对比方法（如开源视频字幕模型的横向比较）。
- **下游任务验证**：
  - **音频-视觉推理**：使用 DailyOmni 和 WorldSense 两个数据集。
  - **时间定位**：使用 Charades-STA。
  - 结果表明生成的密集描述能显著提升上述下游任务性能。
- **实验充分性**：从摘要来看，实验覆盖了主基准、强基线对比和三个下游任务，规模不小；但缺少消融实验、各组件贡献分析、人工评测细节等，因此无法完全判断实验的全面性与公平性。

## 4. 资源与算力

- **未明确说明**：摘要和元数据中均未提及使用的 GPU 型号、数量、训练时长、显存占用等具体算力信息。
- **可推断信息**：模型参数量为 7B（TimeChat-Captioner-7B），通常需要多卡 GPU 训练；且使用了 SFT + GRPO 两阶段，算力开销较大，但具体数值未知。

## 5. 实验数量与充分性

- **实验数量**：至少包含：
  - OmniDCBench 上的主结果；
  - 与 Gemini-2.5-Pro 的对比；
  - 3 个下游数据集（DailyOmni、WorldSense、Charades-STA）的迁移评测。
- **充分性分析**：
  - **优点**：构建了专有基准、训练集、统一指标，并在多个下游任务上验证，结构较完整。
  - **不足**：摘要未展示消融实验（如去掉 GRPO、去掉时间戳、去掉六维结构等的影响）；对比方法仅明确 Gemini-2.5-Pro，缺乏对更多开源/闭源模型的系统性比较；SodaM 指标本身也需要更多消融验证才能判断其鲁棒性。因此，从公开信息看，实验设计有一定说服力，但严格意义上的“充分、客观、公平”尚需阅读正文确认。

## 6. 主要结论与发现

- **主结论**：TimeChat-Captioner 在 OmniDCBench 上达到 **state-of-the-art**，超越 Gemini-2.5-Pro。
- **多模态密集字幕的有效性**：生成的带时间戳、结构化视听字幕能够显著增强下游的音频-视觉推理（DailyOmni、WorldSense）和时间定位（Charades-STA）能力。
- **资源开源**：数据、代码、模型全部公开，有助于后续研究者复现和扩展。
- **应用含义**：该工作提供了一套“数据 + 指标 + 基线”的完整方案，可用于多场景视频的脚本化描述，对短剧脚本生成与内容策划等应用具有辅助价值。

## 7. 优点

- **任务新颖**：首次明确提出“全模态密集字幕”任务，将视频描述提升到“剧本级”结构化叙述层次。
- **数据结构化设计**：六维结构模式 + 时间戳的设计很有创意，使描述具有可读性、可定位性和场景可区分性。
- **指标针对性**：提出 SodaM 专门处理时间感知细节和场景边界模糊问题，弥补了传统字幕指标（如 CIDEr、SPICE）无法评估时间维度的不足。
- **训练策略完整**：SFT + GRPO 的强基线与任务特定奖励机制结合，展现了利用强化学习优化结构化生成的潜力。
- **开源贡献**：公开基准、数据集、模型和代码，科研透明度和复用性强。
- **应用价值**：对短剧/视频脚本自动化生产、内容策划等领域有明显落地潜力。

## 8. 不足与局限

- **信息完整性受限**：现有材料未展开六维结构的具体定义和标注规范，外部研究者难以精确复现。
- **算力成本未报告**：未提供训练时长、GPU 数量等关键资源信息，不利于评估方法的工程可用性。
- **对比不够广泛**：仅明确提到 Gemini-2.5-Pro，缺少与多个主流视频理解模型的平行对比，说服力打折扣。
- **实验细节缺失**：没有消融实验分析（如各维度贡献、时间戳预测的误差分析、SodaM 与人工评价的一致性验证）。
- **模型规模局限**：7B 参数模型虽具代表性，但可能无法充分验证扩展性；更大规模模型下的表现未知。
- **应用偏差风险**：若目标是辅助“短剧”等特定场景，训练数据和评测基准可能偏向该领域，对通用视频描述任务的泛化性有待考察。
- **潜在主观性**：脚本式字幕的“可读性”和“场景想象力”本质上带有主观性，SodaM 是否完全客观仍需进一步验证。

（完）
