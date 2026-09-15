---
title: "MotiMotion: Motion-Controlled Video Generation with Visual Reasoning"
title_zh: MotiMotion：基于视觉推理的运动控制视频生成
authors: "Lee Hsin-Ying, Hanwen Jiang, Yiqun Mei, Jing Shi, Ming-Hsuan Yang, Zhixin Shu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b1e8dd22d2dacf67bb57f6b8bfd7cd90fc93e66c.pdf"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 推理后生成减少不合理运动结果
tldr: 现有运动控制图生视频模型僵硬遵循稀疏、不精确且因果不完整的轨迹，常产生不自然或不合理的结果。本文提出MotiMotion，将运动控制重构为推理后生成，用免训练视觉语言推理器精化主轨迹坐标并想象合理的次级运动。配合置信度感知控制方案，提升了运动自然性与因果合理性，为更符合常识与物理因果的可控视频生成提供新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 运动控制视频生成僵硬遵循稀疏且因果不完整的轨迹，导致结果不自然或不合物理。
method: 提出MotiMotion，将运动控制重构为推理后生成，用视觉语言推理器精化轨迹并补全次级运动。
result: 结合置信度感知控制方案，提升了生成运动的自然性与因果合理性。
conclusion: 为更符合常识与物理因果的可控视频生成提供了新思路。
---

## Abstract
Current motion-controlled image-to-video generation models rigidly follow user-provided trajectories that are often sparse, imprecise, and causally incomplete. 
Such reliance often yields unnatural or implausible outcomes, especially by missing secondary causal consequences. 
To address this, we introduce MotiMotion, a novel framework that reformulates motion control as a reasoning-then-generation problem. 
To encourage causally grounded and commonsense-consistent interactions, we leverage a training-free vision-language reasoner to refine image-space coordinates of primary trajectories and to hallucinate plausible secondary motions. 
To further improve motion naturalness, we propose a confidence-aware control scheme that modulates guidance strength, enabling the model to closely follow high-confidence plans while correcting artifacts under low-confidence inputs with its internal generative priors. 
To support systematic evaluation, we curate a new image-to-video benchmark, MotiBench, consisting of interaction-centric scenes where new events are triggered by motion. 
Both VLM-based evaluation and a human study on MotiBench demonstrate that MotiMotion produces videos with more plausible object behaviors and interaction, and is preferred over existing approaches.

---

## 论文详细总结（自动生成）

# MotiMotion 论文总结

> 说明：提供的 PDF 提取文本仅显示 “no healthy upstream”，正文未能成功获取。以下总结主要依据论文标题、摘要、TLDR 与元数据，涉及正文细节、公式、算力与完整实验设置处会明确标注“未说明/无法确认”。

## 1. 核心问题与整体含义
- **研究背景**：当前的运动控制图生视频模型通常要求用户提供轨迹，并让生成视频严格跟随这些轨迹。
- **核心问题**：用户轨迹往往具有三个缺陷：
  - **稀疏**：只给出少量关键点或粗略路径；
  - **不精确**：轨迹本身可能不准确；
  - **因果不完整**：没有描述由主运动引发的次级运动或交互后果。
- **后果**：模型僵硬遵循不完整轨迹，容易生成不自然、不合理、不符合常识或物理因果的视频，尤其会遗漏“次级因果后果”。
- **整体含义**：论文将运动控制重新定义为“先推理、后生成”的问题，试图让模型不仅跟随轨迹，还能理解运动背后的因果与常识，从而提升可控视频生成的自然性与合理性。

## 2. 方法论
- **核心思想**：MotiMotion 将运动控制从“直接条件生成”改为 **reasoning-then-generation**，即先进行视觉推理，再生成视频。
- **关键技术细节**：
  - **免训练视觉语言推理器**：使用 training-free vision-language reasoner，对主轨迹进行推理和精化。
  - **主轨迹精化**：推理器在图像空间坐标上修正用户提供的主轨迹，使其更合理、更精确。
  - **次级运动想象**：推理器进一步“想象”合理的次级运动，补全用户轨迹中缺失的因果后果。
  - **置信度感知控制方案**：提出 confidence-aware control scheme，根据置信度调节引导强度。
    - 高置信度计划：模型更紧密地跟随推理后的运动计划；
    - 低置信度输入：更多依赖生成模型内部的生成先验来纠正伪影。
- **算法流程（文字描述）**：
  1. 输入图像与用户提供的主轨迹；
  2. 免训练视觉语言推理器推理并精化主轨迹坐标；
  3. 推理器补全合理的次级运动；
  4. 根据推理结果的置信度调制控制/引导强度；
  5. 视频生成模型在置信度感知控制下生成最终视频。
- **公式与网络结构**：提供的材料中未给出具体公式、损失函数、模型架构或训练细节，无法进一步总结。

## 3. 实验设计
- **Benchmark**：论文提出一个新的图生视频 benchmark，名为 **MotiBench**。
- **场景特点**：MotiBench 由 **以交互为中心的场景** 构成，其中新事件由运动触发，强调运动引发的因果交互。
- **评估方式**：
  - **VLM-based evaluation**：基于视觉语言模型的自动评估；
  - **Human study**：在 MotiBench 上进行人类主观研究。
- **对比方法**：摘要称与 **existing approaches** 对比，并显示 MotiMotion 更受偏好，但具体对比了哪些方法、基线名称与设置未在提供材料中说明。
- **数据集规模、指标、消融实验**：未说明，无法确认。

## 4. 资源与算力
- 提供的摘要与元数据中 **未提及** GPU 型号、GPU 数量、训练时长、参数量、推理成本等算力信息。
- 由于方法包含“免训练视觉语言推理器”，可能部分组件无需训练，但视频生成模型本身的训练/推理开销无法从现有材料判断。
- **结论**：算力与资源使用情况无法总结，论文提取文本未提供相关细节。

## 5. 实验数量与充分性
- 从摘要可确认的实验包括：
  - 在 **MotiBench** 上的 **VLM 自动评估**；
  - 在 **MotiBench** 上的 **人类研究**。
- 可能还包括与现有方法的定性/定量比较，但具体实验组数、数据集数量、消融实验数量、基线数量均未说明。
- **充分性判断**：
  - 摘要层面同时使用自动评估与人工评估，并引入新 benchmark，具备一定系统性；
  - 但无法判断是否覆盖多种场景、是否进行充分消融、是否报告统计显著性与失败案例。
- **客观与公平性**：由于缺少基线列表、评估协议、人类研究细节与 VLM 评估提示设计，无法判断实验是否完全客观、公平。

## 6. 主要结论与发现
- MotiMotion 能生成具有 **更合理物体行为与交互** 的视频。
- 在 MotiBench 上，VLM 评估与人类研究均显示 MotiMotion **优于现有方法**，更受偏好。
- 置信度感知控制有助于提升运动自然性：高置信度时紧密跟随计划，低置信度时利用生成先验修正。
- 视觉推理器可精化主轨迹并补全次级运动，从而减少不合理运动结果。
- 总体而言，该工作为更符合常识与物理因果的可控视频生成提供了新思路。

## 7. 优点
- **问题洞察好**：明确指出用户轨迹稀疏、不精确、因果不完整这一关键瓶颈。
- **范式新颖**：将运动控制重构为“推理后生成”，而非单纯条件生成。
- **结合 VLM 常识推理**：利用免训练视觉语言推理器补全次级运动，有望提升因果合理性。
- **控制策略合理**：置信度感知控制在高置信度与低置信度输入之间做权衡，兼顾用户控制与生成先验。
- **评估设计有针对性**：提出 MotiBench，聚焦交互中心场景与运动触发事件，并同时使用 VLM 评估和人类研究。

## 8. 不足与局限
- **正文信息缺失**：由于 PDF 提取失败，无法验证方法细节、公式、网络结构、训练策略与实现方式。
- **实验覆盖未知**：未说明 MotiBench 的规模、场景多样性、基线方法、消融实验、指标与统计显著性。
- **算力与复现性**：未报告 GPU、训练时长、推理成本等资源信息，复现难度与成本不明确。
- **依赖 VLM 推理器**：推理器可能引入自身偏差或幻觉，补全的次级运动未必符合用户真实意图。
- **置信度可靠性**：置信度感知控制依赖置信度估计质量，若估计不准可能影响生成稳定性。
- **评估偏差风险**：VLM 评估与人类研究可能受提示设计、样本选择与主观偏好影响。
- **应用限制**：面向交互中心场景，实时性、计算开销与泛化到开放域复杂场景的能力尚未说明。

（完）
