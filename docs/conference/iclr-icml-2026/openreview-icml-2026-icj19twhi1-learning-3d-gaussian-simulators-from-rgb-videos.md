---
title: Learning 3D-Gaussian Simulators from RGB Videos
title_zh: 从RGB视频学习3D高斯模拟器
authors: "Mikel Zhobro, Andreas René Geist, Georg Martius"
date: 2026-04-30
pdf: "https://openreview.net/pdf/9b95acfedbf37fc1df0b28904c857dfe5fb89968.pdf"
tags: ["query:phys-video"]
score: 8.0
evidence: 从RGB视频学习物理交互并将物理规律嵌入3D高斯模拟器
tldr: 视频生成模型从数据中捕获物理规律时，常面临空间一致性和物体永久性不足的问题。3DGSim提出从多视角RGB视频学习3D物理模拟器，使用MVSplat学习潜在粒子表示，Point Transformer预测粒子动力学，并结合时序合并模块与高斯泼溅渲染。通过联合训练逆渲染和动力学预测，模型能够在生成新视角视频时保持物理真实性与时空一致性，为数据驱动的物理模拟提供了新方向。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频生成模型捕获物理规律时面临空间一致性和物体永久性不足，需要直接学习物理动力学。
method: 采用MVSplat粒子表示、Point Transformer动力学预测与3D高斯渲染，端到端联合训练逆渲染和动力学模型。
result: 在物理场景中生成的新视角视频展现更好的物理一致性和物体永久性，验证了物理嵌入的有效性。
conclusion: 从RGB视频学习3D高斯模拟器为捕获真实物理并用于一致视频生成提供了可行路径。
---

## Abstract
Realistic simulation is critical for applications ranging from robotics to animation. Video generation models have emerged as a way to capture real-world physics from data, but they often face challenges in maintaining spatial consistency and object permanence, relying on memory mechanisms to compensate. As a complementary direction, we present 3DGSim, a learned 3D simulator that directly learns physical interactions from multi-view RGB videos. 3DGSim adopts MVSplat to learn a latent particle-based representation of 3D scenes, a Point Transformer for the particle dynamics, a Temporal Merging module for consistent temporal aggregation, and Gaussian Splatting to produce novel view renderings. By jointly training inverse rendering and dynamics forecasting, 3DGSim embeds physical properties into point-wise latent features. This enables the model to capture diverse behaviors, from rigid and elastic to cloth-like dynamics and boundary conditions (e.g., fixed cloth corners), while producing realistic lighting effects. We show that 3DGSim can generate physically plausible results even in out of distribution cases, e.g. ground removal or multi-object interactions, despite being trained only on single-body collisions.

---

## 论文详细总结（自动生成）

## 论文中文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：现实世界中的物理模拟对机器人、动画等领域至关重要。近年来，视频生成模型成为从数据中学习真实物理规律的一种途径，但这类方法普遍存在**空间不一致性**和**物体永久性不足**的问题，往往依赖额外的记忆机制进行补偿，难以真正内化物理规律。
- **研究动机**：为了弥补视频生成模型的不足，作者提出从**多视角 RGB 视频**出发，直接学习一个**可迭代的 3D 物理模拟器**，将物理动态嵌入显式的 3D 粒子表征中，从而在生成新视角视频时保持物理一致性和物体永久性。
- **整体含义**：这项工作开辟了一条“从视频直接学习 3D 物理模拟器”的互补路径，不再依赖隐式的像素级视频生成，而是通过可微渲染与动力学预测的联合训练，让模型理解并模拟真实世界的物理交互。

### 2. 方法论：核心思想、关键技术细节与算法流程

- **核心思想**：将物理模拟视为一个“可学习的 3D 场景动态建模”问题，通过显式的粒子表征和点云动力学模型，将物理属性（刚体、弹性、布料、边界条件等）编码到逐点潜特征中，并利用三维高斯泼溅实现可微渲染。
- **关键技术组件**：
  - **MVSplat**：用于从多视角 RGB 图像学习 3D 场景的**潜在粒子表征**，将场景表示为一系列可学习的粒子点云。
  - **Point Transformer**：作为**动力学预测网络**，在粒子表征上迭代预测下一步的粒子位置和属性变化，学习粒子间的物理交互。
  - **Temporal Merging 模块**：负责**时序一致性聚合**，确保跨时间步的粒子状态平滑且稳定地演化。
  - **Gaussian Splatting（3D 高斯泼溅）**：将预测后的粒子状态渲染为**新视角图像**，实现可微渲染，支持端到端训练。
- **训练流程**：
  1. 输入多视角 RGB 视频帧。
  2. 通过 MVSplat 提取 3D 粒子表征（逆渲染）。
  3. 利用 Point Transformer 与 Temporal Merging 对粒子动力学进行预测。
  4. 将预测的粒子状态用 Gaussian Splatting 渲染为视频帧。
  5. 联合训练逆渲染（重建损失）和动力学预测（预测损失），使潜特征自动嵌入物理属性。
- **模型能力**：能够捕捉刚体、弹性体、布料（含固定角点等边界条件）以及多物体交互等多种物理行为，并产生合理的光照效果。

### 3. 实验设计：数据集、基准与对比方法

- **数据集 / 场景**：论文摘要未给出具体数据集名称，但明确提到训练数据为**单物体碰撞**场景的**多视角 RGB 视频**，测试时包括单物体、多物体交互、地面移除等分布外场景。
- **Benchmark**：摘要未明确说明统一的公开基准，而是以**物理一致性、物体永久性、新视角合成质量**等作为评估指标。
- **对比方法**：摘要未列出具体对比方法，但针对的是视频生成模型（存在空间一致性和物体永久性不足）的互补方向，暗示与主流的视频生成模型进行对比。

### 4. 资源与算力

- **论文摘要中未提供任何关于算力、GPU 型号/数量、训练时长等具体信息。**
- 因此无法评估训练成本，需查阅全文或附录才能获取相关细节。

### 5. 实验数量与充分性

- **摘要中仅概括了实验结论，未列出具体实验组数、消融实验数量或对比实验明细。**
- 从描述看，实验至少覆盖了：
  - 单物体碰撞（训练分布内）；
  - 分布外场景：地面移除、多物体交互；
  - 多种物理行为：刚体、弹性体、布料及边界条件；
  - 新视角渲染与光照效果。
- **充分性评估**：由于摘要信息有限，无法判断实验是否完整/公平。但论文特别强调了分布外泛化能力，这在一定程度上增强了说服力。总体而言，实验设计的客观性和全面性有待全文确认。

### 6. 主要结论与发现

- 3DGSim 作为**从 RGB 视频学习 3D 高斯模拟器**的模型，能够直接学习物理交互，并在生成新视角视频时保持较好的**物理一致性**和**物体永久性**。
- 通过联合训练逆渲染和动力学预测，模型成功将物理属性嵌入点级潜特征，从而泛化到**单物体碰撞训练分布之外**的情形（如地面移除、多物体交互）。
- 该方法证明“从视频学习物理并用于一致视频生成”是一条可行且有效的路径，可作为视频生成模型的有力补充。

### 7. 优点

- **显式 3D 表征**：采用粒子 + 高斯泼溅的显式表示，解决了视频生成模型常见的物体漂移／消失问题。
- **物理属性自嵌入**：无需人工标注物理参数，通过可微渲染与动力学联合训练自动学到刚体、弹性、布料等属性。
- **时序一致性**：Temporal Merging 模块有效聚合时间信息，提升长期视频稳定性。
- **强泛化能力**：即使仅训练单物体碰撞，也能推广到多物体交互、地面移除等分布外场景，体现模型具备物理规律内化能力。
- **可微渲染闭环**：将渲染和动力学预测联合训练，形成“感知-预测-渲染”的统一框架。

### 8. 不足与局限

- **实验细节缺失**：摘要中未提供具体数据集、评估指标、基线方法、量化结果，难以全面验证其性能优势。
- **算力需求未知**：未提及训练资源，无法评估可复现性和部署成本。
- **应用范围有限**：主要面向多视角 RGB 视频，对单目视频、动态光照、复杂流体等场景可能尚不适用。
- **潜在偏差风险**：训练数据仅含单物体碰撞，尽管展示了分布外泛化，但真实世界物理场景极其多样，模型能否扩展到更复杂的接触、摩擦、流体等仍存疑。
- **长期稳定性**：虽然有时序合并模块，但粒子动力学在多步迭代后是否存在累积误差，需更长时间序列实验验证。

（完）
