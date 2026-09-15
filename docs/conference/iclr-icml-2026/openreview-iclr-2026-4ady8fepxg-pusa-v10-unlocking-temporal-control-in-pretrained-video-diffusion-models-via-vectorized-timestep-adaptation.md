---
title: "Pusa V1.0: Unlocking Temporal Control in Pretrained Video Diffusion Models via Vectorized Timestep Adaptation"
title_zh: Pusa V1.0：通过向量化时间步适配解锁预训练视频扩散模型的时间控制
authors: "Yaofang Liu, Yumeng REN, Aitor Artola, Yuxuan Hu, Xiaodong Cun, Xiaotong Zhao, Alan Zhao, Raymond H. Chan, Suiyun Zhang, Rui Liu, Dandan Tu, Jean-michel Morel"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=4adY8FepXg"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 向量化时间步适配实现视频扩散细粒度时间控制
tldr: 视频扩散模型受限于标量时间步导致的帧演化刚性同步，现有适配存在计算低效、灾难性遗忘或适用面窄等问题。本文提出Pusa V1.0，通过向量化时间步适配VTA在统一扩散框架内实现细粒度时间控制，且为无损适配，可完整保留预训练模型能力。该工作提升了视频时间建模的灵活性与效率。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 视频扩散模型受标量时间步限制，帧演化刚性同步，现有适配方案存在低效或遗忘问题。
method: 提出Pusa V1.0，采用向量化时间步适配VTA实现统一框架内的细粒度时间控制。
result: VTA为非破坏性适配，在保持预训练能力的同时提升时间建模灵活性。
conclusion: 为预训练视频扩散模型的时间控制提供了通用高效方案。
---

## Abstract
The rapid advancement of video diffusion models has been hindered by fundamental limitations in temporal modeling, particularly the rigid synchronization of frame evolution imposed by conventional scalar timestep variables. While task-specific adaptations and autoregressive models have sought to address these challenges, they remain constrained by computational inefficiency, catastrophic forgetting, or narrow applicability. In this work, we present \textbf{Pusa} V1.0, a versatile model that leverages \textbf{vectorized timestep adaptation (VTA)} to enable fine-grained temporal control within a unified video diffusion framework. Note that VTA is a non-destructive adaptation, which means that it fully preserves the capabilities of the base model.
\textbf{Unlike conventional methods like Wan-I2V, which finetune a base text-to-video (T2V) model with abundant resources to do image-to-video (I2V), we achieve comparable results in a zero-shot manner after an ultra-efficient finetuning process based on VTA. Moreover, this method also unlocks many other zero-shot capabilities simultaneously, such as start-end frames and video extension ---all without task-specific training. Meanwhile, it keeps the T2V capability from the base model.} Mechanistic analyses also reveal that our approach preserves the foundation model's generative priors while surgically injecting temporal dynamics, avoiding the combinatorial explosion inherent to the vectorized timestep. This work establishes a scalable, efficient, and versatile paradigm for next-generation video synthesis, democratizing high-fidelity video generation for research and industry alike.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 正文提取失败（503 / “no healthy upstream”），以下总结主要依据论文标题、摘要与元数据；凡未在给定材料中出现的实验、数据集、算力等细节，均明确标注为“未说明”，不作编造性补充。

## 1. 核心问题与整体含义

- **研究动机**：视频扩散模型在时间建模上存在根本限制。传统扩散模型通常使用**标量时间步变量**，导致所有帧的演化被刚性同步，难以实现细粒度的时间控制。
- **现有方案不足**：任务特定适配和自回归模型虽尝试解决该问题，但分别受限于计算低效、灾难性遗忘或适用面窄。
- **整体含义**：论文提出 **Pusa V1.0**，通过**向量化时间步适配（VTA）**，在统一视频扩散框架内实现细粒度时间控制。其关键定位是**非破坏性适配**，即完整保留预训练基础模型能力，同时以高效、通用方式解锁多种时间控制任务。
- **元数据定位**：该工作被标注为 ICLR-2026 Accepted，元数据评分 7.0，核心贡献被概括为“向量化时间步适配实现视频扩散细粒度时间控制”。

## 2. 方法论

- **核心思想**：将传统标量时间步扩展为**向量化时间步**，使扩散过程中的时间控制不再全局同步，从而支持不同帧或时间位置具有更灵活的时间步配置。从标题与摘要可推断，这是实现细粒度时间控制的关键。
- **关键特性**：
  - **非破坏性适配**：VTA 完整保留基础模型能力，避免灾难性遗忘。
  - **统一框架**：在同一视频扩散框架内支持多种时间控制能力，而非为每个任务单独设计模型。
  - **零样本多任务**：在基于 VTA 的超高效微调后，以零样本方式完成 I2V，并同时解锁起止帧控制、视频扩展等能力。
  - **保留 T2V 能力**：适配后仍保持基础模型的文本到视频生成能力。
- **流程概述**：
  1. 以预训练视频扩散模型为基础；
  2. 引入向量化时间步适配 VTA；
  3. 通过超高效微调注入时间动态；
  4. 在不针对特定任务训练的情况下，零样本支持 I2V、起止帧、视频扩展等任务；
  5. 机制分析表明，该方法保留基础模型生成先验，同时“外科手术式”注入时间动态，避免向量化时间步带来的组合爆炸。
- **未提供细节**：给定材料未给出具体公式、损失函数、网络结构、向量化时间步的数学定义、训练算法伪代码或实现细节。

## 3. 实验设计

- **数据集 / 场景**：给定材料**未说明**使用了哪些数据集或具体场景。
- **Benchmark**：**未说明**具体 benchmark、评价指标或定量结果。
- **对比方法**：摘要层面提到与传统方法 **Wan-I2V** 对比。Wan-I2V 需要大量资源微调基础 T2V 模型来完成 I2V；Pusa 则声称在基于 VTA 的超高效微调后，以零样本方式达到与之相当的结果。
- **涉及任务**：I2V、起止帧控制、视频扩展，以及保持基础模型 T2V 能力。
- **缺失信息**：未提供分辨率、视频时长、用户研究、定量指标、消融实验、基线列表等。

## 4. 资源与算力

- 给定材料**未明确说明** GPU 型号、数量、训练时长、参数量、数据规模或总计算量。
- 仅出现定性表述：
  - VTA 微调被描述为“**ultra-efficient finetuning**”；
  - 对比方法 Wan-I2V 被描述为使用“**abundant resources**”进行微调。
- 因此，无法从现有材料总结具体算力开销，也无法判断“超高效”的量化程度。

## 5. 实验数量与充分性

- 给定材料**未给出实验组数**，也未说明使用了多少数据集、做了多少消融实验或进行了哪些定量对比。
- 因此，**无法评估实验充分性、客观性与公平性**。
- 需全文验证的问题包括：
  - 与 Wan-I2V 的对比是否在相同数据、分辨率、时长、评价指标和算力条件下进行；
  - 零样本 I2V 的“comparable results”是否有定量证据；
  - 起止帧、视频扩展等能力是否经过系统评测；
  - 是否验证了 T2V 能力无退化；
  - 是否报告失败案例、偏差和泛化边界。

## 6. 主要结论与发现

- VTA 是一种**非破坏性适配**，可在提升时间建模灵活性的同时保留预训练模型能力。
- Pusa V1.0 能在统一扩散框架内实现细粒度时间控制。
- 基于 VTA 的超高效微调后，Pusa 可以零样本完成 I2V，并达到与 Wan-I2V 相当的结果。
- 同一方法还同时解锁起止帧控制和视频扩展等零样本能力，且无需任务特定训练。
- 机制分析表明，该方法保留基础模型生成先验，避免向量化时间步固有的组合爆炸。
- 总体结论：为预训练视频扩散模型的时间控制提供了**可扩展、高效、通用**的新范式。

## 7. 优点

- **非破坏性适配**：避免灾难性遗忘，保留基础模型 T2V 能力。
- **统一框架**：一个模型支持多种时间控制任务，减少任务特定训练成本。
- **零样本多能力**：I2V、起止帧、视频扩展等无需任务特定训练。
- **效率潜力**：相比 Wan-I2V 等需大量资源微调的方法，VTA 微调被描述为超高效。
- **机制清晰度**：强调保留生成先验并避免向量化时间步组合爆炸，具备较强概念吸引力。
- **应用意义**：若成立，可降低高保真视频生成的研究与

与应用门槛，并为视频编辑、内容创作、长视频生成等场景提供更灵活的时间控制接口。

## 8. 局限与待验证问题

- **证据基础受限**：由于 PDF 正文提取失败，当前总结主要依据标题、摘要与元数据，无法核对方法公式、训练细节、实验设置与统计显著性。
- **方法细节缺失**：VTA 的向量化时间步如何定义、如何与现有扩散 Transformer/UNet 结合、训练目标、微调数据与规模、推理成本均未说明。
- **实验充分性未知**：未提供数据集、benchmark、评价指标、基线列表、消融实验或用户研究，无法判断零样本 I2V 与 Wan-I2V 的“comparable results”是否公平、稳健。
- **泛化与鲁棒性待验证**：起止帧控制、视频扩展等能力是否在不同分辨率、时长、运动复杂度、域外文本提示下稳定，给定材料未说明。
- **效率声明待量化**：“ultra-efficient finetuning”缺少 GPU 时数、参数量、显存占用、训练样本量等指标，难以与 Wan-I2V 的“abundant resources”进行客观比较。
- **能力保持验证不足**：是否定量验证 T2V 能力无退化，是否出现时间一致性、身份保持、运动自然度下降，未说明。
- **伦理与安全讨论缺失**：视频生成可能涉及深伪、版权、隐私与滥用风险，给定材料未说明安全措施或防护机制。
- **可复现性信息不足**：至少在给定材料中，未提供代码、模型权重、训练配方或评测协议。

## 9. 总体评价

- 从摘要与元数据看，Pusa V1.0 的核心思想具有较高概念价值：将标量时间步扩展为向量化时间步，并以非破坏性适配方式统一多种视频时间控制任务。若实验成立，可能对视频扩散模型的可控生成、编辑和扩展产生推动作用。
- 但当前可验证信息有限，尚不能确认其相对 Wan-I2V 的优势幅度、效率收益、零样本能力的稳定性与公平性。
- 建议在全文可用后重点核查：VTA 的数学形式与实现、训练数据与算力、定量对比、消融实验、T2V 保持性、失败案例以及安全伦理讨论。
- 元数据评分 7.0 与 ICLR-2026 Accepted 表明其可能具备一定学术认可度，但最终结论仍需以完整论文与公开实验为准。

（完）
