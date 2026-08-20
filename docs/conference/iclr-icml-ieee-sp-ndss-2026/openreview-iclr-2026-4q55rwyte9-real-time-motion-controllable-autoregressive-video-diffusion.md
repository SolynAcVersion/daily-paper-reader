---
title: Real-Time Motion-Controllable Autoregressive Video Diffusion
title_zh: 实时运动可控的自回归视频扩散
authors: "Kesen Zhao, Jiaxin Shi, Beier Zhu, Junbao Zhou, Xiaolong Shen, Yuan Zhou, Qianru Sun, Hanwang Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=4Q55RwYte9"
tags: ["query:phys-video"]
score: 6.0
evidence: 使用强化学习改善视频生成中的运动质量，对物理合理性RL改进有借鉴作用
tldr: 实时运动可控的视频生成面临双向扩散延迟和自回归少步生成伪影等挑战。本文提出AR-Drag，首个RL增强的少步自回归视频扩散模型，先微调基础模型支持运动控制，再用轨迹奖励的强化学习优化，并通过Self-Rollout保持马尔可夫性。在图像到视频生成中实现实时控制与多样运动，减少了运动伪影，为结合RL提升视频生成运动合理性提供了可迁移方法。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 双向扩散模型延迟高且缺少有效的自回归方法，现有自回归视频扩散模型在少步生成中存在质量下降和运动伪影问题。
method: 提出AR-Drag，首个RL增强的少步自回归视频扩散模型，先微调基础I2V模型支持运动控制，再用基于轨迹奖励的强化学习进一步提升。
result: 实现实时图像到视频生成与多样化运动控制，减少运动伪影并保持质量。
conclusion: 通过强化学习与自回归架构结合，为实时运动可控的视频生成提供新方案。
---

## Abstract
Real-time motion-controllable video generation remains challenging due to the inherent latency of bidirectional diffusion models and the lack of effective autoregressive (AR) approaches. Existing AR video diffusion models are limited to simple control signals or text-to-video generation, and often suffer from quality degradation and motion artifacts in few-step generation. To address these challenges, we propose AR-Drag, the first RL-enhanced few-step AR video diffusion model for real-time image-to-video generation with diverse motion control. We first fine-tune a base I2V model to support basic motion control, then further improve it via reinforcement learning with a trajectory-based reward model. Our design preserves the Markov property through a Self-Rollout mechanism and accelerates training by selectively introducing stochasticity in denoising steps. Extensive experiments demonstrate that AR-Drag achieves high visual fidelity and precise motion alignment, significantly reducing latency compared with state-of-the-art motion-controllable VDMs, while using only 1.3B parameters.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

> **论文标题**：Real-Time Motion-Controllable Autoregressive Video Diffusion（实时运动可控的自回归视频扩散）  
> **作者**：Kesen Zhao, Jiaxin Shi, Beier Zhu, Junbao Zhou, Xiaolong Shen, Yuan Zhou, Qianru Sun, Hanwang Zhang  
> **来源**：ICLR 2026（已录用）

---

## 1. 核心问题与整体含义

- **研究动机**：实时、运动可控的视频生成在交互式内容创作中具有重要应用价值，但当前技术面临双重瓶颈：
  - **双向扩散模型（bidirectional diffusion models）** 虽然生成质量高，但推理延迟大，难以满足实时交互需求；
  - **现有自回归（AR）视频扩散模型** 要么仅支持简单的控制信号，要么局限于文本到视频生成，缺乏对多样化运动控制的支持。
- **关键挑战**：自回归方式下进行少步（few-step）生成时，视频质量显著下降，并容易出现运动伪影（motion artifacts），严重影响生成结果的物理合理性和视觉自然度。
- **核心问题**：能否构建一个**实时**、**支持多样化运动控制**、且**保持高视觉质量**的自回归视频生成模型？
- **整体意义**：该研究探索了将强化学习（RL）与自回归视频扩散架构相结合的新范式，为实时运动可控视频生成提供了一条可迁移的技术路径，尤其对提升视频生成中的运动质量与物理合理性具有重要参考价值。

---

## 2. 提出的方法论：AR-Drag

### 核心思想
- 提出 **AR-Drag**，据作者称是**首个** RL 增强的少步自回归视频扩散模型，面向实时图像到视频（I2V）生成任务，支持多样化运动控制。
- 总体思路分为两个阶段：（1）先通过微调使基础模型具备运动控制能力；（2）再利用强化学习进一步优化运动质量。

### 关键技术细节

**阶段一：基础模型微调**
- 以一个基础 I2V 视频扩散模型为底座，通过微调使其支持基本的运动控制信号（如拖拽轨迹等）。

**阶段二：强化学习优化**
- 引入**基于轨迹（trajectory）的奖励模型**，通过 RL 对生成结果进行进一步优化，以增强运动控制的精确性和运动的自然性。

**Self-Rollout 机制**
- 设计了一种 **Self-Rollout** 机制，在自回归生成过程中保持**马尔可夫性质（Markov property）**，确保每一步生成只依赖于当前状态，从而减少误差累积，稳定自回归生成过程。

**训练加速**
- 通过**选择性地在去噪步骤中引入随机性（stochasticity）**，在不牺牲生成质量的前提下加速训练过程，提升训练效率。

### 公式/算法流程（文字说明）
1. 输入：一张起始图像 + 运动控制信号（如轨迹点）；
2. 将基础 I2V 扩散模型微调为支持运动条件输入的少步自回归生成器；
3. 在训练阶段，模型通过自回归方式逐步生成后续视频帧；
4. 对生成的完整视频轨迹计算奖励（如运动对齐度和视觉质量）；
5. 利用强化学习（如策略梯度类方法）更新模型参数，最大化期望奖励；
6. 通过 Self-Rollout 保持每步生成的马尔可夫性，防止长序列生成中的误差累积；
7. 选择性去噪随机性控制训练稳定性与效率。

---

## 3. 实验设计

> ⚠️ **说明**：由于本次仅获取到论文的摘要与元数据，以下信息基于摘要内容的推断，具体实验细节需查阅全文。

- **任务场景**：图像到视频（I2V）生成，支持多样化运动控制（如拖拽轨迹控制）。
- **数据集**：摘要中未明确列出所使用的具体数据集名称，需查阅全文确认。
- **Benchmark**：与当前最先进的运动可控视频扩散模型（SOTA motion-controllable VDMs）进行对比。
- **对比方法**：摘要中未列出具体对比方法名称，仅提及与 SOTA 方法对比。
- **评估维度**：
  - 视觉保真度（visual fidelity）
  - 运动对齐精度（motion alignment）
  - 推理延迟（latency）

---

## 4. 资源与算力

- 摘要和元数据中**未明确说明**使用的 GPU 型号、数量、训练时长等算力信息。
- 仅提到模型参数量为 **1.3B**，相对于当前主流视频扩散模型（通常数十亿甚至更大）属于轻量级，这本身暗示了较低的资源需求。
- 如需更具体的算力信息（如 GPU 卡数、训练时间），需要查阅论文全文的实验设置部分。

---

## 5. 实验数量与充分性

- 摘要中指出进行了 **"Extensive experiments"（大量实验）**，覆盖图像到视频生成、运动控制质量、延迟对比等维度。
- 但**缺乏具体实验细节**，无法判断：
  - 具体使用了多少个数据集；
  - 是否包含消融实验（如对 Self-Rollout 机制、选择性随机性的消融）；
  - 对比方法是否全面、基线选择是否公平；
  - 是否有人工评估（user study）等。
- **总体判断**：从摘要可见实验覆盖了主要技术指标（质量、运动对齐、延迟），但实验的充分性和公平性需要阅读全文后进一步评估。

---

## 6. 主要结论与发现

1. **实时性**：AR-Drag 显著降低了推理延迟，实现了实时的图像到视频生成。
2. **运动控制能力**：支持多样化的运动控制信号，运动对齐精度优于现有方法。
3. **视觉质量**：在少步自回归生成条件下仍能保持较高的视觉保真度，减少了运动伪影。
4. **轻量高效**：仅用 1.3B 参数即可超越更大型的 SOTA 方法，体现了良好的效率-质量平衡。
5. **方法论价值**：证明了 RL 与自回归视频扩散结合的有效性，为后续研究提供了新方向。

---

## 7. 优点

- **问题定位精准**：准确抓住了双向扩散延迟大和 AR 方法少步生成质量差这两个核心痛点。
- **方法创新性强**：首次将 RL 引入少步自回归视频扩散模型，弥补了现有 AR 方法在运动控制上的空白。
- **Self-Rollout 机制**：通过保持马尔可夫性质来维持生成稳定性，是一个设计巧妙的技术贡献。
- **训练加速策略**：选择性去噪随机性的引入体现了对训练效率的考量。
- **轻量高效**：1.3B 参数在视频生成领域属于较小规模，却实现了超越 SOTA 的效果，实用价值高。
- **实时性突破**：为视频生成从离线走向实时交互迈出了重要一步。

---

## 8. 不足与局限

- **实验信息不足**（基于当前摘要）：具体数据集、基线方法、消融实验等细节未披露，难以全面评估实验的覆盖面和公平性。
- **参数量与可扩展性**：1.3B 虽小但在高分辨率、长视频生成上的表现未知。
- **通用性**：方法在 I2V 任务上验证有效，但对其他视频生成任务（如 text-to-video、视频编辑、多对象运动控制）的泛化能力尚不明确。
- **物理合理性**：摘要中提到减少了运动伪影，但未明确涉及深层物理合理性（如重力、碰撞等物理规律的遵循），这也是视频生成领域普遍面临的挑战。
- **实时性边界**："实时"的实现是否依赖于特定硬件条件（如高端 GPU）尚不明确。
- **应用风险**：视频生成技术可能涉及深度伪造（deepfake）等伦理安全问题，论文是否讨论了相关风险未知。

---

（完）
