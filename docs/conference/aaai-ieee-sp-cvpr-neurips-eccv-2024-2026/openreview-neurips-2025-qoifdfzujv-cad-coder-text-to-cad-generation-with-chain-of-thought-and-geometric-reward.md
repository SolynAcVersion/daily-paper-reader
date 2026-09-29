---
title: "CAD-Coder: Text-to-CAD Generation with Chain-of-Thought and Geometric Reward"
title_zh: CAD-Coder：结合思维链与几何奖励的文本到CAD生成
authors: "Yandong Guan, Xilin Wang, XiMing Xing, Jing Zhang, Dong Xu, Qian Yu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=QoiFdfZUJv"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 将文本到CAD建模为生成CadQuery脚本并用几何奖励强化学习
tldr: 文本到CAD生成面临代码有效性与几何保真度难以兼顾的问题。该文提出CAD-Coder，把任务重构为生成参数化CadQuery脚本，从而支持直接几何验证并复用大语言模型能力。方法采用监督微调加基于几何奖励与格式奖励的GRPO强化学习两阶段流程，并引入思维链规划提升推理。实验表明生成代码的有效性与几何精度显著提升，并构建了大规模数据集。其贡献在于打通了语言到可验证CAD几何的生成路径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 文本到CAD生成难以同时保证代码有效性与几何保真度，缺乏可直接验证的表示。
method: 将任务重构为生成参数化CadQuery脚本，采用监督微调加GRPO强化学习，并以几何和格式奖励引导，引入思维链规划。
result: 实验显示生成脚本的有效性与几何精度明显提升，并构建了大规模数据集。
conclusion: 打通了从自然语言到可验证CAD几何的生成路径。
---

## Abstract
In this work, we introduce CAD-Coder, a novel framework that reformulates text-to-CAD as the generation of CadQuery scripts—a Python-based, parametric CAD language.
This representation enables direct geometric validation, a richer modeling vocabulary, and seamless integration with existing LLMs. 
To further enhance code validity and geometric fidelity, we propose a two-stage learning pipeline: (1) supervised fine-tuning on paired text–CadQuery data, and (2) reinforcement learning with Group Reward Policy Optimization (GRPO), guided by a CAD-specific reward comprising both a geometric reward (Chamfer Distance) and a format reward.
We also introduce a chain-of-thought (CoT) planning process to improve model reasoning, and construct a large-scale, high-quality dataset of 110K text–CadQuery–3D model triplets and 1.5K CoT samples via an automated pipeline. Extensive experiments demonstrate that CAD-Coder enables LLMs to generate diverse, valid, and complex CAD models directly from natural language, advancing the state of the art of text-to-CAD generation and geometric reasoning.

---

## 论文详细总结（自动生成）

# CAD-Coder 论文中文总结

> 说明：提供的 PDF 提取文本仅为 OpenReview 浏览器验证页面，未包含论文正文；以下总结主要依据论文摘要与元数据。凡摘要未明确说明的内容，均标注为“未说明”。

## 1. 核心问题与整体含义

- **研究动机**：文本到 CAD 生成需要同时保证生成代码的有效性与几何模型的保真度，但现有方法难以兼顾。
- **核心问题**：自然语言到 CAD 几何的生成缺乏可直接验证的表示，导致代码可执行性、几何精度和建模复杂度难以统一。
- **整体含义**：论文将文本到 CAD 重构为生成 **CadQuery 脚本**，即一种基于 Python 的参数化 CAD 语言。该表示可直接执行和几何验证，并能复用大语言模型的代码生成能力。
- **目标**：提升生成脚本的代码有效性、几何保真度和推理能力，推进 text-to-CAD 与几何推理的 SOTA。

## 2. 方法论

- **核心思想**：把 text-to-CAD 任务转化为“自然语言 → CadQuery 参数化脚本 → 可验证 3D CAD 模型”的生成问题。
- **表示优势**：
  - 可直接进行几何验证；
  - 拥有更丰富的建模词汇；
  - 可与现有 LLM 无缝集成。
- **两阶段学习流程**：
  1. **监督微调（SFT）**：在成对的文本–CadQuery 数据上微调 LLM，学习生成可执行脚本。
  2. **强化学习（GRPO）**：采用 Group Reward Policy Optimization，奖励由 CAD 专用奖励构成，包括：
     - 几何奖励：Chamfer Distance；
     - 格式奖励：约束生成脚本格式。
- **思维链规划（CoT）**：引入 chain-of-thought planning，提升模型对建模步骤的推理能力。
- **数据构建**：通过自动化流水线构建大规模高质量数据集，包含 **110K 文本–CadQuery–3D 模型三元组**和 **1.5K CoT 样本**。
- **流程概述**：输入自然语言描述 → CoT 规划 → 生成 CadQuery 脚本 → 执行/解析脚本 → 计算几何奖励与格式奖励 → 通过 GRPO 优化模型；SFT 作为初始冷启动阶段。
- **公式与算法细节**：提供的摘要未给出具体公式或完整算法伪代码。

## 3. 实验设计

- **数据集**：
  - 110K 文本–CadQuery–3D 模型三元组；
  - 1.5K CoT 样本；
  - 数据由自动化流水线构建。
- **场景**：自然语言直接生成多样、有效、复杂的 CAD 模型。
- **Benchmark**：摘要仅称进行了 extensive experiments，未明确命名具体 benchmark。
- **对比方法**：提供内容中未说明具体基线或对比方法。
- **评价维度**：
  - 生成代码的有效性；
  - 几何保真度；
  - 生成模型的多样性与复杂度；
  - 几何奖励使用 Chamfer Distance，但测试阶段具体指标未说明。

## 4. 资源与算力

- 提供的摘要与元数据中**未说明**使用的 GPU 型号、数量、训练时长、模型参数量或总体算力成本。
- 因此无法从现有信息评估训练开销与复现所需资源。

## 5. 实验数量与充分性

- 摘要声称进行了 extensive experiments，但未列出具体实验组数。
- 未说明是否包含：
  - 不同数据集划分；
  - 消融实验；
  - 与多个基线的定量对比；
  - 统计显著性或误差分析。
- 因此，基于当前提供内容，**无法客观判断实验是否充分、公平、可复现**。
- 从方法设计看，SFT、GRPO、几何奖励、格式奖励和 CoT 均可能对应消融实验，但具体证据未在摘要中呈现。

## 6. 主要结论与发现

- CAD-Coder 能让 LLM 直接从自然语言生成多样、有效且复杂的 CAD 模型。
- 两阶段 SFT + GRPO 训练，以及几何奖励与格式奖励，显著提升了生成代码的有效性和几何精度。
- CoT 规划有助于改善模型推理。
- 论文构建了大规模文本–CadQuery–3D 数据集与 CoT 样本，推动 text-to-CAD 生成和几何推理达到新的 SOTA。
- 核心贡献在于打通了“自然语言 → 可验证 CAD 几何”的生成路径。

## 7. 优点

- **表示选择合理**：使用 CadQuery 参数化脚本，使生成结果可直接执行和几何验证。
- **训练流程完整**：SFT 提供冷启动，GRPO 进一步用奖励优化代码有效性与几何保真度。
- **奖励设计针对性强**：同时考虑几何奖励和格式奖励，直接面向 CAD 任务需求。
- **引入 CoT 规划**：增强复杂建模任务的推理能力。
- **数据规模较大**：110K 三元组和 1.5K CoT 样本为训练提供支撑。
- **复用 LLM 能力**：利用 LLM 的代码生成能力，避免从零设计专用生成架构。

## 8. 不足与局限

- **正文信息不足**：提供的 PDF 文本为验证页面，无法评估完整方法、实验和实现细节。
- **实验细节缺失**：benchmark、对比方法、消融实验、评价指标和统计结果未在摘要中明确。
- **算力与复现性未报告**：缺少 GPU 型号、数量、训练时长等关键资源信息。
- **表示空间受限**：CadQuery 只能覆盖其 API 可表达的 CAD 模型，对复杂装配、工程约束和工业级建模的覆盖可能有限。
- **奖励可能偏置**：Chamfer Distance 主要衡量表面几何差异，可能忽略拓扑结构、参数合法性和可编辑性；格式奖励也可能不足以约束语义正确性。
- **数据噪声风险**：自动化流水线构建的大规模数据可能引入噪声或偏差，摘要未说明质量控制与数据分布。
- **强化学习风险**：GRPO 可能出现奖励黑客行为，且代码执行涉及安全与沙箱问题。
- **应用限制**：实际部署需要 CadQuery 执行环境、CAD 内核依赖，并需处理生成脚本错误、依赖差异和跨平台兼容性。

（完）
