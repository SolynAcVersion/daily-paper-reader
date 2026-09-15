---
title: Towards One-step Causal Video Generation via Adversarial Self-Distillation
title_zh: 面向一步因果视频生成的对抗自蒸馏
authors: "Yongqi Yang, Huayang Huang, Xu Peng, Xiaobin Hu, Donghao Luo, Jiangning Zhang, Chengjie Wang, Yu Wu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=P3O0fNmnWa"
tags: ["query:video-gen-rl"]
score: 6.0
evidence: 分布匹配蒸馏对齐去噪步的分布
tldr: 混合视频生成模型结合自回归时序动态与扩散空间去噪，但其串行迭代特性导致误差累积与推理缓慢。本文提出面向高效因果视频生成的蒸馏框架，基于分布匹配蒸馏（DMD）并引入对抗自蒸馏策略，在分布层面将学生模型n步去噪的输出与n+1步版本对齐，从而提供更平滑的监督。该方法在极少去噪步数下实现高质量一步因果视频生成，兼顾效率与质量。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 混合自回归扩散视频模型串行迭代导致误差累积与推理缓慢。
method: 基于分布匹配蒸馏提出对抗自蒸馏，在分布层面把n步去噪输出与n+1步对齐。
result: 在极少去噪步数下实现高质量的一步因果视频生成。
conclusion: 为高效因果视频生成提供了分布层面的蒸馏监督新思路。
---

## Abstract
Recent hybrid video generation models combine autoregressive temporal dynamics with diffusion-based spatial denoising, but their sequential, iterative nature leads to error accumulation and long inference times. In this work, we propose a distillation-based framework for efficient causal video generation that enables high-quality synthesis with extreme limited denoising steps. Our approach builds upon Distribution Matching Distillation (DMD) framework and proposes a novel form of Adversarial Self-Distillation (ASD) strategy, which aligns the outputs of the student model's $n$-step denoising process with its $(n+1)$-step version in the distribution level. This design provides smoother supervision by bridging small intra-student gaps and more informative guidance by combining teacher knowledge with locally consistent student behavior, substantially improving training stability and generation quality in extremely few-step scenarios. In addition, we present a First-Frame Enhancement (FFE) strategy, which allocates more denoising steps to the initial frames to mitigate error propagation while applying larger skipping steps to later frames. Extensive experiments on VBench demonstrate that our method surpasses state-of-the-art approaches in both one-step and two-step video generation. Notably, our framework produces a single distilled model that flexibly supports multiple inference-step settings, eliminating the need for repeated re-distillation and enabling efficient, high-quality video synthesis.

---

## 论文详细总结（自动生成）

# 论文总结：Towards One-step Causal Video Generation via Adversarial Self-Distillation

> 说明：提供的 PDF 正文提取结果为“no healthy upstream”，未能获取论文全文。以下总结主要依据论文摘要与元数据字段（标题、TLDR、motivation、method、result、conclusion）整理；凡涉及训练细节、实验组数、算力等信息，若原文未在可用内容中披露，均会明确标注为“未说明/无法确认”。

## 1. 核心问题与整体含义

- **研究背景**：近期混合视频生成模型将**自回归时序动态**与**扩散式空间去噪**结合，以兼顾时序因果建模和空间生成质量。
- **核心问题**：这类模型具有串行、迭代的生成特性，导致两个突出问题：
  - **误差累积**：自回归逐步生成时，早期错误会向后传播。
  - **推理缓慢**：扩散去噪需要多步迭代，难以满足高效生成需求。
- **整体含义**：论文试图通过蒸馏框架，在**极少去噪步数**甚至**一步生成**条件下，实现高质量因果视频生成，从而同时改善效率与质量。
- **目标定位**：面向高效因果视频生成，提出新的蒸馏监督思路，减少推理步数并保持生成质量。

## 2. 方法论

### 核心思想

- 基于 **Distribution Matching Distillation, DMD** 框架，提出 **Adversarial Self-Distillation, ASD**。
- ASD 的关键是：将学生模型 **n 步去噪输出**与**n+1 步版本**在**分布层面**进行对齐。
- 该设计不是单纯依赖教师模型监督，而是利用学生模型自身不同去噪步数之间的小差距，形成更平滑的监督信号。
- 通过结合**教师知识**与**学生局部一致行为**，为极少步场景提供更有信息量的引导，提升训练稳定性和生成质量。

### 关键技术细节

- **对抗自蒸馏 ASD**：
  - 在分布层面对齐学生模型 n 步与 n+1 步去噪结果。
  - 利用学生自身不同步数版本之间的差距，作为额外监督。
  - 摘要称该策略能桥接学生内部的小差距，并提升极少步训练稳定性。
- **首帧增强 First-Frame Enhancement, FFE**：
  - 为初始帧分配更多去噪步数，以缓解自回归生成中的误差传播。
  - 对后续帧采用更大的跳步策略，从而降低整体推理成本。
- **单一模型多步支持**：
  - 训练得到的单个蒸馏模型可灵活支持多种推理步数设置。
  - 无需针对不同步数重复再蒸馏。

### 算法流程的文字说明

1. 在 DMD 蒸馏框架下训练学生视频生成模型。
2. 对同一学生模型获取 n 步去噪输出与 n+1 步去噪输出。
3. 在分布层面匹配二者，构造自蒸馏监督信号。
4. 结合教师知识与学生自身局部一致性，形成对抗式自蒸馏训练目标。
5. 在推理阶段使用首帧增强策略，对初始帧分配更多去噪步，对后续帧采用更大跳步。
6. 最终模型可在一步、两步等不同推理步数下灵活使用。

> 注：摘要未给出具体损失函数、网络结构、对抗判别器形式或完整训练算法，因此无法进一步展开公式细节。

## 3. 实验设计

- **数据集 / 场景**：
  - 主要使用 **VBench** 进行实验。
  - 任务场景为**因果视频生成**，重点评估**一步生成**与**两步生成**。
- **Benchmark**：
  - **VBench**。
- **对比方法**：
  - 摘要声称方法在一步和两步视频生成上**超越 state-of-the-art approaches**。
  - 但可用文本中**未列出具体基线方法名称**，也未给出具体指标数值。
- **评估设置**：
  - 一步视频生成。
  - 两步视频生成。
- **消融实验**：
  - 从摘要推断，ASD 与 FFE 可能是关键组件。
  - 但可用内容中**未说明具体消融实验数量、配置和结果**。

## 4. 资源与算力

- 可用摘要与元数据中**未提及**以下信息：
  - GPU 型号、数量；
  - 训练时长；
  - 模型参数量；
  - 训练数据规模；
  - 推理硬件与效率指标。
- 因此，**无法总结论文使用的算力资源**，需查阅全文或补充材料。

## 5. 实验数量与充分性

- 从可用信息看，实验主要围绕 **VBench** 上的**一步与两步视频生成**展开。
- 摘要声称超过 SOTA，但未提供：
  - 具体基线数量；
  - 不同数据集或场景的扩展实验；
  - 消融实验组数；
  - 统计显著性、人工评估或用户研究；
  - 公平性设置，如是否控制模型规模、训练数据、推理预算等。
- 因此，**无法判断实验数量是否充分、对比是否完全公平**。
- 仅从摘要层面看，实验设计直接针对核心主张，但全文缺失导致无法核实充分性。

## 6. 主要结论与发现

- **ASD 有效**：在分布层面将学生 n 步去噪输出与 n+1 步版本对齐，可提供更平滑监督，提升极少步场景下的训练稳定性和生成质量。
- **FFE 有效**：对初始帧分配更多去噪步，可缓解自回归误差传播；对后续帧增大跳步，有利于效率。
- **性能表现**：在 VBench 上，一步和两步视频生成均超过当时 SOTA 方法。
- **多步兼容**：单个蒸馏模型即可灵活支持多种推理步数，无需重复再蒸馏。
- **总体意义**：为高效因果视频生成提供了“分布层面蒸馏监督”的新思路。

## 7. 优点

- **问题重要**：针对混合自回归 + 扩散视频模型的误差累积与推理缓慢问题，具有实际应用价值。
- **方法有新意**：提出对抗自蒸馏，利用学生模型自身 n 步与 n+1 步的分布差距，而非仅依赖教师监督。
- **多步兼容性强**：一个蒸馏模型支持多种推理步数，减少重复训练成本，实用性较高。
- **首帧增强策略合理**：针对因果视频生成中早期帧影响后续帧的特点，设计 FFE 缓解误差传播。
- **极端少步场景**：聚焦一步、两步生成，符合高效视频生成的发展方向。

## 8. 不足与局限

- **全文不可得导致无法全面评估**：PDF 提取失败，本文总结只能基于摘要和元数据，无法验证方法细节与实验完整性。
- **算力与训练成本未披露**：未说明 GPU 型号、数量、训练时长、数据规模等，难以评估可复现性与实际成本。
- **实验覆盖有限**：目前仅知在 VBench 上评估，未说明是否覆盖长视频、高分辨率、复杂运动、物理一致性等场景。
- **基线信息不足**：未列出具体对比方法、指标数值和统计显著性，无法判断 SOTA 声明是否充分公平。
- **消融细节缺失**：ASD 与 FFE 的各自贡献、超参数敏感性、不同步数配置等未在可用内容中说明。
- **潜在训练稳定性风险**：虽然摘要称 ASD 改善稳定性，但对抗式训练本身可能引入不稳定，需全文证据支持。
- **应用限制未知**：对真实世界视频、开放域生成、多模态条件生成等泛化能力尚未说明。

（完）
