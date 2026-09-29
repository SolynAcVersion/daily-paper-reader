---
title: "Seeing from Another Perspective: Evaluating Multi-View Understanding in MLLMs"
title_zh: 换一个视角看：评估多模态大模型的多视图理解能力
authors: "Chun-Hsiao Yeh, Chenyu Wang, Shengbang Tong, Ta-Ying Cheng, Ruoyu Wang, Tianzhe Chu, Yuexiang Zhai, Yubei Chen, Shenghua Gao, Yi Ma"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38188/42150"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 多视图几何一致性评测基准
tldr: 多视图理解是具身智能体的基础能力，但现有多模态大模型在多视图几何一致性与跨视图对应上表现不佳。本文提出All-Angles Bench基准，包含来自90个真实场景的2100余组问答对。对38个通用及三维空间推理模型的评测显示，它们在多视图场景推理上仍存在明显短板，揭示了当前模型的关键局限。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1831, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1852, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1824, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 886, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1832, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 866, \"height\": 640, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 305, \"height\": 233, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 305, \"height\": 230, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38188/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 868, \"height\": 689, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38188/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1496, \"height\": 1327, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38188/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 874, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38188/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 874, \"height\": 375, \"label\": \"Table\"}]"
motivation: 多模态大模型在多视图几何一致性和跨视图对应上表现薄弱。
method: 构建含2100余问答对、覆盖90个真实场景的All-Angles Bench基准。
result: 对38个模型的评测揭示其在多视图推理上的明显不足。
conclusion: 为多视图场景理解提供了系统评测基准。
---

## Abstract
Multi-view understanding, the ability to  reconcile visual information across diverse viewpoints for effective navigation, manipulation, and 3D scene comprehension, is a fundamental challenge in Multi-Modal Large Language Models (MLLMs) to be used as embodied agents. While recent MLLMs have shown impressive advances in high-level reasoning and planning, they frequently fall short when confronted with multi-view geometric consistency and cross-view correspondence. To comprehensively evaluate the challenges of MLLMs in multi-view scene reasoning, we introduce All-Angles Bench, a human carefully benchmark with over 2,100 question-answer pairs from 90 diverse, real-world scenes. Our broad evaluation across 38 general-purpose and 3D spatial reasoning MLLMs reveals a substantial performance gap compared to humans. More critically, our analysis identifies two root failure modes: (1) cross-view object mismatch—the inability to establish consistent object correspondence across views; and (2) cross-view spatial misalignment—the failure to infer accurate camera poses and spatial layouts. These findings underscore a lack of multi-view awareness in current MLLMs, calling for architectural innovations beyond prompt tuning alone. We believe that our benchmark offers valuable insights toward building spatially-intelligent MLLMs.

---

## 论文详细总结（自动生成）

# 论文总结：Seeing from Another Perspective: Evaluating Multi-View Understanding in MLLMs

## 1. 核心问题与整体含义
- **研究动机**：多视图理解是 MLLM 作为具身智能体进行导航、操作和 3D 场景理解的基础能力，要求模型在不同视角间保持几何一致性和物体对应关系。
- **核心问题**：当前 MLLM 虽在高层推理和规划上表现突出，但在多视图几何一致性、跨视图对应、相机位姿推断等方面明显不足。
- **论文提出两个问题**：  
  1. MLLM 是否能同时理解多个视角？  
  2. MLLM 实现更好多视图理解的关键挑战是什么？
- **整体含义**：论文构建 **All-Angles Bench**，系统评测 MLLM 的多视图理解能力，揭示其与人类之间的显著差距，并指出两个根失败模式：  
  - **跨视图物体不匹配**：无法在不同视角间建立一致的物体对应；  
  - **跨视图空间错位**：无法准确推断相机位姿和空间布局。  
- **结论指向**：仅靠 prompt tuning 不足以解决多视图理解问题，需要架构或训练层面的创新。

## 2. 方法论
- **核心思想**：构建一个人工精标、面向真实世界多视图场景的基准，通过多类空间推理任务和配对问题，评估 MLLM 的几何一致性与跨视图对应能力。
- **数据来源与规模**：  
  - 来自 **Ego-Exo4D** 和 **EgoHumans**；  
  - 包含 **90 个真实多视图场景**，每个场景至少 3 个视角；  
  - 共 **2,132 个多选题问答对**。
- **六类任务**：  
  1. Counting（计数）  
  2. Attribute Identification（属性识别）  
  3. Relative Distance（相对距离）  
  4. Relative Direction（相对方向）  
  5. Object Manipulation（物体操作/轨迹推理）  
  6. Camera Pose Estimation（相机位姿估计）  
  - Counting 和 Camera Pose Estimation 使用全部视角；其他任务使用两个随机选取的视角。
- **构建流程**：  
  - 先用 GPT-4o 生成初始问题；  
  - 再由人工标注者校验、修正逻辑矛盾与歧义，并标注唯一正确答案；  
  - 形成“人类在环”的高质量问答对。
- **配对问题设计**：  
  - 通过交换视角引用、反转方向语言等方式，生成语义等价但表述/视角变化的配对问题；  
  - 用于测试模型是否真正理解
