---
title: Aligning Cross-View Visual Geometries in LVLMs Through Human-Like Reasoning Learning
title_zh: 通过类人推理学习对齐LVLM中的跨视图视觉几何
authors: "Yuming Qiao, Liang Luo, Dan Meng, Yifan Yang, Qingyuan Wang, Juntuo Wang, Yuwei Zhang, Ru Zhen, Yanhao Zhang, Haonan Lu, Xudong Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39011/42973"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 大模型中的跨视图空间推理
tldr: 现有工作多在单一坐标系内增强大视觉语言模型的空间理解，难以应对需要一致跨视图推理的真实任务。本文提出CVVG-Reasoner，通过模仿人类跨视图推理机制，将单帧空间理解提升为统一的跨视图空间理解。方法还构建了可扩展的跨视图空间推理数据生成流程MV3DSR。实验表明该框架显著改善了跨视图视觉几何对齐能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39011/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1676, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39011/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1629, \"height\": 859, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39011/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 678, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39011/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39011/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1734, \"height\": 679, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39011/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1844, \"height\": 816, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39011/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1835, \"height\": 551, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39011/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 248, \"label\": \"Table\"}]"
motivation: 现有模型局限于单帧坐标系空间理解，难以进行跨视图一致推理。
method: 模仿人类跨视图推理机制，并构建可扩展的跨视图空间推理数据生成流程。
result: 显著提升模型跨视图视觉几何对齐与空间理解能力。
conclusion: 推动大视觉语言模型的统一跨视图空间推理。
---

## Abstract
Spatial understanding is a critical capability for LVLMs (Large Vision-Language Models) to advance embodied AI applications. Existing works primarily focus on enhancing spatial understanding within a single frame, i.e., injecting 3D spatial concepts into LVLMs under single coordinate system. However, such improvements struggle in real-world tasks that require consistent cross-view spatial reasoning. In this paper, we propose CVVG-Reasoner(Cross-View Visual Geometries) that lifts single-frame spatial comprehension to unified cross-view spatial understanding by mimicking human-like cross-view reasoning mechanisms. First, we introduce MV3DSR(Multi-View 3D Spatial Reasoning), a scalable pipeline for cross-view spatial reasoning data generation, and construct MV3DSR-Dataset, a large-scale dataset with diverse 3D cross-view reasoning tasks. Based on MV3DSR, we propose MV3DSR-Bench, a comprehensive benchmark for evaluating cross-view spatial reasoning capabilities. Second, we design a three-stage training strategy: the first two stages progressively equip the model with (1) fundamental spatial knowledge and (2) human-like cross-view reasoning patterns, while the final stage employs reinforcement learning to further boost its performance. Extensive experiments demonstrate that our CVVG-Reasoner significantly outperforms existing 3D LLMs(Large Language Models) and advanced LVLMs in cross-view tasks while maintaining robust performance on out-of-domain data. Ablations further reveal that injecting human-like reasoning patterns yields 44% performance gain, validating the effectiveness of our design.

---

## 论文详细总结（自动生成）

# 论文总结：Aligning Cross-View Visual Geometries in LVLMs Through Human-Like Reasoning Learning

## 1. 核心问题与整体含义
- **研究背景**：LVLM 在 2D 图像理解上进展迅速，但在导航、机器人等真实交互场景中，需要跨视角、跨坐标系的稳定空间推理能力。
- **核心问题**：现有工作多聚焦于**单帧、单相机坐标系**下的 3D 空间理解，通过注入 3D 概念提升空间能力；但这类方法难以处理需要一致跨视图几何对齐的任务。
- **整体含义**：论文试图将 LVLM 的“单帧空间理解”提升为“统一跨视图空间理解”，通过模仿人类跨视图推理机制，增强模型在多视角场景中的几何推理能力。
- **主要贡献**：
  - 提出可扩展的跨视图空间推理数据生成管线 **MV3DSR**，并构建 **MV3DSR-Dataset**。
  - 提出综合基准 **MV3DSR-Bench**。
  - 提出 **CVVG-Reasoner**，采用三阶段训练策略，使模型具备类人跨视图几何推理能力。

## 2. 方法论
- **核心思想**：受人类认知启发，将跨视图几何思考分解为：
  - **低层思维**：在单视图内提取基础 3D 空间信息，如方向、距离、物体属性。
  - **高层思维**：跨视图匹配共现物体，建立参考点，推断旋转与平移，并进一步预测运动轨迹和视角变化。
- **MV3DSR 数据生成管线**：
  - **2D 标注**：RAM 做物体标签，Grounding DINO + SAM 生成边界框和实例掩码。
  - **3D 标注**：VGGT 估计逐帧相机外参、内参和 3D 点云；UniDepth 将相对深度转换为度量尺度。
  - **2D-3D 对齐**：将 3D 点投影到两个相机坐标系，按可见点 IoU 选择图像对，阈值 >0.3；对物体掩码内投影 3D 点计算 IoU，>0.4 视为跨视图共现物体。
  - **场景图构建**：生成结构化跨视图场景图，包含物体属性、物体间空间关系、相机位姿和度量尺度 3D 信息。
  - **数据生成**：从场景图采样生成 QA；使用类人推理模板构造复杂任务，并用强 LLM 改写 QA 以增强多样性。
- **任务体系**：共 7 类：
  - 单视图基础：相对方向、相对距离、物体属性。
  - 跨视图推理：跨视图 grounding、相机位姿估计、跨视图运动跟踪、姿态感知变化分析。
- **三阶段训练策略**：
  - **SFT 第一阶段**：在单视图 3D 基础数据和跨视图 grounding 数据上微调，建立基础空间感知。
  - **SFT 第二阶段**：使用类人跨视图推理数据微调，学习高层几何推理模式。
  - **RL 阶段**：采用 GRPO 和任务特定奖励函数进一步优化。
- **关键奖励设计**：
  - 多输出任务：\(R_{mul}=N_{correct}-\alpha N_{error}-\beta N_{miss}\)。
  - 距离奖励：预测距离在 \([0.8d,1.25d]\) 得 1.0，在 \([0.5d,2.0d]\) 得 0.5，否则 0。
  - 方向奖励：角度误差 \(\Delta\theta \le 30^\circ\) 得 1.0。
  - 可见性和 IoU 奖励用于跨视图 grounding。
  - 相机位姿：用相对旋转矩阵 \(R_{rel}=R_1^T R_2\)、相对平移 \(t_{rel}=R_1^T(t_2-t_1)\)，角度 \(\theta=\arccos((\mathrm{tr}(R_{rel})-1)/2)\)，并设计旋转奖励 \(R_{rot}=1-\theta/\pi\)、平移奖励 \(R_{tra}=1-\|t_{rel}\|^2/(\|t_{rel}\|^2+1.5)\)。

## 3. 实验设计
- **数据集与基准**：
  - 训练数据来自 DL3DV 视频，经 MV3DSR 生成 300K 样本；人工清洗后保留 100K 高质量样本，另有 200K 未验证样本。
  - **MV3DSR-Bench**：4,500 个问题，来自 500 个 held-out 视频，单视图与跨视图任务比例 1:1；非定量
