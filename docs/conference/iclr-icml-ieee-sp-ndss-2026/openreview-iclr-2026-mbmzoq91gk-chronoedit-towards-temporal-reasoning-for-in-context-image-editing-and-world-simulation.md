---
title: "ChronoEdit: Towards Temporal Reasoning for In-Context Image Editing and World Simulation"
title_zh: ChronoEdit：面向上下文图像编辑与世界模拟的时间推理
authors: "Jay Zhangjie Wu, Xuanchi Ren, Tianchang Shen, Tianshi Cao, Kai He, Yifan Lu, Ruiyuan Gao, Enze Xie, Shiyi Lan, Jose M. Alvarez, Jun Gao, Sanja Fidler, Zian Wang, Huan Ling"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=MbMzoQ91Gk"
tags: ["query:phys-video"]
score: 9.0
evidence: 明确关注编辑中的物理一致性，并利用视频模型隐式物理
tldr: 图像编辑与上下文生成常忽略物理一致性，导致对象在编辑后不连贯。ChronoEdit将图像编辑视为视频生成问题，把输入图和编辑图作为首尾帧，利用大规模预训练视频生成模型捕获的运动与交互隐式物理规律，并引入时间推理机制确保物体跨帧连贯。该方法面向世界模拟任务，在保持外观一致性的同时显著提升物理合理性。这表明将编辑任务转化为视频生成并配合时间推理，是保证物理一致性的有效途径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有编辑模型难以保证编辑对象在时间上的物理一致性与连贯性，制约了世界模拟应用。
method: ChronoEdit将图像编辑重构为视频生成，把首尾帧作为视频起止，并利用视频模型的时间一致性与时间推理增强物理合理性。
result: 在图像编辑与世界模拟任务中，编辑对象的物理一致性与时间连贯性显著提升。
conclusion: 通过时间推理和视频生成范式，可有效解决编辑场景中的物理一致性问题。
---

## Abstract
Recent advances in large generative models have greatly enhanced both image editing and in-context image generation, yet a critical gap remains in ensuring physical consistency, where edited objects must remain coherent. This capability is especially vital for world simulation related tasks. In this paper, we present ChronoEdit, a framework that reframes image editing as a video generation problem. First, ChronoEdit treats the input and edited images as the first and last frames of a video, allowing it to leverage large pretrained video generative models that capture not only object appearance but also the implicit physics of motion and interaction through learned temporal consistency. Second, ChronoEdit introduces a temporal reasoning stage that explicitly performs editing at inference time. Under this setting, target frame is jointly denoised with reasoning tokens to imagine a plausible editing trajectory that constrains the solution space to physically viable transformations. The reasoning tokens are then dropped after a few steps to avoid the high computational cost of rendering a full video. To validate ChronoEdit, we introduce PBench-Edit, a new benchmark of image–prompt pairs for contexts that require physical consistency, and demonstrate that ChronoEdit surpasses state-of-the-art baselines in both visual fidelity and physical plausibility. Project page for code and models: https://research.nvidia.com/labs/toronto-ai/chronoedit

---

## 论文详细总结（自动生成）

# ChronoEdit：面向上下文图像编辑与世界模拟的时间推理

## 1. 核心问题与研究动机

- 尽管大规模生成模型在图像编辑与上下文图像生成上取得显著进展，但仍存在一个关键缺口：**物理一致性**。即编辑后的物体必须在时间上保持连贯、符合现实物理规律，例如运动轨迹、交互方式、形变过程等。
- 该能力对**世界模拟**类任务尤其重要，因为这类任务要求模型不仅生成静态合理的图像，还要能预测和呈现动态演化过程中的物理合理性。
- 现有编辑方法通常只关注外观或语义匹配，忽视了时间维度上的物理约束，导致编辑结果在连续帧中可能出现不连贯、不符合直觉的物理行为。

## 2. 方法论

- **核心思想**：将图像编辑重构为视频生成问题，从而借助大规模预训练视频生成模型隐式学到的物理规律和时序一致性。
- **关键技术细节**：
  - 将输入图像和编辑后的图像分别视为视频的**首帧和末帧**，构建一个完整的视频生成任务。
  - 利用预训练视频模型捕捉物体外观之外的运动与交互中的隐式物理，依靠其时间一致性机制约束编辑过程。
  - 引入**时间推理阶段**：在推理时显式执行编辑，将目标帧与**推理标记（reasoning tokens）** 联合去噪，想象出一条合理的编辑轨迹，从而将解空间限制在物理可行的变换范围内。
  - 推理标记在若干步后被**丢弃**，以避免渲染完整视频带来的高计算成本，实现效率与质量的平衡。

## 3. 实验设计

- 作者提出并使用了新的基准 **PBench-Edit**：包含需要物理一致性的图像-提示对，用于评估模型在物理合理性上的表现。
- 对比方法：与当前最先进的（state-of-the-art）图像编辑与上下文生成基线进行对比。
- 评估维度：**视觉保真度**（visual fidelity）和**物理合理性**（physical plausibility）两个主要方面。

## 4. 资源与算力

- 论文提供的元数据和摘要中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力信息。
- 仅能推断该方法依赖大规模预训练视频生成模型，推理阶段采用了“先联合去噪、后丢弃推理标记”的策略来降低计算开销，但具体硬件资源未披露。

## 5. 实验数量与充分性

- 从摘要看，实验包括：新基准构建（PBench-Edit）、与 SOTA 基线的对比、在视觉保真度与物理合理性上的量化评估。
- 摘要未列出具体实验组数、消融研究的详细数量或细分场景，因此**无法精确判断实验的全面性**。
- 总体而言，实验设计具有明确针对性（物理一致性），但公开信息有限，无法充分评估其在不同编辑类型、不同物理场景下的泛化能力与公平性细节。

## 6. 主要结论与发现

- ChronoEdit 在图像编辑与世界模拟任务中，显著提升了编辑对象的物理一致性和时间连贯性。
- 实验表明，该方法在视觉保真度和物理合理性上均优于现有最先进基线。
- 结论：通过将图像编辑转化为视频生成，并引入时间推理，可以有效解决编辑场景中的物理一致性问题。

## 7. 优点

- **范式创新**：将图像编辑与视频生成统一，利用视频模型已有的时间一致性能力，思路新颖且自然。
- **物理合理性**：明确针对现有编辑模型的痛点（物理不一致），提出显式时间推理机制，具有较强的实际价值。
- **计算效率设计**：推理标记在早期步骤后丢弃，避免了完整视频生成的高开销，兼顾质量与成本。
- **基准贡献**：提出 PBench-Edit 基准，为后续研究提供了针对物理一致性的评测工具。

## 8. 不足与局限

- **信息不透明**：摘要未提供算力、训练细节、完整实验配置，难以复现或对比成本。
- **实验范围限制**：仅提及“与 SOTA 对比”，未展示在不同任务类型（如多物体交互、复杂物理场景、长视频）上的细分结果，可能缺乏广泛覆盖。
- **依赖预训练视频模型**：方法的物理合理性上限受限于所用视频生成模型的隐式物理知识，对于极端或罕见物理规律可能仍无法保证。
- **推理策略的鲁棒性**：丢弃推理标记后，后续去噪过程如何维持物理轨迹的稳定性尚需更多实验验证。
- **评价指标**：物理合理性本身难以用单一指标衡量，基准的客观性和全面性有待进一步论证。

（完）
