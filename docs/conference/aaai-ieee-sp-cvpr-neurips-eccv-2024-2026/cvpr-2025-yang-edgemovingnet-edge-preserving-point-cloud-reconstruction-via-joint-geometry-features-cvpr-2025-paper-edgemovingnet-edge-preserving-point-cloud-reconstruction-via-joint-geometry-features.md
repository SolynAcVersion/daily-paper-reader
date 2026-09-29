---
title: "EdgeMovingNet: Edge-preserving Point Cloud Reconstruction via Joint Geometry Features"
title_zh: EdgeMovingNet：基于联合几何特征的保边点云重建
authors: "Yang, Xinran, Ji, Donghao, Li, Yuanqi, Xie, Junyuan, Guo, Jie, Guo, Yanwen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yang_EdgeMovingNet_Edge-preserving_Point_Cloud_Reconstruction_via_Joint_Geometry_Features_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: CAD模型点云重建与边缘保持
tldr: 针对点云重建CAD模型时边缘采样点稀少、重建出现伪影的问题，本文提出EdgeMovingNet一体化框架。它联合回归点到边方向、点到边距离与点法向三种几何特征来估计边缘，并据此精化上采样点。实验表明该方法能让上采样点更准确地贴合模型边缘，改善边缘保持的重建质量。该工作为CAD模型的高质量逆向工程与三维表示提供了有效手段。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 856, \"height\": 251, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1778, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 263, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 867, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 182, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 855, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 866, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1591, \"height\": 2326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 837, \"height\": 661, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 826, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 860, \"height\": 281, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 851, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 854, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 843, \"height\": 169, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 865, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 859, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 858, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-edgemovingnet-edge-preserving-point-cloud-reconstruction-via-joint-geometry-features-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 903, \"height\": 281, \"label\": \"Table\"}]"
motivation: 点云重建是三维表示与逆向工程的关键环节，但采集时边缘处采样点稀少，导致CAD模型重建出现明显伪影。
method: 提出一体化框架，通过联合回归点到边方向、点到边距离和点法向三种几何特征来估计边缘，并据此精化上采样点。
result: 该方法使上采样点更准确地对齐模型边缘，改善了CAD模型的边缘保持重建效果。
conclusion: 联合几何特征回归为点云边缘保持重建提供了有效途径，有助于CAD模型的高质量逆向工程。
---

## Abstract
Point cloud reconstruction is a critical process in 3D representation and reverse engineering. When it comes to CAD models, edges are significant features that play a crucial role in characterizing the geometry of 3D shapes. However, few points are exactly sampled on edges during acquisition, resulting in apparent artifacts for the reconstruction task. Upsampling point cloud is a direct technical route, but there is a main challenge that the upsampled points may not align with the model edge accurately. To overcome this, we develop an integrated framework to estimate edges by joint regression of three geometry features--point-to-edge direction, point-to-edge distance and point normal. Benefiting these features, we implement a novel refinement process to move and produce more points which lie accurately on edges of the model, allowing for high-quality edge-preserving reconstruction. Experiments and comparisons against previous methods demonstrate our method's effectiveness and superiority.

---

## 论文详细总结（自动生成）

# EdgeMovingNet 论文总结

## 1. 核心问题与整体含义

- **研究背景**：点云重建是三维表示与逆向工程中的关键任务，尤其对于 CAD 模型，边缘是刻画几何结构的重要特征。
- **核心问题**：原始点云中很少有点恰好采样在模型边缘上，导致重建结果在边缘处出现明显伪影。直接对点云上采样虽然可以增加密度，但上采样点往往不能准确对齐模型边缘。
- **整体含义**：论文提出一种联合几何特征回归与精化流程，使生成的点能够精确落在模型边缘上，从而提升 CAD 模型等对象的保边重建质量。该工作为稀疏、无法向、可能含噪点云的边缘保持重建提供了有效技术路线。

## 2. 方法论

### 2.1 总体框架

- 采用**两阶段框架**：
  1. 使用 EdgeMovingNet 从输入点云中联合预测三种逐点几何特征：点法向、点到边方向、点到边距离。
  2. 基于预测特征设计精化过程，生成并优化位于边缘上的点，再结合基础重建方法与顶点重定位策略，实现保边网格重建。
- 输入为**无法向点云**，点云可能稀疏、含噪，且边缘处采样点稀少。

### 2.2 特征提取：EdgeMovingNet

- **输入预处理**：将点云中心归一化到原点，并缩放到单位球内。
- **三种几何特征定义**：
  - **点法向 \(n\)**：逐点表面法向。
  - **点到边方向 \(n_e\)**：从当前点到最近锐边最近点的单位方向向量。
  - **点到边距离 \(d_e\)**：当前点到最近锐边最近点的距离。
- **边缘点投影公式**：  
  \[
  c_e = c + n_e \cdot d_e
  \]
  其中 \(c\) 为原始点，\(c_e\) 为投影到最近边缘上的点。
- **网络结构**：
  - 输入为 \(N \times 3\) 点坐标。
  - 特征编码器输出 \(N \times 256\) 的逐点特征。
  - 三个解码器分别输出点法向、点到边方向、点到边距离。
  - 采用全局预测策略，而非分块处理，以适应稀疏点云和整体尖锐先验。
- **损失函数**：  
  \[
  L = L_n + L_{d_e} + \text{edgemask} \cdot (L_{n_e} + L_s + L_t)
  \]
  - \(L_n, L_{n_e}, L_{d_e}\)：分别为法向、点到边方向、点到边距离的 L1 损失。
  - **Surface loss \(L_s\)**：约束投影边缘点 \(\hat{c}_e = c + \hat{n}_e \cdot \hat{d}_e\) 位于原点所在表面上，使用点到平面距离。
  - **Tangent loss \(L_t\)**：约束边缘点切向同时垂直于点法向和点到边方向，利用边缘点集合中 \(k=5\) 个最近邻估计切向。
  - **edgemask**：仅对预测点到边距离 \(d_e \leq \delta\) 的近边点计算方向相关损失，实验中 \(\delta = 0.05\)，避免远离边缘点的方向歧义。

### 2.3 精化过程

- 从 EdgeMovingNet 获得原始边缘点集合 \(C_e\)：将预测距离小于阈值 \(\delta'\) 的近边点投影到边缘，同时保留所有原始点。
- **边缘邻域定义**：
  - 半径 \(r = 0.1\) 内；
  - 法向夹角 \(\leq \theta\)；
  - 点到边方向夹角 \(\leq \theta\)；
  - 实验中 \(\theta = 10^\circ\)。
- **离群点剔除**：邻域点数少于 3 的边缘点视为离群点并移除。
- **加密**：在边缘点与其邻域点之间取中点，作为额外边缘点，以增密边缘表示。
- **均匀化**：对全部边缘点使用最远点采样，获得数量合适且分布较均匀的边缘点。
- **位置优化**：
  \[
  \min_{\hat{c}_e'} \sum_{\hat{c}_{e_j} \in Neigh(\hat{c}_{e_i})} ((\hat{c}_e' - \hat{c}_{e_j}) \cdot \hat{n}_j)^2 + \mu \|\hat{c}_e' - \hat{c}_{e_i}\|^2
  \]
  - 利用预测法向将边缘点拉向局部表面，并有助于拉向角点。
  - 默认 \(\mu = 0.01\)。

### 2.4 保边重建

- 首先使用 Poisson 重建对原始输入点云和预测法向生成基础表面。该步骤也可替换为其他重建求解器，如 Voronoi 方法。
- 然后采用**顶点重定位策略**：将重建网格中的顶点移动到阈值 \(\delta'\) 内最近的预测边缘点 \(C_e'\)。
- 重定位不改变顶点连接关系，仅调整顶点位置，从而在保持基础网格拓扑的同时覆盖边缘，实现边缘保持重建。

## 3. 实验设计

- **数据集**：
  - 主实验基于 **ABC 数据集**：选取 13,369 个含锐边 CAD 模型，划分为 10,000 训练、2,000 验证、1,369 测试。
  - 每个模型采样 10k 点，并计算真实点到边方向和距离用于监督。
  - 泛化实验使用 **ModelNet**、**ShapeNet** 以及真实扫描点云 **AIM@SHAPE-VISIONAIR Shape Repository**。
- **Benchmark 与评价指标**：
  - 重建精度指标：Chamfer Distance、Hausdorff Distance、Normal Consistency。
  - 采样匹配指标：Precision、Recall、F-score，匹配阈值为 L2 距离小于 0.01。
- **对比方法**：
  - 传统方法：Poisson、Voronoi。
  - 学习型方法：POCO、PCP、RFEPS、GeoUDF、NKSR。
- **输入设置**：
  - 多数方法使用从 ABC 采样的 8,192 点。
  - POCO 按其预训练模型要求使用 10,000 点。
  - Poisson 和 RFEPS 需要点法向，因此提供真实法向；其他方法包括本文方法仅使用 3D 坐标。
- **鲁棒性实验**：
  - 噪声鲁棒性：加入 1% 和 2% 高斯噪声，与 Voronoi、PCP、POCO 比较。
  - 稀疏鲁棒性：在 2k 和 4k 输入点下与 POCO 进行视觉比较。
- **泛化实验**：
  - 在 ModelNet 和 ShapeNet 上直接使用预训练模型，不重新训练或修改。
  - 在真实扫描点云上测试。
- **消融实验**：
  - 去掉点到边方向与距离联合预测；
  - 去掉 surface loss；
  - 去掉 tangent loss；
  - 去掉 refinement process。

## 4. 资源与算力

- 论文明确给出训练配置：
  - 使用 **2 块 NVIDIA 2080Ti GPU**。
  - 训练 **200 epochs**，batch size 为 8。
  - 总训练时长约 **3 天**。
  - 优化器为 Adam，学习率 \(1e-4\)，\(\beta=(0.9,0.999)\)，weight decay 0.002。
  - 精化中的约束优化使用 LBFGS 求解。
- 未明确提及推理阶段的计算开销、内存占用或部署效率。

## 5. 实验数量与充分性

- 实验覆盖较广，主要包括：
  - ABC 主重建实验，对比 7 种以上方法。
  - 1% 与 2% 噪声鲁棒性实验。
  - 2k 与 4k 稀疏输入实验。
  - ModelNet 与 ShapeNet 泛化实验。
  - 真实扫描点云实验。
  - 4 项核心消融实验。
- **充分性**：
  - 从数据集、噪声、稀疏性、泛化、真实扫描和消融多个角度验证方法，整体较充分。
  - 定量指标包括 CD、HD、NC、Precision、Recall、F-score，评价较全面。
- **公平性**：
  - 作者尽量统一输入点数和训练/测试设置，但存在一定差异：
    - POCO
