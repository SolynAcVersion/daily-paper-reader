---
title: "UniVDC: A Zero-Shot Unified Diffusion Framework for Consistent Video Depth Completion"
title_zh: UniVDC：面向一致性视频深度补全的零样本统一扩散框架
authors: "Yupei Zeng, Haining Guan, Yuhang Dong, Chao.Lu, wanghuanran, Guanzhong Tian"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=3P2oSzQ8Db"
tags: ["query:frame-dist"]
score: 5.0
evidence: 通过视频时空扩散获得时间稳定的深度
tldr: 动态视频的深度补全在稀疏噪声测量与结构空洞共存时，易出现尺度漂移与时间闪烁，单帧方法缺乏时间校正，而现有视频深度方法未充分利用稀疏几何。本文提出UniVDC，首个面向长程视频深度补全的零样本时空扩散框架，融合细粒度相对深度等几何先验与语义先验。实验表明该方法提升了度量一致性与时间稳定性。其贡献在于统一时空建模以缓解帧间不一致。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 动态视频深度补全存在尺度漂移与闪烁，单帧方法缺乏时间校正。
method: 提出零样本时空扩散框架，融合多源几何与语义先验。
result: 在长程视频深度补全中提升度量一致性与时间稳定性。
conclusion: 统一时空扩散有效缓解深度估计的尺度漂移与闪烁。
---

## Abstract
Recovering metrically consistent and temporally stable depth from dynamic videos remains challenging, particularly when sparse, noisy measurements coexist with structural voids, occlusion reveals, motion drift, and sensor dropouts. Under these conditions, single-frame methods lack temporal correction while existing video depth estimation approaches underutilize explicit sparse geometry, leading to scale drift and flicker. To address this, we introduce UniVDC, the first unified zero-shot spatiotemporal diffusion framework for long-range video depth completion. Our approach centers on multi-source geometric and semantic priors. We combine two geometric inputs: fine-grained relative depth with structural and edge cues from a depth estimator, and coarse metric depth obtained by inverse-distance–weighted interpolation of sparse measurements. Unlike methods that feed RGB frames directly, we extract global semantic features and inject them hierarchically into the diffusion network, yielding compact geometric inputs and scene context robust to frame-level appearance noise. A four-stage training protocol stabilizes prior fusion and calibrates the long-horizon scale. In inference, we introduce bidirectional overlapping sliding-window (BOSW) to reduce scale drift and boundary error accumulation over long sequences and alleviate occlusion in one-directional inference. Experiments show that UniVDC achieves state-of-the-art performance on multiple zero-shot video depth completion benchmarks in terms of completion accuracy, structural consistency, and temporal coherence.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页面，未包含论文正文。以下总结主要依据给出的标题、作者、摘要、TLDR、motivation、method、result、conclusion 与元数据；凡是正文未提供的信息，均明确标注为“未说明”。

## 1. 核心问题与整体含义

- **研究背景**：从动态视频中恢复同时具备**度量一致性**与**时间稳定性**的深度仍然困难。
- **核心问题**：当视频深度补全面临以下挑战时，深度估计容易失败：
  - 稀疏、噪声测量；
  - 结构空洞；
  - 遮挡区域暴露；
  - 运动漂移；
  - 传感器丢失。
- **现有方法局限**：
  - **单帧方法**缺乏时间维度校正，容易在视频序列中产生尺度漂移与闪烁；
  - **现有视频深度估计方法**未充分利用显式稀疏几何信息。
- **整体含义**：论文提出 **UniVDC**，声称是首个面向长程视频深度补全的**零样本统一时空扩散框架**，目标是在稀疏测量与结构缺失共存的动态视频中，提升度量一致性与时间稳定性。

## 2. 方法论

### 核心思想

- 使用**零样本时空扩散框架**统一建模视频深度补全中的空间结构与时间一致性。
- 不单纯依赖 RGB 帧，而是融合**多源几何先验**与**语义先验**，以缓解尺度漂移、闪烁和外观噪声。
- 面向长程视频，强调长时程尺度校准与推理阶段的稳定性。

### 关键技术细节

- **两类几何输入**：
  - 细粒度相对深度：来自深度估计器，并带有结构与边缘线索；
  - 粗度量深度：通过**反距离加权插值**对稀疏测量进行插值得到。
- **语义先验注入**：
  - 不直接输入 RGB 帧；
  - 提取全局语义特征；
  - 将语义特征**分层注入扩散网络**；
  - 目的是获得紧凑几何输入和场景上下文，增强对帧级外观噪声的鲁棒性。
- **四阶段训练协议**：
  - 用于稳定先验融合；
  - 校准长时程尺度。
- **推理策略：BOSW**：
  - 提出**双向重叠滑动窗口**；
  - 用于减少长序列中的尺度漂移和边界误差累积；
  - 缓解单向推理中的遮挡问题。

### 算法流程（文字说明）

1. 从视频与稀疏深度测量中构建输入。
2. 利用深度估计器获得细粒度相对深度及结构/边缘线索。
3. 利用反距离加权插值从稀疏测量得到粗度量深度。
4. 提取全局语义特征，并分层注入扩散网络。
5. 通过四阶段训练稳定几何先验与语义先验融合，并校准长时程尺度。
6. 推理时采用双向重叠滑动窗口 BOSW，输出长程一致深度。
7. 目标结果：同时提升补全精度、结构一致性与时间一致性。

### 缺失信息

- 提供的文本未给出具体网络结构、扩散过程公式、损失函数、训练目标、窗口大小、四阶段细节等。

## 3. 实验设计

- **数据集/场景**：摘要仅称在“多个零样本视频深度补全基准”上实验，未列出具体数据集名称、场景类型或数据规模。
- **Benchmark**：论文声称使用多个零样本视频深度补全 benchmark，但未说明具体 benchmark 名称。
- **对比方法**：未列出对比方法名称，也未说明对比方法类别。
- **评价指标**：提到从以下方面评估：
  - 补全精度；
  - 结构一致性；
  - 时间一致性。
- **主要实验结论**：论文声称 UniVDC 在多个零样本视频深度补全 benchmark 上达到**state-of-the-art**。

## 4. 资源与算力

- 提供的文本中**未说明**使用的 GPU 型号、GPU 数量、训练时长、参数量、推理成本或训练数据规模。
- 因此无法评估其算力需求、训练可复现性与计算开销。

## 5. 实验数量与充分性

- 提供的文本未说明具体实验组数。
- 未提供消融实验、数据集数量、对比方法数量、统计显著性检验等细节。
- 因此无法判断实验是否充分、客观、公平。
- 元数据记录显示：
  - `score: 5.0`；
  - `source: ICLR-2026-Rejected-Public`。
  这只能说明该论文处于公开评审来源且评分中等/被拒，不能替代对实验细节的独立评估。
- 总体而言：**实验充分性与公平性无法从当前材料判断**。

## 6. 主要结论与发现

- UniVDC 作为零样本统一时空扩散框架，可面向长程视频深度补全。
- 通过融合相对深度、稀疏度量深度与语义先验，有助于缓解尺度漂移与时间闪烁。
- 四阶段训练协议有助于稳定先验融合并校准长时程尺度。
- 推理阶段的双向重叠滑动窗口 BOSW 有助于减少长序列尺度漂移、边界误差累积和单向推理中的遮挡问题。
- 论文声称在多个零样本视频深度补全 benchmark 上取得 SOTA，提升补全精度、结构一致性和时间一致性。

## 7. 优点

- **问题设定有现实意义**：动态视频、稀疏噪声测量、结构空洞、遮挡与传感器丢失共存，是深度补全中的困难场景。
- **统一时空建模**：将空间补全与时间一致性放在同一扩散框架中处理。
- **多源先验融合**：结合细粒度相对深度、粗度量深度、结构/边缘线索与全局语义特征。
- **避免直接 RGB 输入**：通过全局语义特征注入，可能提升对外观噪声的鲁棒性。
- **长程推理设计**：BOSW 针对长序列尺度漂移、边界误差累积和遮挡问题，具有明确动机。
- **零样本定位**：若成立，可减少对特定场景训练数据的依赖，提升泛化潜力。

## 8. 不足与局限

- **正文信息严重不足**：当前提取文本未包含论文正文，无法验证方法细节、公式、网络架构、损失函数和训练策略。
- **实验细节缺失**：
  - 未列出数据集、场景、benchmark 名称；
  - 未列出对比方法；
  - 未给出定量结果、消融实验和统计显著性；
  - 无法判断实验是否充分、公平、可复现。
- **算力与效率未知**：未说明 GPU、训练时长、推理开销，难以评估实际部署成本。
- **零样本泛化风险**：零样本能力依赖预训练深度估计器与语义模型，可能存在域偏移；对稀疏测量质量、噪声水平和传感器丢失模式的敏感性未知。
- **BOSW 的代价未知**：双向重叠滑动窗口可能增加推理计算量，窗口大小与重叠比例的影响未说明。
- **应用限制**：主要面向长程动态视频深度补全，是否适用于实时系统、移动端或极端光照/天气场景尚不明确。
- **评审背景**：元数据来源为 `ICLR-2026-Rejected-Public`，评分为 `5.0`，但具体审稿意见未提供，不能据此判断具体缺陷。

（完）
