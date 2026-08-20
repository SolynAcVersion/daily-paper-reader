---
title: "3DPhysVideo: 3D Scene Reconstruction and Physical Animation Leveraging a Video Generation Model via Consistency-Guided Flow SDE"
title_zh: 3DPhysVideo：利用一致性引导流SDE的视频生成模型实现3D场景重建与物理动画
authors: "Hwidong Kim, Yunho Kim, Tae-Kyun Kim"
date: 2025-09-03
pdf: "https://openreview.net/pdf?id=8TgzLrWgrk"
tags: ["query:phys-video"]
score: 9.0
evidence: 免训练流程，利用视频生成模型重建3D场景并生成物理真实的动态视频
tldr: 视频生成模型常产生违背真实物理动态的视觉伪影，已有方法如PhysGen3D在流体建模与真实感上仍有不足。3DPhysVideo提出免训练流程，复用现成视频模型作为新视角合成器，通过约束引导流SDE重建360度3D场景几何，并生成物理真实的动态视频。该方法能处理流体动力学等复杂物理效果，提升从单张图像生成视频的物理合理性与真实感，为物理动画生成提供高效方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频生成模型常产生违反真实物理动态的伪影，现有方法对流体动力学与真实感建模仍有不足。
method: 3DPhysVideo采用免训练流程，将现成视频模型复用为新视图合成器，用约束引导流SDE重建三维几何并生成物理动画。
result: 实验证明该方法能生成物理真实、包含流体效果的单图视频动画，优于已有物理生成方法。
conclusion: 该工作为单图物理动画提供免训练新途径，同时改善物理合理性、三维重建与真实感。
---

## Abstract
Video generative models have made remarkable progress, yet they often yield visual artifacts that violate grounding in real-world physical dynamics. Recent works such as PhysGen3D tackle single image-to-3D physics through mesh reconstruction and Physically-Based Rendering, but challenges remain in modeling fluid dynamics and photorealism. This work introduces 3DPhysVideo, a novel training-free pipeline that generates physically realistic videos from a single image. We repurpose an off-the-shelf video model for two stages. First, we use it as a novel view synthesizer to reconstruct complete 360-degree 3D scene geometry by guiding the image-to-video (I2V) flow model with rendered point clouds derived from an initial 3D estimation. Second, after applying Material Point Method (MPM) physics simulation to this geometry, the simulated point cloud is used to guide the same I2V flow model to synthesize final, high-quality videos. Consistency-Guided Flow SDE, which decomposes the predicted velocity of the I2V flow model into denoising and consistency bias, allows us to effectively repurpose the model for both 3D reconstruction and simulation-guided video generation. Our method successfully bridges the gap from single-images to physically plausible videos  while remaining efficient to run on a single consumer gpu. In the extensive experiments, our approach outperforms state-of-the-art baselines on both GPT-based evaluations and VideoPhy physics-consistency benchmark, across diverse scenarios including single-object, multi-object, and fluid interaction sequences.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：视频生成模型虽然取得了显著进展，但经常生成违反真实物理动态的视觉伪影，例如物体运动不符合重力、碰撞或流体行为不自然。
- **已有方法的不足**：现有工作如 PhysGen3D 通过网格重建和物理渲染（PBR）来生成单图到 3D 的物理动画，但在流体动力学建模和照片级真实感方面仍存在明显短板。
- **核心问题**：如何从单张静态图像出发，高效生成既具备 3D 场景一致性、又符合真实物理规律的动态视频？
- **整体含义**：论文旨在弥合“单张图像”与“物理合理的动态视频”之间的鸿沟，提出一种无需训练、可在单张消费级 GPU 上运行的端到端方案。

## 2. 论文提出的方法论

- **核心思想**：复用现成的视频生成模型（图像到视频，I2V）作为核心引擎，通过“约束引导流 SDE”将其同时用于 3D 场景重建和物理仿真引导的视频生成，从而避免额外训练专用模型。
- **技术流程**分为两个阶段：
  1. **3D 场景重建阶段**：先对输入单图进行初始 3D 估计，渲染得到点云；然后利用该点云引导 I2V 流模型合成新视角图像，逐步重建完整的 360 度 3D 场景几何。
  2. **物理仿真与视频生成阶段**：对重建的 3D 几何施加物质点法（Material Point Method, MPM）物理仿真，模拟刚体、软体及流体等物理行为；将仿真后的点云作为引导条件，输入同一个 I2V 流模型，合成最终的高质量、物理合理的动态视频。
- **关键技术细节**：
  - 采用 **Consistency-Guided Flow SDE**，将 I2V 流模型预测的速度分解为“去噪分量”和“一致性偏置”两个部分，从而实现对模型的灵活复用，既支持新视图合成，也支持仿真引导生成。
  - 全过程无需训练，仅利用现有预训练模型，保证了高效性。
- **公式/算法流程**（文字描述）：
  - 输入单张图像 → 初始深度/几何估计 → 渲染点云 → 以点云为条件引导 I2V 模型生成多个新视角 → 融合重建完整 3D 场景；
  - 对场景进行 MPM 物理仿真（如重力、碰撞、流体运动）→ 得到逐帧物理状态点云；
  - 将每帧仿真点云作为引导输入，通过一致性引导流 SDE 控制 I2V 模型生成对应帧的视频内容，最终合成物理动画。

## 3. 实验设计

- **使用的数据集/场景**：涵盖多种场景类型，包括：
  - 单物体（single-object）场景；
  - 多物体（multi-object）交互场景；
  - 流体交互（fluid interaction）序列。
- **Benchmark**：使用了 **VideoPhy 物理一致性基准**，同时采用 **GPT-based 评估**（利用大型语言模型/视觉模型进行自动化质量评估）。
- **对比方法**：与现有最先进的方法（如 PhysGen3D 等）进行对比，评估物理合理性、3D 重建质量和视觉真实感等指标。

## 4. 资源与算力

- 摘要中明确提到：方法“**efficient to run on a single consumer gpu**”，即可在单张消费级 GPU 上运行。
- 但论文内容（仅摘要）中 **未明确给出 GPU 具体型号**（如 RTX 3090/4090）、**数量**（单卡）、**训练时长**（由于是免训练方法，推理时间也未提及）等详细信息。
- 因此，关于精确算力配置和耗时，需要查阅论文全文或附录才能获得更完整数据。

## 5. 实验数量与充分性

- 公开信息中提及的实验覆盖了**三类场景**（单物体、多物体、流体交互），并在 **VideoPhy 基准** 和 **GPT-based 评估** 上进行了对比。
- 关于**消融实验**：当前内容未明确列出消融研究（如对 Consistency-Guided Flow SDE 各分量、点云引导的作用等），但作为 ICLR 投稿论文，通常会在全文包含消融分析，本总结受限于可见文本无法确认。
- **充分性评价**：
  - 场景多样性较好，覆盖了从刚体到流体的复杂物理现象；
  - 评估方式结合了自动化基准（VideoPhy）和 GPT-based 主观/语义评估，具有一定客观性；
  - 但未提供人类用户研究、定量指标数值（如成功率、误差）、以及跨不同视频生成模型的泛化测试，因此严格意义上实验充分性有待全文验证。
  - 对比方法是否包含足够强的基线（如 PhysGen3D）以及是否所有对比方法在同样的输入和计算约束下运行，也需要全文确认。

## 6. 论文的主要结论与发现

- 3DPhysVideo 成功地将单张图像转换为物理合理的动态视频，同时保持 3D 场景几何的一致性和视觉真实感。
- 通过复用现成视频生成模型，结合 Consistency-Guided Flow SDE，能够在**无需训练**的情况下完成 3D 重建和物理动画生成，显著降低了计算成本。
- 在多个场景和基准上，该方法**优于现有的 SOTA 基线**，尤其是在流体动力学建模和照片级真实感方面，弥补了 PhysGen3D 等方法的不足。

## 7. 优点

- **免训练设计**：无需额外训练专用模型，直接复用强大的预训练视频生成模型，实用性和可推广性强。
- **统一框架**：同一视频模型同时承担新视角合成和物理引导视频生成两个任务，通过 SDE 分解优雅地实现了模型功能复用。
- **物理仿真真实**：采用 MPM 方法模拟连续介质（尤其适合流体），比传统网格/刚体模拟更擅长处理大变形和流体动力学。
- **完整的 3D 重建**：利用视频模型生成多视角信息，重建 360 度场景几何，而非仅是单视角深度估计，提升了后续物理仿真的空间一致性。
- **计算效率高**：单张消费级 GPU 即可运行，具备实际部署价值。
- **评估较全面**：覆盖单物体、多物体、流体交互等多样场景，并使用物理基准和 GPT 评估，角度较丰富。

## 8. 不足与局限

- **信息不完整**：本总结基于摘要和元数据，无法获取完整的实验细节、超参数、消融结果和失败案例。
- **潜在偏差风险**：
  - GPT-based 评估可能受预训练模型中语言/视觉偏置影响，未必能完全反映真实物理精确性；
  - 视频生成模型本身存在幻觉倾向，即使有引导也可能在某些极端情况下输出不合理物理现象。
- **物理精度有限**：MPM 仿真简化和引导方式可能无法精确模拟复杂接触、多物体碰撞或流体飞溅的细粒度细节，真实物理准确性仍有上限。
- **通用性未知**：方法对输入图像的类型（自然图像、合成图像、透明物体、复杂光照等）的鲁棒性尚未在摘要中说明。
- **算力细节缺失**：未提供 GPU 型号、推理耗时、内存占用等量化指标，影响复现和公平对比的可验证性。
- **应用限制**：单图输入的固有信息不足可能导致重建的 3D 几何存在歧义，后续仿真和视频生成可能因此产生误差。

（完）
