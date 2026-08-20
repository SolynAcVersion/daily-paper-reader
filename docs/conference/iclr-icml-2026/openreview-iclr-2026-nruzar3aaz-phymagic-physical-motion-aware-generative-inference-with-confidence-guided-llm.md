---
title: "PhyMAGIC: Physical Motion-Aware Generative Inference with Confidence-guided LLM"
title_zh: PhyMAGIC：置信度引导LLM的物理运动感知生成推理
authors: "Siwei Meng, Yawei Luo, Ping Liu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=nruZar3Aaz"
tags: ["query:phys-video"]
score: 9.0
evidence: 免训练框架，结合视频扩散与可微物理模拟器，生成物理一致的动态
tldr: 现有视频扩散模型常生成违反动量守恒、物体相互穿透等物理不合理结果，而物理感知方法多依赖任务特定微调或有监督数据。为此提出PhyMAGIC，一个免训练框架：整合预训练图像到视频扩散模型、置信度引导的大语言模型推理与可微物理模拟器，从单张图像生成物理一致的动态。实验表明该方法能有效减少物理违例，并具备良好泛化性，为视频生成提供可扩展的物理约束方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 针对视频扩散模型动态生成中动量违例与物体穿插等问题，且现有物理感知方法依赖特定微调或监督数据。
method: 提出免训练框架PhyMAGIC，融合预训练图像到视频扩散模型、置信度引导的LLM推理与可微物理模拟器生成物理一致动态。
result: 实验表明能有效降低动量违例与物体穿插，提升生成视频的物理一致性，且无需任务特定微调。
conclusion: 该工作为物理一致性视频生成提供可扩展、免训练的推理路径，兼顾视觉质量与物理合理性。
---

## Abstract
Recent advances in 3D content generation have amplified demand for dynamic models that are both visually realistic and physically consistent. However, state-of-the-art video diffusion models frequently produce implausible results such as momentum violations and object interpenetrations. Existing physics-aware approaches often rely on task-specific fine-tuning or supervised data, which limits their scalability and applicability. To address the challenge, we present PhyMAGIC, a training-free framework that generates physically consistent motion from a single image. PhyMAGIC integrates a pre-trained image-to-video diffusion model, confidence-guided reasoning via large language models (LLMs), and a differentiable physics simulator to produce 3D assets ready for downstream physical simulation without fine-tuning or manual supervision. By iteratively refining motion prompts using LLM-derived confidence scores and leveraging simulation feedback, PhyMAGIC steers generation toward physically consistent dynamics. Comprehensive experiments demonstrate that PhyMAGIC outperforms state-of-the-art video generators and physics-aware baselines, enhancing physical property inference and motion–text alignment while maintaining visual fidelity.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **研究动机**：随着3D内容生成技术的进步，人们对兼具视觉真实感与物理一致性的动态模型需求日益增长。然而，现有的视频扩散模型（如SOTA模型）在生成动态时经常出现**动量守恒违例**和**物体相互穿透**等物理不合理现象。
- **现有方法的不足**：已有的物理感知方法往往依赖**任务特定微调**或**监督数据**，导致可扩展性和通用性受限。
- **核心问题**：如何在不进行微调、不依赖手动监督的前提下，从单张图像生成物理一致且视觉逼真的动态视频/3D资产？
- **整体含义**：该工作提出一种**免训练（training-free）** 的推理路径，将生成模型与物理模拟器结合，为物理一致性视频生成提供可扩展的解决方案，兼顾问视觉质量与物理合理性。

## 2. 方法论

- **核心思想**：通过“生成-反馈-修正”的迭代闭环，利用大语言模型（LLM）的推理能力和可微物理模拟器的量化反馈，引导视频扩散模型生成满足物理规律的动态。
- **方法名称**：PhyMAGIC（Physical Motion-Aware Generative Inference with Confidence-guided LLM）
- **三大组件**：
  1. **预训练图像到视频扩散模型**：负责生成初始动态视频/3D资产。
  2. **置信度引导的LLM推理**：LLM对生成结果进行评估，输出置信度分数，并根据物理合理性迭代修正运动提示（motion prompt）。
  3. **可微物理模拟器**：模拟生成内容的物理行为，提供模拟反馈（如动量、碰撞等物理指标），用于指导LLM的修正方向。
- **算法流程**（文字描述）：
  1. 输入单张静态图像；
  2. 由图像到视频扩散模型生成初始动态候选；
  3. 将生成结果送入可微物理模拟器，计算物理违例指标；
  4. LLM根据模拟反馈与置信度分数，分析物理不一致原因，并修改运动提示；
  5. 使用修正后的提示重新驱动视频生成；
  6. 重复上述过程，直到物理一致性与视觉质量达到平衡。
- **关键技术细节**：
  - 利用LLM的置信度分数自动判断是否继续迭代或终止；
  - 无需对扩散模型进行任何微调，也无须人工标注；
  - 输出可直接用于下游物理模拟的3D资产。

## 3. 实验设计

- **数据与场景**：摘要中**未明确列出具体数据集名称**（如未见对UCF-101、SkyTimelapse等常见基准的提及），也未说明具体场景类型（如刚体运动、流体、人物动作等）。
- **Benchmark**：论文提到与“SOTA视频生成器”和“物理感知基线”进行对比，但**未给出具体的基准名称或评价指标体系**（如PSNR、LPIPS、FVD、物理违规率等）。
- **对比方法**：包括现有SOTA视频扩散模型以及物理感知方法（具体方法名称未在摘要中给出）。
- **评估维度**：
  - 物理属性推断能力（physical property inference）
  - 运动-文本对齐（motion-text alignment）
  - 视觉保真度（visual fidelity）
  - 物理一致性的整体提升（如减少动量违例与物体穿插）
- **注意**：由于仅提供摘要，详细实验设置（如训练/测试划分、评价指标细节）无法获知。

## 4. 资源与算力

- 论文摘要中**完全没有提及**任何算力相关信息，例如：
  - GPU型号（A100、V100等）与数量
  - 训练时长或推理耗时
  - 显存占用、参数量等
- **结论**：无法从现有文本中总结资源消耗情况。如果完整论文有实验细节，需要进一步查看原文。

## 5. 实验数量与充分性

- **已知实验量**：摘要仅概括性地提到“综合实验”（Comprehensive experiments），表明进行了多组实验，但具体数量不明。
- **可能的实验类型**：
  - 与SOTA视频生成器的对比；
  - 与物理感知基线的对比；
  - 可能包含消融实验（如去除置信度引导、去除模拟器反馈等），但摘要未明确列出。
- **充分性与公平性评估**：
  - **积极方面**：对比对象覆盖了通用生成器与物理感知方法，评估维度较全面（物理、文本对齐、视觉）。
  - **不足之处**：
    - 未报告具体实验数量与数据集，难以判断统计显著性；
    - 未提供数值结果，无法验证“优于”的幅度是否客观；
    - 未说明是否采用用户研究或标准公开基准，存在偏差风险；
    - 免训练框架的公平性取决于基线的调优程度，但文中未提及控制变量方法。

## 6. 主要结论与发现

- PhyMAGIC能够**有效降低动量违例和物体穿插**，提升生成视频的物理一致性；
- 在**物理属性推断**和**运动-文本对齐**方面优于现有SOTA视频生成器与物理感知基线；
- 同时**保持视觉保真度**，不会因引入物理约束而明显牺牲画质；
- 该框架**无需任务特定微调或手动监督**，具有良好的泛化性和可扩展性；
- 证明了将LLM推理与可微物理模拟器结合，能够作为视频扩散模型的有效物理“校准器”。

## 7. 优点

- **免训练设计**：无需微调扩散模型，即插即用，大幅降低计算成本和应用门槛。
- **模块化架构**：各组件可独立替换（如换用更强的扩散模型或模拟器），易于扩展。
- **置信度引导机制**：利用LLM的置信度动态调节迭代过程，避免过度修正或无效循环，提高推理效率。
- **物理与视觉平衡**：通过模拟反馈指导生成，兼顾物理正确性与视觉质量。
- **泛化性**：不依赖特定任务数据，理论上可适用于多种动态生成场景。

## 8. 不足与局限

- **信息不完整**：当前提供的文本仅含摘要，缺乏实验细节、数据集、定量结果、超参数设置等关键信息，难以全面评估方法的可靠性与可复现性。
- **实验覆盖未知**：未说明是否测试了多种物体类型（柔性体、刚体、流体）、相机运动、复杂场景等，适用边界尚不清晰。
- **潜在偏差风险**：
  - LLM的置信度可能对某些物理规律理解不准确，导致错误引导；
  - 可微模拟器的物理近似可能不足以描述真实世界复杂现象（如摩擦、空气阻力）；
  - 评价指标选择可能偏向于与自己方法契合的物理指标，存在潜在选择性报告。
- **应用限制**：
  - 依赖单张图像作为输入，对初始图像的姿态、遮挡敏感；
  - 迭代式推理可能增加推理延迟，不适合实时或高吞吐场景；
  - 文献未提及与大规模训练生成方法的效率对比，实际计算开销未知。
- **公平性存疑**：对比基线是否经过同等调优、是否使用统一评价协议，未在摘要中说明，需原文确认。

（完）
