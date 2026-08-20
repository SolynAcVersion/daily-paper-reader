---
title: Learning 3D-Gaussian Simulators from RGB Videos
title_zh: 从RGB视频学习3D高斯模拟器
authors: "Mikel Zhobro, Andreas René Geist, Georg Martius"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qwsCjNSHMz"
tags: ["query:phys-video"]
score: 6.0
evidence: 从多视角RGB视频学习物理交互，构建3D模拟器
tldr: 视频生成模型虽然能从数据中捕捉真实物理，但常面临空间一致性和物体持久性挑战。为此提出3DGSim，从多视角RGB视频学习潜在粒子表示，结合Point Transformer动力学预测与高斯泼溅渲染。通过联合训练逆渲染与动力学预测，3DGSim嵌入物理规律，实现了稳定的时空聚合和新视角渲染，为学习物理交互提供了新路径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视频生成模型虽能捕捉真实世界物理，但常面临空间一致性与物体持久性挑战。
method: 提出3DGSim，从多视角RGB视频学习潜在粒子表示，结合Point Transformer动力学预测与高斯泼溅渲染。
result: 通过联合训练逆渲染与动力学预测，模型嵌入物理规律，实现稳定时空聚合和新视角渲染。
conclusion: 从真实视频学习3D模拟器为捕捉物理交互提供了一条补充路径。
---

## Abstract
Realistic simulation is critical for applications ranging from robotics to animation. 
Video generation models have emerged as a way to capture real-world physics from data, but they often face challenges in maintaining spatial consistency and object permanence, relying on memory mechanisms to compensate. 
As a complementary direction, we present 3DGSim, a learned 3D simulator that directly learns physical interactions from multi-view RGB videos.
3DGSim adopts MVSplat to learn a latent particle-based representation of 3D scenes, a Point Transformer for the particle dynamics, a Temporal Merging module for consistent temporal aggregation, and Gaussian Splatting to produce novel view renderings.
By jointly training inverse rendering and dynamics forecasting, 3DGSim embeds physical properties into point-wise latent features. This enables the model to capture diverse behaviors, from rigid and elastic to cloth-like dynamics and boundary conditions (e.g., fixed cloth corners), while producing realistic lighting effects. We show that 3DGSim can generate physically plausible results even in out of distribution cases, e.g. ground removal or multi-object interactions, despite being trained only on single-body collisions.

---

## 论文详细总结（自动生成）

# 《从RGB视频学习3D高斯模拟器》论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：真实感物理模拟在机器人、动画等领域至关重要。近年来，视频生成模型成为一种从数据中学习真实世界物理的新范式，但其在推理时往往面临**空间一致性（spatial consistency）**和**物体持久性（object permanence）**的根本性挑战——模型需要依赖隐式记忆机制来补偿物体的消失或变形。
- **核心问题**：能否直接学习一个真正的3D物理模拟器，而不是依赖2D视频生成模型？即从真实捕捉的多视角RGB视频中，构建一个具备物理规律、能支持新视角渲染的3D动态场景模型。
- **整体含义**：该论文提出了一条**有别于视频生成模型**的补充路径——3DGSim，直接从多视角RGB视频学习潜在粒子表示和动力学，实现从数据到3D物理模拟器的端到端学习，从而在长时程推演和新视角合成中保持空间一致性与物体持久性。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将3D场景表示为潜在粒子系统，用神经网络学习粒子间的物理交互，并通过可微渲染（高斯泼溅）实现从潜在表示到图像的映射。整个模型以多视角RGB视频为监督信号，联合优化逆渲染（inverse rendering）和动力学预测（dynamics forecasting）。
- **整体架构由四个模块构成**：
  1. **MVSplat**——用于从多视角RGB图像学习3D场景的**潜在粒子表示（latent particle-based representation）**，为每个粒子赋予点级潜在特征。
  2. **Point Transformer**——作为**动力学预测网络**，在粒子空间上建模交互并预测下一时刻的粒子状态，从而学习物理演化规律。
  3. **Temporal Merging模块**——用于**时序上的稳定聚合**，确保跨时间步的特征一致性和平滑过渡。
  4. **Gaussian Splatting（高斯泼溅）**——作为可微渲染器，将预测得到的粒子/高斯表示渲染为**新视角图像**。
- **联合训练策略**：逆渲染模块与动力学预测模块以端到端方式联合训练，这使得物理特性（如刚性、弹性、布料行为、边界条件）被内嵌到逐点的潜在特征中，无需显式物理方程。
- **算法流程**（文字描述）：
  1. 输入多视角RGB视频帧 → 使用MVSplat提取每帧的3D潜在粒子表示；
  2. 将当前及历史粒子状态输入Point Transformer，预测下一时刻的粒子状态；
  3. 通过Temporal Merging对时序状态进行融合聚合，保持时间一致性；
  4. 将预测的粒子状态转化为3D高斯表示，经过高斯泼溅渲染出目标视角的图像；
  5. 用渲染图像与真实视频帧之间的重建损失（以及动力学一致性约束）进行联合监督，反向传播更新整个网络。

## 3. 实验设计

- **数据与场景**：论文摘要和元数据中未详细列出具体公开数据集的名称，但从描述来看，训练数据为**多视角RGB视频**，涵盖多样化的物理行为，包括：
  - 刚体碰撞
  - 弹性形变
  - 布料动力学
  - 带边界条件的场景（如布料角落被固定）
- **Benchmark与对比方法**：论文摘要未明确列明对比基线。但根据上下文，其核心对比方向应当是：
  - 与**视频生成模型**（如基于扩散或自回归的视频预测模型）在空间一致性、物体持久性上进行对比；
  - 与**传统物理模拟器**或**其他神经模拟器**在准确性、泛化能力上进行对比。
- **泛化测试（Out-of-Distribution, OOD）**：该论文特别强调了两个泛化场景：
  1. **地面移除（ground removal）**——训练中接触地面的物体在测试中移除地面后的行为；
  2. **多物体交互（multi-object interactions）**——这是OOD的核心亮点之一：**模型仅在单物体碰撞数据上训练**，却能够推广到多物体交互场景。
- 这一泛化设计表明实验重点在于验证模型是否真正学到了底层物理规律，而非单纯的记忆/插值。

## 4. 资源与算力

- **论文元数据中未明确说明**所使用的GPU型号、数量、训练时长以及总计算量。
- 仅从方法层面推测，训练涉及多视角视频渲染和逐帧粒子动力学联合优化，**计算成本预计较高**（涉及Stable Video 4D、实时渲染优化等模块），但由于原论文文本未披露，无法给出具体数字。

## 5. 实验数量与充分性评价

- **元数据提供的信息有限**，无法统计精确的实验数量（如数据集数量、消融实验组数、对比方法数量）。
- **从摘要可确认的实验设计**：
  - 主要实验场景包括刚体、弹性体、布料、边界条件等多样物理行为；
  - 泛化实验包含地面移除和多物体交互两类OOD测试；
  - 模型在**单物体碰撞训练**后能泛化到多物体交互，说明实验设计有意识地去检验物理规律学习的泛化性。
- **评价**：从有限的描述来看，实验设计在**泛化能力验证**上是有亮点且相对客观的——通过限制训练数据分布（单物体），挑战模型的物理理解能力，这比仅仅在同类分布内测试更能说明问题。但**原始论文未在元数据中展示完整的定性与定量对比结果**，例如与具体基线方法的数值对比、消融研究的细目（如去掉Point Transformer或Temporal Merging各自的影响）、不同相机视角数量对性能的影响等，因此**从本摘要文本角度无法完全判断实验充分性**。

## 6. 主要结论与发现

- 3DGSim **能够从多视角RGB视频中学习到物理上合理的3D模拟器**，实现对新行为的预测和新视角的渲染。
- 通过联合训练逆渲染和动力学预测，模型将物理属性自然嵌入点级潜在特征中，从而能够**统一捕捉刚体、弹性、布料以及边界条件等多种物理行为**。
- 关键发现：即使仅在单一物体碰撞数据上训练，模型也能在**地面移除**和**多物体交互**等分布外场景中产生物理合理的结果——这暗示模型学到的不只是表面视觉模式，而是某种通用的物理交互规律。
- 该工作为从真实视频学习3D模拟器提供了一条**补充于视频生成模型**的有效路径。

## 7. 优点

- **架构新颖**：将MVSplat（场景建模） + Point Transformer（动力学） + Temporal Merging（时序聚合） + Gaussian Splatting（渲染）组合成一个端到端的可微框架，覆盖了感知→物理→渲染的完整链路。
- **物理嵌入的设计**：不显式定义物理方程，而是通过联合训练将物理属性隐式嵌入到潜在特征中。这种设计思路简洁、通用性强，且能处理复杂边界条件。
- **优秀的泛化能力**：单物体训练→多物体推理的OOD泛化能力是该论文最大的亮点，说明模型学习到了超越训练分布的物理规律。
- **渲染效果**：高斯泼溅支持新视角渲染，并且能产生真实的光照效果（realistic lighting effects）。
- **问题定位清晰**：精准指出了视频生成模型在空间一致性和物体持久性上的缺陷，并给出了一个有说服力的替代方案。

## 8. 不足与局限

- **信息透明性不足**：论文元数据中缺乏足够的实现细节和完整的实验数据，难以对方法的稳健性和结果进行深入检验。
- **实验覆盖有限**：根据描述，训练场景集中于常规物理交互（碰撞、布料、弹性体），未提及流体的行为、复杂场景遮挡、大规模刚体集群等情况，应用范围有待拓展。
- **OOD测试仍有限**：虽然地面移除和多物体交互是很好的泛化测试，但真实世界物理复杂程度远超这些场景（如摩擦、断裂、流体力学等）。
- **3D-GS的固有缺陷**：高斯泼溅在重建时可能出现无界或模糊的高斯，影响长期动力学预测的稳定性；未提及对长期稳定性的评估。
- **潜在的暴露偏差（exposure bias）**：联合动力学预测模型在自回归推理时可能出现误差累积，论文未展示长时程推演（long-horizon rollout）的结果。
- **应用限制**：数据要求为多视角RGB视频，采集成本较高；模型的泛化能力可能受限于训练数据的物体类别和物理尺度。
- **评审结论**：该论文被ICLR-2026拒绝（score=6.0），说明虽然有一定创新性，但在实验严谨性或综述必要性等方面可能仍存在问题。

（完）
