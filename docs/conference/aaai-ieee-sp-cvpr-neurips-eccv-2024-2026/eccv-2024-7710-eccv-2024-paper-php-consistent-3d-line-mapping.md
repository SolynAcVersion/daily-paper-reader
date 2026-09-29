---
title: Consistent 3D Line Mapping
title_zh: 一致的三维线段建图
authors: "Xulong Bai, Hainan Cui*, Shuhan Shen* ;"
date: 2024-10-01
pdf: "https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/07710.pdf"
tags: ["query:cad-spatial"]
score: 6.0
evidence: 施加二维共线约束以从多视图重建一致的三维线段
tldr: 从多视图重建三维线段及线段轨迹时，经典流程在二维到三维的支撑关系与轨迹构建中存在固有的不一致问题。该文提出迭代算法处理最佳提案选择中的不一致性，并在线段轨迹构建中施加二维共线约束以增强元素一致性，最后进行非线性优化。实验表明重建结果的一致性显著提升。其贡献在于用显式投影约束提升多视图三维重建的尺度与结构一致性，与从二维视图恢复三维几何并注入投影约束的思路高度契合。
source: ECCV-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1173, \"height\": 220, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1024, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 520, \"height\": 173, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 617, \"height\": 222, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 971, \"height\": 186, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1143, \"height\": 683, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1213, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 904, \"height\": 194, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1010, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1008, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1009, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1007, \"height\": 137, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1007, \"height\": 137, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7710-eccv-2024-paper-php/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1009, \"height\": 314, \"label\": \"Table\"}]"
motivation: 经典多视图三维线段重建在提案选择与轨迹构建中存在固有的二维到三维不一致问题。
method: 提出迭代算法处理提案选择的不一致性，并在轨迹构建中施加二维共线约束，最后做非线性优化。
result: 实验表明重建出的三维线段与轨迹一致性显著提升。
conclusion: 验证了显式投影约束对提升三维重建一致性的有效性。
---

## Abstract
"We address the problem of reconstructing 3D line segments along with line tracks from multiple views with known camera poses. The basic pipeline is first generating 3D line segment proposals for each 2D line segment, then selecting the best proposals, merging them to produce 3D line segments and line tracks, and finally performing non-linear optimization. Our key contributions are focused on exploring and alleviating the inconsistency problems in classical approaches. In the best proposal selection, we analyze the inherent inconsistency problem of support relationships from 2D to 3D determined during proposal evaluation using multiple views and propose an iterative algorithm to handle it. In line track building, we impose 2D collinearity constraints to enhance the consistency of the elements in each line track. In optimization, we introduce coplanarity constraints and jointly optimize points, lines, planes, and vanishing points, enhancing the consistency of the structure of the line map. Experimental results demonstrate that our emphasis on consistency enables our line maps to achieve state-of-the-art completeness and accuracy, while also generating longer and more robust line tracks. Code is available at https://github. com/3dv-casia/clmap."

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：论文关注在相机位姿已知的多视图条件下，重建 **3D 线段（3D line segments）** 及其 **线段轨迹（line tracks）**。相比 3D 点，3D 线段冗余更低，更适合表达弱纹理、细长结构以及人造环境中的规则结构。
- **应用价值**：3D 线段地图可用于视觉定位、表面重建、位姿精化、网格精化等任务。
- **核心问题**：经典无一对一线匹配方法通常为每个 2D 线段选取 top-K 匹配并生成多个 3D 线段提案，再选择最佳提案、聚类成轨迹并优化。但该流程存在三类不一致：
  1. **最佳提案选择不一致**：经典方法独立为每个 2D 线段选择最佳提案，导致“支撑关系”与支撑线段自身的最佳提案可能不共线。
  2. **线段轨迹构建不一致**：忽略 2D 共线约束，可能把同一图像中非共线的 2D 线段错误聚到同一轨迹。
  3. **优化结构不一致**：缺少线-面共面约束；线到面距离依赖坐标原点；不同能量项权重依赖手工设定。
- **整体含义**：论文提出一套强调一致性的 3D 线段建图系统，通过改进提案生成、最佳提案选择、轨迹构建和联合优化，提升线段地图的完整性、精度和轨迹鲁棒性。

## 2. 方法论：核心思想与关键技术

- **整体流程**：输入已定位图像和 SfM 点，依次进行 2D 线段/VP 检测与匹配、3D 线段提案生成、最佳提案选择、线段轨迹构建、点-线-面-VP 联合优化。
- **3D 线段提案生成**：
  - 对每个参考 2D 线段 \(l_r\) 与其匹配线段 \(l_m\)，使用 LIMAP 中的四类方法生成提案：Line+Line、Multiple Points、Line+Point、Line+VP。
  - 关键改进：不仅使用同时落在 \(l_r\) 和 \(l_m\) 上的**共享 3D 点**，还引入只落在其中之一上的**非共享 3D 点**，并通过重投影误差检验，以提升完整性。
- **最佳提案选择与迭代一致性增强**：
  - 经典方法按式 (1) 独立选择最佳提案，导致支撑关系不一致。
  - 论文提出迭代算法：用匹配线段在上一轮迭代中的最佳提案来评分当前提案，即
    \[
    \hat{k}^{(m)} = \arg\max_k \sum_{p\in N_i}\max_{q\in Q^p_{ij}} s(L^k_{ij}, \hat{L}^{(m-1)}_{pq})
    \]
  - 初始化使用经典式 (1)；仅分数大于阈值 \(t_s=1.5\) 的最佳提案可被其他提案看到；当最佳提案变化比例低于 \(t_c=30\%\) 时停止。
  - 定义有支撑线段的提案为有效最佳提案，仅使用有效最佳提案进入后续模块。
- **线段轨迹构建**：
  - 以有效最佳提案对应的 2D 线段为节点，top-K 匹配为边，边权为最佳提案相似度。
  - 按权重降序使用 Union-Find 合并。
  - 合并时施加 **2D 共线约束**：同一图像中的两条线段若角度差 \(>2^\circ\)、最大垂直距离 \(>2\) 像素或重叠比 \(>0\)，则避免合并。
  - 对每个轨迹用 PCA 拟合 3D 无限线，再投影端点得到鲁棒 3D 线段。
- **联合优化**：
  - 最小化能量：
    \[
    E = w_PE_P + w_LE_L + w_{PL}E_{PL} + w_{P\Pi}E_{P\Pi} + w_{L\Pi}E_{L\Pi} + w_{LVP}E_{LVP}
    \]
  - 同时优化点、线、平面和消失点，引入点-面、线-面软关联。
  - 线-面距离采用**坐标无关**方式：取初始线段 \(L\) 的中点投影到无限线 \(L_{\inf}\) 上作为固定点，而非使用世界原点最近点。
  - 自适应权重：\(w_i = E^{(0)}_L / E^{(0)}_i\)，以平衡不同单位能量项。

## 3. 实验设计

- **数据集/场景**：
  - 合成数据集：**Hypersim**，使用前 8 个场景，每场景 100 张图像。
  - 真实数据集：**Tanks and Temples** 的 train split，遵循 LIMAP 建议去除几乎无线结构的 Ignatius 场景。
- **Benchmark 与指标**：
  - 使用 LIMAP 评估框架，以 GT 点云评估 3D 线段地图。
  - 指标包括：长度召回 \(R_\tau\)、内点百分比 \(P_\tau\)、平均支撑数。
  - 额外提出一致性指标 \(CP_{\tau_a/\tau_d}\)，衡量支撑关系与支撑线段最佳提案之间的共线一致性。
- **对比方法**：
  - **L3D++**
  - **LIMAP**
  - 分别使用传统 **LSD** 检测器和学习型 **DeepLSD** 检测器。
- **主要实验类型**：
  - 线建图定量比较。
  - 最佳提案选择迭代过程分析。
  - 提案生成、最佳提案选择、轨迹构建模块消融。
  - 线到面距离方法比较。
  - 自适应权重 vs 手工权重。
  - 联合优化中各能量项消融。

## 4. 资源与算力

- 论文**未明确报告** GPU 型号、数量、训练时长或显存消耗。
- 仅报告了运行时间：在 3.4GHz 处理器上，每个 Hypersim 场景（100 张图像）平均约 **60 秒**，LIMAP 约 **51 秒**；该时间不包含特征检测与匹配。
- 因此，无法从论文中判断其训练/推理算力规模，只能确认方法比 LIMAP 略慢。

## 5. 实验数量与充分性

- **实验数量**：
  - 两个数据集：Hypersim 和 Tanks and Temples。
  - 两种线检测器：LSD 与 DeepLSD。
  - 对比两个 SOTA：L3D++ 与 LIMAP。
  - 多组消融：提案生成、最佳提案选择、轨迹构建三模块组合；迭代过程 6 个子图；线-面距离；权重策略；联合优化 6 个能量项组合。
- **充分性**：
  - 整体较充分，覆盖合成与真实数据、不同检测器、多模块消融和优化项消融。
  - 使用相同评估框架和检测器，对比相对公平。
- **局限**：
  - 数据集仍偏少，主要是室内合成与部分真实场景。
  - 未评估动态场景、极端光照、大规模户外等。
  - GT 为点云而非真实 3D 线，评估存在近似性。
  - 阈值如 \(t_s, t_c, t_a, t_p, t_o\) 为经验设定，可能影响泛化。

## 6. 主要结论与发现

- 强调一致性后，3D 线段地图在完整性和精度上达到 SOTA，并生成更长、更鲁棒的线段轨迹。
- 迭代最佳提案选择可逐步提升支撑关系一致性，减少最佳提案变化比例，同时提升长度召回和内点率。
- 2D 共线约束能避免非共线 2D 线段被错误聚入同一轨迹，显著提升轨迹一致性。
- 联合优化中，引入线-面共面约束效果显著；同时优化点、线、平面和 VP 取得最佳整体表现。
- 坐标无关的线到面距离优于经典最近点法；自适应权重优于手工权重。
- 方法还能输出点-面、线-面等额外关联，而 LIMAP 主要提供点-线、线-VP 关联。

## 7. 优点

- **问题切入清晰**：系统分析经典 3D 线建图中的三类不一致问题，并提出对应解决方案。
- **方法一致性强**：从提案选择、轨迹构建到联合优化均围绕一致性设计。
- **实用改进明确**：非共享 3D 点提升完整性；迭代选择提升支撑一致性；2D 共线约束提升轨迹质量。
- **优化设计合理**：引入共面约束、坐标无关线面距离和自适应权重，减少手工调参和坐标依赖。
- **实验较全面**：合成与真实数据、两种检测器、多组消融，且开源代码。
- **输出更丰富**：可生成点-面、线-面关联，有利于后续重建和定位任务。

## 8. 不足与局限

- **速度较慢**：迭代算法和带平面的联合优化使运行时间高于 LIMAP，不利于实时应用。
- **依赖上游质量**：需要已知相机位姿、SfM 点、线检测与匹配结果；上游误差会影响最终建图。
- **共面假设限制**：现实场景并非所有线段都满足共面关系，在自然场景或非规则结构中可能受限
