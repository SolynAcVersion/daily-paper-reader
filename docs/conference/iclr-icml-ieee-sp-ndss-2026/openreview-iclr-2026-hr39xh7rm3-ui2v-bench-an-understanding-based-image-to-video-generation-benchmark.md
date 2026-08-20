---
title: "UI2V-Bench: An Understanding-based Image-to-video Generation Benchmark"
title_zh: UI2V-Bench：基于理解的图像到视频生成基准
authors: "Ailing Zhang, Lina Lei, Dehong Kong, Zhixin Wang, Jiaqi Xu, Fenglong Song, Chun-Le Guo, Chang Liu, Fan Li, Jie Chen"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=hR39xH7rm3"
tags: ["query:phys-video"]
score: 9.0
evidence: 基准评测I2V模型对物理定律与常识的符合程度
tldr: 现有图像到视频（I2V）基准大多只关注画质和时间一致性，忽略了模型对输入图像语义的深层理解以及生成内容是否符合物理规律和人类常识。为此，UI2V-Bench提出了一个侧重语义理解与推理的评测基准，引入空间理解、属性绑定等多个维度。实验结果表明该基准能有效区分不同I2V模型在这类物理与语义合理性上的表现，为评测生成视频的物理正确性提供了新工具。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有I2V基准忽略语义理解和物理规律，需要新评测基准。
method: 提出UI2V-Bench，围绕空间理解与属性绑定等维度构建评测任务。
result: 该基准能有效区分模型在物理和语义合理性上的表现。
conclusion: 为图像到视频生成提供了更全面的物理与语义评测体系。
---

## Abstract
Generative diffusion models are developing rapidly and attracting increasing attention due to their wide range of applications. Image-to-Video (I2V) generation has become a major focus in the field of video synthesis. However, existing evaluation benchmarks primarily focus on aspects such as video quality and temporal consistency, while largely overlooking the model's ability to understand the semantics of specific subjects in the input image or to ensure that the generated video aligns with physical laws and human commonsense. To address this gap, we propose UI2V-Bench, a novel benchmark for evaluating I2V models with a focus on semantic understanding and reasoning. It introduces four primary evaluation dimensions: spatial understanding, attribute binding, category understanding, and reasoning. To assess these dimensions, we design two evaluation methods based on Multimodal Large Language Models (MLLMs): an instance-level pipeline for fine-grained semantic understanding, and a feedback-based reasoning pipeline that enables step-by-step causal assessment for more accurate evaluation. UI2V-Bench includes approximately 500 carefully constructed text–image pairs and evaluates a range of both open source and closed-source I2V models across all defined dimensions. We further incorporate human evaluations, which show strong alignment with the proposed MLLM-based metrics. Overall, UI2V-Bench fills a critical gap in I2V evaluation by emphasizing semantic comprehension and reasoning ability, offering a robust framework and dataset to support future research and model development in the field.

---

## 论文详细总结（自动生成）

# UI2V-Bench：基于理解的图像到视频生成基准 —— 中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- 扩散生成模型发展迅速，图像到视频（Image-to-Video, I2V）生成成为视频合成领域的重要方向。
- **现有评测基准的缺陷**：已有基准主要关注视频画质和时间一致性（如帧间平滑、运动自然度等），却忽略了两项关键能力：
  - 对输入图像中特定主体的**语义理解**能力；
  - 生成内容是否符合**物理规律和人类常识**。
- **研究缺口**：缺乏一个能系统评估I2V模型“是否真正理解图像内容并据此生成合理物理运动”的评测工具。
- **本文贡献**：提出 **UI2V-Bench**，一个以语义理解与推理为核心的I2V评测基准，填补现有评估体系的空白，为模型开发提供更全面的指导。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将I2V模型的评估从“低层视觉质量”转向“高层语义理解与物理合理性”，通过设计细粒度的评测任务来检验模型是否理解图像中的物体、空间关系、属性以及常识因果关系。
- **四个主要评测维度**：
  - **空间理解**：评估模型是否理解物体间的空间位置关系（如上下、左右、前后等）。
  - **属性绑定**：评估模型能否将颜色、形状、材质等属性正确绑定到对应物体上。
  - **类别理解**：评估模型能否正确识别输入图像中的物体类别。
  - **推理**：评估模型能否进行物理因果和常识推理（如重力、碰撞、遮挡等）。
- **两种基于多模态大语言模型（MLLM）的评估方法**：
  - **实例级流水线（Instance-level pipeline）**：对每个实例进行细粒度语义理解判断，直接检测生成视频中的语义错误。
  - **基于反馈的推理流水线（Feedback-based reasoning pipeline）**：通过逐步的因果评估，模拟人类推理过程，提升评估的准确性和可解释性。
- **评测数据**：构建了约 **500 个精心构造的文本-图像对**，每个对包含输入图像和对应的提示文本，用于触发特定维度的语义/物理测试。

## 3. 实验设计

- **数据集/场景**：论文自建的 UI2V-Bench 基准数据集，包含约500个文本-图像对，覆盖四个维度（空间理解、属性绑定、类别理解、推理）。
- **Benchmark 构成**：通过 MLLM 自动评估，并与人类评估对照。
- **对比方法**：
  - 评估了多种 **开源和闭源 I2V 模型**（具体模型名称未在摘要中列出）。
  - 使用 **人类评估** 作为基准，验证 MLLM 评估指标与人类判断的一致性。
- **评估方式**：所有模型在相同的文本-图像对上生成视频，再分别用提出的两种MLLM流水线和人类评估进行打分。

## 4. 资源与算力

- **文中未明确提及**任何具体的算力信息，例如 GPU 型号、数量、训练时长或推理资源等。
- 仅从摘要无法推断模型训练或评估所消耗的计算资源。

## 5. 实验数量与充分性

- **实验组数**：摘要仅提到在“所有定义维度”上评估了多种开源和闭源模型，但未给出具体的模型数量、视频生成数量或消融实验细节。
- **消融实验**：未提及针对评估方法本身的消融（如不同MLLM组件的影响）。
- **充分性评价**：
  - **优点**：包括人类评估对照，增强了指标可信度；覆盖四个维度，初步具备多维评估能力。
  - **不足**：由于缺少详细的实验配置、基线模型列表、统计显著性检验等，难以判断实验的全面性；且没有公开具体的失败案例或维度间的相关性分析，客观性验证不足。

## 6. 主要结论与发现

- UI2V-Bench 能有效区分不同I2V模型在语义理解和物理合理性上的表现。
- 提出的 MLLM 评估指标与人类评估结果具有**高度一致性**，说明该自动评估框架可靠。
- 现有I2V模型在语义理解和物理常识方面存在明显短板，而过去被画质/一致性指标掩盖。
- 该基准为I2V领域提供了更全面的物理与语义评测体系，有助于推动未来模型发展。

## 7. 优点（方法或实验设计的亮点）

- **填补空白**：首次系统地将“语义理解+物理常识”纳入I2V评测，超越了传统画质和时序一致性。
- **多维度设计**：空间理解、属性绑定、类别理解、推理四个维度覆盖了人类感知物理世界的关键方面。
- **双流水线评估**：实例级细粒度检测与反馈式推理评估结合，兼顾准确性、可解释性和逐步因果分析。
- **人类评估验证**：通过人类评估对齐，增强自动指标的可靠性。
- **公开性潜力**：提供约500个构造文本-图像对的数据集，可作为标准benchmark供后续研究使用。

## 8. 不足与局限

- **信息缺失**：由于提供的文本仅为摘要，缺乏方法细节、具体数据集样例、模型配置、评测代码等，难以完全复现和评判。
- **实验覆盖有限**：未说明模型是否涵盖主流最新I2V架构、多尺度分辨率、不同视频长度等；也未涉及中文或更多语言场景。
- **偏差风险**：500个样本规模相对较小，四个维度的题目分布可能不均衡；构造的文本-图像对可能引入人工设计偏差。
- **MLLM依赖**：评估结果受所选MLLM的固有偏见和错误影响，未讨论MLLM误判导致的指标噪声。
- **应用限制**：基准主要面向通用I2V生成，未针对特定领域（如医学、自动驾驶）或长视频/复杂叙事场景；物理合理性评估可能难以覆盖所有真实物理规律。

---

（完）
