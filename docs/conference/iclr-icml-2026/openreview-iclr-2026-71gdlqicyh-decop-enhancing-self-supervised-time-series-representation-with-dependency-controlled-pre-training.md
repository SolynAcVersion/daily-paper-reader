---
title: "DeCoP: Enhancing Self-Supervised Time Series Representation with Dependency Controlled Pre-training"
title_zh: DeCoP：基于依赖控制预训练的自监督时间序列表示增强
authors: "Yuemin Wu, Zhongze Wu, Xiu Su, Feng Yang, Hongyan Xu, Xi Lin, Wenti Huang, Shan You, Chang Xu"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=71GdLqicyH"
tags: ["query:frame-dist"]
score: 4.0
evidence: 动态多尺度时间依赖建模
tldr: 针对时间序列预训练中动态时间依赖随分布漂移与多尺度模式演变、统一归一化与单尺度建模难以捕捉复杂时间变化的问题，作者提出依赖控制预训练DeCoP，引入实例级块归一化并显式建模动态多尺度依赖，模拟演化的块间依赖。实验表明该方法更好捕捉复杂时间变化并提升下游泛化，其依赖建模思路可迁移至视频帧间分布关系，但本身面向时间序列。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 时间序列预训练中动态时间依赖随分布漂移与多尺度模式演变，统一归一化与单尺度建模难以捕捉复杂时间变化。
method: 提出依赖控制预训练DeCoP，引入实例级块归一化并显式建模动态多尺度依赖，模拟演化的块间依赖。
result: 该方法更好捕捉复杂时间变化，提升预训练模型在下游任务上的泛化。
conclusion: 通过多尺度依赖建模为时序表示学习提供了可迁移思路，但面向时间序列而非视频帧。
---

## Abstract
Modeling dynamic temporal dependencies is a critical challenge in time series pre-training, which evolve due to distribution shifts and multi-scale patterns. This temporal variability severely impairs the generalization of pre-trained models to downstream tasks. Existing frameworks often adopt uniform instance-level normalization, which overlooks patch-specific characteristics, and model dependencies at a single scale, failing to capture complex temporal variations. To address these limitations, we propose DeCoP, a Dependency Controlled Pre-training framework that explicitly models dynamic, multi-scale dependencies by simulating evolving inter-patch dependency. DeCoP first introduces Instance-wise Patch Normalization (IPN) to mitigate distributional shifts while preserving the unique characteristics of each patch, creating a robust foundation for representation learning. Building on this, a hierarchical Dependency Controlled Learning (DCL) strategy explicitly models inter-patch dependencies across multiple temporal scales within the latent space. This is complemented by a global Instance-level Contrastive Module (ICM), which enhances generalization by learning instance-discriminative representations from time-invariant positive pairs. DeCoP achieves state-of-the-art results on ten datasets, improving MSE by 3% on ETTh1 over PatchTST using only 37% of the FLOPs.

---

## 论文详细总结（自动生成）

> 说明：提供的“论文 PDF 提取文本”实际是 OpenReview 的 CAPTCHA 验证页，未包含论文正文。以下总结主要依据论文元数据、摘要与 tldr；涉及实验细节、算力等无法从摘要确认的内容会明确标注。

## 1. 核心问题与整体含义

- **研究动机**：时间序列预训练中的动态时间依赖会随分布漂移和多尺度模式演变，导致预训练模型向下游任务泛化时表现受损。
- **现有不足**：
  - 多数框架采用统一的实例级归一化，忽略不同 patch 的特定特征。
  - 依赖建模通常局限于单一尺度，难以捕捉复杂时间变化。
- **整体含义**：论文提出 **DeCoP**，即依赖控制预训练框架，试图通过显式建模动态、多尺度的块间依赖，提升时间序列自监督表示学习的效果与泛化能力。
- **定位**：论文面向时间序列预训练；元数据指出其依赖建模思路可迁移至视频帧间分布关系，但论文本身并非面向视频帧任务。

## 2. 方法论：核心思想与关键技术

- **核心思想**：显式建模动态、多尺度的 inter-patch dependency，模拟演化的块间依赖，以增强自监督时间序列表示。
- **关键技术模块**：
  - **Instance-wise Patch Normalization, IPN（实例级块归一化）**：
    - 用于缓解分布漂移。
    - 同时保留每个 patch 的独特特征。
    - 为后续表示学习提供更稳健的基础。
  - **Hierarchical Dependency Controlled Learning, DCL（分层依赖控制学习）**：
    - 在潜空间中跨多个时间尺度显式建模 patch 间依赖。
    - 目标是捕捉动态、多尺度的时间依赖结构。
  - **Global Instance-level Contrastive Module, ICM（全局实例级对比模块）**：
    - 从 time-invariant positive pairs（时间不变正样本对）中学习实例判别表示。
    - 通过对比学习增强模型泛化能力。
- **算法流程（文字化）**：
  1. 输入时间序列被划分为多个 patch。
  2. 使用 IPN 对每个 patch 进行实例级归一化，减少分布漂移并保留 patch 特性。
  3. 在潜空间中使用 DCL 分层建模多个时间尺度上的 patch 间依赖。
  4. 引入全局 ICM，通过时间不变正样本对学习实例级判别表示。
  5. 联合优化上述表示，用于下游时间序列任务。
- **公式与细节**：摘要未给出具体公式、损失函数或算法伪代码，因此无法进一步核实。

## 3. 实验设计

- **数据集 / 场景**：
  - 摘要称在 **十个数据集** 上取得 state-of-the-art 结果。
  - 仅明确点名 **ETTh1**。
  - 指标使用 **MSE**，暗示主要面向时间序列预测类下游任务。
- **Benchmark**：
  - 以时间序列预训练与下游预测任务为基准。
  - 与 **PatchTST** 进行了明确对比。
- **对比方法**：
  - 摘要明确提到 PatchTST。
  - 其他对比方法、完整 baseline 列表未在摘要中给出。
- **主要实验结果**：
  - 在十个数据集上达到 SOTA。
  - 在 ETTh1 上，相比 PatchTST，MSE 改善 **3%**。
  - 仅使用 PatchTST **37% 的 FLOPs**。

## 4. 资源与算力

- 摘要与元数据中 **未明确说明** 使用的 GPU 型号、数量、训练时长、参数量或总计算开销。
- 仅提到推理 / 计算效率相关指标：ETTh1 上使用 PatchTST 的 **37% FLOPs**。
- 因此无法评估其训练算力成本、可复现性与实际部署开销。

## 5. 实验数量与充分性

- **从摘要可见的实验规模**：
  - 十个数据集上的主实验。
  - 至少包含 ETTh1 上与 PatchTST 的 MSE 和 FLOPs 对比。
  - 方法包含 IPN、DCL、ICM 三个模块，暗示可能有消融实验，但摘要未报告具体消融结果。
- **充分性评估**：
  - 十个数据集覆盖较广，若能包含多类时间序列任务，则有一定说服力。
  - 但缺少完整实验设置、数据集列表、baseline 配置、随机种子、统计显著性、超参敏感性等信息，无法判断实验是否充分。
- **客观与公平性**：
  - 使用 MSE 与 FLOPs 是常见且可量化指标，有利于公平比较。
  - 但仅凭摘要无法确认是否对所有方法采用相同预处理、相同训练预算与相同评价协议。
  - 因此公平性无法完全验证。

## 6. 主要结论与发现

- DeCoP 通过 IPN、DCL 和 ICM 显式建模动态多尺度依赖，能更好捕捉复杂时间变化。
- 该方法提升预训练模型在下游任务上的泛化能力。
- 在十个数据集上取得 SOTA；在 ETTh1 上相比 PatchTST，MSE 改善 3%，且仅用 37% FLOPs。
- 多尺度依赖建模思路具有可迁移潜力，可用于理解视频帧间分布关系，但论文本身聚焦时间序列。

## 7. 优点

- **问题定位清晰**：直接指出统一实例级归一化忽略 patch 特性、单尺度依赖建模不足两大缺陷。
- **方法模块化**：IPN 处理分布漂移，DCL 建模多尺度依赖，ICM 增强实例判别，分工明确。
- **效率优势**：在 ETTh1 上以更低 FLOPs 取得更优 MSE，显示一定计算效率。
- **泛化导向**：强调自监督预训练向下游任务的泛化，符合时间序列预训练的核心目标。
- **跨模态启发**：依赖建模思路可迁移到视频帧间分布关系等场景。

## 8. 不足与局限

- **正文不可得**：提供的 PDF 文本为验证页面，无法核实公式、损失函数、网络结构和完整实验。
- **算力信息缺失**：未报告 GPU 型号、数量、训练时长等，难以评估训练成本与可复现性。
- **实验细节不足**：仅知十个数据集和 ETTh1 结果，未列出全部数据集、任务类型、baseline 与消融实验。
- **对比范围有限**：摘要仅明确与 PatchTST 对比，缺少与其他 SOTA 方法的完整比较信息。
- **任务覆盖未知**：MSE 指标暗示预测任务，尚不清楚是否覆盖分类、异常检测、插补等下游任务。
- **应用限制**：方法面向时间序列，依赖多尺度 patch 间依赖假设；迁移到视频等模态仍属潜在方向，未在本文验证。
- **评审信号**：元数据中 score 为 4.0，可能反映会议评审意见，但不宜仅凭此判断论文质量。

（完）
