---
title: Learning to Generate Object Interactions with Physics-Guided Video Diffusion
title_zh: 通过物理引导的视频扩散学习生成物体交互
authors: "David Romero, Ariana Bermudez, Hao Li, Fabio Pizzati, Ivan Laptev"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=vrY91av397"
tags: ["query:phys-video"]
score: 9.0
evidence: 物理引导的视频扩散，从单张图像和速度生成真实刚体交互与控制
tldr: 针对视频生成中物体交互缺乏物理合理性的问题，提出KineMask物理引导视频扩散方法。给定单张图像与物体速度，该方法通过两阶段策略生成推断运动与未来交互，支持刚体控制与物理效果，为世界模型和机器人决策提供了可实时控制的物理感知生成手段。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 当前视频生成模型仍难以生成物理上合理的物体交互，且缺乏物理引导的控制机制。
method: 采用两阶段物理引导视频扩散，从单张图像和速度推断刚体运动与相互作用的视觉生成。
result: 实现对生成物体交互的物理可控，生成运动符合刚体动力学并在多场景中表现稳健。
conclusion: 为物理引导的视频扩散建模与可控交互生成建立了新框架。
---

## Abstract
Recent models for video generation have achieved remarkable progress and are now deployed in film, social media production, and advertising. Beyond their creative potential, such models also hold promise as world simulators for robotics and embodied decision making. Despite strong advances, however, current approaches still struggle to generate physically plausible object interactions and lack physics-grounded control mechanisms. To address this limitation, we introduce KineMask, an approach for physics-guided video generation that enables realistic rigid body control, interactions, and effects. Given a single image and a specified object velocity, our method generates videos with inferred motions and future object interactions. We propose a two-stage training strategy that gradually removes future motion supervision via object masks. Using this strategy we train video diffusion models (VDMs) on synthetic scenes of simple interactions and demonstrate significant improvements of object interactions in real scenes. Furthermore, KineMask integrates low-level motion control with high-level textual conditioning via predictive scene descriptions, leading to effective support for synthesis of complex dynamical phenomena. Extensive experiments show that KineMask achieves strong improvements over recent models of comparable size. Ablation studies further highlight the complementary roles of low- and high-level conditioning in VDMs. Our code, model, and data will be made publicly available

---

## 论文详细总结（自动生成）

## 论文总结：KineMask——物理引导的视频扩散模型

### 1. 论文的核心问题与整体含义（研究动机与背景）

- **研究动机**：尽管视频生成模型在电影、社交媒体和广告等领域已取得显著进展，并有望成为机器人学与具身决策的“世界模拟器”，但现有方法仍难以生成**物理上合理的物体交互**，且缺乏**基于物理的生成控制机制**。
- **核心问题**：如何让视频扩散模型在生成物体交互时遵循真实物理规律，同时具备可控性。
- **整体含义**：论文提出的 KineMask 方法填补了物理感知视频生成与控制之间的空白，为视频生成从“视觉逼真”迈向“物理可信”提供了新方向，也为机器人与世界模型提供了可实时控制的物理感知生成手段。

### 2. 论文提出的方法论：核心思想、关键技术

- **核心思想**：通过物理引导的视频扩散，从**单张输入图像**与**指定的物体速度**生成包含真实刚体运动、交互与物理效应的视频。
- **两阶段训练策略**：
  - 阶段一：在合成场景中训练视频扩散模型（VDM），使用含完整未来运动信息的监督信号；
  - 阶段二：逐步移除未来运动的监督，通过**物体掩码（object masks）**作为辅助条件，使模型学会在缺乏完整轨迹标注的情况下推断和生成合理的交互运动。
- **多层次条件控制**：
  - **低层控制**：直接指定物体速度等物理量，实现对运动的细粒度控制；
  - **高层控制**：通过**预测性场景描述（predictive scene descriptions）** 提供文本条件，将物理控制与语义描述结合，支持复杂动力学现象的合成。
- **算法流程**：输入单张图像 + 物体速度 → 经两阶段训练的扩散模型生成视频 → 输出包含推断运动与未来交互的帧序列。

### 3. 实验设计：数据集、基准、对比方法

- **训练数据**：在**合成场景**上训练，场景包含简单的刚体交互（如碰撞、堆叠等）。
- **评估场景**：在**真实场景**中展示生成物体交互的显著改进，验证模型从合成到真实的泛化能力。
- **基准与对比**：与近期**同规模（comparable size）视频扩散模型**进行了大量对比实验。
- **消融研究**：对高层文本条件与低层物理条件的贡献进行消融分析。
- **说明**：文中未明确给出具体数据集名称、benchmark 标准或对比方法列表，细节有限。

### 4. 资源与算力

- **未明确说明**：论文中**未披露**所使用的 GPU 型号、数量、训练时长等算力信息。
- 因此，无法评估其计算成本或复现门槛。

### 5. 实验数量与充分性

- **实验数量**：论文声称进行了“大量实验（Extensive experiments）”，包括多场景真实图像测试与消融分析，但未列出具体实验次数。
- **充分性评估**：
  - 从报告内容看，实验覆盖了**合成训练 → 真实测试**迁移、**同类模型对比**以及**消融研究**三个维度，设计较完整。
  - **但存在不足**：缺乏对失败案例的分析、缺乏与最强 baseline 的系统性统计比较；基于合成数据训练的泛化能力与物理准确性有待更严格验证；消融实验的具体设置和量化结果也未在现有材料中给出。

### 6. 论文的主要结论与发现

- KineMask 能够生成**物理上合理的刚体交互**，并在真实场景中优于近期同等规模的视频扩散模型。
- **低层物理控制与高层文本条件具有互补作用**：两者结合可更有效地支持复杂动态现象的合成。
- 两阶段训练策略（逐步移除未来运动监督）能有效训练模型在缺乏完整物理标注的情况下学习物理交互。
- 为物理引导视频扩散建模与可控交互生成建立了新的框架。

### 7. 优点：方法与实验设计亮点

- **物理可控性**：通过指定速度实现刚体运动的低层控制，直接回应了视频生成中“缺乏物理引导控制”的核心痛点。
- **两阶段训练**：从全监督到弱监督的平滑过渡，缓解了真实视频中物理标注稀缺的问题。
- **分层条件建模**：将速度控制（物理）与场景描述（语义）统一到同一扩散框架中，兼顾控制精度与生成多样性。
- **合成到真实的迁移**：在合成数据上训练，在真实场景中验证，展示了较强的泛化能力。
- **开放性**：代码、模型与数据将公开，便于后续研究复现与扩展。

### 8. 不足与局限

- **信息缺失**：论文正文未提供完整的实验细节（具体数据集、评估指标、GPU 资源、训练时间等），且当前只有摘要与元数据可用，难以全面验证其声明的可靠性。
- **物理范围有限**：方法聚焦于**刚体交互**，对流体、弹性体、软体等复杂物理现象可能不适用。
- **偏差风险**：在合成场景上训练可能引入合成到真实的分布偏差，真实场景中的物理精度仍需更广泛的测试。
- **控制粒度**：仅以速度作为物理引导条件，可能难以应对更精细的交互（如接触力、摩擦力、变形等）。
- **可扩展性**：方法是否适用于高分辨率、长时间跨度、多物体复杂交互场景尚不明确。

（完）
