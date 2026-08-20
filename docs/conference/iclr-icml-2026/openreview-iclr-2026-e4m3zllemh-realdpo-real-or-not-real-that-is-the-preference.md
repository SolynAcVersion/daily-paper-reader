---
title: "RealDPO: Real or Not Real, that is the Preference"
title_zh: RealDPO：真实与否，在于偏好
authors: "Guo Cheng, Danni Yang, Ziqi Huang, Jianlou Si, Chenyang Si, Ziwei Liu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=E4m3ZLleMH"
tags: ["query:phys-video"]
score: 8.0
evidence: 利用真实视频作为正样本进行DPO偏好学习，提升视频运动自然度与物理合理性
tldr: 该论文发现传统监督微调（SFT）无法提供充足的纠正反馈，导致视频生成中的复杂运动不自然。为此提出RealDPO，基于真实世界视频作为正样本进行直接偏好优化（DPO），并设计定制损失函数增强运动真实性。实验表明该方法比SFT更能生成自然、流畅且上下文一致的运动，为提升物理合理的视频生成提供了新的对齐思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频生成模型难以生成自然、流畅且上下文一致的运动，SFT纠正反馈有限。
method: 提出RealDPO，用真实视频作为正样本进行DPO偏好学习，定制损失函数优化运动真实性。
result: 实验证明RealDPO相比SFT能显著提升视频运动生成的自然度和真实性。
conclusion: 偏好对齐（DPO）利用真实数据可有效提升视频运动的物理合理性，是SFT的有力补充。
---

## Abstract
Video generative models have recently achieved notable advancements in synthesis quality. However, generating complex motions remains a critical challenge, as existing models often struggle to produce natural, smooth, and contextually consistent movements. This gap between generated and real-world motions limits their practical applicability. To address this issue, we introduce RealDPO, a novel alignment paradigm that leverages real-world data as positive samples for preference learning, enabling more accurate motion synthesis. Unlike traditional supervised fine-tuning (SFT), which offers limited corrective feedback, RealDPO employs Direct Preference Optimization (DPO) with a tailored loss function to enhance motion realism. By contrasting real-world videos with erroneous model outputs, RealDPO enables iterative self-correction, progressively refining motion quality. To support post-training in complex motion synthesis, we propose RealAction-5K, a curated dataset of high-quality videos capturing human daily activities with rich and precise motion details. Extensive experiments demonstrate that RealDPO significantly improves video quality, text alignment, and motion realism compared to state-of-the-art models and existing preference optimization techniques.

---

## 论文详细总结（自动生成）

# 论文总结：RealDPO: Real or Not Real, that is the Preference

## 1. 核心问题与整体含义

- **研究背景**：视频生成模型在合成质量上取得了显著进步，但生成复杂运动仍然充满挑战。现有模型难以生成自然、流畅且上下文一致的运动，生成运动与真实世界运动之间存在明显差距，限制了实际应用。
- **核心问题**：如何让视频生成模型生成更加物理合理、真实自然的运动？传统监督微调（SFT）无法提供充足的纠正反馈，导致模型在复杂运动场景下仍然存在问题。
- **整体含义**：本文提出一种新的对齐范式 RealDPO，将真实世界视频作为正样本用于偏好学习，以更准确地合成运动。这为提升视频生成的物理合理性和运动真实度提供了新思路。

## 2. 方法论

- **核心思想**：利用真实世界视频作为正样本，与模型生成的错误输出进行对比，通过直接偏好优化（DPO）实现迭代式自我纠正，逐步细化运动质量。
- **关键要点**：
  - 不同于传统 SFT 的有限纠正反馈，RealDPO 采用 Direct Preference Optimization（直接偏好优化）。
  - 设计了定制化的损失函数，专门用于增强运动的真实性。
  - 通过“真实 vs 虚假”的对比，让模型学会区分自然运动与不自然运动，从而优化生成结果。
- **支持资源**：提出了 RealAction-5K 数据集，包含高质量的人类日常活动视频，具有丰富且精确的运动细节，用于支撑复杂运动合成的后训练。
- **算法流程（文字描述）**：
  1. 收集高质量真实视频作为正样本（RealAction-5K）。
  2. 使用基线模型生成对应的负样本（不自然、有错误的运动输出）。
  3. 基于 DPO 框架，构造偏好对（真实视频为“被偏好”样本，生成视频为“不被偏好”样本）。
  4. 通过定制损失函数进行优化，鼓励模型生成更接近真实运动的输出。
  5. 迭代进行自我纠正，逐步提升运动质量。

## 3. 实验设计

- **数据集**：核心为自建数据集 RealAction-5K，聚焦人类日常活动，包含丰富运动细节。
- **Benchmark**：未明确提及具体基准测试集名称，但实验涵盖了视频质量、文本对齐、运动真实度等维度的评估。
- **对比方法**：与当前最先进的视频生成模型（state-of-the-art models）以及已有的偏好优化技术（existing preference optimization techniques）进行了对比。

## 4. 资源与算力

- 原文中**未说明**具体使用的 GPU 型号、数量或训练时长等算力信息。只能确定实验使用了 RealAction-5K 数据集进行后训练，但硬件资源细节缺失。

## 5. 实验数量与充分性

- **实验数量**：原文仅提到“大量实验”（Extensive experiments），未给出具体实验组数、消融实验细节或不同设置的对比表。
- **充分性评估**：从摘要看，实验涵盖了与 SOTA 和现有偏好优化方法的对比，并验证了视频质量、文本对齐、运动真实度等方面的提升，结论较为积极。但由于缺乏详细的实验设置和消融数据，无法完全判断其客观性和公平性。尤其缺少对不同数据集、不同基座模型、不同损失函数组件的消融分析，因此充分性有限。

## 6. 主要结论与发现

- RealDPO 相比 SFT 能显著提升视频生成的运动真实度、自然性和上下文一致性。
- 通过利用真实数据作为正样本的偏好优化，能有效改善复杂运动的生成质量。
- 实验证明 RealDPO 在视频质量、文本对齐和运动真实度上优于当前 SOTA 模型和已有偏好优化技术。

## 7. 优点

- **创新的对齐范式**：将真实世界视频引入 DPO 偏好学习，突破了 SFT 反馈有限的瓶颈。
- **定制损失函数**：针对运动真实性设计专门的目标，更贴合视频生成任务。
- **高质量数据集**：构建 RealAction-5K，为复杂运动的后训练提供有力支撑。
- **迭代式自我纠正**：通过对比真实与生成结果，模型能逐步细化运动质量，具有清晰的优化路径。

## 8. 不足与局限

- **算力信息缺失**：未披露训练成本，难以评估方法的可复现性和资源门槛。
- **实验细节不透明**：未列出具体实验数量、消融研究和统计显著性检验，结论的稳健性需进一步验证。
- **数据域局限**：数据集主要聚焦人类日常活动，对大规模场景、物体运动、物理交互等复杂运动的泛化能力未知。
- **偏好定义风险**：使用真实视频作为“正样本”可能隐含假设真实视频都是理想输出，但真实视频也存在模糊、遮挡或低质量情况，可能引入偏差。
- **应用限制**：偏好优化可能过度拟合真实数据分布，导致生成结果缺乏多样性或创造性。

（完）
