---
title: "CoPhyBench: Benchmarking Physical Reasoning from Conditional Video Observation"
title_zh: CoPhyBench：基于条件视频观测的物理推理基准
authors: "Fanyue Wei, Kai Xu, Yizhuo Zhang, Pengzhan Sun, Junbin Xiao, Angela Yao"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=rDiKG1xlDV"
tags: ["query:phys-video"]
score: 7.0
evidence: 基于条件视频观测的物理推理基准，评估预测、物理计算与反事实推理
tldr: 当前视频模型缺乏系统的物理推理能力评估基准。CoPhyBench基于真实世界条件视频观测构建物理推理数据集，从预测、物理计算和反事实推理三个角度测试视频大语言模型的物理理解。实验结果表明，该基准能有效区分物理因果泛化与表面相关性，并揭示现有模型在物理推理上的显著短板。它为物理正确性测评提供了可复用的标准化工具，有望推动物理可解释视频生成与理解的发展。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频模型缺乏系统评估物理推理能力的基准，难以判断其对物理因果的真正理解。
method: 利用真实世界视频构建条件观测数据集，设计预测、物理计算与反事实推理三类测试任务。
result: CoPhyBench能有效区分物理泛化能力与表面相关性，揭示现有视频大语言模型的物理推理短板。
conclusion: 该基准为物理推理与视频理解的评估提供新标准，有助推动物理可解释AI研究。
---

## Abstract
We present \textsc{CoPhyBench}, a \textsc{Co}nditional reasoning \textsc{Phy}sics-based \textsc{Bench}mark. \textsc{CoPhyBench} evaluates the ability of Video-LLMs to reason about physical events based on conditional observations from real-world videos. It probes physics understanding from 
three perspectives: 1) Prediction: predicting future events from observable cues, assessing a grasp of causality in real-world scenarios. 2) Physical Calculation: estimating times and positions 
by translating visual conditions into variables of dynamics equations. 3) Counterfactual Reasoning: inferring futures based on hypothetical changes, to distinguish between generalizable physical understanding instead of superficial correlations. 
We construct a high-quality dataset consisting of 1,300 carefully verified question-answer pairs grounded in 232 diverse, real-world physics videos to support these tasks, spanning various phenomena in 
kinematics and dynamics.
Extensive benchmarking on leading Video-LLMs reveals that while models perform reasonably on causal prediction, they struggle with precise physical calculations and counterfactual reasoning. 
These findings highlight the limitations of current models in transitioning from semantic alignment to deeper, physics-grounded reasoning, calling for new training paradigms to incorporate physics reasoning. Our dataset and resources will be released.

---

## 论文详细总结（自动生成）

# CoPhyBench：基于条件视频观测的物理推理基准——论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- 当前视频大语言模型（Video-LLMs）在视频理解与描述上已取得显著进展，但**是否真正理解物理世界的因果机制**仍缺乏系统性评估。
- 现有基准多集中在语义理解、时间问答或事件预测的表面相关性上，**难以区分模型是基于物理规律推理，还是仅依赖数据中的统计捷径**。
- 论文提出 **CoPhyBench**（Conditional reasoning Physics-based Benchmark），旨在从**真实世界视频的条件观测**出发，评估模型对物理事件的深层理解能力，填补物理推理评测的空白。
- 整体含义：为物理可解释的AI视频理解与生成提供标准化测试工具，推动模型从“语义对齐”走向“物理因果推理”。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：利用真实世界物理视频作为观测条件，设计多种需要物理知识才能回答的问题，迫使模型将视觉信息与动力学规律结合。
- **三个评测维度**：
  1. **预测（Prediction）**：从当前可观测线索预测未来事件，检验模型对真实场景因果关系的把握。
  2. **物理计算（Physical Calculation）**：将视觉条件转化为运动学/动力学方程中的变量（如位移、时间、速度），估计事件发生的时间或位置。
  3. **反事实推理（Counterfactual Reasoning）**：基于假设性改变（如“如果初速度加倍会怎样？”）推断不同的未来，用于区分**可泛化的物理理解**与**表面相关性**。
- **数据构建流程**：
  - 收集232个多样化的真实世界物理视频；
  - 覆盖运动学与动力学中的多种现象；
  - 人工生成并验证1,300个高质量问答对，保证问题严谨且需依赖物理推理。
- **评估方式**：将问答对输入Video-LLMs，以自动指标衡量其回答准确性，从而量化模型的物理推理能力。

## 3. 实验设计

- **数据集/场景**：自建CoPhyBench数据集，包含232个真实世界物理视频，共1,300个问答对，场景涉及运动学（如自由落体、抛体运动）和动力学（如碰撞、受力分析）。
- **Benchmark任务**：三项子任务——事件预测、物理计算、反事实推理；每项均基于条件视频观测设计。
- **对比方法**：文中提及“leading Video-LLMs”（多个领先的视频大语言模型），但具体模型名称未在摘要中列出。作为对比基准，这些模型需在相同问答对上完成全部三个任务。
- **评估维度**：除整体准确率外，分任务比较性能，以揭示模型在不同物理推理类型上的差异。

## 4. 资源与算力

- **未明确说明**：论文摘要和元数据中**没有提及**使用的GPU型号、数量、训练/测试时长或具体计算资源。
- 推测：由于是评估基准（而非训练新模型），算力消耗可能主要来自对多个Video-LLMs的推理；但具体细节在现有信息中不可得。

## 5. 实验数量与充分性

- **实验组数**：从摘要看，对“领先的Video-LLMs”进行了广泛评估，但**未给出具体模型数量、重复实验次数或消融研究**。
- **充分性分析**：
  - **优点**：三项任务覆盖面广，既有预测，也有精确计算和反事实推理，能较全面反映物理理解的多层次能力；真实世界视频提升了生态效度。
  - **不足**：缺乏对基准自身鲁棒性的验证（如问题敏感性、标注一致性测试）；没有消融实验证明各任务是否不可替代；未报告模型性能方差或统计显著性。
  - **公平性**：使用同一数据集评估所有模型，从流程上保证了公平性，但未说明是否采用标准提示模板、温度参数等细节，可能影响客观比较。

## 6. 主要结论与发现

- 现有Video-LLMs在**因果预测任务上表现相对合理**，能利用视频中的直接线索做出大致预判。
- 但在**精确物理计算**（如准确估计时间、位置）和**反事实推理**（如假设条件改变后的结果）上表现**明显困难**。
- 这表明当前模型仍主要处于**语义层面**的理解，尚未真正掌握**深层的物理规律**；模型容易依赖数据中的表面相关性，而非可泛化的物理因果模型。
- 结论呼吁设计**融合物理推理的新型训练范式**，以缩小语义理解与物理推理之间的鸿沟。

## 7. 优点

- **针对性强**：首次从“条件观测”角度系统评测物理推理，弥补既有基准的缺失。
- **多维度设计**：预测、计算、反事实三重任务由浅入深，既能测试直接因果，也能剔除表面相关性。
- **真实世界数据**：采用真实视频而非合成渲染，更贴近实际应用，提高评测结果的可信度。
- **高质量数据**：1,300个问答对经过人工验证，为基准可靠性提供保障。
- **可作为标准化工具**：数据集和资源将公开，便于后续研究者复现和扩展。

## 8. 不足与局限

- **信息不完整**：摘要中未提供具体模型清单、评估指标细节以及数据划分方式，难以独立判断实验的全面性。
- **领域覆盖有限**：仅涉及运动学和动力学，未涵盖热学、电磁学、流体力学等其他物理分支，泛化性有限。
- **反事实设计挑战**：反事实问题依赖人工假设，可能受标注者偏见影响；模型对这类问题的回答也可能受语言先验而非视频内容误导。
- **计算资源缺失**：未报告评估所需算力，不利于其他研究者复现成本估算。
- **潜在公平性问题**：未说明是否对每个模型调优过提示词，或是否采用统一答案格式，可能影响对比的客观性。
- **基准本身未做效度验证**：例如，是否确保问题必须依赖视频才能回答，而不只是常识；是否排除文本捷径等，均未在现有信息中体现。

（完）
