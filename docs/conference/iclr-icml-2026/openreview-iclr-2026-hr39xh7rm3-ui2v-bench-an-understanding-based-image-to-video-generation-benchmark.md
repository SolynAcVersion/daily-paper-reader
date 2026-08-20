---
title: "UI2V-Bench: An Understanding-based Image-to-video Generation Benchmark"
title_zh: UI2V-Bench：一种基于理解的图像到视频生成基准
authors: "Ailing Zhang, Lina Lei, Dehong Kong, Zhixin Wang, Jiaqi Xu, Fenglong Song, Chun-Le Guo, Chang Liu, Fan Li, Jie Chen"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=hR39xH7rm3"
tags: ["query:phys-video"]
score: 8.0
evidence: 用于评估图像到视频生成是否符合物理规律的基准
tldr: 针对图像到视频生成评估仅聚焦质量和时间一致性而忽略语义理解与物理常识的问题，该工作提出UI2V-Bench基准。基准设计了空间理解、属性绑定等四个主要评估维度，并明确关注生成视频是否符合物理定律和人类常识。通过该基准可更全面地衡量I2V模型对具体主体的语义理解能力，为提升生成视频的物理合理性与语义一致性提供评测工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有图像到视频基准忽略对具体主体语义的理解以及生成视频是否符合物理规律和常识。
method: 提出UI2V-Bench基准，从空间理解、属性绑定等维度评估I2V模型。
result: 提供多维度评估框架，突出物理规律与常识符合性。
conclusion: 为图像到视频生成模型的理解能力与物理合理性评测提供新基准。
---

## Abstract
Generative diffusion models are developing rapidly and attracting increasing attention due to their wide range of applications. Image-to-Video (I2V) generation has become a major focus in the field of video synthesis. However, existing evaluation benchmarks primarily focus on aspects such as video quality and temporal consistency, while largely overlooking the model's ability to understand the semantics of specific subjects in the input image or to ensure that the generated video aligns with physical laws and human commonsense. To address this gap, we propose UI2V-Bench, a novel benchmark for evaluating I2V models with a focus on semantic understanding and reasoning. It introduces four primary evaluation dimensions: spatial understanding, attribute binding, category understanding, and reasoning. To assess these dimensions, we design two evaluation methods based on Multimodal Large Language Models (MLLMs): an instance-level pipeline for fine-grained semantic understanding, and a feedback-based reasoning pipeline that enables step-by-step causal assessment for more accurate evaluation. UI2V-Bench includes approximately 500 carefully constructed text–image pairs and evaluates a range of both open source and closed-source I2V models across all defined dimensions. We further incorporate human evaluations, which show strong alignment with the proposed MLLM-based metrics. Overall, UI2V-Bench fills a critical gap in I2V evaluation by emphasizing semantic comprehension and reasoning ability, offering a robust framework and dataset to support future research and model development in the field.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：生成式扩散模型发展迅速，图像到视频（Image-to-Video, I2V）生成已成为视频合成领域的重要方向。
- **现存问题**：已有的 I2V 评估基准主要聚焦于生成视频的质量（如画质、流畅度）和时间一致性，但严重忽略了两个关键能力：
  - 模型对输入图像中**具体主体（specific subject）语义**的理解能力；
  - 生成视频是否符合**物理规律和人类常识**。
- **核心动机**：现有评估体系无法衡量 I2V 模型是否真正“看懂”了输入图像，也无法判断生成的动态过程是否物理合理，这阻碍了模型语义理解能力的提升。
- **整体含义**：论文提出 **UI2V-Bench**——一个以**语义理解与推理能力**为核心的 I2V 评估基准，旨在填补现有评估体系在语义与物理常识维度的空白，为 I2V 模型的发展提供更全面的评测工具。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：将 I2V 模型的评估从“画质导向”转向“理解导向”，重点考察模型对输入图像内容的**深层语义理解**与**因果推理**能力。
- **四大评估维度**：
  1. **空间理解（Spatial Understanding）**：模型能否正确理解并保持物体间的空间位置关系；
  2. **属性绑定（Attribute Binding）**：模型能否将颜色、形状、材质等属性准确绑定到正确的主体上；
  3. **类别理解（Category Understanding）**：模型能否正确识别图像中主体的类别并生成相应语义一致的动态；
  4. **推理（Reasoning）**：模型能否基于常识和物理规律对场景的未来演化进行合理推断。
- **两种评估方法（基于多模态大语言模型 MLLM）**：
  1. **实例级管道（Instance-level Pipeline）**：针对单个测试实例进行细粒度的语义理解评估，逐项核查生成视频是否满足语义要求；
  2. **基于反馈的推理管道（Feedback-based Reasoning Pipeline）**：采用逐步因果评估的方式，通过多轮反馈与推理对生成结果进行更精确的判断，适合评估复杂推理类任务。
- **数据集构建**：构建了约 **500 个精心设计的文本-图像对**，每个测试项都明确对应某一评估维度，保证评测覆盖的全面性和针对性。

## 3. 实验设计：数据集、基准与对比方法

- **数据集**：论文自建的 UI2V-Bench 数据集，包含约 500 个手工设计的文本-图像对（text-image pairs），覆盖四个评估维度。
- **评估基准**：UI2V-Bench 本身即为提出的新基准，采用基于 MLLM 的自动评估管道为主要评估手段。
- **评估对象**：涵盖多种 **开源与闭源（open-source and closed-source）I2V 模型**，覆盖当前主流 I2V 生成方法。
- **人类评估**：额外引入了人类评估（human evaluation），用于验证 MLLM 自动评估指标的可靠性，比较两者的对齐程度。
- **说明**：文中未具体列出参与评测的模型名称清单、各维度得分对比结果等细节，但明确指出评估跨所有定义维度完成。

## 4. 资源与算力

- **文中未明确说明**：摘要和元数据中均未提及训练或评估所使用的 GPU 型号、数量、训练时长、总计算量等具体算力信息。
- **说明**：由于 UI2V-Bench 属于评估基准而非模型训练工作，其核心成本可能主要在数据集构建和 MLLM 推理评估上，但文中未提供相应量化数据。

## 5. 实验数量与充分性

- **实验规模**：
  - 数据集规模约 500 个测试对，覆盖四个维度；
  - 评估了多种开源和闭源 I2V 模型；
  - 加入了人类评估作为对照。
- **充分性分析**：
  - **积极方面**：四个维度的划分较为系统，多模型对比加上人类评估，使基准具有初步的可信度和覆盖度；
  - **局限性**：从摘要来看，论文未展示详细的消融实验（如各评估管道单独效果的对比）、未报告每个维度上的模型表现差异分析，也未说明 500 个样本在各维度上的分布是否均衡；因此实验的**粒度与细节仍有不足**，难以完全判断各评估方法和维度的独立有效性。

## 6. 论文的主要结论与发现

- **基准有效性**：UI2V-Bench 能有效评估 I2V 模型在语义理解与物理常识方面的能力，填补了现有评估体系的空白。
- **指标一致性**：提出的基于 MLLM 的自动评估指标与人类评估结果**表现出较强的一致性**，说明 MLLM 评估管道具有较高的可靠性。
- **模型差异**：评测揭示了不同 I2V 模型在语义理解维度上的能力差异，证明仅靠视频质量和时间一致性无法全面反映模型水平。
- **价值贡献**：为 I2V 领域提供了一个以语义理解和推理为核心的**评测框架与数据集**，可支持未来模型研发和评估标准建设。

## 7. 优点

- **问题定位精准**：识别出 I2V 评估中被普遍忽视的语义理解和物理常识维度，切入点新颖且有实际意义。
- **评估维度系统化**：四个维度覆盖了从低级属性到高级推理的多层次语义理解能力，结构清晰完整。
- **评估方法有创新**：提出实例级和反馈式推理两种互补的 MLLM 评估管道，兼顾细粒度判断与因果推理评估。
- **人工验证充分**：纳入人类评估并对齐 MLLM 指标，增强了基准的可信度与客观性。
- **覆盖面较好**：同时评估开源和闭源模型，样本数量约 500 对，在保证质量的同时具备一定规模。

## 8. 不足与局限

- **实验细节披露不足**：摘要中未给出具体评估模型清单、各维度详细结果以及消融实验，难以评估基准在实际应用中的区分度和稳定性。
- **算力信息缺失**：完全未提及数据集构建和评估过程的算力开销，不利于他人复现和成本预估。
- **数据规模有限**：500 个文本-图像对对于评估复杂 I2V 语义理解能力可能仍显不足，部分维度（尤其是推理维度）的样本量可能偏少。
- **MLLM 评估的固有偏差**：依赖 MLLM 可能引入模型自身偏见，文中未讨论 MLLM 的误判率或失败案例。
- **物理规律评估的深度未知**：摘要仅表示涉及“物理规律与常识”，但未说明如何量化物理合理性，评估深度和粒度有待明确。
- **应用限制**：作为评估基准，其适用范围受限于图像输入类 I2V 模型，对文本生成视频（T2V）等任务不适用；同时基准的长期适应性（是否能跟上快速演进的生成模型）尚未讨论。

（完）
