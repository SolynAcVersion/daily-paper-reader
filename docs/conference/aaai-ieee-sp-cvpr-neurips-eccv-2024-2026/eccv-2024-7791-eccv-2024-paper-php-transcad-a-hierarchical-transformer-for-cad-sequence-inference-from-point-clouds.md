---
title: "TransCAD: A Hierarchical Transformer for CAD Sequence Inference from Point Clouds"
title_zh: TransCAD：用于从点云推断CAD序列的层级Transformer
authors: "Elona Dupont*, Kseniya Cherenkova, Dimitrios Mallis, Gleb A Gusev, Anis Kacem, Djamila Aouada ;"
date: 2024-10-01
pdf: "https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/07791.pdf"
tags: ["query:cad-spatial"]
score: 6.0
evidence: 从三维点云推断CAD模型序列，属三维逆向工程
tldr: 论文针对三维逆向工程中从扫描点云恢复CAD模型的问题，提出TransCAD端到端Transformer架构，利用CAD序列的层级结构进行分层学习，并设计环优化器回归草图基元参数。在DeepCAD和Fusion360数据集上取得最优结果，同时提出CAD序列的平均精度新指标以弥补现有评测不足。该工作为从三维数据重建结构化CAD模型提供了可迁移的序列生成思路。
source: ECCV-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1242, \"height\": 384, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1258, \"height\": 282, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1030, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1228, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1103, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1253, \"height\": 199, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1258, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 637, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7791-eccv-2024-paper-php/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1142, \"height\": 187, \"label\": \"Table\"}]"
motivation: 从物理物体扫描点云恢复CAD模型是三维逆向工程的重要方向，具有广泛实用价值。
method: 提出端到端Transformer，利用CAD序列层级结构分层学习，并用环优化器回归草图基元参数。
result: 在DeepCAD与Fusion360数据集上达到最优结果，并提出CAD序列平均精度新指标。
conclusion: 为从三维数据生成结构化CAD序列提供了有效框架与更合理的评测方式。
---

## Abstract
"3D reverse engineering, in which a CAD model is inferred given a 3D scan of a physical object, is a research direction that offers many promising practical applications. This paper proposes , an end-to-end transformer-based architecture that predicts the CAD sequence from a point cloud. leverages the structure of CAD sequences by using a hierarchical learning strategy. A loop refiner is also introduced to regress sketch primitive parameters. Rigorous experimentation on the DeepCAD [?] and Fusion360 [?] datasets show that achieves state-of-the-art results. The result analysis is supported with a proposed metric for CAD sequence, the mean Average Precision of CAD Sequence, that addresses the limitations of existing metrics."

---

## 论文详细总结（自动生成）

# TransCAD 论文总结

## 1. 核心问题与整体含义
- **研究动机**：3D 逆向工程旨在从物理对象的 3D 扫描/点云中恢复 CAD 模型，具有工业制造与 CAD 软件集成价值。现有工作多聚焦 CAD 生成或补全，逆向工程关注相对不足。
- **核心问题**：如何从点云直接推断**显式、参数化、可编辑的 CAD 构建序列**，而非仅恢复 CSG、B-Rep 或隐式表示。现有方法常需后处理，或依赖预定义 latent space，难以适应真实扫描中的噪声与不规则性。
- **整体含义**：论文提出 **TransCAD**，一个端到端、单阶段、非自回归的层级 Transformer，用于从点云预测 sketch-extrusion 形式的 CAD 序列，并指出已有评测指标的不足，提出新指标 APCS。

## 2. 方法论
- **核心思想**：利用 CAD 序列天然的层级结构：CAD 模型 → sketch/extrusion 序列 → sketch 内 loop → loop 内 primitive。网络先学习高层 loop-extrusion embedding，再分别解码 loop 与 extrusion 参数，并用 loop refiner 修正量化误差。
- **CAD 表示**：
  - 每个 primitive 用 start、mid、end 三个 2D 坐标表示，共 6 维；类型不显式编码，而由点配置推断。直线 mid 点用 dummy 值。
  - loop 保持闭合，使用 8-bit 量化；extrusion 用 11 维量化参数表示。
- **网络结构**：
  - **点云编码器**：4 层 PointNet++，输入点坐标与估计法线，输出逐点特征。
  - **Loop-Extrusion Decoder**：学习常量 embedding 先自注意力，再与点云特征交叉注意力；多层堆叠后预测每个位置类型：loop、extrusion 或 end，并用交叉熵监督。
  - **Extrusion Decoder**：3 层 MLP + softmax，预测 11 维量化 extrusion 参数。
  - **Loop Decoder**：4 层多头 Transformer，学习 loop primitive 的量化参数，输出 6 维 primitive 参数概率。
  - **Loop Refiner**：4 层 MLP，输入 loop embedding 与预测参数概率，回归量化预测到未量化 GT 的 offset，提升参数精度。
- **损失函数**：总损失为类型损失、loop 参数损失、extrusion 参数损失与 refiner MSE 损失之和：  
  `Ltotal = Lρ,e + Lρ + Le + Lr`。
- **评测创新**：提出 **APCS**（mean Average Precision of CAD Sequence），基于未量化参数空间和 CSSS 相似度，对 primitive 类型匹配、参数误差、过预测/欠预测进行惩罚，弥补 ACC_cmd、ACC_param 与 CD 的局限。

## 3. 实验设计
- **数据集**：
  - **DeepCAD**：训练 140,294、验证 7,773、测试 7,036 个 CAD 模型；点云 4096 点。
  - **Fusion360**：6,794 个样本，用于跨数据集评估。
- **Benchmark / 指标**：
  - 主要指标：**APCS ↑**、**CD ↓**、**IR ↓**（无法重建的预测比例）。
  - CD 在 4096 点上计算，报告值乘以 10³。
  - 同时分析模型复杂度对 APCS 与 CD 的影响。
- **对比方法**：
  - **Retrieval baseline**：用训练好的 DeepCAD 点云编码器检索最近 latent，输出训练集 CAD 序列。
  - **DeepCAD**：按原论文设置重训。
  - **MultiCAD**：因代码不可用，直接引用原论文结果。
- **实验场景**：
  - DeepCAD 主实验与 Fusion360 跨数据集实验。
  - 消融实验：无层级结构、无 refiner、完整模型。
  - 鲁棒性实验：加入 Perlin 噪声、制造小孔洞。
  - 定性结果、失败案例与模型复杂度分析。

## 4. 资源与算力
- 文中明确提到：训练使用 **NVIDIA RTX A6000 GPU**。
- 训练设置：100 epochs，batch size 72，Adam 优化器，学习率 0.001，线性 warm-up 2000 步。
- 输入点云：4096 点；点特征维度 `dp=16`，loop
