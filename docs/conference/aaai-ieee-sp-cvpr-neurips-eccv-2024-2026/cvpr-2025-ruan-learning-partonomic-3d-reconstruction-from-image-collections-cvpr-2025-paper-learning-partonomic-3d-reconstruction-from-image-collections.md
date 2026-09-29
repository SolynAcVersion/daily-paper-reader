---
title: Learning Partonomic 3D Reconstruction from Image Collections
title_zh: 从图像集合学习部件级三维重建
authors: "Ruan, Xiaoqian, Yu, Pei, Jia, Dian, Park, Hyeonjeong, Xiong, Peixi, Tang, Wei"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ruan_Learning_Partonomic_3D_Reconstruction_from_Image_Collections_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 5.0
evidence: 从单视图图像进行三维重建与部件分解
tldr: 针对现有基于可微渲染的三维重建方法多关注整体形状、忽视部件划分的问题，本文研究从图像集合学习部件级三维重建。方法仅用二维标注，在重建整体形状的同时将形状分解为语义部件，并应对单视图中的遮挡与解空间扩张。实验表明该方法能在单视图图像上实现带部件结构的三维重建，有助于智能体与物理环境交互。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 849, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 818, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1320, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 844, \"height\": 425, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 694, \"height\": 665, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1510, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1536, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1505, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 855, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1539, \"height\": 206, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 806, \"height\": 128, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ruan-learning-partonomic-3d-reconstruction-from-image-collections-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 849, \"height\": 187, \"label\": \"Table\"}]"
motivation: 现有图像集合三维重建方法多聚焦整体形状，忽略对智能体交互重要的部件结构。
method: 仅用二维标注，从图像集合学习同时重建形状并分解为语义部件。
result: 可在单视图图像上完成带语义部件的三维重建，缓解遮挡与解空间问题。
conclusion: 为部件级三维重建与具身交互提供了方法基础。
---

## Abstract
Reconstructing the 3D shape of an object from a single-view image is a fundamental task in computer vision. Recent advances in differentiable rendering have enabled 3D reconstruction from image collections using only 2D annotations. However, these methods mainly focus on whole-object reconstruction and overlook object partonomy, which is essential for intelligent agents interacting with physical environments. This paper aims at learning partonomic 3D reconstruction from collections of images with only 2D annotations. Our goal is not only to reconstruct the shape of an object from a single-view image but also to decompose the shape into meaningful semantic parts. To handle the expanded solution space and frequent part occlusions in single-view images, we introduce a novel approach that represents, parses, and learns the structural compositionality of 3D objects. This approach comprises: (1) a compact and expressive compositional representation of object geometry, achieved through disentangled modeling of large shape variations, constituent parts, and detailed part deformations as multi-granularity neural fields; (2) a part transformer that recovers precise partonomic geometry and handles occlusions, through effective part-to-pixel grounding and part-to-part relational modeling; and (3) a 2D-supervised learning method that jointly learns the compositional representation and part transformer, by bridging object shape and parts, image synthesis, and differentiable rendering. Extensive experiments on ShapeNetPart, PartNet, and CUB-200-2011 demonstrate the effectiveness of our approach on both overall and partonomic reconstruction. Code, models, and data are avaliable at https://github.com/XiaoqianRuan1/Partonomic_Reconstruction.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：单视图图像三维重建是计算机视觉基础任务，现有基于可微渲染的方法可从图像集合中仅用二维标注学习整体物体重建，但通常忽略物体的**部件结构（partonomy）**。
- **部件级理解的重要性**：智能体与物理世界交互时，往往需要理解物体的语义部件及其功能，例如椅子的座面用于坐、桌子的顶部用于放置物品。
- **核心问题**：本文研究**仅使用二维物体/部件掩码标注**，从图像集合中学习“部件级三维重建”：既要重建物体整体形状，又要将形状分解为有语义的部件。
- **主要挑战**：
  - 部件分解使解空间进一步扩大；
  - 单视图输入中部件频繁遮挡，视觉信息不足且歧义强；
  - 训练时没有任何三维形状、位姿、多视图或深度监督。
- **整体含义**：该任务对机器人、具身智能、AR/VR、三维打印等应用具有潜在价值，论文尝试为“从二维监督学习部件级三维结构”提供可行方案。

## 2. 方法论

### 2.1 核心思想

- 提出一种利用物体**部分—整体结构组合性**的框架，包含三部分：
  1. 紧凑且表达能力强的组合式三维表示；
  2. 基于 Part Transformer 的鲁棒解析；
  3. 仅用二维监督的端到端学习。
- 总体流程：输入单视图图像 → 推断物体位姿、整体形状、部件潜变量和纹理 → 通过可微渲染生成图像、物体掩码、部件掩码 → 与二维真值比较并优化。

### 2.2 组合式三维物体表示

- 将物体几何表示为：
  - **条件形状模板 CST**：建模大尺度形状变化与组成部件；
  - **部件变形场 PDFs**：建模每个部件的细节变形。
- **CST**：
  - 输入固定球面网格顶点 \(u_i\) 和物体潜变量 \(h_{obj}\)；
  - 通过 MLP 输出粗物体形状顶点 \(\bar v_i\) 以及每个顶点对各部件的软分配 \(\bar w_i \in [0,1]^K\)。
- **PDFs**：
  - 先对 CST 网格进行细分上采样，得到更精细顶点 \(\hat v_i\) 和部件分配 \(\hat w_i\)；
  - 再对每个顶点做变形：
    \[
    v_i = \hat v_i + \sum_k \hat w_{i,k} \, \text{MLP}(\hat v_i, h_{part_k}; \Theta_{pdf_k})
    \]
  - 即每个顶点的变形由所有部件变形场预测的偏移加权组合得到。
- **设计动机**：CST 负责大变化和部件组成，PDFs 负责细节变形，从而解耦组合复杂度，使表示既紧凑又表达力强。

### 2.3 Part Transformer

- 输入图像经卷积骨干网络得到特征图 \(F_{img}\)，同时使用 \(K\) 个可学习部件 token \(Q_{part}\)。
- **PDFs 解码器**：
  - 通过**交叉注意力**，让部件 token 从图像特征中聚集与自身相关的像素级信息，实现 part-to-pixel grounding；
  - 通过**自注意力**，建模部件 token 之间的关系，实现 part-to-part relational modeling，以应对遮挡。
- 另有姿态解码器、纹理解码器、CST 解码器，分别推断位姿、纹理、整体形状潜变量。
- 使用多头注意力、残差连接、层归一化和 dropout。

### 2.4 二维监督学习

- 使用可微渲染器将预测的位姿、形状、部件和纹理渲染为：
  - 图像 \(I'\)；
  - 物体掩码 \(M'\)；
  - 部件掩码 \(P'\)。
- 总损失：
  \[
  L = L_{rgb} + \lambda_{obj} L_{obj} + \lambda_{part} L_{part} + \lambda_{reg} L_{reg}
  \]
  - \(L_{rgb}\)：渲染图像与输入图像的 MSE；
  - \(L_{obj}\)：物体掩码 IoU 损失；
  - \(L_{part}\)：部件掩码逐像素多类交叉熵；
  - \(L_{reg}\)：平滑性与一致性正则。
- 整个组合表示和 Part Transformer 端到端训练，仅依赖二维物体/部件掩码。

### 2.5 实现细节

- 按物体类别分别训练模型。
- 初始球面网格：162 顶点、320 面；上采样后：642 顶点、1280 面。
- 输入图像和部件掩码分辨率：64×64。
- 骨干网络：U-Net，4 层编码器、4 层解码器。
- 损失权重：物体掩码 0.1，部件掩码 0.1，正则项 1。
- 纹理图分辨率 32×32，并上采样到 64×64。
- 优化器：Adam，学习率 \(1\times 10^{-4}\)。

## 3. 实验设计

### 3.1 数据集与场景

- **ShapeNetPart**：
  - 16,881 个三维形状，16 类，每实例 2–5 个部件标签；
  - 实验选用 5 类：airplane、car、chair、lamp、table；
  - 使用官方训练/测试划分。
- **PartNet**：
  - 26,671 个三维模型，24 类，具有细粒度层级部件标注；
  - 实验选用 5 类：bottle、bowl、display、knife、mug；
  - 使用最粗层级部件。
- **CUB-200-2011**：
  - 11,788 张鸟类图像，200 个子类；
  - 使用前 70 类进行训练，因这些类有二维部件标注；
  - 主要用于真实图像上的定性评估，包括已见和未见物种。

### 3.2 评价指标

- **Chamfer-L1 距离**：评估整体形状重建。
- **Part Chamfer-L1 距离**：按部件计算 Chamfer-L1 后取平均，评估部件级几何。
- **Part Classification Accuracy**：三维顶点部件分类正确率。
- **Part mIoU**：部件分割平均 IoU。
- 评估前使用带各向异性缩放的 ICP 变体将预测形状与真值对齐。

### 3.3 对比方法

- 由于没有完全相同的先前工作，作者将两个最先进的整体物体重建方法扩展为部件级版本：
  - **Unicorn\***：在 Unicorn 基础上建模每个网格顶点的部件类别，并加入部件渲染损失；
  - **AST\***：在 AST 基础上做同样扩展。
- 对比方法均使用相同二维监督设置。

### 3.4 消融与附加实验

- 组件消融：Base Model、+Deform、Ours。
- 不同掩码监督：None、Object、Object & Part。
- 网格细分影响。
- 可见区域与不可见区域的重建精度比较。
- CUB-200-2011 上的定性泛化结果。

## 4. 资源与算力

- 论文正文**未明确说明**使用的 GPU 型号、GPU 数量、训练总时长、参数量或能耗等算力细节。
- 仅提到 Adam 优化器、学习率 \(1\times 10^{-4}\)，以及按类别训练。
- 致谢中提到部分工作受 NSF 资助、NAIRR Pilot 和通过 CloudBank 提供的 AWS 云资源支持，但未给出具体计算资源规模。
- 因此，无法从论文中评估训练成本、可复现性和计算效率。

## 5. 实验数量与充分性

- **主实验**：
  - ShapeNetPart 上定量比较整体与部件重建；
  - PartNet 上定量比较整体与部件重建；
  - CUB-200-2011 上定性展示真实图像部件级重建。
- **消融实验**：
  - 组合表示与 Part Transformer 组件消融；
  - 不同二维掩码监督强度；
  - 网格细分；
  - 可见/不可见区域重建误差。
- **表格数量**：正文包含 7 个主要表格，另有定性图和多组可视化。
- **充分性**：
  - 覆盖两个三维部件数据集和一个真实图像数据集；
  - 指标包括整体形状、部件几何、部件分类和分割；
  - 对比了扩展后的 S
