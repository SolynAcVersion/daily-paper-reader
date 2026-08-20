---
title: "PhysMaster: Mastering Physical Representation for Video Generation via Reinforcement Learning"
title_zh: PhysMaster：通过强化学习掌握视频生成的物理表征
authors: "Sihui Ji, Xi Chen, Xin Tao, Pengfei Wan, Hengshuang Zhao"
date: 2025-09-09
pdf: "https://openreview.net/pdf?id=CG2VPDZkwM"
tags: ["query:phys-video"]
score: 10.0
evidence: 用强化学习提升视频生成的物理合理性
tldr: 视频生成模型虽能生成视觉逼真的内容，但常违反物理定律，限制了其作为世界模型的能力。该论文提出PhysMaster，通过强化学习将物理知识编码为表征，用于引导图像到视频生成模型，使其从输入图像中提取相对位置与物体交互等物理先验。PhysEncoder将物理信息编码为引导条件，增强模型对物理规律的感知，从而生成物理合理的动态。实验表明该方法能显著提升生成的物理合理性，为将强化学习用于物理感知视频生成提供了有效范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频生成模型缺乏物理感知，难以生成符合物理规律的动态。
method: 利用强化学习捕获物理知识作为表征，并设计PhysEncoder从输入图像编码物理信息以引导视频生成。
result: 显著提升图像到视频生成中的物理合理性与物理感知能力。
conclusion: 证明了强化学习能够有效赋予视频生成模型物理知识，提升其作为世界模型的潜力。
---

## Abstract
Video generation models nowadays are capable of generating visually realistic videos, but often fail to adhere to physical laws, limiting their ability to generate physically plausible videos and serve as ''world models''. To address this issue, we propose PhysMaster, which captures physical knowledge as a representation for guiding video generation models to enhance their physics-awareness. Specifically, PhysMaster is based on the image-to-video task where the model is expected to predict physically plausible dynamics from the input image. Since the input image provides physical priors like relative positions and potential interactions of objects in the scenario, we devise PhysEncoder to encode physical information from it as an extra condition to inject physical knowledge into the video generation process. The lack of proper supervision on the model's physical performance beyond mere appearance motivates PhysEncoder to apply reinforcement learning with human feedback to physical representation learning, which leverages feedback from generation models to optimize physical representations with Direct Preference Optimization (DPO) in an end-to-end manner. PhysMaster provides a feasible solution for improving physics-awareness of PhysEncoder and thus of video generation, proving its ability on a simple proxy task and generalizability to wide-ranging physical scenarios. This implies that our PhysMaster, which unifies solutions for various physical processes via representation learning in the reinforcement learning paradigm, can act as a generic and plug-in solution for physics-aware video generation and broader applications.

---

## 论文详细总结（自动生成）

# PhysMaster 论文总结

## 1. 核心问题与研究动机

- **背景**：当前视频生成模型已能生成视觉上高度逼真的视频内容，但其生成结果常常违反基本物理定律（如重力、运动惯性、碰撞守恒等），导致视频动态不具备物理合理性。
- **核心问题**：现有视频生成模型缺乏对物理规律的内在感知与表征能力，限制了其作为“世界模型”（World Model）的应用潜力——即无法基于静态输入预测符合物理法则的未来动态。
- **研究意义**：如何让视频生成模型具备物理感知能力，是提升生成视频可信度、推动视频生成走向通用世界模型的关键一步。

## 2. 方法论：PhysMaster

- **总体思路**：以图像到视频生成（Image-to-Video）为任务载体，通过强化学习将物理知识编码为可引导生成的表征，使生成模型在预测动态时具备物理先验。
- **核心组件：PhysEncoder**
  - 从输入图像中提取物理先验信息（如物体相对位置、潜在交互关系等）。
  - 将这些物理信息编码为额外的引导条件（condition），注入到视频生成过程中，增强模型对物理规律的感知。
- **关键机制：强化学习 + DPO**
  - 由于缺乏对模型“物理表现”的直接监督（传统损失仅关注外观），作者引入强化学习与人类反馈机制。
  - 利用生成模型自身的反馈信号，通过**Direct Preference Optimization（DPO）** 以端到端方式优化物理表征学习，避免依赖人工标注的物理评分。
- **方法定位**：PhysMaster 将各种物理过程统一为表征学习问题，可作为即插即用的通用模块，适配广泛的物理场景。

## 3. 实验设计

- **代理任务**：论文在一个简单代理任务上验证了物理表征学习的有效性，但具体任务细节（如具体物理情境）在现有资料中未明确展开。
- **泛化验证**：进一步验证了方法在广泛物理场景中的泛化能力，表明该方法不止适用于单一任务。
- **对比方法**：现有资料未列出具体对比基线，无法确认对比的详细方法集合。

## 4. 资源与算力

- 论文资料中**未明确说明**具体的 GPU 型号、数量、训练时长或总计算量（FLOPs），无法评估其算力开销。

## 5. 实验数量与充分性

- **实验组数**：从资料看，至少包含一组代理任务验证和一组泛化性实验；但**消融实验**、多数据集验证、与基线方法的系统对比等细节均未见于当前资料。
- **充分性评估**：由于实验细节披露极为有限，难以判断实验是否充分、客观和公平。当前信息只能说明方法在若干场景下有效，但缺乏对方法各组件贡献的定量拆解。

## 6. 主要结论与发现

- PhysMaster 能够**显著提升**图像到视频生成中的物理合理性和物理感知能力。
- 证明了**强化学习范式可以有效赋予视频生成模型物理知识**，使其在作为世界模型方面展现出更强的潜力。
- 通过表征学习统一各类物理过程，PhysMaster 可以作为通用、即插即用的解决方案，适用于物理感知视频生成及更广泛的应用。

## 7. 方法亮点

- **新颖的方法路线**：将强化学习引入物理表征学习，是对传统监督学习范式的有效补充，解决物理表现缺乏直接监督的难题。
- **端到端优化**：DPO 策略使得物理表征学习与视频生成联合优化，无需额外的人工物理标注。
- **即插即用性**：PhysEncoder 作为额外条件注入生成过程，不破坏原有生成架构，具备良好的兼容性和推广潜力。
- **通用性设计**：以表征学习统一不同类型的物理过程，避免了为每种物理场景单独设计模型的高成本。

## 8. 不足与局限

- **实验细节严重不足**：目前可获得的资料未提供足够的数据集描述、基线对比、消融实验等关键信息，难以独立验证方法的有效性和优势来源。
- **评估标准不透明**：如何量化“物理合理性”这一指标在资料中未明确说明，存在评估主观性或偏差的风险。
- **算力成本未知**：未报告训练资源，难以评估方法在实际应用中的可负担性。
- **场景覆盖有限**：代理任务与真实复杂物理世界之间仍有距离，对极端物理场景（如流体力学、柔性体形变等）的适应能力尚未验证。
- **强化学习的潜在不稳定性**：利用生成模型反馈进行 DPO 优化，可能受限于生成模型自身的偏差，存在反馈信号噪声或偏好偏差的风险，但该问题在原文中未见充分讨论。

（完）
