---
title: "GSCV: Compressing Gaussian Splatting Sequence with Video Codec"
title_zh: GSCV：用视频编解码器压缩高斯泼溅序列
authors: "Qi Yang, Shuting Xia, Le Yang, Geert Van der Auwera, Zhu Li"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=LafrTql67m"
tags: ["query:frame-dist"]
score: 4.0
evidence: 增强高斯泼溅图间的帧间相关性以利于视频编码
tldr: 该文针对高斯泼溅序列压缩中原始PLAS排序随机性导致帧间相关性弱的问题，提出GSCV方法，引入简洁的Inter-PLAS使I帧与P帧图像更接近，从而显著提升视频编解码器的帧间性能。方法还基于高比特深度图像构建新压缩管线，兼顾更高压缩率与质量上限。实验表明其在压缩性和质量上均优于既有方案。其贡献在于压缩效率提升，与视频帧分布关系建模仅有方法层面的弱关联。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 原始PLAS的随机性导致高斯泼溅转换的2D图帧间相关性弱，影响视频编码压缩效果。
method: 提出Inter-PLAS方法，使I帧与P帧图像更接近，并基于高比特深度图像构建新压缩管线。
result: 在提升帧间编码性能的同时实现更高压缩率并提高质量上限。
conclusion: 贡献在于高斯泼溅序列的高效压缩，与帧间分布建模仅弱相关。
---

## Abstract
This paper presents a novel effective Gaussian Splatting (GS) sequence Compression method that utilizes the Video codec (GSCV). Existing video-based GS sequence compression relies on the Parallel Linear Assignment Sorting (PLAS) to convert GS into smooth 2D maps. Using the vanilla PLAS, however, can generate images exhibiting weak inter-frame correlation, due to its stochastic nature. GSCV incorporates a simple yet efficient Inter-PLAS method to produce close images between the I- and P-frames of GS, enhancing the inter-frame performance of video codec greatly. GSCV also realizes a new pipeline based on the state-of-the-art video codecs with high bit-depth GS images, achieving higher compressibility while simultaneously raising the upper limit of the quality. Experiment results show that the proposed GSCV exhibits evidently improved performance over MPEG video and point cloud-based anchors in GS sequence compression.

---

## 论文详细总结（自动生成）

> 说明：当前提供的 PDF 提取文本仅为 OpenReview 的人机验证页面，未包含论文正文。以下总结主要依据标题、作者、摘要、TLDR 与元数据生成；凡正文未提供的信息，均明确标注为“未说明/无法确认”。

## 1. 论文的核心问题与整体含义

- **论文主题**：GSCV，即“Compressing Gaussian Splatting Sequence with Video Codec”，中文可译为“用视频编解码器压缩高斯泼溅序列”。
- **研究背景**：高斯泼溅（Gaussian Splatting, GS）序列压缩中，已有基于视频的方法通常依赖 Parallel Linear Assignment Sorting（PLAS）将 GS 转换为平滑的 2D maps，再交给视频编解码器压缩。
- **核心问题**：原始 PLAS 具有随机性，导致转换得到的 2D 图像帧间相关性较弱。视频编解码器高度依赖帧间相关性，因此这种随机性会削弱 I 帧与 P 帧之间的预测效率，进而影响整体压缩性能。
- **整体含义**：论文试图通过改善 GS 到 2D 图像序列的排序/映射方式，使帧间内容更接近，从而更充分地利用视频编解码器的帧间压缩能力；同时结合高比特深度 GS 图像，提升压缩率与质量上限。

## 2. 论文提出的方法论

- **核心思想**：提出一种简单但有效的 **Inter-PLAS** 方法，替代或改进原始 PLAS，使 GS 序列转换出的 I 帧与 P 帧图像更加接近。
- **关键技术细节**：
  - 通过 Inter-PLAS 增强 GS 转换图像之间的帧间相关性，减少原始 PLAS 随机性带来的帧间不一致。
  - 让视频编解码器的帧间预测更有效，从而提升压缩效率。
  - 构建基于当前先进视频编解码器的新压缩管线，并面向高比特深度 GS 图像进行设计。
  - 高比特深度管线旨在同时提高可压缩性，并抬高重建质量的上限。
- **算法流程文字说明**：论文先对 GS 序列进行排序/映射，将其转为 2D 图像序列；其中 Inter-PLAS 用于生成相邻帧之间更一致的图像布局与内容；随后将高位深图像输入视频编解码器进行压缩。摘要未给出具体公式、伪代码或完整算法步骤。

## 3. 实验设计

- **数据集/场景**：当前可获取内容未说明具体数据集、场景类型或序列数量。
- **Benchmark / 对比基线**：摘要明确指出与 **MPEG video** 和 **point cloud-based anchors** 在 GS 序列压缩任务上进行比较。
- **对比方法**：
  - 基于 MPEG 视频编解码器的 GS 序列压缩方案。
  - 基于点云的锚点方法。
- **评价指标**：当前内容未说明具体指标，如 PSNR、LPIPS、BD-Rate、压缩率、比特率等均未提供。

## 4. 资源与算力

- 当前可获取内容中**未明确说明**使用的 GPU 型号、GPU 数量、训练/压缩时长、显存消耗或其他算力资源。
- 因此无法对算力开销、训练成本或推理成本进行总结。

## 5. 实验数量与充分性

- 当前内容未提供具体实验组数，例如不同数据集、不同场景、消融实验、跨序列泛化实验等。
- 从摘要可知，至少包含与两类基线方法的对比：MPEG video 和 point cloud-based anchors。
- 但由于缺少正文、表格和实验细节，无法判断实验是否充分、客观、公平。
- 也未见统计显著性、用户研究、失败案例分析、复杂度分析等信息，因此对实验覆盖面的评估受限。

## 6. 论文的主要结论与发现

- Inter-PLAS 能生成 I 帧与 P 帧之间更接近的 GS 图像，显著提升视频编解码器的帧间性能。
- 基于高比特深度 GS 图像的新压缩管线，可在提高压缩率的同时提升质量上限。
- 实验结果显示，GSCV 在 GS 序列压缩上明显优于 MPEG video 和 point cloud-based anchors。
- 元数据进一步指出，该论文贡献主要在于高斯泼溅序列的高效压缩，与视频帧分布关系建模仅有方法层面的弱关联。

## 7. 优点

- **问题定位明确**：直接指出原始 PLAS 随机性导致帧间相关性弱，这是视频编码压缩 GS 序列的关键瓶颈。
- **方法简洁**：Inter-PLAS 被描述为简单且高效，可能易于集成到现有 GS 到视频的压缩流程中。
- **兼容性强**：方法面向当前先进视频编解码器，并支持高比特深度 GS 图像。
- **目标平衡**：同时追求更高压缩率与更高质量上限，而非仅优化单一指标。
- **对比基线有代表性**：与 MPEG 视频方案和点云锚点方法比较，覆盖了视频编码与点云压缩两条相关路线。

## 8. 不足与局限

- **全文不可得**：提供的 PDF 文本是验证页面，无法核验方法细节、公式、实验表格与结论。
- **实验信息缺失**：未说明数据集、场景数量、评价指标、消融实验、算力消耗和复杂度。
- **泛化性未知**：Inter-PLAS 是否适用于不同 GS 序列长度、动态场景、复杂光照或大尺度场景，当前无法判断。
- **应用限制可能包括**：依赖 PLAS 类排序流程、依赖视频编解码器对高比特深度的支持，以及编解码复杂度、实时性等问题未在可获取内容中讨论。
- **元数据提示评审争议**：该论文来源标注为 ICLR-2026-Rejected-Public，评分为 4.0，说明其贡献可能未获一致认可；但这属于元数据信息，不能替代对正文的技术判断。
- **与帧分布建模关系弱**：若研究目标是视频帧分布建模，该论文贡献更偏向压缩工程与编码效率提升，而非分布建模理论。

（完）
