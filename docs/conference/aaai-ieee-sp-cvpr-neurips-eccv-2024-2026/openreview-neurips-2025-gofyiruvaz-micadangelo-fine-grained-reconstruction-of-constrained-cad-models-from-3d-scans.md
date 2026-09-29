---
title: "MiCADangelo: Fine-Grained Reconstruction of Constrained CAD Models from 3D Scans"
title_zh: MiCADangelo：从三维扫描精细重建受约束CAD模型
authors: "Ahmet Serdar Karadeniz, Dimitrios Mallis, Danila Rukhovich, Kseniya Cherenkova, Anis Kacem, Djamila Aouada"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=GoFYIRUVAz"
tags: ["query:cad-spatial"]
score: 6.0
evidence: 带草图级约束的CAD逆向工程
tldr: 针对将三维扫描转换为参数化CAD表示的高精度与结构复杂性难题，本文提出MiCADangelo。现有方法或无法产出完整参数化输出，或忽视细粒度几何细节，且忽略草图级约束。方法在重建中引入草图级约束以保持参数化结构，实现精细的约束CAD模型重建，推动了CAD逆向工程的发展。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 将三维扫描转为参数化CAD模型难度大，现有方法缺乏参数化输出或忽略细粒度细节与草图约束。
method: 在CAD逆向工程中引入草图级约束，兼顾几何细节与参数化结构进行重建。
result: 能重建精细且带约束的CAD模型，弥补了自底向上与自顶向下方法的不足。
conclusion: 为高精度参数化CAD逆向工程提供了新思路。
---

## Abstract
Computer-Aided Design (CAD) plays a foundational role in modern manufacturing and product development, often requiring designers to modify or build upon existing models. Converting 3D scans into parametric CAD representations—a process known as CAD reverse engineering—remains a significant challenge due to the high precision and structural complexity of CAD models. Existing deep learning-based approaches typically fall into two categories: bottom-up, geometry-driven methods, which often fail to produce fully parametric outputs, and top-down strategies, which tend to overlook fine-grained geometric details. Moreover, current methods neglect an essential aspect of CAD modeling: sketch-level constraints. In this work, we introduce a novel approach to CAD reverse engineering inspired by how human designers manually perform the task. Our method leverages multi-plane cross-sections to extract 2D patterns and capture fine parametric details more effectively. It enables the reconstruction of detailed and editable CAD models, outperforming state-of-the-art methods and, for the first time, incorporating sketch constraints directly into the reconstruction process.

---

## 论文详细总结（自动生成）

> **信息范围说明**：提供的 PDF 提取文本实际为 OpenReview 验证页面，未包含论文正文、方法公式、实验表格或附录。以下总结主要依据论文摘要与元数据；凡未在摘要/元数据中出现的信息，均标注为“未说明/无法判断”，不进行臆测。

## 1. 核心问题与整体含义

- **研究背景**：计算机辅助设计（CAD）在现代制造与产品开发中具有基础性作用，设计师经常需要修改或扩展现有模型。将三维扫描转换为参数化 CAD 表示，即 CAD 逆向工程，是重要但困难的任务。
- **核心问题**：从 3D 扫描重建高精度、结构复杂且可编辑的参数化 CAD 模型。现有深度学习方法主要分为两类：
  - **自底向上、几何驱动方法**：常无法输出完整参数化模型。
  - **自顶向下方法**：常忽略细粒度几何细节。
  - 此外，现有方法普遍忽略 CAD 建模中的关键要素：**草图级约束**。
- **整体含义**：论文试图弥合“几何细节”与“参数化结构/约束”之间的鸿沟，使扫描重建结果不仅几何精细，而且可编辑、符合 CAD 建模习惯，从而推动 CAD 逆向工程发展。

## 2. 论文提出的方法论

- **核心思想**：受人类设计师手动执行 CAD 逆向工程的启发，利用**多平面截面**从三维扫描中提取二维图案，从而更有效地捕捉细粒度参数细节。
- **关键技术细节**（据摘要）：
  - 使用多平面截面将三维问题分解为多个二维截面/图案识别问题。
  - 从二维图案中提取参数化细节，以重建详细且可编辑的 CAD 模型。
  - **首次将草图约束直接纳入重建过程**，以保持 CAD 模型的参数化结构。
- **输出目标**：生成详细、可编辑、带草图级约束的 CAD 模型，而不是仅输出不可编辑的几何表示。
- **公式/算法流程**：提供的文本未给出具体网络架构、约束表示、损失函数、优化流程或公式，无法进一步说明。

## 3. 实验设计

- **数据集/场景**：摘要未说明使用了哪些数据集、扫描场景或 CAD 类别。
- **Benchmark**：未说明具体 benchmark 或评价指标。
- **对比方法**：仅称“outperforming state-of-the-art methods”，未列出对比方法名称。
- **元数据信息**：论文来源标注为 NeurIPS-2025-Accepted，OpenReview score 为 6.0，标签为 `query:cad-spatial`。这些可作为质量信号，但不能替代实验细节。

## 4. 资源与算力

- 提供的摘要与元数据**未提及** GPU 型号、数量、训练时长、参数量、推理成本或任何算力资源。
- 因此无法总结该论文的算力使用情况。

## 5. 实验数量与充分性

- 提供文本未说明实验组数、数据集数量、消融实验、用户研究或统计显著性分析。
- 无法判断实验是否充分、客观、公平。
- 仅从摘要可知：作者声称方法优于现有 SOTA，并首次将草图约束纳入重建；但缺少定量证据、baseline 细节与失败案例分析。

## 6. 论文的主要结论与发现

- 提出 **MiCADangelo**，用于从三维扫描精细重建受约束 CAD 模型。
- 多平面截面策略能够提取 2D patterns，并更有效地捕获细粒度参数细节。
- 方法可重建详细且可编辑的 CAD 模型。
- 首次在 CAD 逆向工程中直接将草图级约束纳入重建过程。
- 声称优于现有 SOTA 方法，并弥补自底向上与自顶向下方法的不足。

## 7. 优点

- **问题选择重要**：CAD 逆向工程连接三维扫描与参数化设计，具有明确工业价值。
- **方法直觉合理**：模仿人类设计师使用截面理解几何，可能比纯端到端几何回归更利于提取参数结构。
- **同时关注几何细节与参数化结构**：试图避免“只重建网格”或“只输出粗略参数”的两类缺陷。
- **首次引入草图级约束**：若成立，可显著提升重建结果的可编辑性和 CAD 合规性。
- **发表信号**：NeurIPS 2025 接收与 OpenReview 评分表明工作获得一定认可。

## 8. 不足与局限

- **文本信息严重不足**：提供的 PDF 提取内容不是论文正文，无法验证方法、实验与结论。
- **实验细节缺失**：数据集、benchmark、对比方法、评价指标、消融实验均未披露。
- **算力与可复现性未知**：未说明训练资源、代码、模型细节。
- **约束处理细节未知**：草图约束的类型、提取方式、冲突处理、约束推断可靠性均未说明。
- **潜在应用限制**：方法可能受扫描噪声、遮挡、截面选择策略影响；对复杂装配体、自由曲面或大规模 CAD 的泛化能力未知。
- **评估公平性无法判断**：缺少与 SOTA 的公平对比证据，OpenReview score 6.0 也属中等，需谨慎看待结论。

（完）
