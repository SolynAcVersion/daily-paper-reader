---
title: "PhyMix: Towards Physically Consistent Single-Image 3D Indoor Scene Generation with Implicit–Explicit Optimization"
title_zh: PhyMix：基于隐式-显式优化的物理一致单图像三维室内场景生成
authors: "Dongli Wu, Jingyu Hu, Ka-Hei Hui, Xiaobao Wei, Zhengzhe Liu, Jianqiang Li"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=RK6j9cwSK4"
tags: ["query:phys-video"]
score: 6.0
evidence: 统一物理评估器，为场景生成中的物理一致性建立基准
tldr: 单图像三维室内场景生成结果往往视觉上合理但违反物理规律。该论文提出统一的物理评估器，从接触、稳定性、几何先验与可部署性四个维度共九个子约束度量物理一致性，并建立首个物理一致性基准。基于该评估器发现现有方法大多缺乏物理意识。进一步提出在训练与推理中整合评估器反馈的隐式-显式优化框架，提升生成场景的物理合理性。这项工作为三维场景生成中的物理约束提供了可量化基准与优化手段。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有单图像三维场景生成虽视觉逼真却常违背物理规律，需要统一的物理一致性评估与优化方法。
method: 构建包含四方面九子约束的物理评估器，并在训练和推理中通过隐式-显式优化融入评估器反馈。
result: 基准表明现有方法物理意识弱，所提框架能显著改善生成场景的物理一致性。
conclusion: 为三维场景生成提供了首个物理一致性基准与可反馈优化的新框架。
---

## Abstract
Existing single-image 3D indoor scene generators often produce results that look visually plausible but fail to obey real-world physics, limiting their reliability in robotics, embodied AI, and design. To examine this gap, we introduce a unified Physics Evaluator that measures four main aspects: contact, stability, geometric priors, and deployability, which are further decomposed into nine sub-constraints, establishing the first benchmark to measure physical consistency. Based on this evaluator, our analysis shows that state-of-the-art methods remain largely physics-unaware. To overcome this limitation, we further propose a framework that integrates feedback from the Physics Evaluator into both training and inference, enhancing the physical plausibility of generated scenes. Specifically, we propose PhyMix, which is composed of two complementary components: (i) implicit alignment via Scene-GRPO, a critic-free group-relative policy optimization that leverages the Physics Evaluator as a preference signal and biases sampling towards physically feasible layouts, and (ii) explicit refinement via a plug-and-play Test-Time Optimizer (TTO) that uses differentiable evaluator signals to correct residual violations during generation. Overall, our method unifies evaluation, reward shaping, and inference-time correction, producing 3D indoor scenes that are both visually faithful and physically plausible. Extensive evaluations on synthetic dataset confirm state-of-the-art performance in both visual fidelity and physical plausibility, and extensive qualitative examples on stylized and real-world images further showcase the method’s robustness.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 研究动机：现有单图像 3D 室内场景生成方法虽然能产生视觉上逼真的结果，但常常违反真实物理规律（如接触不实、稳定性差、几何不合理等），这严重限制了它们在机器人、具身智能和设计等对物理可靠性有高要求的领域中的应用。
- 整体含义：论文试图解决“视觉合理但物理不合理”这一关键鸿沟，并提出一套统一的物理一致性度量基准与优化方法，推动三维场景生成从“看起来对”走向“物理上可用”。

## 2. 论文提出的方法论

- 核心思想：构建统一的物理评估器，并将其反馈同时整合到训练和推理阶段，形成“评估—奖励修正—测试时修正”的闭环优化框架。
- 物理评估器：从四个主要维度度量物理一致性：接触（contact）、稳定性（stability）、几何先验（geometric priors）、可部署性（deployability），进一步分解为九个子约束，并以此建立首个物理一致性基准。
- 隐式优化（Scene-GRPO）：一种无需评论家（critic-free）的组相对策略优化方法，将物理评估器作为偏好信号，将采样过程偏向物理可行的布局。
- 显式优化（Test-Time Optimizer, TTO）：即插即用的测试时优化器，利用可微的评估器信号，在生成过程中对残留的物理违规进行逐点修正。
- 整体流程（文字说明）：生成器输出初始场景 → 物理评估器计算各子约束的违规程度 → 训练阶段通过 Scene-GRPO 将评估分数转化为策略优化信号；推理阶段通过 TTO 对场景进行迭代微调，最终输出既保持视觉保真又满足物理约束的场景。
- 说明：摘要和元数据中没有给出具体的数学公式或算法伪代码，因此只能进行文字级描述。

## 3. 实验设计

- 数据集/场景：在合成数据集上进行了大量定量评估（具体数据集名称与规模未披露）；同时提供风格化图像与真实世界图像上的大量定性示例，以展示鲁棒性。
- Benchmark：首次建立的物理一致性基准，由统一物理评估器定义，包含四个维度、九个子约束。
- 对比方法：与当前最先进（SOTA）的室内场景生成方法进行比较，但摘要中未列出具体基线方法名称。
- 评估指标：视觉保真度与物理合理性并重，在合成数据集上达到 SOTA。

## 4. 资源与算力

- 所提供文本（摘要与元数据）中未明确说明使用的 GPU 型号、GPU 数量、训练时长、参数量、显存占用或推理时间等算力相关信息。

## 5. 实验数量与充分性

- 从公开信息看，实验包括：合成数据集上的定量对比，以及风格化/真实图像上的定性展示。
- 但摘要中未展示具体实验数量、数值表格、消融实验、统计显著性检验或与多个基线方法的全面比较。
- 由于缺乏详细实验章节和具体数据，无法准确判断实验的充分性、客观性和公平性；实现细节与基线设置均未公开。

## 6. 论文的主要结论与发现

- 现有 SOTA 单图像室内场景生成方法大多“物理无意识”，生成结果虽视觉合理但物理一致性较差。
- 提出的统一物理评估器可以量化场景的物理一致性，并构成有效的基准。
- 提出的 PhyMix 框架通过隐式（Scene-GRPO）与显式（TTO）优化，能够显著提升生成场景的物理合理性，同时保持视觉保真度，在合成数据集上达到 SOTA。
- 在风格化图像与真实图像上的定性实验进一步验证了方法的鲁棒性和泛化能力。

## 7. 优点

- 领域创新：首次为三维室内场景生成建立物理一致性基准，填补了评估工具的空白。
- 统一量化：将物理一致性分解为四个维度、九个子约束，可计算、可比较、可优化。
- 闭环设计：将评估器同时用于训练阶段的奖励塑造与推理阶段的修正，而非仅作为事后评估指标。
- 技术新颖性：Scene-GRPO 免评论家设计降低训练复杂度；TTO 即插即用，易于适配不同生成模型。
- 验证范围广：涵盖合成、风格化与真实世界图像，展示了一定泛化能力。

## 8. 不足与局限

- 信息不完整：目前仅提供摘要与元数据，缺少网络结构、损失函数、算法流程、评估器具体定义等关键细节，难以复现验证。
- 实验透明度不足：未披露具体数据集、基线方法、定量指标数值、消融实验与误差分析，实验充分性与公平性难以评估。
- 算力成本未提及：未报告训练/推理的资源消耗，不利于实际部署评估。
- 物理覆盖有限：九个子约束能否完整覆盖复杂真实场景中的全部物理规律仍存疑。
- 发表状态提示：该论文在 OpenReview 上标注为 ICLR-2026-Rejected-Public，可能说明其方案或实验证据存在尚未解决的问题，但由于未提供评审意见，不便进一步推测。

（完）
