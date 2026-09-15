---
title: "DRFusion: Drift-Resilient Temporally Consistent Infrared–Visible Video Fusion"
title_zh: DRFusion：抗漂移的时序一致红外-可见光视频融合
authors: "Xingyuan Li, HaoYuan Xu, Shulin Li, Xiang Chen, Zhiying Jiang, Jinyuan Liu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/ef42286a6094b2a342e6fcfa2c835d10a711d330.pdf"
tags: ["query:frame-dist"]
score: 6.0
evidence: 跨视频帧的时序约束与误差累积
tldr: 针对红外与可见光视频融合中时序一致性难以保持、逐帧扩散模型在自回归设置下缺乏时序约束并产生误差累积与漂移的问题，本文提出抗漂移的视频融合方法，将任务重构为历史条件下的运动生成。方法引入稳定历史引导机制，显式建模帧间依赖，抑制伪影随时间放大。实验表明该方法能有效缓解漂移并提升时序一致性，为视频帧间相关性的建模提供了思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 逐帧扩散融合模型缺乏时序约束，易产生误差累积和漂移。
method: 将融合重构为历史条件下的运动生成，并引入稳定历史引导机制。
result: 有效抑制伪影随时间放大，提升视频融合的时序一致性。
conclusion: 为建模帧间依赖和缓解时序漂移提供了可借鉴的思路。
---

## Abstract
Infrared and visible video fusion is essential for achieving comprehensive perception in dynamic scenes. However, maintaining temporal consistency remains a formidable challenge. Conventional methods relying on optical flow often suffer from geometric rigidity and ghosting artifacts. Moreover, standard diffusion-based fusion models typically operate in a frame-by-frame manner; when extended to autoregressive settings, they lack intrinsic temporal constraints and are prone to severe error accumulation and drifting, where minor artifacts amplify over time. To address these limitations, we propose a drift-resilient video fusion method that reformulates the task as history-conditioned motion generation. We introduce Stabilized History Guidance and Soft Temporal Anchoring to reframe temporal consistency as spectral filtering, implicitly aggregating motion dynamics without rigid alignment. Furthermore, our Decoupled Structure-Motion Adaptation strategy bridges pre-trained priors and structural constraints via two-stage training and latent refinement. Extensive experiments demonstrate that our method achieves state-of-the-art performance in both fusion quality and temporal stability.

---

## 论文详细总结（自动生成）

## 说明
- 提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页，未包含论文正文。
- 以下总结主要依据论文元数据与摘要；凡正文未提供之处，均标注为“未说明/无法核验”。

### 1. 核心问题与整体含义
- **研究背景**：红外与可见光视频融合用于动态场景中的综合感知，但保持时序一致性非常困难。
- **现有问题**：
  - 依赖光流的传统方法容易出现几何刚性、鬼影等伪影。
  - 基于扩散模型的融合方法通常逐帧处理；扩展到自回归视频设置后，缺乏内在时序约束，容易产生严重误差累积与漂移，微小伪影会随时间放大。
- **整体含义**：论文将视频融合重新定义为“历史条件下的运动生成”，目标是实现抗漂移、时序一致的红外-可见光视频融合。

### 2. 方法论
- **核心思想**：不依赖光流刚性对齐，而是在历史帧条件下生成当前运动/动态，从而隐式建模帧间依赖并抑制漂移。
- **关键技术**：
  - **Stabilized History Guidance（稳定历史引导）**：显式建模帧间依赖，提供稳定的历史条件，抑制伪影随时间放大。
  - **Soft Temporal Anchoring（软时序锚定）**：将时序一致性重新表述为谱滤波，在非刚性对齐条件下隐式聚合运动动态。
  - **Decoupled Structure-Motion Adaptation（解耦结构-运动自适应）**：通过两阶段训练与潜在精炼，桥接预训练先验与结构约束。
- **算法流程（据摘要概括）**：
  1. 输入历史帧/历史融合结果与当前红外-可见光帧；
  2. 以历史为条件生成当前帧的运动或动态；
  3. 通过稳定历史引导聚合历史动态，通过软时序锚定在谱域施加柔性时序约束；
  4. 采用两阶段训练：先利用预训练先验，再进行潜在精炼以注入结构约束；
  5. 输出当前融合帧，并作为后续帧的历史条件。
- **公式**：摘要未给出具体公式。

### 3. 实验设计
- **数据集/场景**：未说明。摘要仅提及“动态场景”中的红外-可见光视频融合。
- **Benchmark**：未说明。摘要仅称在融合质量与时序稳定性上达到 state-of-the-art。
- **对比方法**：未列出具体基线。摘要仅将传统光流方法和标准扩散逐帧/自回归方法作为问题背景。
- **评价指标**：未说明。摘要提到“融合质量”和“时序稳定性”，但未列出具体指标。

### 4. 资源与算力
- 未说明。
- 论文摘要与可获取元数据中未提及 GPU 型号、数量、训练时长、参数量或推理速度，因此无法总结算力开销。

### 5. 实验数量与充分性
- 摘要称进行了“Extensive experiments”，但未给出具体实验组数、数据集数量、消融实验数量或统计检验。
- 由于正文不可获取，无法判断实验是否充分、是否客观、是否公平。
- 元数据标注为 ICML-2026-Accepted，score 为 6.0，这可作为接收信号，但不能替代对实验细节的核验。

### 6. 主要结论与发现
- 所提方法能有效缓解自回归扩散融合中的误差累积与漂移。
- 在融合质量和时序稳定性上达到 state-of-the-art。
- 稳定历史引导与软时序锚定可抑制伪影随时间放大。
- 解耦结构-运动自适应能够桥接预训练先验与结构约束。
- 将时序一致性建模为谱滤波、隐式聚合运动动态，为帧间依赖建模提供了新思路。

### 7. 优点
- **问题定位清晰**：明确针对光流刚性和扩散自回归漂移两个核心痛点。
- **方法有创新性**：将融合重构为历史条件下的运动生成，并引入软时序锚定、稳定历史引导和解耦结构-运动适配。
- **避免刚性对齐**：不依赖光流，有望减少鬼影和几何刚性伪影。
- **训练策略合理**：两阶段训练与潜在精炼可兼顾预训练先验和结构约束。
- **若结果成立**：可显著提升视频融合的时序一致性和长期稳定性。

### 8. 不足与局限
- **信息不完整**：PDF 提取文本为验证页，无法核验方法公式、网络结构、训练细节和实验数据。
- **实验覆盖未知**：未说明数据集、场景类型、视频长度、帧率、对比基线和评价指标。
- **公平性无法判断**：未说明是否在相同训练预算、相同骨干网络和相同指标下对比。
- **资源开销未知**：未报告 GPU、训练时长、推理速度，难以评估实际部署可行性。
- **潜在方法局限**：
  - 历史条件自回归仍可能在极长视频中累积误差。
  - 软时序锚定的谱滤波可能带来细节模糊或锐度损失。
  - 两阶段训练可能增加复杂度与超参敏感性。
- **应用限制**：未讨论不同模态、天气、光照、运动速度下的泛化能力，也缺少失败案例分析。

（完）
