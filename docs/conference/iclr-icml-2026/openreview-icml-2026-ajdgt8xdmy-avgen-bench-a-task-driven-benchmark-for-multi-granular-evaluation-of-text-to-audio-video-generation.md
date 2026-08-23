---
title: "AVGen-Bench: A Task-Driven Benchmark for Multi-Granular Evaluation of Text-to-Audio-Video Generation"
title_zh: AVGen-Bench：文本到音视频生成的多粒度任务驱动评测基准
authors: "Ziwei Zhou, Zeyuan Lai, Rui Wang, Yifan Yang, Yuqing Yang, Qi Dai, Lili Qiu, Chong Luo"
date: 2026-04-30
pdf: "https://openreview.net/pdf/57c4c9711ec3d7151dcc7e519fcaea8a003cf366.pdf"
tags: ["query:manga-drama"]
score: 5.0
evidence: 文本到音视频生成的任务驱动基准，细粒度评估联合正确性，适用于短视频平台内容。
tldr: 本文指出现有文本到音视频生成评测各自为政，无法反映真实场景中的联合正确性。为此提出AVGen-Bench，覆盖11类真实世界提示，并设计多粒度评估框架，结合轻量专家模型与多模态大模型，从感知质量到细粒度语义可控性全面评测。该基准为短剧等音视频内容的生成质量评估提供了更完备的参照体系。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 文本到音视频生成的评测碎片化，音频和视频孤立评估，无法捕捉真实提示下的联合正确性。
method: 构建AVGen-Bench基准，覆盖11类真实世界提示，提出多粒度评估框架，结合轻量专家模型和多模态大模型。
result: 提供从感知质量到细粒度语义可控性的全面评估能力。
conclusion: 为音视频生成提供统一评测基准，有助于短剧等多媒体内容生成质量评估。
---

## Abstract
Text-to-Audio-Video (T2AV) generation is rapidly becoming a core interface for media creation, yet its evaluation remains fragmented.
Existing benchmarks largely assess audio and video in isolation or rely on coarse embedding similarity, failing to capture fine-grained joint correctness required by realistic prompts.
We introduce AVGen-Bench, a task-driven benchmark for T2AV generation, featuring high-quality prompts across 11 real-world categories.
To support comprehensive assessment, we propose a multi-granular evaluation framework that combines lightweight specialist models with Multimodal Large Language Models (MLLMs), enabling evaluation from perceptual quality to fine-grained semantic controllability.
Our evaluation reveals a pronounced gap between strong audio-visual aesthetics and weak semantic reliability, including persistent failures in text rendering, speech coherence, physical reasoning, and universal breakdown in musical pitch control.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **背景**：文本到音视频生成（T2AV）正快速成为媒体创作的核心接口，但现有评测体系高度碎片化。
- **核心问题**：已有基准大多将音频和视频分开评测，或仅依赖粗糙的嵌入相似度，无法捕捉真实提示词所要求的“音视频联合正确性”（fine-grained joint correctness）。
- **整体含义**：缺乏统一、细粒度的评测标准，严重制约了 T2AV 生成模型的可靠性和落地能力，需要一个新的任务驱动的基准来系统衡量模型在真实场景下的生成质量。

## 2. 方法论

- **核心思想**：提出任务驱动的评测基准 AVGen-Bench，从真实世界需求出发，设计高质量提示词，并构建“多粒度”评估框架。
- **技术细节**：
  - 覆盖 **11 类真实世界提示词类别**，确保评测内容的多样性和实际相关性。
  - 评估框架结合 **轻量专家模型**（如音频/视频专用小模型）与 **多模态大语言模型（MLLMs）**，实现从低层感知质量到高层语义可控性的分层评测。
  - 评估粒度包括：感知质量（画质、音质等）、音视频联合一致性、文本渲染、语音连贯性、物理合理性、音高控制等细粒度属性。
- **流程（文字说明）**：输入 T2AV 提示词 → 生成音视频样本 → 轻量专家模型提取感知级特征与音视频匹配信号 → MLLM 进行语义、逻辑与可控性判断 → 汇总多粒度评分，形成综合评测结果。

## 3. 实验设计

- **Benchmark 构成**：AVGen-Bench，包含 11 类真实世界提示词，覆盖常见内容创作需求（如短剧、自然场景、人物说话等）。
- **评测对象**：当前常见的 T2AV 生成模型（原文未列出具体模型名称）。
- **对比方法**：现有碎片化评测方法，即“仅评测音频”“仅评测视频”“使用粗糙嵌入相似度”的方法作为参照或基线。
- **评测维度**：音视频美学质量、语义可靠性、文本渲染、语音连贯性、物理推理、音高控制等。

## 4. 资源与算力

- 论文原文**未明确说明**使用的 GPU 型号、数量、训练时长或推理算力等资源信息。
- 由于该工作主要聚焦于构建评测基准和评估框架，可能不涉及大规模模型训练，但原文未提供任何算力细节，需查阅论文全文或附录确认。

## 5. 实验数量与充分性

- 实验数量方面：论文摘要是概述，未给出具体实验组数（如多少模型、多少提示词、多少人工评估等）。
- 充分性判断：
  - **覆盖范围**：11 类真实世界提示词覆盖面较广，能反映多种内容生成场景，这是其充分性优势。
  - **对比公平性**：未列出详细基线和方法实现细节，难以判断是否所有模型在同一环境下公平评估。
  - **客观性**：结合专家模型与 MLLM 可减少纯主观误差，但 MLLM 自身的偏差仍需验证。
  - 总体来说，基准设计思路合理，但若缺少消融实验（如不同评估粒度对结果的影响、轻量模型与 MLLM 的权重分配等），其稳健性有待补充。

## 6. 主要结论与发现

- 现有 T2AV 模型在“音视频美学质量”与“语义可靠性”之间**存在显著鸿沟**：视觉/听觉观感较好，但语义层面常出错。
- 主要失败模式包括：
  - **文本渲染不可靠**（生成画面中的文字内容错误或模糊）
  - **语音连贯性差**（语音与上下文不连贯或语义不匹配）
  - **物理推理失败**（违背物理规律的生成结果）
  - **音高控制普遍崩溃**（音乐/声调生成无法准确控制音高）
- 这些发现表明，当前模型对细粒度语义指令的服从能力严重不足，需要新的评测基准来引导优化。

## 7. 优点

- **任务驱动**：从真实世界创作需求出发设计提示词，评测结果更具实际参考价值。
- **多粒度框架**：同时考虑感知质量与语义可控性，避免单一指标缺陷。
- **联合正确性**：强调音视频的联合一致性，弥补了以往音频/视频分离评估的不足。
- **轻量模型 + MLLM 结合**：在成本与能力之间取得平衡，既保证可扩展性又具备高层语义理解力。
- **明确问题导向**：清晰揭示了当前模型的系统性失败模式，为后续研究提供了改进方向。

## 8. 不足与局限

- **细节缺失**：论文摘要未提供基准的完整构建过程、提示词示例、标注协议、评估协议等关键技术细节。
- **模型覆盖不明确**：未列出评测了哪些具体生成模型，难以评估结论的普适性。
- **实验充分性不足**：未见消融研究、人工评测一致性分析、不同 MLLM 对结果的影响等，客观性和稳定性证据较弱。
- **潜在偏差**：MLLM 作为评测器可能存在固有的语义偏好；轻量专家模型对某些音频/视频特征的灵敏度也可能影响结果。
- **应用限制**：基准主要面向短视频平台内容（如短剧），对长视频、高动态交互或专业级音视频制作场景的覆盖可能不足。

（完）
