---
title: "MoSA: Motion-Coherent Human Video Generation via Structure-Appearance Decoupling"
title_zh: MoSA：基于结构-外观解耦的运动连贯人体视频生成
authors: "Haoyu Wang, Hao Tang, Donglin Di, Zhilu Zhang, Wangmeng Zuo, Feng Gao, Siwei Ma, Shiliang Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=JKIa2rTxdB"
tags: ["query:phys-video"]
score: 8.0
evidence: 通过结构-外观解耦避免生成视频中物理不合理的人体运动
tldr: 现有视频生成模型在合成复杂人体运动时往往出现物理不合理和结构不连贯。MoSA 将生成过程解耦为结构生成与外观生成：先由 3D 结构 Transformer 从文本生成运动序列，再据此合成外观。实验证明该方法能更好地生成全身运动、长程动态以及人-环境交互，提升物理合理性和结构连贯性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频生成模型偏重外观保真，合成复杂人体运动时易产生不现实、物理不合理且结构不连贯的问题。
method: 将人体视频生成解耦为结构生成与外观生成，先用 3D 结构 Transformer 生成运动序列，再据此引导视频外观合成。
result: 实验表明该方法能合成复杂、长程且包括人-环境交互的人体运动，提升物理合理性和结构连贯性。
conclusion: 结构-外观解耦有效改善人体视频生成的运动连贯性与物理合理性。
---

## Abstract
Existing video generation models predominantly emphasize appearance fidelity while exhibiting limited ability to synthesize complex human motions, such as whole-body movements, long-range dynamics, and fine-grained human–environment interactions. This often leads to unrealistic or physically implausible movements with inadequate structural coherence. To conquer these challenges, we propose MoSA, which decouples the process of human video generation into two components, i.e., structure generation and appearance generation. MoSA first employs a 3D structure transformer to generate a human motion sequence from the text prompt. The remaining video appearance is then synthesized under the guidance of this structural sequence. We achieve fine-grained control over the sparse human structures by introducing Human-Aware Dynamic Control modules with a dense tracking constraint during training. The modeling of human–environment interactions is improved through the proposed contact constraint. Those two components work comprehensively to ensure the structural and appearance fidelity across the generated videos. This paper also contributes a large-scale human video dataset, which features more complex and diverse motions than existing human video datasets. We conduct comprehensive comparisons between MoSA and a variety of approaches, including general video generation models, human video generation models, and human animation models. Experiments demonstrate that MoSA substantially outperforms existing approaches across the majority of evaluation metrics.

---

## 论文详细总结（自动生成）

## MoSA：基于结构-外观解耦的运动连贯人体视频生成

### 1. 论文的核心问题与整体含义

- **背景**：现有视频生成模型在合成人体运动时，普遍将重心放在外观保真（appearance fidelity）上，即生成画面“看起来像什么”，而对于人体运动的物理合理性和结构连贯性关注不足。
- **核心问题**：当面对复杂的人体运动——如全身运动（whole-body movements）、长程动态（long-range dynamics）、以及细粒度的人-环境交互（fine-grained human–environment interactions）时，现有模型生成的结果往往出现物理上不合理（physically implausible）、结构不连贯（inadequate structural coherence）的运动。
- **整体含义**：运动是否合理是人体视频生成区别于一般视频生成的核心瓶颈。该论文指出，单纯提升外观生成能力无法解决结构层面的缺陷，需要显式地对人体运动结构进行建模，再以结构引导外观生成，从而从“画面真实”走向“运动真实”。

### 2. 论文提出的方法论

- **核心思想**：将人体视频生成过程**解耦为结构生成（structure generation）与外观生成（appearance generation）两个独立阶段**，以“先定运动骨架，再丰富视觉细节”的方式替代传统的端到端外观优先生成范式。
- **第一模块：3D 结构 Transformer（3D Structure Transformer）**
  - 负责从文本提示（text prompt）生成一段人体运动序列，即决定“人怎么动”。
  - 以 3D 结构信息为基础，保证生成的运动在骨骼关节层面具有物理合理性和时间连续性。
- **第二模块：外观生成（Appearance Generation）**
  - 在运动结构序列的引导下，合成视频中的外观内容（纹理、光照、背景等）。
  - 将外观生成建立在已确定的结构之上，从而避免结构与外观之间的冲突。
- **关键技术一：Human-Aware Dynamic Control 模块**
  - 用于对稀疏的人体结构进行细粒度控制（fine-grained control）。
  - 训练过程中引入**密集跟踪约束（dense tracking constraint）** ，强化结构序列对画面像素的引导能力。
- **关键技术二：接触约束（Contact Constraint）**
  - 针对人-环境交互场景，当人体与场景物体发生接触（如抓取、坐、靠）时，显式约束接触点的位置与时间对齐，从而提升交互动作的物理合理性。
- **算法流程概括**：文本输入 → 3D 结构 Transformer 生成运动序列 → 在外观生成阶段以结构序列为引导，施加 Human-Aware Dynamic Control（含密集跟踪约束）和接触约束 → 输出运动连贯、结构合理、外观逼真的视频。

### 3. 实验设计

- **数据集**：论文贡献了一个**大规模人体视频数据集**，其特点是包含比现有公开人体视频数据集更复杂、更多样的运动类型。
- **Benchmark 设定**：以文本提示为条件，评估生成视频的运动合理性、结构连贯性及外观保真度。
- **对比方法**：实验覆盖面广，包含三类对比对象：
  - 通用视频生成模型（general video generation models）
  - 人体视频生成模型（human video generation models）
  - 人体动画模型（human animation models）
- **评估方式**：在大多数评估指标上与上述三类方法进行系统比较。

### 4. 资源与算力

- 摘要与元数据中**未明确披露** GPU 型号、数量、训练时长、参数量等算力信息。
- 需要指出，这类细节通常出现在论文正文的实验设置或附录中，但所给文本对该部分内容未覆盖，因此无法获知具体的计算资源消耗。

### 5. 实验数量与充分性

- **实验组数量**：从摘要可确认的实验环节包括：
  - 与三类方法（通用生成、人体生成、人体动画）的横向对比；
  - 新数据集的构建与验证；
  - 提出的两个约束（密集跟踪约束、接触约束）的消融或效果分析（摘要中称“协同保障”结构/外观保真，暗示存在相关实验）。
- **充分性评估**：
  - **优势**：对比基线覆盖面较广，涵盖从通用到专用的人体生成方法；数据集规模与运动多样性优于现有基准，增强了评估的可信度。
  - **不足**：由于全文细节缺失，无法确认消融实验的完整程度（如是否逐项验证每个模块的贡献）、以及是否存在多数据集交叉验证或仅依赖单一自建数据集。若仅在一个自建数据集上评估，可能存在基准偏置风险。

### 6. 论文的主要结论与发现

- **解耦有效**：将结构生成与外观生成分离，显著改善了复杂人体运动视频的生成质量。
- **多约束协同**：Human-Aware Dynamic Control 模块配合密集跟踪约束，保证了稀疏结构到稠密画面的精细控制；接触约束则针对性提升人-环境交互的物理合理性。
- **全面超越**：在大多数评估指标上，MoSA 优于通用视频生成模型、人体视频生成模型和人体动画模型。
- **数据贡献**：构建的大规模复杂运动人体视频数据集，为后续该方向的研究提供了新资源。

### 7. 优点

- **问题定位精准**：直击人体视频生成的“运动物理合理性”痛点，而非泛泛地追求画质。
- **建模思路清晰**：结构与外观解耦的架构设计在逻辑上自洽——先有合理的运动，再谈合理的画面，避免了外观与结构互相干扰。
- **控制粒度深入**：通过 Human-Aware Dynamic Control + 密集跟踪约束实现稀疏结构的细粒度控制，解决了结构引导中常见的“信息丢失”问题。
- **针对性强**：接触约束是针对人-环境交互这一难点场景的定制化设计，体现了对问题细分的深入思考。
- **数据贡献**：大规模、运动复杂性更高的数据集是对该领域基础设施的有力补充。
- **对比全面**：对比了通用、专用、动画三类生成方法，实验视野开阔。

### 8. 不足与局限

- **细节信息缺失**：由于可获得的文本内容有限（仅摘要），无法评估具体的数值结果、消融实验的完整矩阵、以及训练/推理的算力成本。
- **数据集自建风险**：若评测主要依赖自建数据集，且未与公开基准进行充分对齐，则客观上可能存在评估偏差或过拟合数据分布的风险。
- **泛化性存疑**：摘要未说明模型在跨主体（多人）、跨场景、复杂遮挡、以及极端姿态下的表现，限制了对其泛化能力的判断。
- **接触约束的覆盖范围**：人类-环境交互除了接触外，还包括力反馈、物体形变等，当前约束是否覆盖全部交互类型尚不明确。
- **实际应用限制**：作为视频生成模型，其推理效率、可控交互界面、以及在影视/游戏等实际生产环境中的可用性均未在摘要中说明。

---

**（完）**
