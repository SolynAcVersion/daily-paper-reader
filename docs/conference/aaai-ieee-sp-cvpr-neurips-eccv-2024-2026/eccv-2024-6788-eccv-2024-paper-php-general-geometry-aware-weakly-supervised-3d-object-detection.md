---
title: General Geometry-aware Weakly Supervised 3D Object Detection
title_zh: 通用的几何感知弱监督三维目标检测
authors: "Guowen Zhang*, Junsong Fan, Liyi Chen, Zhaoxiang Zhang, Zhen Lei, Lei Zhang ;"
date: 2024-10-01
pdf: "https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/06788.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 借助先验注入从二维框学习三维框
tldr: 针对大规模三维数据标注成本高、现有弱监督方法依赖复杂人工先验且难以泛化的问题，本文提出统一的几何感知弱监督三维目标检测框架。它从RGB图像与二维框学习三维检测器，包含先验注入等通用组件以获取几何先验。实验表明该方法可便捷迁移到新场景与类别，减少对人工先验的依赖，提升泛化性。该工作为弱监督三维检测提供了通用方案。
source: ECCV-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 748, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1243, \"height\": 665, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 897, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 519, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1225, \"height\": 440, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 890, \"height\": 677, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 885, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1014, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1142, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1264, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 727, \"height\": 200, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-6788-eccv-2024-paper-php/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 730, \"height\": 402, \"label\": \"Table\"}]"
motivation: 大规模三维数据集标注成本高，现有弱监督方法依赖复杂人工先验，难以泛化到新类别与场景。
method: 提出统一框架，从RGB图像与2D框学习三维检测器，包含先验注入模块等通用组件以获取几何先验。
result: 该方法可便捷迁移到新场景与类别，减少对人工先验的依赖，提升弱监督三维检测的泛化性。
conclusion: 几何感知先验注入为弱监督三维目标检测的泛化提供了通用方案。
---

## Abstract
"3D object detection is an indispensable component for scene understanding. However, the annotation of large-scale 3D datasets requires significant human effort. To tackle this problem, many methods adopt weakly supervised 3D object detection that estimates 3D boxes by leveraging 2D boxes and scene/class-specific priors. However, these approaches generally depend on sophisticated manual priors, which is hard to generalize to novel categories and scenes. In this paper, we are motivated to propose a general approach, which can be easily adapted to new scenes and/or classes. A unified framework is developed for learning 3D object detectors from RGB images and associated 2D boxes. In specific, we propose three general components: prior injection module to obtain general object geometric priors from LLM model, 2D space projection constraint to minimize the discrepancy between the boundaries of projected 3D boxes and their corresponding 2D boxes on the image plane, and 3D space geometry constraint to build a Point-to-Box alignment loss to further refine the pose of estimated 3D boxes. Experiments on KITTI and SUN-RGBD datasets demonstrate that our method yields surprisingly high-quality 3D bounding boxes with only 2D annotation. The source code is available at https://github.com/gwenzhang/GGA."

---

## 论文详细总结（自动生成）

# 论文总结：General Geometry-aware Weakly Supervised 3D Object Detection

## 1. 核心问题与整体含义

- **研究背景**：3D 目标检测是自动驾驶、机器人等场景理解任务的关键组件，但大规模 3D 标注成本极高。相比 3D 框，2D 框标注速度快约 3 到 16 倍，且已有成熟的大规模 2D 检测/分割模型可提供高质量 2D 框。
- **核心问题**：如何仅利用 RGB 图像及其对应的 2D 边界框，训练可泛化到新场景和新类别的 3D 目标检测器。
- **现有方法局限**：
  - 基于几何规则的方法依赖特定类别在 LiDAR 点云中的手工先验。
  - 半监督方法需要部分精确标注的 3D 场景或实例。
  - 模板/SDF 方法依赖合成数据或预训练形状模型，难以推广到新类别。
  - 这些方法通常绑定特定类别或模型结构，泛化能力不足。
- **整体含义**：论文提出统一的 **General Geometry-Aware (GGA)** 弱监督 3D 检测框架，将问题分解为 **先验注入、2D 空间投影约束、3D 空间几何约束** 三个子任务，旨在摆脱复杂人工先验，实现跨室内外场景、跨类别的通用弱监督 3D 检测。

## 2. 方法论

### 2.1 核心思想

- 给定 RGB 图像和对应点云（LiDAR 或深度相机），以 2D 框作为弱监督信号。
- 通过三类通用约束共同估计高质量 3D 伪框：
  1. **先验注入**：从大语言模型获取类别级几何比例先验。
  2. **2D 空间投影约束**：使预测 3D 框投影到图像平面后与 2D 框边界对齐。
  3. **3D 空间几何约束**：使预测 3D 框紧密包裹对应点云簇，缓解 2D 到 3D 的歧义。
- 生成的 3D 伪框再用于训练全监督 3D 检测器。

### 2.2 数据准备与基础框架

- **In-Box-Points**：利用点云-图像标定参数，将点云投影到图像平面，选取落在 2D 框内的点作为目标初始点集。
- 室内场景使用预训练 2D 实例分割网络过滤异常点；室外使用区域生长算法去噪。
- 使用 RANSAC 去除地面点；室内点云用最远点采样降至约 \(10^6\) 点。
- 初始伪框：包裹所有 In-Box-Points 的最小周长 3D 框。
- **Backbone**：
  - 室外：CenterPoint（基于体素的一阶段 anchor-free 方法）。
  - 室内：FCAF3D（稀疏 3D 卷积的 anchor-free 方法）。
- **Proposal head**：输出目标性分数、预测 3D 框和类别。预测 3D 框统一表示为：
  \[
  B_{3d}=(x,y,z,l,w,h,\sin(\alpha),\cos(\alpha))\in \mathbb{R}^8
  \]
  其中 \((x,y,z)\) 为中心，\((l,w,h)\) 为尺寸，\(\alpha\) 为偏航角。

### 2.3 边界投影损失 BPL

- 将预测 3D 框的 8 个角点投影到图像平面，计算其最小外接矩形边界 \((x_p^{min}, y_p^{min}, x_p^{max}, y_p^{max})\)。
- 最小化投影边界与 2D 框边界 \((x^{min}, y^{min}, x^{max}, y^{max})\) 的 L1 距离：
  \[
  L_{BPL}=L(x_p^{min},x^{min})+L(x_p^{max},x^{max})+L(y_p^{min},y^{min})+L(y_p^{max},y^{max})
  \]
- **室内调整**：由于相机姿态多样，投影框与 2D 框可能对齐差距大，因此将初始伪框投影得到的伪 2D 框与原始 2D 框的最小包围矩形作为新的 2D 约束。

### 2.4 语义比例损失 SRL

- 观察：网络不需要细粒度形状先验，基本比例信息足以帮助捕捉物体形状。
- 使用 GPT-4 获取类别级 BEV 宽高比先验 \(r\)。
- 对预测框，取较短边为宽、较长边为高，计算预测比例：
  \[
  \frac{\min(l,w)}{\max(l,w)}
  \]
- 用 L1 损失约束其接近先验比例 \(r\)：
  \[
  L_{SRL}=L\left(\frac{\min(l,w)}{\max(l,w)}, r\right)
  \]
- 该设计避免手工规则，便于扩展到新类别。

### 2.5 点-框对齐损失 PAL

- 目的：解决仅靠 2D 投影约束时，多个不同朝向/尺寸的 3D 框可投影到同一 2D 框的歧义问题。
- 在 BEV 平面计算每个 In-Box-Point 到预测框四条边的距离 \(d_i^1,d_i^2,d_i^3,d_i^4\)。
- **PAL1**：惩罚点超出预测框范围，即要求 3D 框覆盖前景点：
  \[
  L_{PAL1}=\sum_{i=1}^{N}\left(\sum_{j\in\{1,2\}}\phi(d_i^j-\frac{l}{2})+\sum_{k\in\{2,3\}}\phi(d_i^k-\frac{w}{2})\right)
  \]
  其中 \(\phi\) 为 ReLU。
- **PAL2**：由于单视角 RGB-D 点云通常只覆盖物体一侧，点往往集中在 BEV 边界附近，因此最小化每个点到四条边的最短距离：
  \[
  L_{PAL2}=\sum_{i=1}^{N}\min(d_i^1,d_i^2,d_i^3,d_i^4)
  \]
- 二者共同作为 3D 空间隐式监督，细化位置、旋转和尺寸。

### 2.6 网络优化

- 总损失为：
  \[
  L=\lambda_1 L_{BPL}+\lambda_2 L_{SRL}+\lambda_3(L_{PAL1}+L_{PAL2})+\lambda_4 L_{score}+\lambda_5 L_{cls}
  \]
- \(L_{score}\) 为 CenterPoint 热图回归损失或 FCAF3D 中心度损失，\(L_{cls}\) 为分类交叉熵。
- 训练后，将预测 3D 框作为伪标签，按全监督协议训练最终 3D 检测网络。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- **KITTI**：
  - 室外自动驾驶数据集。
  - 训练集 3,712 张图像，验证集 3,769 张，测试集 7,518 张。
  - 评估类别：Car、Pedestrian、Cyclist。
  - 指标：AP\(_{BEV}\)、AP\(_{3D}\)，IoU 阈值包括 0.25/0.5/0.7，主要报告 Car IoU=0.7，部分报告 AP\(_{40}\) 或 AP\(_{11}\)。
- **SUN-RGBD**：
  - 室内 RGB-D 数据集，超过 10,000 张图像。
  - 训练/验证分别 5,285 和 5,050 个点云场景。
  - 评估 10 类，指标 AP@0.25 mAP。

### 3.2 对比方法

- **单目 3D 检测**：
  - 全监督：FQNet、Deep3DBox、OFTNet、RoI-10D、MonoDIS、MonoPSR、D4LCN、MonoRun、PatchNet、PGD、DCD、MonoDTR、MonoDETR 等。
  - 弱监督：AutoSDF、WeakM3D、WeakMono3D。
- **LiDAR-based 3D 检测**：
  - 全监督：MV3D、VoxelNet、SECOND、F-PointNet、PointPillars、PointRCNN。
  - 弱监督：VS3D、AutoSDF、Lifting 等。
- **室内 3D 检测**：
  - 全监督：DSS、VoteNet、H3DNet、GroupFree、FCAF3D。
  - 半监督/弱监督：BoxPC。
- **下游检测器**：PointRCNN、PGD、MonoDETR、FCAF3D。

### 3.3 主要实验结果

- **KITTI val 单目**：MonoDETR+GGA 在 AP\(_{3D}\) 上达到 21.18/14.96/12.25（Easy/Mod./Hard），优于 WeakM3D，且部分指标超过全监督方法 MonoRun。
- **KITTI test 单目**：PGD+GGA 在 Car 上明显优于 WeakM3D、WeakMono3D，接近部分全监督方法。
- **KITTI test LiDAR BEV**：PointRCNN+GGA 在 Car 上 Easy/Mod./Hard 为 77.25/63.27/54.70，并可处理 Pedestrian、Cyclist，而多数弱监督方法仅限车辆。
- **SUN-RGBD 室内**：FCAF3D+GGA 达到 48.5 mAP，超过半监督 BoxPC 的 37.2 mAP，且优于全监督 DSS 的 42.1 mAP。
- **消融**：
  - BPL 是定位基础；单独 SRL 或 PAL 难以收敛。
  - BPL+PAL 相比仅 BPL 在 Car IoU=0.7 Easy/Hard 上提升 +18.47/+9.61。
  - BPL+SRL 相比仅 BPL 在 Easy/Hard 上提升 +34.29/+22.85。
  - 三者结合最佳，Car IoU=0.7 Easy/Mod./Hard 达 56.02/40.35/33.15。
- **语义比例敏感性**：比例 \(r\) 在 2.3 到 2.7 之间性能较稳定，2.4 最优，表明方法对比例先验具有一定鲁棒性。

## 4. 资源与算力

- 论文正文未明确说明使用的 **GPU 型号、数量、训练时长、显存规模或总算力**。
- 仅提及：
  - 使用 mmdetection3d 实现。
  - 优化器为 AdamW。
  - 室外训练 120 epochs，室内训练 12 epochs。
  - RANSAC 阈值室内 0.04、室外 0.2。
  - 损失权重 \(\lambda_{1-5}\) 在 SUN-RGBD 为 2e-3、2e-3、1e-4、1、1；KITTI 省略 \(L_{cls}\)，\(\lambda_{1-4}\) 为 0.3、0.1、0.1、5。
- 因此，无法从论文文本中评估其训练成本与可复现性所需的硬件条件。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 2 个主要数据集：KITTI、SUN-RGBD。
  - 3 类任务：单目 3D 检测、LiDAR-based 3D 检测、室内 3D 检测。
  - KITTI val、KITTI test、SUN-RGBD val 多个 benchmark。
  - 对比大量全监督与弱监督方法。
  - 消融实验：
    - 3 个损失组合共 4 组主要配置。
    - 语义比例 \(r\) 从 1.9 到 2.9 共 11 组敏感性实验。
  - 定性可视化：室外 BEV、室内 3D 框、行人伪框等。
- **充分性评价**：
  - 覆盖室内外、单目与 LiDAR、多类别，实验范围较广。
  - 消融验证了三个组件的互补性，比例敏感性分析增强了鲁棒性论证。
  - 对比方法数量多，包含全监督和弱监督基线。
- **公平性与客观性**：
  - 论文声称在相同弱监督设定下比较，并遵循常见弱监督协议。
  - 但部分指标使用 AP\(_{11}\)、AP\(_{40}\) 或不同 IoU，跨表比较需谨慎。
  - 伪标签质量评估部分依赖 KITTI 3D 真值，而论文也指出 3D 标注本身存在歧义。
  - 消融主要在 KITTI LiDAR Car 上完成，室内和其他类别的消融覆盖相对有限。
  - 未提供算力与训练成本，复现公平性信息不足。

## 6. 主要结论与发现

- 仅使用 2D 框，GGA 可以生成高质量 3D 伪框，并训练出有竞争力的 3D 检测器。
- 三个通用组件具有互补性：
  - BPL 提供 2D 投影定位约束。
  - SRL 注入语义比例先验，加速收敛并提升形状感知。
  - PAL 在 3D 空间细化框的姿态，缓解 2D-3D 歧义。
- 方法不依赖类别特定手工规则，能同时处理 Car、Pedestrian、Cyclist 以及室内 10 类物体。
- 在 KITTI 和 SUN-RGBD 上，GGA 优于多数弱监督方法，部分指标超过全监督方法。
- 预测伪框有时比人工 3D 真值更紧贴点云，说明弱监督伪标签在点云对齐意义上可能具有优势，但也反映 3D 标注存在固有歧义。
- 对远处、点云稀疏的目标，性能下降明显，是主要局限。

## 7. 优点

- **通用性强**：统一框架适用于室内外场景、多种类别和不同 backbone，不绑定特定类别或模型结构。
- **减少人工先验**：用 LLM 获取类别比例先验，替代复杂手工规则，便于扩展到新类别。
- **损失设计合理**：
  - BPL 从 2D 投影角度提供定位监督。
  - SRL 以极简比例先验补偿 2D-3D 信息差。
  - PAL 利用点云与框的几何关系，在 BEV 中隐式解耦位置、尺寸和旋转。
- **即插即用**：生成的伪标签可用于训练多种下游检测器，如 PointRCNN、PGD、MonoDETR、FCAF3D。
- **实验覆盖广**：同时验证单目、LiDAR 和室内 RGB-D 任务，包含多类物体和定性可视化。
- **消融清晰**：通过组合实验证明三个损失互补，且比例先验在一定范围内鲁棒。

## 8. 不足与局限

- **远处稀疏点云鲁棒性差**：论文明确承认，远离相机的物体点云极少，难以可靠预测旋转、位置和尺寸；未来计划从密集点云对象向稀疏点云对象迁移知识。
- **类别间性能不均衡**：
  - 行人等类别检测性能相对较低。
  - 弱监督方法多局限于车辆类别，GGA 虽扩展到多类，但非车类指标仍有
