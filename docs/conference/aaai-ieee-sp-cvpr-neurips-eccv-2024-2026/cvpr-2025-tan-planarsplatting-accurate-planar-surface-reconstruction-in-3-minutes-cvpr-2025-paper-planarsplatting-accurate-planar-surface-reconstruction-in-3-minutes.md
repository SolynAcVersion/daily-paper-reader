---
title: "PlanarSplatting: Accurate Planar Surface Reconstruction in 3 Minutes"
title_zh: PlanarSplatting：三分钟内实现精确平面表面重建
authors: "Tan, Bin, Yu, Rui, Shen, Yujun, Xue, Nan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Tan_PlanarSplatting_Accurate_Planar_Surface_Reconstruction_in_3_Minutes_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 从多视角图像重建三维平面表面
tldr: 针对室内场景平面表面重建依赖二维三维平面检测与匹配跟踪、流程繁琐的问题，本文提出PlanarSplatting。方法以三维平面基元为优化目标，通过平面溅射直接拟合深度与法向图，并借助CUDA实现加速。实验表明该方法可在三分钟内完成精确的平面表面重建，兼具速度与结构表达能力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1807, \"height\": 950, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1743, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 382, \"height\": 263, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1667, \"height\": 782, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 779, \"height\": 299, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 865, \"height\": 238, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1625, \"height\": 1544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 730, \"height\": 633, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1783, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1779, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tan-planarsplatting-accurate-planar-surface-reconstruction-in-3-minutes-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 861, \"height\": 247, \"label\": \"Table\"}]"
motivation: 室内平面表面重建通常依赖二维三维平面检测与匹配跟踪，流程复杂且耗时。
method: 以三维平面基元为优化对象，用平面溅射直接拟合深度与法向图并做CUDA加速。
result: 可在三分钟内完成高精度平面表面重建，省去平面检测与匹配步骤。
conclusion: 为快速结构化的室内表面重建提供了高效方案。
---

## Abstract
This paper presents PlanarSplatting, an ultra-fast and accurate surface reconstruction approach for multi-view indoor images. We take the 3D planes as the main objective due to their compactness and structural expressiveness in indoor scenes, and develop an explicit optimization framework that learns to fit the expected surface of indoor scenes by splatting the 3D planes into 2.5D depth and normal maps. As our PlanarSplatting operates directly on the 3D plane primitives, it eliminates the dependencies on 2D/3D plane detection and plane matching/tracking for planar surface reconstruction. Furthermore, with the essential merits of plane-based representation coupled with CUDA-based implementation of planar splatting functions, PlanarSplatting reconstructs an indoor scene in 3 minutes while having significantly better geometric accuracy. Thanks to our ultra-fast reconstruction speed, the largest quantitative evaluation on the ScanNet and ScanNet++ datasets over hundreds of scenes clearly demonstrated the advantages of our method. We believe that our accurate and ultrafast planar surface reconstruction method will be applied in the structured data curation for surface reconstruction in the future. The code of our CUDA implementation will be publicly available.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义
- **研究动机**：室内场景具有强结构化特征，3D 平面是描述墙面、地板、桌面等物理表面的紧凑且表达能力强的表示。传统图像级平面重建通常依赖 2D/3D 平面检测、跨视角平面匹配/跟踪、融合，流程复杂且易受平面标注稀缺限制。
- **核心问题**：如何从已标定多视角图像中，**无需平面检测、匹配、跟踪或平面标注**，直接、快速、准确地重建室内场景的 3D 平面表面。
- **整体含义**：论文提出 PlanarSplatting，将 3D
