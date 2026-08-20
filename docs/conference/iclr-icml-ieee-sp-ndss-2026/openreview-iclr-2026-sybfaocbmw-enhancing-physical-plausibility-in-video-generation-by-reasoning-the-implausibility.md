---
title: Enhancing Physical Plausibility in Video Generation by Reasoning the Implausibility
title_zh: 通过不合理性推理增强视频生成的物理合理性
authors: "Yutong Hao, Chen Chen, Ajmal Saeed Mian, Chang Xu, Daochang Liu"
date: 2025-09-14
pdf: "https://openreview.net/pdf?id=SYBfaOcbmw"
tags: ["query:phys-video"]
score: 9.0
evidence: 显式物理感知推理；反事实提示避免物理不合理
tldr: 扩散模型生成的视频仍常违反基本物理定律，而依赖大规模文本-视频数据隐式学习物理推理成本高且难以扩展。本文提出免训练推理框架，通过轻量物理感知推理构造编码物理违规行为的反事实提示，并提出同步解耦引导策略，在采样时引导生成远离不合理运动。该方法无需额外训练即可提升视频物理合理性，为生成模型融入物理约束提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有扩散模型隐式学习物理推理成本高，视频仍违反物理定律。
method: 构建物理违规反事实提示，采用同步解耦引导在采样时规避不合理运动。
result: 免训练框架即能提升生成视频的物理合理性。
conclusion: 为视频生成融入物理约束提供新思路。
---

## Abstract
Diffusion models can generate realistic videos, but existing methods rely on implicitly learning physical reasoning from large-scale text-video datasets, which is costly, difficult to scale, and still prone to producing implausible motions that violate fundamental physical laws. We introduce a training-free framework that improves physical plausibility at inference time by explicitly reasoning about implausibility and guiding the generation away from it. Specifically, we employ a lightweight physics-aware reasoning pipeline to construct counterfactual prompts that deliberately encode physics-violating behaviors. Then, we propose a novel *Synchronized Decoupled Guidance* (SDG) strategy, which leverages these prompts through synchronized directional normalization to counteract lagged suppression and trajectory-decoupled denoising to mitigate cumulative trajectory bias, ensuring that implausible content is suppressed immediately and consistently throughout denoising. Experiments across different physical domains show that our approach substantially enhances physical fidelity while maintaining photorealism, despite requiring no additional training. Ablation studies confirm the complementary effectiveness of both the physics-aware reasoning component and SDG. In particular, the aforementioned two designs of SDG are also individually validated to contribute critically to the suppression of implausible content and the overall gains in physical plausibility. This establishes a new and plug-and-play physics-aware paradigm for video generation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 扩散模型在视频生成方面已能生成逼真视频，但现有方法主要依赖从大规模文本-视频数据中**隐式学习**物理推理。
- 这种隐式学习方式存在三大问题：
  - 成本高昂（需要海量数据与算力）；
  - 难以扩展（物理规律的多样性和组合性难以覆盖）；
  - 生成结果仍经常违反基本物理定律，产生不合理的运动（如物体穿透、重力异常、动量不守恒等）。
- 论文的核心动机是：**在不引入额外训练的前提下，通过显式推理“物理不合理性”，并在推理阶段引导生成过程远离这些不合理内容**，从而提升生成视频的物理合理性。
- 整体含义：提出一种即插即用、无需训练的物理感知范式，为将物理约束融入视频生成模型提供了新的思路，弥补了隐式学习的不足。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
- 不再试图教模型“什么是对的物理”，而是显式推理“什么是错的物理”，然后引导生成避开这些错误。
- 采用**反事实提示**（counterfactual prompts）将物理违规行为编码进文本提示，用于在采样过程中抑制不合理运动。

### 关键技术细节

1. **轻量级物理感知推理管线**
   - 使用一个轻量级、物理感知的推理模块（可能基于预训练模型或规则）分析视频内容，识别可能违反物理规律的行为。
   - 基于识别结果构造**反事实提示**：这些提示故意描述物理违规行为（如“物体漂浮在天花板上”“球违反重力上升”），作为负样本信号。

2. **同步解耦引导（Synchronized Decoupled Guidance, SDG）**
   - 该策略包含两个互补设计，在去噪过程中联合作用：

   - **同步方向归一化（Synchronized Directional Normalization）**
     - 解决“滞后抑制”（lagged suppression）问题：传统引导可能响应延迟，导致不合理内容在早期去噪步骤未被及时压制，后期再修正效果差。
     - 通过对引导方向进行同步归一化，使不合理内容在每一步去噪中都被立即、持续地抑制。

   - **轨迹解耦去噪（Trajectory-Decoupled Denoising）**
     - 解决“累积轨迹偏差”（cumulative trajectory bias）问题：单个步骤的小偏差可能在多步去噪后累积成大误差，使生成轨迹偏离物理合理区域。
     - 通过将去噪轨迹与不合理引导轨迹解耦，避免引导信号带来的系统性偏差累积。

### 算法流程（文字说明）
1. 输入：待生成的视频文本提示、扩散模型、预训练物理感知推理模块。
2. 推理阶段：对当前生成样本进行轻量级物理感知分析，产生描述物理违规行为的反事实提示。
3. 采样过程：使用SDG策略，在每一步去噪时，结合正常提示和反事实提示计算引导方向；采用同步方向归一化确保即时抑制，采用轨迹解耦去噪防止偏差累积。
4. 输出：物理合理性增强且保持照片级真实感的视频。

## 3. 实验设计：数据集 / 场景 / benchmark / 对比方法

- **场景覆盖**：实验覆盖**多个不同的物理领域**（具体领域名称在摘要中未详细列出，但暗示包含如重力、碰撞、流体等常见物理现象）。
- **数据集 / benchmark**：论文摘要未明确给出具体数据集名称或标准benchmark，但说明在不同物理领域进行了实验。
- **对比方法**：
  - 与基线扩散模型方法对比（现有隐式学习物理的方法）。
  - 进行了**消融实验**：
    - 移除物理感知推理组件，仅用SDG；
    - 移除SDG，仅用物理感知推理；
    - 移除SDG中的两个设计之一（同步方向归一化或轨迹解耦去噪），分别验证其贡献。
- **评估指标**：虽然摘要未列出具体指标，但提到“substantially enhances physical fidelity while maintaining photorealism”，暗示同时评估物理合理性和视觉真实性。

## 4. 资源与算力

- 论文摘要和提供的元数据中**未明确说明**使用的GPU型号、数量、训练时长等算力资源。
- 由于本方法是**免训练**框架，仅需在推理阶段运行轻量级物理感知推理和SDG，因此算力开销主要集中在推理时的额外计算，但具体数值未给出。
- 需要指出：论文未提供任何资源使用细节，无法评估其计算成本的实际大小。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验：跨多个物理领域的对比实验。
  - 消融实验：至少包含三组（去推理组件、去SDG、分别去SDG的两个子设计）。
- **充分性评价**：
  - 实验覆盖了多个物理领域，且分别验证了方法论中两个核心组件（物理感知推理与SDG）的贡献，以及SDG内部两个设计的独立作用，说明消融设计较为系统。
  - 但摘要未给出数据集规模、具体数量、统计显著性、用户研究等细节，因此**实验的全面性难以完全判断**。
  - 缺乏与已有专门物理约束方法的定量对比列表，也没有说明是否在标准benchmark（如常见视频生成物理合理性评测集）上测试，故客观性和公平性证据不足。
  - 总体而言，实验设计显示出清晰的组件验证逻辑，但细节披露不足，不能称为“充分且完全客观”的实验证明。

## 6. 论文的主要结论与发现

- 提出的**免训练框架**能够显著提升生成视频的物理合理性，同时保持照片级真实感。
- 物理感知推理组件负责识别并编码物理不合理行为，SDG负责在采样时有效抑制这些行为，两者**互补**。
- SDG中的两个设计——同步方向归一化和轨迹解耦去噪——**均对抑制不合理内容和整体物理合理性提升有重要且独立的贡献**。
- 该方法无需额外训练，可作为即插即用模块应用于现有扩散视频生成模型，建立了一种新的物理感知视频生成范式。

## 7. 优点

- **创新性**：将“不合理性推理”作为显式引导信号，而非隐式学习物理规则，思路新颖。
- **免训练**：无需修改或微调生成模型，直接用于推理阶段，成本低、易于部署。
- **即插即用**：可适配不同的扩散视频生成器，具有较强通用性。
- **方法设计有针对性**：明确解决了传统引导中的滞后抑制和累积偏差两个技术难点，并给出解耦方案，技术细节扎实。
- **消融完善**：不仅验证整体组件的互补性，还单独验证了SDG内部每个子设计的必要性，增强了结论的可信度。

## 8. 不足与局限

- **信息不完整**：论文摘要和元数据未提供具体物理领域、数据集名称、评估指标、对比方法细节，导致读者难以准确评估方法的适用范围和性能水平。
- **算力信息缺失**：未说明推理时的额外计算开销，虽然免训练但实际时间复杂度未知。
- **实验充分性有限**：缺少大规模标准benchmark上的系统评测，也未见用户研究或物理规律自动判分器细节，无法确认结果是否具有统计显著性和跨场景泛化性。
- **潜在偏差风险**：物理感知推理组件本身可能引入偏见，例如对某些物理违规的识别不准确，可能导致错误引导；反事实提示的构建也依赖于手工设计或轻量模型，其鲁棒性未知。
- **应用限制**：框架主要针对去噪采样阶段，若生成模型本身对物理场景的表征能力不足，可能仍有瓶颈；且对复杂多物体交互、细粒度物理规律的支持可能有限。
- **可复现性**：由于未给出实现细节（如推理模型的具体形式、SDG的公式、超参数），难以被社区直接复现验证。

（完）
