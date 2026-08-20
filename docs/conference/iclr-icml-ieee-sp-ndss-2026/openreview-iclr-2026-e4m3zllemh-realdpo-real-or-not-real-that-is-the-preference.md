---
title: "RealDPO: Real or Not Real, that is the Preference"
title_zh: RealDPO：真实与否，即为偏好
authors: "Guo Cheng, Danni Yang, Ziqi Huang, Jianlou Si, Chenyang Si, Ziwei Liu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=E4m3ZLleMH"
tags: ["query:phys-video"]
score: 9.0
evidence: 基于真实视频的DPO偏好学习提升运动真实感
tldr: 视频生成模型在复杂运动合成上仍常产生不自然、不连贯的动作。RealDPO提出一种新的对齐范式，把真实视频作为偏好学习中的正样本，结合定制损失函数进行直接偏好优化（DPO），相比传统SFT提供更有效的修正反馈。实验表明其能显著提升生成运动的真实感和准确性。这项工作为利用偏好学习提升视频运动物理合理性提供了可行路径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频生成模型复杂运动不自然、不连贯，传统SFT缺乏有效修正反馈。
method: 提出RealDPO，将真实视频作为正样本用于直接偏好优化DPO，定制损失函数提升运动真实感。
result: 实验证明其生成运动比传统SFT更准确、自然。
conclusion: 为利用偏好学习增强视频运动物理合理性提供有效路径。
---

## Abstract
Video generative models have recently achieved notable advancements in synthesis quality. However, generating complex motions remains a critical challenge, as existing models often struggle to produce natural, smooth, and contextually consistent movements. This gap between generated and real-world motions limits their practical applicability. To address this issue, we introduce RealDPO, a novel alignment paradigm that leverages real-world data as positive samples for preference learning, enabling more accurate motion synthesis. Unlike traditional supervised fine-tuning (SFT), which offers limited corrective feedback, RealDPO employs Direct Preference Optimization (DPO) with a tailored loss function to enhance motion realism. By contrasting real-world videos with erroneous model outputs, RealDPO enables iterative self-correction, progressively refining motion quality. To support post-training in complex motion synthesis, we propose RealAction-5K, a curated dataset of high-quality videos capturing human daily activities with rich and precise motion details. Extensive experiments demonstrate that RealDPO significantly improves video quality, text alignment, and motion realism compared to state-of-the-art models and existing preference optimization techniques.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：视频生成模型在合成质量上已取得显著进步，但复杂运动的生成仍是关键瓶颈——现有模型常难以产生自然、平滑、上下文一致的动作，生成运动与真实世界运动之间存在明显差距，限制了实际应用。
- **核心问题**：如何让视频生成模型学会生成更真实、更准确的运动？传统监督微调（SFT）对运动错误的修正反馈有限，难以有效缩小这一差距。
- **整体含义**：论文提出将真实世界视频作为偏好学习中的正样本，通过直接偏好优化（DPO）让模型在与错误输出的对比中迭代自我修正，从而提升运动真实感。这项工作为利用偏好学习增强视频运动物理合理性提供了新路径。

## 2. 论文提出的方法论

- **核心思想**：RealDPO 是一种新的对齐范式，核心在于把真实视频作为偏好学习中的正样本，将模型生成的错误动作作为负样本，通过对比学习使模型偏向更真实、更自然的运动输出。
- **关键技术细节**：
  - 采用 Direct Preference Optimization（DPO）而非传统 SFT，以提供更强的修正信号。
  - 定制损失函数（tailored loss function），专门针对运动真实性进行优化，使模型在训练中逐步逼近真实物理动作。
  - 通过“真实视频 vs 错误模型输出”的对比，实现迭代式自我修正，渐进式提升运动质量。
  - 为支持复杂运动的后训练，构建了 RealAction-5K 数据集，包含高质量、运动细节丰富的人类日常活动视频。
- **算法流程概述**（基于论文描述的推理性说明）：
  1. 收集真实视频（正样本）与模型生成的错误运动输出（负样本），构成偏好对；
  2. 利用 DPO 框架优化策略模型，使其对真实视频对应的生成结果赋予更高概率；
  3. 结合定制损失函数，在迭代中持续更新偏好数据或模型参数，逐步修正运动生成质量。

> 注：由于未能获取完整 PDF 正文，公式和伪代码细节未在提供内容中展现。

## 3. 实验设计

- **数据集**：
  - 论文提出并使用了 **RealAction-5K**：一个高质量视频数据集，涵盖人类日常活动，富含精细运动细节，用于复杂运动合成的后训练。
  - 从摘要推测，实验中应同时使用了真实视频数据（作为 DPO 正样本）和模型生成的对比样本。
- **Benchmark 与场景**：主要针对复杂运动合成场景，评估生成视频的运动真实性、文本对齐度和整体视频质量。
- **对比方法**：
  - 与当前最先进（state-of-the-art）的视频生成模型对比；
  - 与现有偏好优化技术对比；
  - 与传统的监督微调（SFT）进行对比，以证明 DPO 类方法在运动修正上的优势。
- **评估指标**：论文提到“视频质量、文本对齐、运动真实性”三个维度，但未列出具体指标名称（如 FVD、CLIP Score 等）——这些细节在提供的内容中缺失。

## 4. 资源与算力

- 提供的内容中**未明确说明**使用了多少 GPU、训练时长、模型参数规模等算力信息。
- 需要指出：RealAction-5K 数据集的构建、DPO 训练对真实视频对比样本的依赖，都暗示了较高的数据标注和计算成本，但论文文本中未给出可量化的算力细节。

## 5. 实验数量与充分性

- **实验数量**：从摘要看，至少进行了：
  - 总体性能对比（视频质量、文本对齐、运动真实性）；
  - 与传统 SFT 的对比；
  - 与其他偏好优化方法的对比；
  - 在 RealAction-5K 上的后训练效果验证。
- **充分性评估**：
  - **积极方面**：评估维度较全面（质量、对齐、运动真实性），对比对象既包括 SOTA 生成模型又包括偏好优化方法，具备基本说服力。
  - **不足之处**：由于无法获取完整正文，无法确认是否包含消融实验（如损失函数各组件的作用、正负样本比例的影响、迭代次数敏感性等）、跨数据集泛化实验、用户研究等。因此**实验的完整性和深度无法从现有信息充分判断**，需阅读全文进一步核实。
  - **公平性风险**：未提供数据集划分、基线超参数调整、评估协议等细节，存在潜在的公平性风险（如 baseline 是否充分调优）。

## 6. 论文的主要结论与发现

- RealDPO 相对于传统 SFT 能提供更有效的修正反馈，显著提升生成运动的真实感和准确性。
- 在视频质量、文本对齐和运动真实性三个维度上，RealDPO 均优于现有 SOTA 模型和已有偏好优化方法。
- 将真实视频作为正样本的 DPO 范式，能够实现模型的迭代自我修正，渐进式改进复杂运动合成效果。
- RealAction-5K 作为高质量运动数据集，为复杂运动后训练提供了有效支撑。
- 结论：为利用偏好学习增强视频运动的物理合理性提供了一条可行且有效的路径。

## 7. 优点

- **方法创新性**：将真实视频而非“人为偏好标注”作为 DPO 正样本，避免了主观偏好标注的不一致性问题，更直接地优化运动真实性。
- **意义明确**：针对运动真实性这一视频生成的痛点，设计专门的偏好损失函数，方向清晰。
- **数据贡献**：提出 RealAction-5K 高质量运动数据集，为复杂运动合成研究提供了可复用的资源。
- **无监督信号**：利用“真实 vs 错误输出”的对比，减少了人工偏好标注成本，具有较好的可扩展性。
- **结果说服力**：在多个维度上超越 SOTA 与现有偏好优化方法，展示了方法的有效性。

## 8. 不足与局限

- **细节缺失**：由于提供内容有限（可能受 CAPTCHA 影响），论文的公式、训练流程、具体损失函数形式、超参数设置等信息均未呈现，难以进行技术复现与深度评估。
- **实验覆盖不明确**：无法确认是否包含消融实验、不同数据集上的泛化实验、长时间运动/多物体交互等复杂场景的测试。
- **偏差风险**：
  - RealAction-5K 可能以人类日常活动为主，对非人类动作、抽象运动或极端物理场景的覆盖可能不足；
  - DPO 方法依赖高质量正样本，若真实视频本身存在模糊、遮挡、多义运动，可能引入噪声；
  - “运动真实性”的评估指标是否与人类感知一致尚不明确，可能存在指标偏差。
- **资源限制**：DPO 需要构造大量“错误输出”作为负样本，训练成本可能较高；同时构建 5K 高质量视频数据集也需大量人工筛选。
- **应用限制**：主要针对运动真实性优化，对语义一致性、风格控制、长时记忆等维度可能提升有限；真实视频作为偏好样本的范式对数据版权和隐私也可能带来挑战。

（完）
