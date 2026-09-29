---
title: "3DRS: MLLMs Need 3D-Aware Representation Supervision for Scene Understanding"
title_zh: 3DRS：多模态大模型需要三维感知表示监督以进行场景理解
authors: "Xiaohu Huang, Jingjing Wu, Qunyi Xie, Kai Han"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=KQuVaVUPL6"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 通过多视角对应监督提升三维感知表示与推理
tldr: 多模态大模型依赖强大的二维预训练进行三维推理，但预训练阶段缺乏显式三维数据，限制其三维表示能力。该文先通过多视角对应评估揭示三维感知表示质量与下游任务性能强正相关，进而提出3DRS框架，引入预训练三维基础模型的监督，将大模型视觉特征与蒸馏出的三维知识对齐。方法有效提升场景理解等下游任务表现。其意义在于证明显式三维监督对空间推理的关键作用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 多模态大模型预训练缺乏显式三维数据，导致三维表示能力不足，限制三维推理表现。
method: 通过多视角对应评估三维感知能力，并引入预训练三维基础模型的监督来对齐视觉特征与三维知识。
result: 实验表明三维感知表示质量与下游性能强正相关，加入三维监督后场景理解效果显著提升。
conclusion: 说明显式三维表示监督对提升模型空间推理能力具有关键价值。
---

## Abstract
Recent advances in scene understanding have leveraged multimodal large language models (MLLMs) for 3D reasoning by capitalizing on their strong 2D pretraining. However, the lack of explicit 3D data during MLLM pretraining limits 3D representation capability. In this paper, we investigate the 3D-awareness of MLLMs by evaluating multi-view correspondence and reveal a strong positive correlation between the quality of 3D-aware representation and downstream task performance. Motivated by this, we propose 3DRS, a framework that enhances MLLM 3D representation learning by introducing supervision from pretrained 3D foundation models. Our approach aligns MLLM visual features with rich 3D knowledge distilled from 3D models, effectively improving scene understanding. Extensive experiments across multiple benchmarks and MLLMs—including visual grounding, captioning, and question answering—demonstrate consistent performance gains. Project: https://visual-ai.github.io/3drs/

---

## 论文详细总结（自动生成）

> 信息源说明：提供的 PDF 正文提取内容为 OpenReview 人机验证页，未包含论文全文；以下总结主要依据论文标题、摘要与元数据，具体实验细节需以原文为准。

## 1. 核心问题与整体含义

- **研究背景**：多模态大模型（MLLMs）在场景理解与 3D 推理中表现突出，主要得益于强大的 2D 预训练能力。
- **核心问题**：MLLM 预训练阶段通常缺乏显式 3D 数据，导致其 3D 表示能力不足，限制了下游三维推理与场景理解表现。
- **关键观察**：作者通过评估多视角对应（multi-view correspondence）研究 MLLM 的 3D 感知能力，发现 3D 感知表示质量与下游任务性能之间存在强正相关。
- **整体含义**：该工作强调显式 3D 表示监督对提升 MLLM 空间推理能力的关键价值，并提出通过预训练 3D 基础模型监督来增强 MLLM 的 3D 表示学习。

## 2. 方法论

- **核心思想**：提出 3DRS 框架，引入预训练 3D 基础模型作为监督来源，将 MLLM 的视觉特征与从 3D 模型中蒸馏出的三维知识对齐，从而增强 MLLM 的 3D-aware representation。
- **关键技术细节**：
  - 先通过多视角对应任务评估 MLLM 的 3D 感知表示质量。
  - 利用预训练 3D 基础模型提供丰富的 3D 知识。
  - 将 MLLM 视觉特征与 3D 知识进行对齐/蒸馏，使 MLLM 在缺乏显式 3D 预训练数据的情况下仍能获得更强的三维表示。
- **算法流程（文字说明）**：
  1. 输入多视角或场景相关数据，由 MLLM 视觉编码器提取视觉特征。
  2. 使用预训练 3D 基础模型提取三维知识或三维表示。
  3. 通过特征对齐或蒸馏监督，约束 MLLM 视觉特征与 3D 知识保持一致。
  4. 训练后的 MLLM 用于视觉定位、描述生成、问答等场景理解任务。
- **公式与损失**：摘要未披露具体公式、损失函数形式或训练目标细节，仅说明方法核心是对齐 MLLM 视觉特征与蒸馏出的 3D 知识。

## 3. 实验设计

- **任务/场景**：场景理解与 3D 推理，包括视觉定位（visual grounding）、描述生成（captioning）和问答（question answering）。
- **Benchmark**：
  - 多视角对应评估，用于衡量 MLLM 的 3D 感知表示质量。
  - 多个下游 benchmark，用于验证场景理解性能。
- **模型范围**：在多个 MLLM 上进行实验，说明方法具有一定通用性。
- **数据集**：摘要未列出具体数据集名称。
- **对比方法**：摘要未给出具体对比方法清单，无法确认基线模型、2D 预训练模型或已有 3D 增强方法的详细比较设置。
- **评价指标**：摘要未具体说明各任务的评价指标。

## 4. 资源与算力

- 摘要与元数据中**未明确说明**使用的 GPU 型号、数量、训练时长、参数量、数据规模或总算力开销。
- 因此无法总结具体算力配置；若需评估训练成本，需要查阅论文正文或附录。

## 5. 实验数量与充分性

- 摘要称进行了 **extensive experiments**，覆盖多个 benchmark 和多个 MLLM，并包含视觉定位、描述生成、问答等任务。
- 从摘要看，至少包括：
  - 多视角对应评估；
  - 多个下游场景理解任务；
  - 跨多个 MLLM 的验证。
- 但摘要未披露具体实验组数、消融实验数量、统计显著性检验、失败案例分析等。
- **充分性判断**：覆盖任务和模型较广，初步显示方法具有通用性；但由于缺少具体数值、消融和训练细节，无法完全判断实验是否充分。
- **客观与公平性**：若实验在相同 backbone、相同数据与评估协议下比较，则较公平；但摘要未说明是否严格控制变量、是否报告方差或置信区间，因此公平性无法完全确认。

## 6. 主要结论与发现

- MLLM 的 3D 感知表示质量与下游任务性能呈强正相关。
- 通过引入预训练 3D 基础模型的监督，3DRS 能有效提升 MLLM 的 3D 表示能力。
- 在视觉定位、描述生成和问答等多个任务上，3DRS 带来一致的性能提升。
- 显式 3D 表示监督对提升模型空间推理与场景理解能力具有关键价值。

## 7. 优点

- **问题重要且动机清晰**：直面 MLLM 缺乏显式 3D 预训练数据的核心瓶颈。
- **评估与方法形成闭环**：先通过多视角对应揭示 3D 感知与下游性能的相关性，再据此设计监督方法。
- **方法简洁通用**：利用已有预训练 3D 基础模型进行知识蒸馏/特征对齐，不依赖从零构建大规模 3D 预训练数据。
- **跨模型与跨任务验证**：在多个 MLLM 和多种场景理解任务上报告一致提升，增强结论说服力。
- **资源开放**：提供了项目页链接，便于复现与后续研究。

## 8. 不足与局限

- **全文信息不足**：提供的 PDF 正文为验证页面，具体数据集、对比方法、指标、算力与消融均未在摘要中说明。
- **依赖 3D 基础模型**：方法效果可能受教师模型质量、域差距和 3D 标注/配准质量影响。
- **训练成本未知**：引入 3D 基础模型监督可能增加训练与推理开销，但摘要未报告。
- **评估覆盖有限**：多视角对应评估未必能完全代表开放场景、动态场景或真实世界 3D 推理能力。
- **泛化风险**：跨数据集、跨传感器、跨场景的泛化能力尚未在摘要中体现。
- **公平性细节缺失**：未说明是否控制训练预算、模型规模、数据量等变量，难以完全排除比较偏差。
- **应用限制**：若目标场景缺少可用 3D 基础模型或高质量多视角数据，方法部署可能受限。

（完）
