---
title: "ArchCAD-400K: A Large-Scale CAD drawings Dataset and New Baseline for Panoptic Symbol Spotting"
title_zh: ArchCAD-400K：大规模CAD图纸数据集与全景符号检测新基线
authors: "Ruifeng Luo, Zhengjie Liu, Tianxiao Cheng, Jie Wang, Tongjie Wang, Fei Cheng, Fu Chai, Yanpeng Li, Xingguang Wei, Haomin Wang, Shenglong Ye, Wenhai Wang, Yanting Zhang, Yu Qiao, Hongjie Zhang, Xianzhong Zhao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=rAGWvnpcKe"
tags: ["query:cad-spatial"]
score: 5.0
evidence: 含自动标注引擎的大规模CAD图纸数据集
tldr: 针对建筑CAD图纸符号识别缺乏大规模高质量标注数据的问题，本文提出一种利用CAD图纸固有属性自动生成标注的数据引擎。基于该引擎构建了ArchCAD-400K数据集，包含五万余张标准化图纸的四十余万切片，规模为现有最大CAD数据集的26倍。并给出全景符号检测的新基线，推动了工程图纸理解研究。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 建筑CAD图纸符号识别重要但缺乏大规模、细粒度标注的数据集。
method: 设计利用CAD图纸固有属性自动生成标注的引擎，并据此构建大规模数据集与基线模型。
result: 数据集含413062个切片、规模为现有最大CAD数据集的26倍，并给出全景符号检测基线。
conclusion: 为CAD工程图纸理解提供了数据与基准支撑。
---

## Abstract
Recognizing symbols in architectural CAD drawings is critical for various advanced engineering applications. In this paper, we propose a novel CAD data annotation engine that leverages intrinsic attributes from systematically archived CAD drawings to automatically generate high-quality annotations, thus significantly reducing manual labeling efforts. Utilizing this engine, we construct ArchCAD-400K, a large-scale CAD dataset consisting of 413,062 chunks from 5538 highly standardized drawings, making it over 26 times larger than the largest existing CAD dataset. ArchCAD-400K boasts an extended drawing diversity and broader categories, offering line-grained annotations. Furthermore, we present a new baseline model for panoptic symbol spotting, termed Dual-Pathway Symbol Spotter (DPSS). It incorporates an adaptive fusion module to enhance primitive features with complementary image features, achieving state-of-the-art performance and enhanced robustness. Extensive experiments validate the effectiveness of DPSS, demonstrating the value of ArchCAD-400K and its potential to drive innovation in architectural design and construction.

---

## 论文详细总结（自动生成）

# ArchCAD-400K 论文总结

> 说明：提供的“PDF 提取文本”实际为 OpenReview 验证页面，未包含论文正文；以下总结主要依据标题、摘要与元数据（tldr、motivation、method、result、conclusion）整理。正文中的公式、实验细节、算力等信息无法从当前材料确认。

## 1. 核心问题与整体含义
- 背景：建筑 CAD 图纸中的符号识别对多种高级工程应用至关重要。
- 问题：该领域缺乏大规模、高质量、细粒度标注的数据集，人工标注成本高。
- 整体含义：论文提出自动标注引擎并构建 ArchCAD-400K，同时给出新基线，为 CAD 工程图纸理解提供数据与基准支撑，推动建筑设计与施工创新。
- 会议信息：据元数据，该论文为 NeurIPS 2025 Accepted。

## 2. 方法论
- 核心思想：设计一种 CAD 数据标注引擎，利用系统归档 CAD 图纸的固有属性自动生成高质量标注，显著减少人工标注。
- 数据构建：基于该引擎构建 ArchCAD-400K。摘要称其包含来自 5,538 张高度标准化图纸的 413,062 个 chunks，规模为现有最大 CAD 数据集的 26 倍以上；具有更广的图纸多样性、更广类别和细粒度标注。
- 注意：元数据 tldr 中“五万余张标准化图纸”与摘要中的 5,538 张不一致，需以正文为准。
- 基线模型：提出 Dual-Pathway Symbol Spotter (DPSS)，用于全景符号检测（panoptic symbol spotting）。
- 关键技术：DPSS 包含自适应融合模块，用互补图像特征增强 primitive features，从而提升性能和鲁棒性。
- 公式/算法流程：当前可用材料未给出具体公式、伪代码或训练流程。

## 3. 实验设计
- 数据集/场景：ArchCAD-400K，面向建筑 CAD 图纸符号识别与全景符号检测。
- Benchmark：论文以 ArchCAD-400K 为基础提出新基线 DPSS；具体评价指标、数据划分协议未在可用内容中说明。
- 对比方法：摘要仅声称达到 state-of-the-art，但未列出具体对比方法；是否跨数据集测试也未说明。

## 4. 资源与算力
- 当前材料未提及 GPU 型号、数量、训练时长、参数量或总算力规模。
- 因此无法总结算力资源，需查阅论文正文。

## 5. 实验数量与充分性
- 摘要称进行了 extensive experiments，验证 DPSS 的有效性。
- 但可用内容未给出实验组数、消融实验、数据集划分、统计显著性或公平性细节。
- 无法判断实验是否充分、客观、公平；只能确认作者声称方法有效并展示数据集价值。

## 6. 主要结论与发现
- 自动标注引擎可利用 CAD 图纸固有属性生成高质量标注，降低人工标注成本。
- ArchCAD-400K 包含 413,062 个 chunks、来自 5,538 张标准化图纸，规模为现有最大 CAD 数据集的 26 倍以上。
- DPSS 在全景符号检测上达到 SOTA，并增强鲁棒性。
- ArchCAD-400K 与 DPSS 有潜力推动建筑设计、施工和工程图纸理解创新。

## 7. 优点
- 针对 CAD 标注稀缺痛点，构建大规模数据集。
- 自动标注利用 CAD 固有属性，降低人工成本。
- 数据具有更广多样性、更广类别和细粒度标注。
- 提出 DPSS，结合图元特征与图像特征，并设计自适应融合模块。
- 同时贡献数据集与基线，便于后续研究比较。

## 8. 不足与局限
- 当前材料仅为摘要/元数据，无法核验方法细节、实验设计和算力。
- 自动标注质量依赖图纸标准化程度与固有属性，对非标准化、扫描或手绘图纸的泛化能力未知。
- 摘要未列具体对比方法、评价指标、消融实验和误差分析，实验透明度有限。
- 可能存在建筑 CAD 领域偏差，迁移到其他 CAD 或工程领域需进一步验证。
- 数据集版权
