---
title: "PMNI: Pose-free Multi-view Normal Integration for Reflective and Textureless Surface Reconstruction"
title_zh: PMNI：面向反光与无纹理表面重建的免位姿多视图法向积分
authors: "Pei, Mingzhi, Cao, Xu, Wang, Xiangyi, Guo, Heng, Ma, Zhanyu"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Pei_PMNI_Pose-free_Multi-view_Normal_Integration_for_Reflective_and_Textureless_Surface_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 在SDF优化中引入表面法向的几何约束
tldr: 论文针对反光与无纹理表面在多视图三维重建中相机标定与形状恢复易失败的问题，提出PMNI方法，使用表面法向图替代RGB图像以引入丰富几何信息。该方法在神经有符号距离函数优化框架内施加法向几何约束与多视图形状一致性，同时恢复精确相机位姿与高保真表面几何。该工作说明显式几何约束有助于提升重建的尺度与结构一致性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 874, \"height\": 862, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 744, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 861, \"height\": 1137, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 842, \"height\": 807, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1803, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1818, \"height\": 461, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1796, \"height\": 670, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 867, \"height\": 307, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 867, \"height\": 643, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-pei-pmni-pose-free-multi-view-normal-integration-for-reflective-and-textureless-surface-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 862, \"height\": 298, \"label\": \"Table\"}]"
motivation: 反光与无纹理表面缺乏可靠跨视图视觉特征，导致相机标定与形状重建常常失败。
method: 以表面法向图替代RGB，在神经SDF优化中施加法向约束与多视图形状一致性。
result: 可同时恢复精确相机位姿与高保真表面几何，在合成与真实数据上验证有效。
conclusion: 表明显式几何约束可提升多视图重建的结构与尺度一致性。
---

## Abstract
Reflective and textureless surfaces remain a challenge in multi-view 3D reconstruction. Both camera pose calibration and shape reconstruction often fail due to insufficient or unreliable cross-view visual features. To address these issues, we present PMNI (Pose-free Multi-view Normal Integration), a neural surface reconstruction method that incorporates rich geometric information by leveraging surface normal maps instead of RGB images. By enforcing geometric constraints from surface normals and multi-view shape consistency within a neural signed distance function (SDF) optimization framework, PMNI simultaneously recovers accurate camera poses and high-fidelity surface geometry. Experimental results on synthetic and real-world datasets show that our method achieves state-of-the-art performance in the reconstruction of reflective surfaces, even without reliable initial camera poses.

---

## 论文详细总结（自动生成）

# PMNI 论文中文总结

## 1. 核心问题与整体含义
- **研究背景**：反光与无纹理表面在多视图三维重建中非常困难。RGB 图像中跨视图视觉特征不足或不可靠，导致相机位姿标定和形状恢复容易失败。
- **核心矛盾
