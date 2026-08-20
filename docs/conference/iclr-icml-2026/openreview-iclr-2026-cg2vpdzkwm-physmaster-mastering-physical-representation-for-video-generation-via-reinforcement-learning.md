---
title: "PhysMaster: Mastering Physical Representation for Video Generation via Reinforcement Learning"
title_zh: PhysMaster：通过强化学习掌握物理表示用于视频生成
authors: "Sihui Ji, Xi Chen, Xin Tao, Pengfei Wan, Hengshuang Zhao"
date: 2025-09-09
pdf: "https://openreview.net/pdf?id=CG2VPDZkwM"
tags: ["query:phys-video"]
score: 9.0
evidence: 用强化学习学习物理表示并引导视频生成模型提升物理合理性
tldr: 视频生成模型虽能生成视觉真实的视频，却常违反物理规律，难以作为世界模型。PhysMaster提出通过强化学习将物理知识学习为表示，用于引导模型提升物理感知。在图像到视频任务中，PhysEncoder从输入图像提取物体相对位置和潜在交互等物理先验，并以此为条件指导模型生成物理上合理的动态。该工作为借助强化学习增强视频生成物理一致性提供了直接方法。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频生成模型常违反物理规律，需要提升物理合理性以成为世界模型。
method: 提出基于强化学习的物理表示学习框架，用PhysEncoder从输入图像编码物理先验并引导生成。
result: 在图像到视频任务中生成更符合物理的动态，提升模型的物理感知能力。
conclusion: 为用强化学习增强视频生成物理一致性提供了直接有效的方案。
---

## Abstract
Video generation models nowadays are capable of generating visually realistic videos, but often fail to adhere to physical laws, limiting their ability to generate physically plausible videos and serve as ''world models''. To address this issue, we propose PhysMaster, which captures physical knowledge as a representation for guiding video generation models to enhance their physics-awareness. Specifically, PhysMaster is based on the image-to-video task where the model is expected to predict physically plausible dynamics from the input image. Since the input image provides physical priors like relative positions and potential interactions of objects in the scenario, we devise PhysEncoder to encode physical information from it as an extra condition to inject physical knowledge into the video generation process. The lack of proper supervision on the model's physical performance beyond mere appearance motivates PhysEncoder to apply reinforcement learning with human feedback to physical representation learning, which leverages feedback from generation models to optimize physical representations with Direct Preference Optimization (DPO) in an end-to-end manner. PhysMaster provides a feasible solution for improving physics-awareness of PhysEncoder and thus of video generation, proving its ability on a simple proxy task and generalizability to wide-ranging physical scenarios. This implies that our PhysMaster, which unifies solutions for various physical processes via representation learning in the reinforcement learning paradigm, can act as a generic and plug-in solution for physics-aware video generation and broader applications.

---

## 论文详细总结（自动生成）

# PhysMaster 论文总结

## 1. 核心问题与整体含义

- **研究背景**：当前视频生成模型（如基于扩散模型的图像到视频生成器）虽然能生成视觉上高度逼真的视频，却常常违反基本物理规律（如重力、运动惯量、物体交互等）。
- **核心问题**：这种"视觉真实但物理不真实"的特性，严重限制了对物理世界有正确预测能力的视频生成模型作为"世界模型"（World Model）的潜力。
- **研究含义**：本文旨在通过强化学习（Reinforcement Learning）范式，将物理知识显式地学习为一种可引导生成的表示（representation），从而提升视频生成模型的物理感知能力（physics-awareness），使其不仅"看起来真实"，而且"动起来符合物理"。

## 2. 方法论

- **整体框架（PhysMaster）**：基于图像到视频（image-to-video）任务，要求模型从输入图像出发，预测物理上合理的动态过程。
- **核心思想**：输入图像本身蕴含丰富物理先验（如物体相对位置、潜在交互关系），若能提取并利用这些信息作为额外条件，可引导生成模型朝物理合理的方向输出。
- **物理编码器（PhysEncoder）**：专门设计一个编码器，从输入图像中编码物理信息，作为额外的条件注入视频生成过程，从而将物理知识"注入"到生成过程中。
- **强化学习与 DPO**：由于缺乏针对模型物理表现（而非单纯外观）的直接监督信号，PhysMaster 引入强化学习中的人类反馈（RLHF），并利用生成模型的反馈，通过直接偏好优化（Direct Preference Optimization, DPO）以端到端方式优化物理表示学习。
- **可插拔性**：PhysMaster 将各种物理过程（不同场景、不同物理规律）统一为表示学习问题，在强化学习范式下训练，可作为通用即插即用模块，嵌入到多种视频生成模型中。

## 3. 实验设计

- **基准任务（Proxy Task）**：论文提到在一个"简单的代理任务"（simple proxy task）上验证了 PhysMaster 的有效性——这类任务通常是能清晰体现某一物理规律（如重力下落、碰撞反弹）的简化场景，便于评估模型是否学习到了物理动态的本质。
- **泛化实验**：在代理任务之外，论文声称方法可泛化到"广泛的物理场景"（wide-ranging physical scenarios），意在展示其多场景适应能力和通用性。
- **数据集与对比方法**：论文摘要中未明确列出具体使用的数据集名称、baseline 方法（如 Sora、Gen-2 等竞品模型），也未提供定量评价指标（如 FVD、物理一致性评分等）的具体数值，因此无法从摘要层面获知实验对比的细节。

## 4. 资源与算力

- **未明确说明**：论文摘录文本中完全没有提及 GPU 型号、数量、训练时长、参数量、显存占用等算力信息。
- 如需了解训练成本、推理效率等信息，需查阅论文正文的实验设置部分（当前提供的文本中缺失）。

## 5. 实验数量与充分性

- **实验数量**：从摘要推断，至少包含一个代理任务的验证实验和一组泛化实验，但具体实验组数（如不同场景、不同 backbone、不同消融组合）无法确认。
- **充分性评估**：
  - 从**方法验证**角度看，代理任务加泛化实验的"由简到繁"设计是合理的；
  - 但从**充分性**角度看，若缺少与主流视频生成模型的系统对比、不同物理场景的定量结果、以及关键组件（PhysEncoder、DPO 策略、奖励设计等）的消融实验，则充分性难以完全判定。
  - 此外，若实验仅依赖代理论证的间接评估（或生成模型反馈），而非直接物理指标（如碰撞检测误差、轨迹偏差），则客观性有待商榷。

## 6. 主要结论与发现

- PhysMaster 通过强化学习结合 DPO 的框架，成功将物理知识编码为表示，引导视频生成模型生成物理上更合理的动态。
- 该方法在简单代理任务上得到验证，并展现出对广泛物理场景的泛化能力，说明"表示学习 + RL"范式有望统一多种物理过程的解决方案。
- 论文的核心贡献在于提供了一种利用反馈信号（而非纯像素监督）来提升生成模型物理一致性的可行、可插拔方案。

## 7. 优点

- **问题切中要害**："视觉真实但物理不真实"确实是当前视频生成领域的核心瓶颈之一，研究动机强且有实用价值。
- **方法新颖**：将强化学习（DPO）引入物理表示学习，用于优化编码器而非仅仅微调生成器，思路巧妙，跳出了单纯依赖像素级损失约束物理一致性的局限。
- **可插拔设计**：PhysEncoder 作为额外条件模块，不要求重训整个生成模型，便于嵌入现有 SOTA 视频生成架构，实用性高。
- **统一视角**：将不同物理过程统一为"表示 + RL"的框架，具有较强的通用性和理论美感。

## 8. 不足与局限

- **信息不完整**：当前论文摘要未提供足够实验细节，包括具体数据集、baseline、定量指标和算力配置，难以在摘要层面全面评估方法的相对优势和可复现性。
- **物理复杂性局限**：用"简单代理任务"表征物理合理性，可能无法充分反映真实世界中的复杂物理现象（如流体力学、柔性体形变、多物体耦合），从代理任务到通用世界模型的迁移仍存在鸿沟。
- **反馈偏差风险**：DPO 依赖生成模型反馈或人类反馈作为偏好信号，若反馈来源本身存在偏差、噪声或与物理真实性的相关性不足，可能误导物理表示学习。
- **泛化深度未知**：论文提到"泛化到广泛物理场景"，但未展示跨场景的失败案例或边界条件，泛化能力的实际边界不明确。
- **评估客观性风险**：若物理一致性的评估依赖生成模型自身或主观偏好，而非第三方物理引擎（如 MuJoCo、PhysX）的精确仿真对比，评估的公平性可能存疑。

（完）
