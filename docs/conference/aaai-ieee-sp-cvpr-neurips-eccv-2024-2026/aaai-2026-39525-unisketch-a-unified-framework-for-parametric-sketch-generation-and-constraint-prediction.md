---
title: "UniSketch: A Unified Framework for Parametric Sketch Generation and Constraint Prediction"
title_zh: UniSketch：参数化草图生成与约束预测的统一框架
authors: "Jing Lin, Fazhi He, Rubin Fan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39525/43486"
tags: ["query:cad-spatial"]
score: 5.0
evidence: 含几何基元与二维约束的大规模CAD草图数据集
tldr: 论文针对现有深度学习草图方法仅支持简单基元与有限约束、难以处理复杂工程任务的问题，构建了UniSketch数据集，包含约383万张草图、7类几何基元与23类二维约束，并统一表示为向量序列。基于该数据集提出统一多任务Transformer框架，同时进行参数化草图生成与约束预测。该工作为CAD草图理解与约束推理提供了大规模监督资源，对构建几何监督数据集具有参考价值。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39525/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1835, \"height\": 897, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39525/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1777, \"height\": 749, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39525/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1662, \"height\": 456, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39525/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1455, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39525/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1328, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39525/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1468, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39525/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1122, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39525/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1119, \"height\": 295, \"label\": \"Table\"}]"
motivation: 现有深度学习草图方法局限于简单基元与少量约束，难以胜任复杂真实工程任务。
method: 构建含383万草图、7类基元与23类约束的UniSketch数据集，并提出统一多任务Transformer。
result: 数据集将草图与约束统一为向量序列，支持生成与约束预测的联合建模。
conclusion: 为CAD参数化草图理解提供了大规模数据与统一建模框架。
---

## Abstract
In modern Computer-Aided Design (CAD), parametric sketches play a crucial role by capturing both the geometric structure and design intent through constraints. However, existing deep learning–based sketch methods remain restricted to simple geometric primitives and limited constraint types, hindering their application to complex real-world engineering tasks. To address this gap, we introduce the UniSketch dataset, comprising 3,836,290 sketches. It offers a comprehensive and diverse collection of 7 types of geometric primitives and 23 types of 2D constraints, all represented as unified vector sequences suitable for deep learning applications. Leveraging the UniSketch dataset, we propose a unified multi-task Transformer framework as a true foundation model for parametric sketch modeling, supporting diverse core tasks like image-to-sketch generation, constraint prediction, and unconditional sketch synthesis. Furthermore, the generated sketches can be efficiently converted to CAD-compatible formats, enabling seamless integration with industrial CAD system for re-editing and reusing. The experimental results show that UniSketch outperforms existing methods in multiple tasks, demonstrating its versatility and practical value in industrial CAD applications.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：参数化草图中同时包含几何结构与设计意图，是机械、航空航天、建筑等 CAD 建模的基础。约束（如重合、平行、相切、对称、偏移等）决定设计意图和后续可编辑性。
- **核心问题**：现有基于深度学习的草图方法多局限于简单几何基元（点、线、圆等）和少量约束类型，且通常面向单任务；真实工业草图常包含椭圆、椭圆弧、圆锥曲线等复杂基元，以及更高阶的二维约束。
- **数据瓶颈**：已有 CAD/草图数据集要么缺少约束标注，要么基元与约束类型有限，或采用不适合深度学习的表示（如 Protocol Buffers、图结构、闭环表示）。
- **整体含义**：论文试图通过大规模、统一向量序列表示的 UniSketch 数据集，以及统一多任务 Transformer 框架，推动参数化草图建模走向“基础模型”式应用，并支持与工业 CAD 系统衔接、再编辑和复用。

## 2. 方法论

- **核心思想**：把参数化草图建模统一为序列生成任务。每个草图被表示为固定长度向量序列，包含基元向量、约束向量和控制标志；模型根据图像和/或部分序列，自回归生成完整草图序列。
- **数据集构建**：
  - 基于 SketchGraphs 的 Onshape 真实用户草图，重新处理原始 JSON。
  - 过滤不支持的基元（样条、文字、图像）和涉及外部引用的约束（如 projected、pierce）。
  - 仅保留 4–16 个基元、总序列长度不超过 200 的样本。
  - 全局平移缩放后，将坐标和参数量化到 64 个等距整数 bin，范围 [0, 64)。
  - 通过哈希去重，渲染为 128×128 灰度图像，最终包含 **3,836,290** 张草图。
- **序列表示**：
  - 支持 **7 类基元**：点、线、圆、圆弧、椭圆、椭圆弧、圆锥曲线。
  - 支持 **23 类二维约束**：重合、平行、相切、相等、角度、半径、rho 等。
  - 每类向量 22 个字段，第 1 位表示向量类型，其余记录参数，未使用字段填 -1。
  - 约束向量包含选择操作与约束操作：第 15 位为基元索引，第 16 位为子组件类型，第 17 位为内部子组件索引，第 18 位为约束类型，第 19–22 位存角度、长度、方向或 rho 等。
  - 控制标志包括 `<SOSK>`、`<EOP>`、`<EOSK>`，分别表示草图开始、基元结束、草图结束。
- **网络架构**：
  - **ViT 编码器**：输入灰度草图图像，切分为 patch，线性投影并加位置嵌入，输出视觉 token 序列 Z；经线性桥接层得到 Z′ 作为解码器交叉注意力上下文。
  - **Transformer 解码器**：自回归生成目标序列。每个 token 嵌入为命令嵌入、参数嵌入和位置嵌入之和。
  - **静态门控机制**：控制解码器是否使用图像交叉注意力。门开启时为图像引导多模态生成；门关闭时退化为仅序列解码器。
  - **双输出头**：基元头和约束头分离。根据当前步 t 与 `<EOP>` 位置选择输出头：t ≤ t<EOP> 用基元头，否则用约束头。
  - **生成概率**：P(S | x) = ∏_{t=1}^T P(s_t | s_<t, x)，其中 x = Z′（图像编码开启）或 x = ∅（关闭）。
- **任务形式化**：
  - 图像到草图生成：输入 `<SOSK>` + 图像。
  - 图像引导约束预测：输入 `<SOSK>`、基元序列、`<EOP>` + 图像。
  - 无条件草图合成：仅输入 `<SOSK>`，无图像。
  - 从基元序列预测约束：输入 `<SOSK>`、基元序列、`<EOP>`，无图像。
  - 草图补全：输入 `<SOSK>` 和部分基元序列。
- **训练策略**：
  - 采用 teacher forcing。
  - 混合批训练：每个 batch 以 p=0.5 概率随机包含图像输入，避免分阶段训练导致灾难性遗忘。
  - 加权损失：对命令类型、参数值以及基元/约束向量分别加权，缓解约束 token 主导问题。

## 3. 实验设计

- **数据集与场景**：
  - 对比实验在 **Vitruvion 数据集** 上进行，将其转换为本文格式并采用 64-bin 量化，因为基线不支持复杂基元和约束。
  - 消融实验在 **UniSketch 数据集** 上进行，随机采样 1,000,000 张草图，划分为训练 900k、验证 50k、测试 50k。
  - 任务覆盖：图像到序列生成、约束预测、无条件草图合成、草图补全。
- **Benchmark 与指标**：
  - 基元建模：teacher forcing 下报告基元级精确匹配准确率；自回归下先用匈牙利匹配对齐预测与真值，再计算参数级准确率、基元级准确率、精确率、召回率、F1。
  - 约束预测：teacher forcing 下报告约束级准确率和参数级准确率；自回归下报告精确率、召回率、F1。
- **对比方法**：
  - **Vitruvion**：分别用于图像到基元生成和从基元预测约束。基元网络在 TF 和 AR 下评估，约束网络仅在 TF 下评估。
  - **SketchGraphs**：基于图神经网络，天然自回归，因此在约束预测 AR 设置下与 UniSketch 比较。
- **主要实验组**：
  - 图像到序列生成：在原始图像和噪声手绘模拟图像上比较，结果以 original/noisy 形式报告。
  - 约束预测：比较 UniSketch、Vitruvion 约束网络、SketchGraphs。
  - 无条件草图合成与草图补全：采用 top-k 采样，图 3 展示定性示例。
  - 消融研究：混合批训练、仅图像-序列、仅序列、去除双头架构等配置。

## 4. 资源与算力

- 论文正文 **未明确说明** GPU 型号、数量、训练时长、模型参数量、训练迭代次数或总计算量。
- 仅在致谢中提到数值计算在 **武汉大学超级计算中心** 的超算系统上完成。
- 因此，无法从文中评估训练成本、可复现性和碳足迹；这一点属于实验报告中的信息缺失。

## 5. 实验数量与充分性

- **实验数量**：
  - 图像到序列生成：2 种方法 × 原始/噪声图像 × TF/AR，形成多组比较。
  - 约束预测：UniSketch 与 Vitruvion、SketchGraphs 在 TF/AR 设置下比较。
  - 消融：4 种配置，考察混合批、输入模态、门控、双输出头影响。
  - 生成任务：无条件合成和草图补全有定性示例。
- **充分性**：
  - 覆盖了多任务、多基线、TF/AR 两种推理模式，并做了架构消融，整体较丰富。
  - 但无条件合成和草图补全主要依赖图 3 定性展示，正文缺少定量指标，补充材料虽有更多结果，但正文证据有限。
  - 未与近期方法如 PICASSO、DAVINCI 等进行实验比较，尽管正文在相关工作中提到它们。
- **公平性**：
  - 对比实验使用 Vitruvion 数据集，原因是基线不支持复杂基元和约束，这一处理合理。
  - 在 TF 设置下，由于不同方法解码粒度不同，论文未直接比较参数级指标，避免粒度偏差。
  - 但不同方法在表示、任务定义和训练数据上的差异仍可能影响可比性；消融实验使用抽样 1M 数据，而非完整 3.8M 数据。

## 6. 主要结论与发现

- UniSketch 数据集是当前较全面的参数化草图数据集之一，覆盖 7 类基元和 23 类二维约束，适合 Transformer 序列建模。
- UniSketch 框架在图像到序列生成上全面优于 Vitruvion：
  - TF 基元准确率约 **51.95/52.54**，优于 Vitruvion 的 **43.97/41.73**。
  - AR 参数准确率约 **73.81/74.98**，优于 Vitruvion 的 **62.92/56.51**。
- 在约束预测上优于 Vitruvion 和 SketchGraphs：
  - UniSketch TF 约束准确率 **79.02**，参数准确率 **91.42**。
  - AR 精确率/召回率/F1 为 **78.34/62.03/66.00**，SketchGraphs 为 **52.34/51.99/52.16**。
- 混合批训练优于纯图像-序列或纯序列训练，说明多模态统一参数空间有助于稳定性和泛化。
- 双输出头优于单头，说明分离基元与约束的语义和参数分布有益。
- 生成的草图可转换为 CAD 兼容格式，支持在 Onshape 等系统中再编辑和复用。

## 7. 优点

- **数据贡献突出**：构建约 383 万草图的大规模数据集，统一向量序列表示，覆盖较丰富的基元和二维约束。
- **统一建模框架**：一个 Transformer 框架支持图像到草图、约束预测、无条件合成、草图补全等多任务，减少任务专用网络。
- **静态门控设计简洁
