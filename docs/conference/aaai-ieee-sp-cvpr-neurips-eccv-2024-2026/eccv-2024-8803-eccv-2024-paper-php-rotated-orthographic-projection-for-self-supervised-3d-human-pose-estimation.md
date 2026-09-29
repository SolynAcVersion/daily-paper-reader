---
title: Rotated Orthographic Projection for Self-Supervised 3D Human Pose Estimation
title_zh: 面向自监督三维人体姿态估计的旋转正交投影
authors: "YAO YAO, Yixuan Pan, Wenjun Shi, Dongchen Zhu, Lei Wang, Jiamao Li* ;"
date: 2024-10-01
pdf: "https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/08803.pdf"
tags: ["query:cad-spatial"]
score: 5.0
evidence: 正交投影与重投影一致性约束
tldr: 自监督三维人体姿态估计常用重投影一致性，但正交投影与透视投影之间的模型差异会造成监督与预测空间的偏移，限制性能。本文提出旋转正交投影，在正交投影前加入旋转操作以几何近似透视投影，并优化参考系。实验表明该投影缩小了投影模型差异带来的偏移，提升了自监督三维姿态估计的表现。该工作强调了投影模型一致性对2D-3D映射的重要性。
source: ECCV-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1225, \"height\": 514, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1235, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1239, \"height\": 526, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 487, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1278, \"height\": 249, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 508, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1256, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1270, \"height\": 653, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1282, \"height\": 763, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 697, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 571, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-8803-eccv-2024-paper-php/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1262, \"height\": 166, \"label\": \"Table\"}]"
motivation: 自监督三维人体姿态估计广泛使用重投影一致性，但正交投影与透视投影之间的模型差异造成监督与预测空间的偏移。
method: 提出旋转正交投影，在正交投影前加入旋转操作，以几何方式近似透视投影，并优化参考系以缓解偏移。
result: 旋转正交投影缩小了投影模型差异带来的偏移，提升了自监督三维姿态估计的性能潜力。
conclusion: 该工作揭示了投影模型一致性对2D-3D映射的重要性，为显式投影约束设计提供了启示。
---

## Abstract
"Reprojection consistency is widely used for self-supervised 3D human pose estimation. However, few efforts have been made to address the inherent limitations of reprojection consistency. Lacking camera parameters and absolute position, self-supervised methods map 3D poses to 2D using orthographic projection, whereas 2D inputs are derived from perspective projection. This discrepancy among the projection models creates an offset between the supervision and prediction spaces, limiting the performance potential. To address this problem, we propose rotated orthographic projection, which achieves a geometric approximation of the perspective projection by adding a rotation operation before the orthographic projection. Further, we optimize the reference point selection according to the human body structure and propose group rotated orthographic projection, which significantly narrows the gap between the two projection models. Meanwhile, the reprojection consistency loss fails to constrain the Z-axis reverse wrong pose in 3D space. Therefore, we introduce the joint reverse constraint to limit the range of angles between the local reference plane and the end joints, penalizing unrealistic 3D poses and clarifying the Z-axis orientation of the model. The proposed method achieves state-of-the-art (SOTA) performance on both Human3.6M and MPII-INF-3DHP datasets. Particularly, it reduces the mean error from 65.9mm to 42.9mm (34.9% improvement) over the SOTA self-supervised method on Human3.6M."

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究背景**：自监督 3D 人体姿态估计通常依赖“重投影一致性”，即让预测 3D 姿态投影回 2D 后与输入 2D 姿态一致。但自监督设定下缺少相机参数和绝对位置，因此常用**正交投影**近似**透视投影**。
- **核心矛盾**：输入 2D 姿态来自透视投影，而预测 3D 姿态通过正交投影映射到 2D，两者投影模型不一致，造成监督空间与预测空间之间存在偏移，限制性能上限。
- **第二个问题**：重投影一致性无法约束 3D 空间中的绝对朝向，当整体 Z 轴反向时，网络仍可能通过错误旋转使 2D 投影保持一致，形成不合理的 3D 姿态。
- **整体含义**：论文试图从投影模型一致性和人体结构先验两方面修正自监督重投影框架，在不使用 3D 真值、相机参数和额外推理计算的前提下提升 3D 人体姿态估计性能。

## 2. 方法论

- **总体框架**：沿用 CanonPose 的自监督多视角交叉重投影框架，包括：
  - PoseNet：从尺度、位置归一化的 2D 姿态预测 canonical 坐标系下的 3D 姿态；
  - CameraNet：预测 canonical 坐标系到各相机坐标系的旋转；
  - 多视角交叉重投影损失：将某一视角预测的 3D 姿态旋转到其他相机坐标系后投影，并与对应 2D 输入比较。
- **网络改进**：
  - PoseNet 由 MLP 替换为 SemGCN，更适合骨架输入；
  - CameraNet 保留 MLP，但将轴角表示替换为 6D 连续旋转表示，缓解轴角在 0° 或 180° 附近的不连续问题。
- **旋转正交投影 ROP**：
  - 核心思想：在正交投影前加入旋转补偿，使物体-相机连线尽量对齐光轴，从而几何近似透视投影中的透视效果。
  - 根据参考点相对图像中心的偏移计算补偿旋转。设参考点为 \(p=(x_p,y_p)\)，焦距为 \(f\)，则绕 y 轴和 x 轴的补偿角分别由参考点位置和焦距计算，构成旋转矩阵 \(R_{o\to p}\)。
  - 重投影损失变为：先对 3D 姿态施加 \(R_{o\to p}\)，再做正交投影，并与输入 2D 姿态计算 L1 一致性。
  - 焦距未知时，论文采用 \(f=\sqrt{w^2+h^2}\) 近似，其中 \(w,h\) 为图像宽高。
  - 旋转补偿仅用于训练，推理阶段不引入额外计算。
- **分组旋转正交投影 G-ROP**：
  - 动机：人体整体使用单一参考点可能对远离身体中心的末端关节补偿过度或不足。
  - 做法：根据人体结构和关节相对距离，将人体分为 7 组，如髋部、左右小腿/脚、脊柱/胸、颈/头/肩、左右前臂/手等，每组独立计算参考点和旋转补偿。
  - 效果：进一步缩小正交投影与透视投影之间的差距。
- **关节反向约束 Joint Reverse Constraint**：
  - 动机：重投影损失无法约束 Z 轴整体反向错误。
  - 做法：利用人体运动先验，限制局部参考平面与末端关节之间的角度，例如用髋-膝平面约束小腿/脚，用肩-肘平面约束前臂/手。
  - 计算三点构成平面的法向量与末端骨骼向量的夹角余弦，若角度落入不合理范围则施加惩罚。论文设置约 5° 容忍膝/肘合理过伸。
  - 该损失作为 3D 空间中的额外监督，弥补 2D 重投影监督的不足。

## 3. 实验设计

- **数据集**：
  - **Human3.6M**：大规模 3D 人体姿态基准，含图像、2D/3D 标注和相机信息。按标准协议使用 S1、S5、S6、S7、S8 训练，S9、S10 测试。
  - **MPI-INF-3DHP**：更具挑战性的姿态和视角，选择 14 个视角中的 8 个，排除大角度俯视，使用官方训练/测试设置，包括绿幕、非绿幕和户外场景。
- **评价指标**：
  - MPJPE、N-MPJPE、P-MPJPE；
  - MPI-INF-3DHP 上额外使用 PCK@150mm。
- **对比方法**：
  - 包括全监督、弱监督和自监督方法，如 SemGCN、EpipolarPose、Iqbal、PCLs、RepNet、Kundu、Chen、Yu、CanonPose、ElePose、PoseTRiplet、Ma、MHCanonNet 等。
- **主要结果**：
  - Human3.6M 上，N-MPJPE 从 CanonPose 的 65.9
