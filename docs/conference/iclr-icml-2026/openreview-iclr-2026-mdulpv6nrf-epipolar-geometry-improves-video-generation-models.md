---
title: Epipolar Geometry Improves Video Generation Models
title_zh: 对极几何改进视频生成模型
authors: "Orest Kupyn, Fabian Manhardt, Federico Tombari, Christian Rupprecht"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=MDulpv6NRF"
tags: ["query:video-gen-rl"]
score: 8.0
evidence: 对极几何约束提升视频生成的真实感与3D一致性
tldr: 扩散Transformer视频生成模型仍存在几何不一致、运动不稳定等破坏真实三维场景感的问题。本文探索对极几何约束，通过对极几何的成对约束与偏好优化来对齐扩散模型，直接改善不稳定的相机轨迹与几何不一致。实验表明该方法能提升生成视频的几何一致性与真实感，有助于下游生成与重建任务。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视频扩散模型仍存在几何不一致与运动不稳定，破坏真实三维场景感。
method: 利用成对极几何约束与偏好优化对齐扩散模型，改善相机轨迹与几何一致性。
result: 提升生成视频的几何一致性与真实感。
conclusion: 将几何先验引入视频生成以增强物理与几何合理性。
---

## Abstract
Video generation models have progressed tremendously through large latent diffusion transformers trained with rectified flow techniques. Yet these models still struggle with geometric inconsistencies, unstable motion, and visual artifacts that break the illusion of realistic 3D scenes. 3D-consistent video generation could significantly impact numerous downstream applications in generation and reconstruction tasks.
We explore how epipolar geometry constraints improve modern video diffusion models. Despite massive training data, these models fail to capture fundamental geometric principles underlying visual content. We align diffusion models using pairwise epipolar geometry constraints via preference-based optimization, directly addressing unstable camera trajectories and geometric artifacts through mathematically principled geometric enforcement.
Our approach efficiently enforces geometric principles without requiring end-to-end differentiability. Evaluation demonstrates that classical geometric constraints provide more stable optimization signals than modern learned metrics, which produce noisy training signals. Training on static scenes with dynamic cameras ensures metric quality while the model still generalize to various dynamic scenes. By bridging data-driven learning with classical geometric computer vision, we present a practical method for generating 3D consistent videos without compromising visual quality.

---

## 论文详细总结（自动生成）

# 论文总结：Epipolar Geometry Improves Video Generation Models

> 说明：给定材料中 PDF 正文未成功提取（URL 返回 503 / no healthy upstream），仅有标题、摘要与元数据。因此以下总结主要依据摘要和元数据；涉及数据集、算力、实验组数等细节无法确认，并已明确标注。

## 1. 核心问题与研究动机
- 视频生成模型已通过大规模潜空间扩散 Transformer 与 rectified flow 技术取得显著进展。
- 但现有模型仍存在几何不一致、运动不稳定和视觉伪影，破坏真实三维场景感。
- 3D 一致的视频生成对生成与重建等下游任务具有重要价值。
- 核心矛盾：即使训练数据规模巨大，模型仍未捕捉视觉内容背后的基本几何原则。
- 研究目标：引入对极几何约束，提升视频扩散模型的几何一致性与真实感，同时不牺牲视觉质量。

## 2. 方法论
- 核心思想：利用对极几何约束改进现代视频扩散模型，通过偏好优化对齐扩散模型。
- 关键思路：
  - 使用成对极几何约束，直接针对不稳定相机轨迹与几何伪影。
  - 以偏好优化方式引入几何约束，避免要求几何约束端到端可微。
  - 强调数学上有原则的几何强制，而非仅依赖数据驱动学习。
  - 经典几何约束被认为比现代学习指标提供更稳定的优化信号，后者可能产生噪声训练信号。
- 训练策略：
  - 在静态场景、动态相机设置上训练，以保证几何度量质量。
  - 模型仍可泛化到多种动态场景。
- 公式与算法流程：
  - 摘要未给出具体公式、损失函数、偏好构造方式或完整算法流程。
  - 可概括理解为：生成候选视频/帧对，依据对极几何一致性形成偏好信号，再用偏好优化更新扩散模型。

## 3. 实验设计
- 摘要仅称评估表明方法有效，但未列出具体数据集、场景、benchmark 或对比方法。
- 可确认或推断的信息：
  - 训练场景：静态场景 + 动态相机。
  - 泛化目标：多种动态场景。
  - 对比信号：经典几何约束 vs. 现代学习指标。
- 具体 benchmark、baseline、评价指标、数据集名称：给定材料未提供，无法总结。

## 4. 资源与算力
- 给定材料未提及 GPU 型号、数量、训练时长、参数量、数据规模或推理成本。
- 因此无法评估该方法的算力需求与可复现性。

## 5. 实验数量与充分性
- 未提供实验组数、消融实验数量、数据集数量或统计显著性分析。
- 从摘要看，至少涉及：
  - 几何约束效果评估。
  - 与学习型指标的优化信号对比。
  - 静态场景训练到动态场景的泛化验证。
- 但由于缺少正文细节，无法判断实验是否充分、客观、公平。

## 6. 主要结论与发现
- 对极几何约束能提升生成视频的几何一致性与真实感。
- 经典几何约束比现代学习指标提供更稳定的优化信号。
- 使用静态场景与动态相机训练，可在保持度量质量的同时泛化到动态场景。
- 方法无需端到端可微，即可生成 3D 一致视频且不牺牲视觉质量。
- 将数据驱动学习与经典几何计算机视觉结合，有助于下游生成与重建任务。

## 7. 优点
- 将经典多视几何先验引入现代视频扩散模型，思路简洁且有理论依据。
- 通过偏好优化绕开不可微几何约束，具有工程可行性。
- 利用经典几何作为偏好/奖励信号，可能减少学习型指标的噪声。
- 训练设置巧妙：静态场景 + 动态相机，有利于获得可靠几何监督并泛化。
- 目标明确：在提升 3D 一致性的同时尽量保持视觉质量。

## 8. 不足与局限
- 给定材料缺少正文，无法核验实验细节、算力开销、对比公平性与复现条件。
- 对极几何通常依赖静态场景或刚性假设；对非刚性物体、多物体独立运动、遮挡、大视差等复杂动态的适用性未说明。
- 偏好优化需要构造偏好数据或奖励信号，可能带来额外成本与偏差。
- 未提供视觉质量、几何一致性、运动稳定性之间的定量权衡。
- 未说明失败案例、超参敏感性、计算开销与可复现性。
- 元数据来源标注为 ICLR-2026-Rejected-Public，但 score 为 8.0；评审结论与公开版本需进一步查证。

（完）
