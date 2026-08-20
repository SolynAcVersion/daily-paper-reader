---
title: Physics-Guided Motion Loss for Video Generation Model
title_zh: 视频生成模型的物理引导运动损失
authors: "Bowen Xue, Giuseppe Claudio Guarnera, Shuang Zhao, Zahra Montazeri"
date: 2026-04-30
pdf: "https://openreview.net/pdf/e8d93979c0e9f9ceb30a8fd994a4e162def94b33.pdf"
tags: ["query:phys-video"]
score: 9.0
evidence: 直接针对物理法则、跨帧一致性与物理真实运动，提出物理引导损失
tldr: "视频扩散模型常生成视觉逼真但物理上不合理的运动，如橡皮膜变形与物体运动不一致。本文提出一种频域物理先验，将平移、旋转和缩放等常见运动模式转化为轻量谱损失，无需修改模型架构即可提升运动合理性。在Open-Sora、MVDIT、Hunyuan及Wan 2.1-14B等模型上，该损失显著提升了运动准确率、动作识别和物理导向指标，用户偏好达74-83%。该方法为视频生成提供了一种即插即用的物理一致性改善手段。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频扩散模型虽然视觉效果逼真，但常出现橡皮膜变形和物体运动不一致等物理伪影。
method: 引入频域物理先验，将平移、旋转、缩放等常见运动模式分解为轻量谱损失，不改动模型架构。
result: "在Open-Sora、MVDIT和Hunyuan上运动准确率和动作识别平均提升约11%，并在Wan 2.1-14B上保持一致的物理与质量指标增益，用户偏好达74-83%。"
conclusion: 频域物理损失能有效提升视频生成的运动物理合理性，且可即插即用于多种模型。
---

## Abstract
Current video diffusion models generate visually compelling content but often struggle with physical motion, producing subtle artifacts like rubber-sheet deformations and 
inconsistent object motion. We introduce a frequency-domain physics prior that improves 
motion plausibility without modifying model architectures. Our method decomposes common 
motion patterns (translation, rotation, scaling) into lightweight spectral losses. 
Applied to Open-Sora, MVDIT, and Hunyuan, our approach improves both motion accuracy and action recognition by ∼11\% on average on OpenVID-1M (relative), while maintaining visual quality. Additional results on Wan 2.1-14B show consistent gains on video-quality and physics-oriented metrics. User studies show 74-83\% preference for our physics-enhanced videos. It also reduces warping error by 22-37\% (depending on the backbone) and improves temporal consistency scores. These results indicate that simple, global spectral cues are an effective drop-in regularizer for physically plausible motion in video diffusion.

---

## 论文详细总结（自动生成）

# 视频生成模型的物理引导运动损失：中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 现有视频扩散模型（如 Open-Sora、MVDIT、Hunyuan、Wan 2.1-14B 等）能够生成视觉上高度逼真的视频，但在物理运动上往往存在明显缺陷。
- 常见伪影包括：
  - **橡皮膜变形**（rubber-sheet deformations）：物体表面像被拉伸的薄膜一样不规则扭曲；
  - **物体运动不一致**：同一物体在不同帧间的运动不符合刚体运动规律。
- 这些伪影表明模型缺乏对现实物理法则的显式约束，仅靠数据驱动难以保证运动的物理合理性。
- 论文的核心目标是：在不更改模型架构的前提下，通过引入一种轻量级的物理先验，提升生成视频中运动的物理真实感。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将常见的刚体运动模式（平移、旋转、缩放）在**频域**中表示，并将其转化为可直接叠加到原始训练损失上的**轻量谱损失**（spectral losses），从而作为“即插即用”的正则化项引导模型生成符合物理规律的运动。
- **关键技术细节**：
  - 利用傅里叶变换将视频帧序列中的运动模式分解到频域；
  - 对不同运动模式（平移、旋转、缩放）构建对应的频谱特征约束；
  - 设计不依赖模型内部结构的损失项，因此可以方便地集成到任意现有视频扩散模型上。
- **算法流程（文字说明）**：
  1. 输入生成视频或中间特征；
  2. 对帧间运动执行频域分解；
  3. 计算分解结果与目标物理运动模式（平移/旋转/缩放）的频谱一致性损失；
  4. 将该项损失与原始生成损失加权相加，用于训练或微调；
  5. 推理阶段无需任何额外改动。

> 注意：原文摘要中未给出具体公式或损失函数权重，此处为基于摘要的合理概括。

## 3. 实验设计：数据集、基准和对比方法

- **基准数据集**：OpenVID-1M（用于运动准确率和动作识别评估）。
- **模型/骨干网络**：
  - Open-Sora
  - MVDIT
  - Hunyuan
  - Wan 2.1-14B（作为额外的大规模验证）
- **评估指标**：
  - 运动准确率（motion accuracy）
  - 动作识别准确率（action recognition）
  - 视频质量指标（video-quality metrics）
  - 物理导向指标（physics-oriented metrics）
  - 用户研究（偏好比例）
  - Warping误差
  - 时间一致性得分
- **对比方法**：摘要中未明确提及与哪些现有物理一致性方法进行对比，仅提供了“未加物理损失”的基线对比（即每个骨干模型自身的默认版本）。

## 4. 资源与算力

- 论文中**未明确说明**使用的 GPU 型号、数量、训练时长或计算资源总量。
- 仅提到该方法为轻量级损失，但未给出具体额外开销或训练成本的量化数据。

## 5. 实验数量与充分性

- 实验覆盖了**四个不同的视频生成骨干模型**，规模从中小型（Open-Sora、MVDIT）到大型（Hunyuan、Wan 2.1-14B），具有一定代表性。
- 评估维度较为丰富，包括自动指标（运动准确率、动作识别、视频质量、物理指标、warping误差、时间一致性）和主观用户研究。
- 但完整实验数量不明：从摘要看，**未提供消融实验**（如不同运动模式权重的组合、损失强度的影响等），也没有报告在多个不同数据集上的泛化表现。
- 也未见与现有物理约束方法的直接对比实验，因此是否达到 SOTA 仍有待确认。

## 6. 论文的主要结论与发现

- 在 Open-Sora、MVDIT 和 Hunyuan 上，平均运动准确率和动作识别提升约 **11%（相对提升）**；
- 在 Wan 2.1-14B 上，视频质量和物理导向指标也获得一致改善；
- Warping 误差降低 **22–37%**（取决于骨干网络）；
- 时间一致性得分提升；
- 用户偏好实验中，**74–83%** 的受试者更喜欢物理增强后的视频；
- 结论：**简单的全局频谱线索可以作为视频扩散模型中物理合理运动的有效“即插即用”正则化器**，无需修改模型架构。

## 7. 优点

- **即插即用**：无需改动模型架构，可集成到多种现有视频生成模型中。
- **轻量高效**：频域损失计算成本低，对训练和推理负担小。
- **跨模型泛化**：在多个不同规模和类型的骨干网络上均有效。
- **多维度验证**：同时使用客观自动指标（运动准确率、动作识别、warping误差、时间一致性）和主观用户研究，结论相对稳健。
- **物理先验简洁**：将平移、旋转、缩放等基本运动模式统一到频域，思想简单且具有理论可解释性。

## 8. 不足与局限

- **原文未公开具体实现细节**：例如损失公式、频域分解的具体算子、权重超参数、训练策略等，导致复现难度较大。
- **未提供算力资源信息**：无法评估方法的实际训练成本。
- **实验完整性有限**：缺少消融实验、不同损失组合的分析、与现有物理约束方法的直接对比，也未见在更广泛数据集（如自然场景、复杂非刚体运动）上的验证。
- **适用范围可能有限**：该物理先验主要覆盖平移、旋转和缩放等**刚体运动模式**，对流体、布料、弹性物体等非线性/非刚体运动可能约束不足。
- **物理合理性仍属于启发式**：频域约束本质上是一种统计正则化，并非完整的物理模拟器，可能无法纠正所有物理伪影。
- **摘要信息量有限**：论文可能尚处于投稿/预印本阶段，完整实验细节和风险分析需以正式版为准。

---

（完）
