---
title: Self-Refining Video Sampling
title_zh: 自精炼视频采样
authors: "Sangwon Jang, Taekyung Ki, Jaehyeong Jo, Saining Xie, Jaehong Yoon, Sung Ju Hwang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/7247a3a140d0d6053ef9efb55873879757557b3a.pdf"
tags: ["query:phys-video"]
score: 8.0
evidence: 通过自精炼采样提升生成视频的物理真实感
tldr: 论文针对视频生成器物理动态不真实的问题，提出自精炼采样方法。该方法将预训练生成器解释为去噪自编码器，在推理阶段进行迭代式内部循环精炼，并通过不确定性感知策略选择性地精炼区域，避免过度精炼产生伪影。实验显示该方法无需外部验证器或额外训练，即能提升物理真实感与细粒度运动质量，为视频生成提供了轻量级改进途径。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频生成器在复杂物理动态上仍欠缺真实感，现有外部验证器或额外训练代价高且捕捉细粒度运动有限。
method: 将预训练视频生成器视为去噪自编码器，在推理时进行内循环自精炼，并用不确定性感知策略选择区域精炼以避免伪影。
result: 无需外部验证器或额外训练，即可提升生成视频的物理真实感与细粒度运动质量。
conclusion: 为提升视频生成物理真实性提供了一种简单且自包含的推理时优化方法。
---

## Abstract
Modern video generators still struggle with complex physical dynamics, often falling short of physical realism. Existing approaches address this using external verifiers or additional training on augmented data, which is computationally expensive and still limited in capturing fine-grained motion. In this work, we present self-refining video sampling, a simple method that uses a pre-trained video generator trained on large-scale datasets as its own self-refiner. By interpreting the generator as a denoising autoencoder, we enable iterative inner-loop refinement at inference time without any external verifier or additional training. We further introduce an uncertainty-aware refinement strategy that selectively refines regions based on self-consistency, which prevents artifacts caused by over-refinement. Experiments on state-of-the-art video generators demonstrate significant improvements in motion coherence and physics alignment, achieving over 70% human preference compared to the default sampler and guidance-based sampler.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：现代视频生成模型在生成复杂物理动态（如物体交互、运动轨迹、力学规律）时，仍普遍存在物理真实性不足的问题——生成结果在视觉上可能流畅，但在物理层面却不合常理。
- **现有方案的局限**：已有的改进方法通常依赖外部验证器（external verifiers）对生成结果进行评估和修正，或使用增强数据对模型进行额外训练。这些方案存在共同短板：
  - **计算成本高昂**：引入额外模块或训练流程显著增加资源开销。
  - **细粒度运动捕捉有限**：外部验证器往往难以感知精细的物理运动细节，修正能力受限。
- **整体意义**：针对上述问题，作者提出一种**自包含、推理时（inference-time）优化**的方法，仅凭预训练生成器自身即可提升生成视频的物理真实感，无需外部验证器、无需额外训练，为视频生成物理一致性提供了轻量级且通用的改进思路。

## 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：将**预训练的视频生成器本身视为一个去噪自编码器（denoising autoencoder）**，使其在推理阶段充当自己的“精炼器”（self-refiner），从而实现自精炼闭环。
- **关键技术细节**：
  1. **迭代式内部循环精炼（iterative inner-loop refinement）**：在推理时，通过内循环机制反复对生成结果进行去噪/重构式优化，使采样过程逐步逼动物理一致性更好的解。
  2. **不确定性感知的精炼策略（uncertainty-aware refinement）**：基于自一致性（self-consistency）判断哪些区域需要被精炼，仅对高不确定性区域进行选择性精炼，避免对已经合理的区域过度处理。
  3. **防止过精炼伪影**：选择性精炼策略的核心目的之一是防止“over-refinement”导致的伪影（artifacts），即反复精炼反而破坏原本良好的生成结果。
- **算法流程（文字说明）**：
  - 输入：预训练视频生成器、初始采样视频。
  - 将生成器重新解释为去噪自编码器，建立内部去噪循环。
  - 在推理阶段执行迭代式内循环：每轮精炼中，计算生成结果各区域的自我一致性/不确定性，识别需要修正的区域，仅对这些区域施加精炼操作。
  - 重复迭代直到满足终止条件，输出最终精炼后的视频。
- **核心优势**：方法为**无需额外训练、无需外部模块**的即插即用式推理增强方案，适用范围可推广到多种现有视频生成器。

## 3. 实验设计

- **基准（Benchmark）**：
  - 使用当前最先进的视频生成器（state-of-the-art video generators）作为实验基础模型。
  - 评估维度涵盖**运动连贯性（motion coherence）** 与**物理对齐（physics alignment）**。
- **对比方法**：
  - 默认采样器（default sampler）。
  - 基于引导的采样器（guidance-based sampler）。
  - 以及本文提出的自精炼采样方法。
- **人类偏好评估**：采用人工评测（human preference）作为主要评估手段之一，衡量生成结果的真实感与质量。
- **具体数据集/场景细节**：摘要与元数据中未明确列出使用的具体数据集名称、视频领域类别或场景枚举，但可推断实验面向通用视频生成任务中的物理动态场景（如物体运动、交互等）。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长等算力细节。
- 由于该方法的核心优势之一在于**无需额外训练**，推理时精炼的额外开销相比训练是大幅降低的，但具体推理耗时、GPU占用等量化数据在提供的材料中未给出。
- 需要指出的是：对算力资源的完整评估需要查阅论文原文的实验设置部分。

## 5. 实验数量与充分性

- **实验数量**：提供的材料中明确提到的实验结果有限，主要有以下组成：
  - 在多个最新视频生成器上的对比实验（相对于默认采样器和引导式采样器）。
  - 人类偏好评测（报告了超过70%的偏好率）。
  - 消融/分析方面未在摘要中明确列出，但从“不确定性感知策略”这一设计来看，应有相应的消融分析，只是当前材料未详述。
- **充分性评估**：
  - **优点**：对比了默认采样器和引导采样器，并引入人工评测，具有一定说服力；超过70%的人工偏好率是较强的量化信号。
  - **不足**：当前提供的元数据与摘要信息有限，无法判断是否覆盖了足够多的数据集、视频类别、模型规模或多样化的物理场景；对于不确定性感知策略的消融、不同迭代次数的效果、失败案例分析等细节未见。
  - **客观性/公平性风险**：未明确说明人类评测的具体人数、评分协议、随机化方式等，难以完全判断评测的客观性和公平性。

## 6. 主要结论与发现

- 通过自精炼采样方法，**无需外部验证器或额外训练**，即能显著提升预训练视频生成器的：
  - **运动连贯性（motion coherence）**
  - **物理对齐（physics alignment）**
- 在人类偏好评测中，相比默认采样器和引导式采样器，该方法获得了**超过70%的偏好率**，说明用户可感知的真实感提升明显。
- **结论**：这是一种简单、自包含、推理期有效的物理真实性增强方案，对现有视频生成器具有即插即用式的改进潜力。

## 7. 优点

- **方法设计亮点**：
  - **自包含**：无需外部验证器，无需额外训练，显著降低了工程落地成本。
  - **原理清晰**：将生成器重新解释为去噪自编码器，为推理时优化提供了坚实的理论抓手。
  - **选择性精炼**：不确定性感知策略解决/缓解了过度精炼导致伪影的问题，方法精细度较高。
  - **通用性强**：可适配多种现有预训练视频生成器，具有较好的推广潜力。
- **实验亮点**：
  - 以人工偏好作为主要评估指标，贴近真实用户感知。
  - 同时对比默认采样器和引导式采样器两种基线，验证了方法相对于常规采样的优势。

## 8. 不足与局限

- **实验覆盖不足（基于现有材料判断）**：
  - 未明确列示所使用的具体数据集、视频类型（如人物动作、物理模拟场景、卡通/写实等）以及生成器的具体型号与规模。
  - 缺乏对不确定性感知策略的详细消融分析（如与全局精炼、随机区域精炼的对比）验证其必要性。
  - 未报告定量指标（如FVD、IS等）与物理一致性自动评估指标的对比，仅以人工偏好作为支撑。
- **偏差风险**：
  - 人类评测的协议细节（评测人数、评分标准、样本数量、统计显著性检验）不明，存在主观偏差可能。
  - 超过70%偏好率是否能推广到所有视频类别/场景尚不清楚，可能在特定物理场景（如刚体碰撞、流体模拟等）效果存在差异。
  - 不同生成器架构对自精炼的适配程度可能不同，跨模型泛化性证据有限。
- **应用限制**：
  - 推理时迭代精炼会增加推理计算延迟，对实时生成场景可能不友好。
  - 对于生成器本身能力不足的物理现象（如模型从未见过的复杂物理规则），自精炼能否真正“补足”物理知识存疑——它更多是在现有生成分布的约束内做一致性优化，而非注入新的物理知识。
  - 不确定性估计的可靠性直接影响精炼效果，在低质量生成器上可能失效或引入新伪影。

（完）
