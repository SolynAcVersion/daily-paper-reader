---
title: Differentiable Convex Polyhedra Optimization from Multi-view Images
title_zh: 基于多视图图像的可微凸多面体优化
authors: "Daxuan Ren*, Haiyi Mei, Hezi Shi, Jianmin Zheng, Jianfei Cai, Lei Yang ;"
date: 2024-10-01
pdf: "https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/01403.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 通过三平面求交实现顶点位置的可微优化
tldr: 论文针对依赖隐式场监督的方法在凸多面体表示上的局限，提出一种可微渲染凸多面体的方法。其核心是借助对偶变换计算超平面交点的非可微过程，并通过三平面求交实现顶点位置的可微优化，从而在无需三维隐式场的情况下进行梯度优化。该方法支持形状解析到紧凑网格重建等多种应用，为基于平面的几何表示提供了新标准。
source: ECCV-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1252, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1248, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1248, \"height\": 251, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1237, \"height\": 953, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1257, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 507, \"height\": 289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1236, \"height\": 347, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1250, \"height\": 364, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 420, \"height\": 272, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1243, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1251, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-1403-eccv-2024-paper-php/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1134, \"height\": 100, \"label\": \"Table\"}]"
motivation: 现有凸多面体方法依赖隐式场监督，限制了几何表示与优化的灵活性。
method: 结合对偶变换的超平面交点与三平面求交的顶点可微优化，无需三维隐式场。
result: 可在无隐式场下进行梯度优化，服务于形状解析与紧凑网格重建。
conclusion: 为凸多面体表示建立了可微优化的新标准。
---

## Abstract
"This paper presents a novel approach for the differentiable rendering of convex polyhedra, addressing the limitations of recent methods that rely on implicit field supervision. Our technique introduces a strategy that combines non-differentiable computation of hyperplane intersection through duality transform with differentiable optimization for vertex positioning with three-plane intersection, enabling gradient-based optimization without the need for 3D implicit fields. This allows for efficient shape representation across a range of applications, from shape parsing to compact mesh reconstruction. This work not only overcomes the challenges of previous approaches but also sets a new standard for representing shapes with convex polyhedra."

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本仅包含论文标题、作者、摘要与元数据（含 9 张图、3 张表），未包含正文、实验设置、数据集、对比方法和算力信息。以下总结主要依据摘要与元数据；未明确处已标注“未说明/无法确认”。

## 1. 论文核心问题与整体含义

- **论文信息**：ECCV 2024 论文《Differentiable Convex Polyhedra Optimization from Multi-view Images》（基于多视图图像的可微凸多面体优化），作者包括 Daxuan Ren、Haiyi Mei、Hezi Shi、Jianmin Zheng、Jianfei Cai、Lei Yang。
- **研究背景**：凸多面体是一种紧凑、可解释的几何表示，适合形状解析、CAD 风格建模、紧凑网格重建等任务。近年来一些方法依赖隐式场监督来优化几何，但这会限制表示与优化的灵活性。
- **核心问题**：如何从多视图图像直接、可微地优化凸多面体，而不依赖三维隐式场监督。
- **整体含义**：论文试图把“凸多面体”本身作为可优化对象，通过可微渲染/优化实现从图像到紧凑凸多面体的梯度更新，为基于平面的几何表示提供新思路。

## 2. 方法论：核心思想与关键技术

- **核心思想**：凸多面体可视为一组超平面/平面相交得到的几何体。论文结合**对偶变换**与**三平面求交**，将超平面交点计算中的非可微过程与顶点位置的可微优化解耦。
- **对偶变换的作用**：利用对偶变换处理超平面相交关系，把平面与顶点/面的组合关系转换到对偶空间，从而便于计算凸多面体的结构。
- **非可微与可微的拆分**：
  - 超平面相交、平面组合拓扑变化通常是非可微或离散的。
  - 论文通过三平面求交实现顶点位置的可微优化：每个顶点可由三个平面确定，求解三平面交点后，顶点坐标对平面参数可导。
- **算法流程（文字描述）**：
  1. 用一组平面/超平面参数化凸多面体；
  2. 通过三平面求交计算候选顶点位置；
  3. 结合对偶变换处理多面体结构与面/顶点关系；
  4. 将凸多面体渲染到多视图图像；
  5. 计算图像损失并反向传播，更新平面/顶点参数；
  6. 无需三维隐式场作为中间监督。
- **主要创新点**：在不依赖 3D 隐式场的情况下，实现凸多面体的梯度优化，并支持形状解析到紧凑网格重建等应用。

## 3. 实验设计

- **任务场景**：多视图图像输入下的凸多面体优化/重建；摘要明确提到可服务“形状解析”和“紧凑网格重建”。
- **数据集 / Benchmark**：提取文本中未给出具体数据集、benchmark 或评价指标，无法确认。
- **对比方法**：摘要仅说明对比了“依赖隐式场监督的近期方法”，但未列出具体方法名称、基线设置或对比指标。
- **实验形式**：元数据显示论文包含 9 张图、3 张表，说明可能有定性可视化、定量表格或消融结果；但提取文本未提供表格内容和实验配置，无法进一步总结。

## 4. 资源与算力

- 提取文本中未提及 GPU 型号、数量、训练时长、显存消耗或计算资源。
- 因此无法总结该论文的算力需求，也无法判断其训练/优化成本。

## 5. 实验数量与充分性

- 从元数据看，论文至少有 9 张图和 3 张表，可能覆盖主实验、可视化与消融实验。
- 但具体实验组数、数据集数量、消融维度、对比方法数量均未在提供文本中说明。
- 因此无法客观判断实验是否充分、是否公平。缺少数据集、评价指标、baseline 和消融细节，无法验证其泛化性与可重复性。

## 6. 主要结论与发现

- 可以通过对偶变换与三平面求交，实现凸多面体顶点位置的可微优化。
- 该方法无需三维隐式场监督，即可进行基于梯度的优化。
- 该表示可支持从形状解析到紧凑网格重建的多种应用。
- 论文声称其工作克服了先前依赖隐式场监督方法的挑战，并为凸多面体表示设定了新的标准。

## 7. 优点

- **表示紧凑**：直接优化凸多面体/平面集合，相比隐式场更接近显式、紧凑的网格表示。
- **无需 3D 隐式场**：减少对中间隐式监督的依赖，可能简化优化流程。
- **可微优化设计**：通过三平面求交使顶点位置可导，为平面参数优化提供梯度路径。
- **多视图驱动**：可从多视图图像进行逆渲染/重建，适合图像到几何的任务。
- **应用面较广**：摘要提到形状解析与紧凑网格重建，说明方法具备一定通用性。

## 8. 不足与局限

- **仅适用于凸多面体**：非凸、凹形或复杂拓扑物体需要分解或近似，应用范围受限。
- **离散拓扑问题**：平面数量、面片连接关系、可见性等组合结构可能非可微，优化可能依赖初始化，并面临局部最优。
- **多视图依赖**：需要足够视角覆盖；稀疏视角、遮挡或噪声图像可能影响优化稳定性。
- **实验细节缺失**：提供的文本未说明数据集、指标、baseline、消融和算力，无法验证泛化性、公平性与可重复性。
- **真实场景鲁棒性未知**：未提供真实扫描、噪声输入、非凸物体分解等失败案例分析。
- **结论强度受限**：摘要中的“新标准”等表述较宏观，但缺少正文实验证据支撑。

（完）
