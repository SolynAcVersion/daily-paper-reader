---
title: Leveraging 3D Geometric Priors in 2D Rotation Symmetry Detection
title_zh: 在二维旋转对称检测中利用三维几何先验
authors: "Seo, Ahyun, Cho, Minsu"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Seo_Leveraging_3D_Geometric_Priors_in_2D_Rotation_Symmetry_Detection_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 在三维预测并投影回二维保证一致性
tldr: 针对基于CNN的旋转对称检测模型受视角畸变影响、难以保证三维几何一致性的问题，本文提出在三维空间直接预测旋转中心与支撑顶点，再将其投影回二维。方法还引入顶点重建阶段以强制三维几何一致性。实验表明该方法在保持结构完整性的同时提升了旋转对称检测的几何一致性。该工作为二维对称检测引入了有效的三维几何先验。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 859, \"height\": 581, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1815, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1809, \"height\": 651, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1808, \"height\": 1236, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1818, \"height\": 1119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1811, \"height\": 1299, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 148, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 768, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 766, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-seo-leveraging-3d-geometric-priors-in-2d-rotation-symmetry-detection-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 678, \"height\": 193, \"label\": \"Table\"}]"
motivation: 旋转对称检测对结构理解很重要，但基于CNN的分割模型受视角畸变影响，难以保证三维几何一致性。
method: 提出直接在三维空间预测旋转中心与支撑顶点，再投影回二维，并加入顶点重建阶段强制三维几何一致性。
result: 该方法在保持结构完整性的同时提升了旋转对称检测的三维几何一致性。
conclusion: 引入三维几何先验并投影回二维，为二维对称检测提供了兼顾几何一致性的方案。
---

## Abstract
Symmetry plays a vital role in understanding structural patterns, aiding object recognition and scene interpretation. This paper focuses on rotation symmetry, where objects remain unchanged when rotated around a central axis, requiring detection of rotation centers and supporting vertices. Traditional methods relied on hand-crafted feature matching, while recent segmentation models based on convolutional neural networks (CNNs) detect rotation centers but struggle with 3D geometric consistency due to viewpoint distortions. To overcome this, we propose a model that directly predicts rotation centers and vertices in 3D space and projects the results back to 2D while preserving structural integrity. By incorporating a vertex reconstruction stage enforcing 3D geometric priors--such as equal side lengths and interior angles--our model enhances robustness and accuracy. Experiments on the DENDI dataset show superior performance in rotation axis detection and validate the impact of 3D priors through ablation studies.

---

## 论文详细总结（自动生成）

# 论文总结：Leveraging 3D Geometric Priors in 2D Rotation Symmetry Detection

## 1. 核心问题与整体含义（研究动机与背景）

- 对称性是理解物体结构、辅助物体识别和场景理解的重要视觉线索。本文聚焦**旋转对称检测**：物体绕中心轴旋转后保持不变，需要预测旋转中心与支撑顶点。
- 传统方法多依赖手工特征提取与匹配；近期基于 CNN 的分割模型能检测旋转中心，但往往忽略支撑顶点和对称群，并且由于视角畸变，难以保证 3D 几何一致性。
- 关键矛盾在于：真实数据集的标注常从人类感知的 3D 视角给出，而 2D 模型只能从图像特征中隐式推断 3D 语义，导致 2D 真值难以反映等边长、等内角等几何约束。
- 论文的整体含义是：将 2D 旋转对称检测提升到 3D 相机坐标中，直接预测 3D 旋转中心与顶点，再投影回 2D，并引入 3D 几何先验以提升结构一致性和鲁棒性。

## 2. 方法论：核心思想、关键技术细节与算法流程

- **核心思想**：把旋转对称检测建模为集合式检测任务，在 3D 相机坐标系中预测旋转中心、种子顶点、旋转轴和对称群，然后根据几何约束重建所有顶点，最后投影到 2D 图像平面。
- **特征学习**
  - 引入 **Camera Queries**：一组网格状可学习参数 \(Q \in \mathbb{R}^{C \times N_x \times N_y}\)，表示相机局部坐标空间中的查询。
  - 提出 **Camera Cross Attention, CCA**：对每个相机查询，沿深度轴采样多个 3D 参考点，将其投影到 2D 图像坐标，再用 deformable attention 聚合 backbone 图像特征，从而把 2D 特征编码到 3D 相机坐标。
  - Transformer encoder 使用 6 层多尺度 deformable attention 进行自注意力，并用 CCA 做交叉注意力，类似 BEVFormer 的思路。
- **检测头**
  - 每个 query 经 transformer decoder 后进入分类分支和回归分支。
  - 分类分支预测旋转对称群 \(g\)，即对称阶数 \(N\)。
  - 回归分支输出 \([c^\top, s^\top, a^\top, \beta]^\top\)：\(c\) 为 3D 旋转中心，\(s\) 为 3D 种子顶点，\(a\) 为 3D 旋转轴向量，\(\beta\) 为角度偏置。
- **顶点重建**
  - 旋转轴 \(a\) 归一化，初始径向向量为 \(r = s - c\)。
  - 对第 \(k\) 个顶点，旋转角为 \(\theta_k = 2\pi k / N\)。
  -
