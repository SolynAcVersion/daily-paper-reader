---
title: "CADCrafter: Generating Computer-Aided Design Models from Unconstrained Images"
title_zh: CADCrafter：从无约束图像生成计算机辅助设计模型
authors: "Chen, Cheng, Wei, Jiacheng, Chen, Tianrun, Zhang, Chi, Yang, Xiaofeng, Zhang, Shangzhan, Yang, Bingchen, Foo, Chuan-Sheng, Lin, Guosheng, Huang, Qixing, Liu, Fayao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Chen_CADCrafter_Generating_Computer-Aided_Design_Models_from_Unconstrained_Images_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 7.0
evidence: 图像到参数化CAD模型生成框架
tldr: 针对从物理世界构建CAD数字孪生依赖昂贵三维扫描与繁琐后处理的问题，本文研究从自然拍摄的CAD图像逆向重建参数化模型。方法提出CADCrafter框架，仅在合成无纹理CAD数据上训练，并弥合图像与参数化CAD表示之间的鸿沟。结果可在真实图像上生成参数化CAD模型，降低了用户使用门槛。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 838, \"height\": 725, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1787, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 713, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 863, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1791, \"height\": 1204, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 858, \"height\": 364, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 858, \"height\": 310, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 785, \"height\": 958, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 832, \"height\": 584, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-chen-cadcrafter-generating-computer-aided-design-models-from-unconstrained-images-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 859, \"height\": 281, \"label\": \"Table\"}]"
motivation: 现有CAD数字孪生依赖昂贵的3D扫描与大量人工后处理，普通用户难以使用。
method: 提出图像到参数化CAD的生成框架，仅在合成无纹理CAD数据上训练以适配真实图像。
result: 可在真实世界图像上生成参数化CAD模型，缩小了图像与CAD表示的差距。
conclusion: 为面向真实图像的CAD逆向工程提供了实用方案。
---

## Abstract
Creating CAD digital twins from the physical world is crucial for manufacturing, design, and simulation. However, current methods typically rely on costly 3D scanning with labor-intensive post-processing. To provide a user-friendly design process, we explore the problem of reverse engineering from unconstrained real-world CAD images that can be easily captured by users of all experiences. However, the scarcity of real-world CAD data poses challenges in directly training such models. To tackle these challenges, we propose CADCrafter, an image-to-parametric CAD model generation framework that trains solely on synthetic textureless CAD data while testing on real-world images. To bridge the significant representation disparity between images and parametric CAD models, we introduce a geometry encoder to accurately capture diverse geometric features. Moreover, the texture-invariant properties of the geometric features can also facilitate the generalization to real-world scenarios. Since compiling CAD parameter sequences into explicit CAD models is a non-differentiable process, the network training inherently lacks explicit geometric supervision. To impose geometric validity constraints, we employ direct preference optimization (DPO) to fine-tune our model with the automatic code checker feedback on CAD sequence quality. Furthermore, we collected a real-world dataset, comprised of multi-view images and corresponding CAD command sequence pairs, to evaluate our method. Experimental results demonstrate that our approach can robustly handle real unconstrained CAD images, and even generalize to unseen general objects.

---

## 论文详细总结（自动生成）

# CADCrafter 论文中文总结

## 1. 核心问题与整体含义
- **研究动机**：从物理世界创建 CAD 数字孪生对制造、设计和仿真非常重要，但现有方法通常依赖昂贵的三维扫描与大量人工后处理。
- **核心问题**：能否直接从用户自然拍摄的、无约束的真实世界 CAD 图像中逆向生成**可编辑的参数化 CAD 命令序列**？
- **主要挑战**：
  - 图像与参数化 CAD 之间存在巨大的表示差异：图像是连续外观信息，CAD 命令是离散操作与连续参数的混合。
  - 真实 CAD 图像数据稀缺，难以直接训练；合成数据与真实图像之间存在纹理、光照、相机姿态等域差距。
  - CAD 编译过程不可微，网络训练缺少显式几何有效性监督，生成序列可能无法编译成有效 CAD 模型。
- **整体含义**：论文提出 CADCrafter，仅在合成无纹理 CAD 数据上训练，却能泛化到真实无约束图像，并输出可导入 CAD 工具编辑的参数化命令序列，降低 CAD 逆向工程门槛。

## 2. 方法论
- **核心思想**：采用“CAD 序列自编码 + 几何条件潜扩散 + 单视图蒸馏 + DPO 微调”的三阶段框架，从图像生成 CAD 命令序列。
- **CAD 命令编码**：
  - 聚焦常用 `sketch` 与 `extrusion`，`sketch` 包含 `SOL`、`L`、`A`、`R` 等命令。
  - 连续参数归一化并量化为 256 级，用 8-bit 整数表示；命令类型 one-hot，未用参数设为 -1，序列 padding 到固定长度。
  - 将命令映射到嵌入空间：命令嵌入 + 参数嵌入 + 位置嵌入。
- **阶段一：CAD 序列自编码**：
  - 训练基于 Transformer 的自编码器，将 CAD 命令序列编码为潜在向量 `z`，再解码重建。
- **阶段二：几何条件潜扩散**：
  - 从输入图像提取深度图与法线图，输入预训练 DINO-V2 编码器获得几何特征。
  - 设计 Transformer 几何编码器，融合多视图、多模态几何特征；加入可学习模态嵌入与旋转位置编码，平均输出条件向量 `f_m`。
  - 使用扩散 Transformer 在 CAD 潜空间去噪。给定 `z_t`、时间嵌入 `γ(t)` 和几何条件 `f_m`，模型直接预测原始 `z_0`。
  - 扩散损失可写为：`L_diff = ||Ω(z_t, γ(t)|f_m) - z_0||²`。
- **多视图到单视图蒸馏**：
  - 单视图存在固有歧义。论文不单独训练单视图模型，而是冻结多视图几何编码器作为参考，让单视图编码器特征 `f_s` 逼近多视图特征 `f_m`。
  - 蒸馏损失：`L_distill = 1 - cos(f_s, f_m)`，即最大化余弦相似度。
- **阶段三：基于 DPO 的 CAD 代码检查器微调**：
  - 用 CAD 编译器自动检查生成序列是否可编译，分为正样本与负样本。
  - 使用直接偏好优化 DPO 微调扩散模型，使模型更偏向可编译、几何有效的正样本，抑制无效负样本。
  - 设置 `β = 20` 控制微调模型与预训练模型的偏离程度。

## 3. 实验设计
- **数据集与场景**：
  - **训练集**：仅使用 DeepCAD 训练集，主要为 CAD 机械
