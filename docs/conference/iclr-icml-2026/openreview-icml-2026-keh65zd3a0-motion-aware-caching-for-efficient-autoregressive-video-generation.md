---
title: Motion-Aware Caching for Efficient Autoregressive Video Generation
title_zh: 面向高效自回归视频生成的运动感知缓存
authors: "Jing Xu, Yuexiao Ma, Xuzhe Zheng, XING WANG, Shiwei Liu, Chenqian Yan, Xiawu Zheng, Rongrong Ji, Fei Chao, Songwei Liu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8953e8ca2feb42a3bf42bd9e8c0cab22112721a4.pdf"
tags: ["query:frame-dist"]
score: 7.0
evidence: 利用帧间差异进行运动感知视频生成缓存
tldr: 自回归视频生成虽适合长视频合成，但顺序迭代去噪带来巨大计算负担。现有缓存复用采用粗粒度块级跳步，无法捕捉细粒度像素动态。本文提出运动感知缓存框架MotionCache，利用帧间差异区分高运动像素与静态像素，并理论上将缓存误差与残差不稳定性关联。方法在加速生成的同时抑制误差累积，为高效自回归视频生成提供了运动感知的新策略。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 自回归视频生成计算负担重，现有缓存粗粒度跳步忽略像素动态。
method: 提出运动感知缓存，利用帧间差异按像素分配去噪步数并理论关联缓存误差。
result: 在加速生成的同时抑制高运动区域的误差累积。
conclusion: 为高效自回归视频生成提供了运动感知的缓存复用策略。
---

## Abstract
Autoregressive video generation paradigms offer theoretical promise for long video synthesis, yet their practical deployment is hindered by the computational burden of sequential iterative denoising.
While cache reuse strategies can accelerate generation by skipping redundant denoising steps, existing methods rely on coarse-grained chunk-level skipping that fails to capture fine-grained pixel dynamics.
This oversight is critical: pixels with high motion require more denoising steps to prevent error accumulation, while static pixels tolerate aggressive skipping.
We formalize this insight theoretically by linking cache errors to residual instability, and propose $\textbf{MotionCache}$, a motion-aware cache framework that exploits inter-frame differences as a lightweight proxy for pixel-level motion characteristics.
MotionCache employs a coarse-to-fine strategy: an initial warm-up phase establishes semantic coherence, followed by motion-weighted cache reuse that dynamically adjusts update frequencies per token.
Extensive experiments on state-of-the-art models like SkyReels-V2 and MAGI-1 demonstrate that MotionCache achieves significant speedups of $\textbf{6.28}\times$ and $\textbf{1.64}\times$ respectively, while effectively preserving generation quality (VBench: 1%$\downarrow$ and 0.01%$\downarrow$ respectively).
The code is available at https://github.com/ywlq/MotionCache.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取内容实际为 OpenReview 的浏览器验证页，未包含论文正文；以下总结主要依据论文元数据、摘要及结构化信息。未在材料中出现的细节，将明确标注为“未说明/无法确认”。

## 1. 核心问题与整体含义

- **研究背景**：自回归视频生成范式在长视频合成上具有理论潜力，但其顺序迭代去噪过程计算负担很重，限制了实际部署。
- **核心问题**：现有缓存复用策略虽然能通过跳过冗余去噪步骤加速生成，但多采用**粗粒度、块级/chunk 级跳步**，无法捕捉细粒度像素动态。
- **关键洞察**：
  - 高运动像素需要更多去噪步骤，以避免误差累积；
  - 静态像素则可以承受更激进的跳步。
- **整体含义**：论文试图在“加速生成”与“保持质量”之间取得更好平衡，提出一种面向自回归视频生成的运动感知缓存框架 MotionCache。

## 2. 方法论

### 核心思想
- 利用**帧间差异**作为像素级运动特征的轻量代理。
- 根据运动强度动态决定不同 token/像素的缓存复用与去噪更新频率。
- 通过“粗到细”的策略，在保持语义一致性的同时实现细粒度加速。

### 关键技术细节
- **理论形式化**：论文将缓存误差与残差不稳定性关联起来，用于解释为何高运动区域不能过度跳步。
- **运动感知缓存**：
  - 高运动像素：分配更多去噪步骤，降低误差累积；
  - 静态像素：更积极地复用缓存，减少冗余计算。
- **粗到细策略**：
  - 初始 warm-up 阶段：建立语义连贯性；
  - 后续阶段：采用运动加权缓存复用，动态调整每个 token 的更新频率。

### 算法流程（文字说明）
1. 在自回归去噪过程中维护缓存；
2. 计算相邻帧差异，作为 token/像素级运动强度代理；
3. 根据运动权重决定哪些 token 需要更新、哪些可以复用缓存；
4. 对高运动 token 提高更新频率，对低运动/静态 token 降低更新频率；
5. 在预热阶段之后逐步进入细粒度运动感知缓存复用，以抑制误差累积。

## 3. 实验设计

- **任务场景**：自回归视频生成，尤其是长视频合成场景。
- **使用模型**：在 SkyReels-V2 和 MAGI-1 等先进模型上进行实验。
- **Benchmark**：主要使用 **VBench** 评估生成质量。
- **对比方法**：与现有缓存复用策略对比，特别是粗粒度块级/chunk 级跳步方法。
- **主要结果**：
  - SkyReels-V2：实现 **6.28×** 加速，VBench 下降约 **1%**；
  - MAGI-1：实现 **1.64×** 加速，VBench 下降约 **0.01%**。
- **数据集细节**：摘要未明确列出具体训练/评估数据集名称，仅说明使用 VBench 和上述模型。

## 4. 资源与算力

- 提供的摘要与元数据中**未说明**使用的 GPU 型号、数量、训练时长、推理硬件或总计算量。
- 因此无法总结具体算力开销，也无法判断训练成本与推理效率实验的硬件公平性。

## 5. 实验数量与充分性

- 从现有材料看，至少包含两个 SOTA 模型上的主实验：SkyReels-V2 与 MAGI-1。
- 使用了 VBench 作为质量评估指标，并报告了加速比与质量下降幅度。
- **但无法确认**：
  - 具体做了多少组数据集实验；
  - 是否有系统消融实验；
  - 是否比较了多种缓存基线；
  - 是否包含人工主观评估、长视频长度敏感性分析、运动强度分层分析等。
- **充分性判断**：现有信息显示主实验具有代表性，但实验覆盖细节不足，难以完全判断充分性、客观性与公平性。VBench 是常用 benchmark，但仅凭摘要中的相对下降数据，无法验证绝对分数、基线配置、随机种子和超参数公平性。

## 6. 主要结论与发现

- MotionCache 能显著加速自回归视频生成，同时较好保持生成质量。
- 运动感知的细粒度缓存策略优于粗粒度块级跳步：
  - 高运动区域通过更频繁更新抑制误差累积；
  - 静态区域通过更激进缓存复用提升效率。
- 论文认为，将缓存误差与残差不稳定性关联，为运动感知缓存提供了理论解释。
- 在 SkyReels-V2 和 MAGI-1 上分别取得 6.28× 和 1.64× 加速，VBench 仅下降 1% 和 0.01%。

## 7. 优点

- **细粒度设计**：从粗粒度块级跳步推进到 token/像素级运动感知缓存，更符合视频中运动分布不均匀的特点。
- **轻量代理**：使用帧间差异估计运动，避免引入复杂运动估计模块，具备较好实用性。
- **理论关联**：尝试将缓存误差与残差不稳定性联系起来，增强方法解释性。
- **粗到细流程**：先预热保证语义一致，再运动加权复用，兼顾稳定性与效率。
- **效果显著**：在多个先进模型上实现明显加速，且 VBench 质量下降较小。
- **开源代码**：提供代码链接，有利于复现和后续研究。

## 8. 不足与局限

- **全文不可得**：当前材料仅为验证页与摘要，无法验证方法细节、公式推导和完整实验。
- **运动代理的局限**：帧间差异可能受遮挡、光照变化、镜头运动、快速运动等影响，未必总能准确反映真实像素运动。
- **额外开销未说明**：计算帧间差异和运动加权本身可能带来开销，摘要未说明其占比。
- **评估维度有限**：主要报告 VBench 和加速比，缺少更多感知指标、主观评价、长视频一致性、时序稳定性等分析。
- **实验覆盖未知**：未说明数据集规模、视频长度、分辨率、基线数量、消融实验和超参数敏感性。
- **算力信息缺失**：未报告 GPU 型号、数量、训练/推理时长，难以评估实际部署成本。
- **应用限制**：方法面向自回归视频生成缓存，可能不直接适用于其他生成范式；在极端复杂运动场景中的鲁棒性仍需验证。

（完）
