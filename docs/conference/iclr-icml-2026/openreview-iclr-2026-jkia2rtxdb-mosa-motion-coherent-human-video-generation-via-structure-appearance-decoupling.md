---
title: "MoSA: Motion-Coherent Human Video Generation via Structure-Appearance Decoupling"
title_zh: MoSA：通过结构-外观解耦实现运动一致的人类视频生成
authors: "Haoyu Wang, Hao Tang, Donglin Di, Zhilu Zhang, Wangmeng Zuo, Feng Gao, Siwei Ma, Shiliang Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=JKIa2rTxdB"
tags: ["query:phys-video"]
score: 8.0
evidence: 通过结构-外观解耦生成更真实、物理合理的人体运动视频
tldr: MoSA 针对视频生成模型难以合成复杂人体运动、容易出现物理上不合理动作的问题，提出将人类视频生成解耦为结构生成和外观生成两个阶段。首先由3D结构Transformer生成完整的人体运动序列，再基于该结构序列引导视频外观合成，从而在生成中保持细粒度运动约束。实验表明该方法能够实现更协调、更符合物理规律的人体动作视频，为人体视频生成提供了新的解耦设计思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频生成重视外观而忽略复杂人体运动与物理合理性，导致动作不真实和结构不一致。
method: 将人类视频生成解耦为结构生成与外观生成，先用3D结构Transformer生成运动序列，再在结构引导下合成外观。
result: 能够生成更真实、结构一致且物理合理的人体运动视频。
conclusion: 结构-外观解耦可有效提升人体视频生成的运动协调性和物理合理性。
---

## Abstract
Existing video generation models predominantly emphasize appearance fidelity while exhibiting limited ability to synthesize complex human motions, such as whole-body movements, long-range dynamics, and fine-grained human–environment interactions. This often leads to unrealistic or physically implausible movements with inadequate structural coherence. To conquer these challenges, we propose MoSA, which decouples the process of human video generation into two components, i.e., structure generation and appearance generation. MoSA first employs a 3D structure transformer to generate a human motion sequence from the text prompt. The remaining video appearance is then synthesized under the guidance of this structural sequence. We achieve fine-grained control over the sparse human structures by introducing Human-Aware Dynamic Control modules with a dense tracking constraint during training. The modeling of human–environment interactions is improved through the proposed contact constraint. Those two components work comprehensively to ensure the structural and appearance fidelity across the generated videos. This paper also contributes a large-scale human video dataset, which features more complex and diverse motions than existing human video datasets. We conduct comprehensive comparisons between MoSA and a variety of approaches, including general video generation models, human video generation models, and human animation models. Experiments demonstrate that MoSA substantially outperforms existing approaches across the majority of evaluation metrics.

---

## 论文详细总结（自动生成）

# MoSA：通过结构-外观解耦实现运动一致的人类视频生成 — 论文中文总结

## 1. 核心问题与整体含义
- **研究动机**：现有视频生成模型大多侧重于外观保真度，在合成复杂人体运动（如全身运动、长时间动态、细粒度的人-环境交互）时能力有限，常导致生成结果出现不真实或物理上不合理的动作，且结构连贯性不足。
- **核心问题**：如何在视频生成中同时保证人体运动的结构一致性和物理合理性，而不牺牲外观质量。
- **整体含义**：本文提出一种“结构-外观解耦”的生成范式，将人类视频生成拆分为“结构生成”与“外观生成”两个阶段，从而在生成过程中显式控制人体运动结构，改善视频中动作的协调性与物理可信度。

## 2. 方法论
- **核心思想**：将人类视频生成解耦为两个独立又协同的阶段：
  1. **结构生成**：先用一个 3D 结构 Transformer 从文本提示生成完整的人体运动序列。
  2. **外观生成**：在该结构序列的引导下，合成视频中剩余的外观信息。
- **关键技术细节**：
  - **Human-Aware Dynamic Control 模块**：在训练中引入稠密跟踪约束，实现对稀疏人体结构的细粒度控制。
  - **接触约束（Contact Constraint）**：用于改进人与环境的交互建模，使生成的运动更符合物理规律。
  - 两个阶段的协同工作保证了生成视频在结构和外观两个维度上的保真度。
- **算法流程（文字描述）**：
  1. 输入文本提示 → 3D 结构 Transformer 生成人体运动序列（骨架/结构表示）。
  2. 以运动序列作为引导条件 → 外观生成网络合成逐帧的视频外观。
  3. 在训练过程中同时施加稠密跟踪约束和接触约束，优化结构控制与人-环境交互质量。

## 3. 实验设计
- **数据集**：
  - 论文贡献了一个**大规模人类视频数据集**，其中包含比现有数据集更复杂、更多样的人体动作。
  - 未具体提及用于训练和测试的公开数据集名称（如 HumanML3D、TikTok 等），但明确新数据集作为主要实验基准。
- **Benchmark**：基于新提出的大规模人类视频数据集，评估生成视频的运动一致性、物理合理性与外观保真度。
- **对比方法**：涵盖了三大类方法：
  - 通用视频生成模型
  - 人类视频生成模型
  - 人体动画模型
- 说明：实验对比面较宽，能较好反映 MoSA 相对于不同技术路线的优势。

## 4. 资源与算力
- 原文与元数据中**未明确说明**具体的 GPU 型号、数量、训练时长等信息。
- 仅在整体实验设置中暗示使用了深度学习训练框架，但缺乏可复现的算力细节。

## 5. 实验数量与充分性
- **实验组数**：提到了“comprehensive comparisons”，即与多类方法进行广泛对比，并包含了消融相关组件（动态控制模块、接触约束）的验证，但具体消融实验组数未在摘要中列出。
- **充分性评估**：
  - **优点**：对比方法覆盖三大类别，数据集规模更大、动作更复杂，评价指标多元化，基本能够支撑主要结论。
  - **不足**：缺少对算力资源、具体训练/测试协议、消融设置细节（如每个模块单独与联合的贡献）的公开描述，可能影响实验的完整可复现性。

## 6. 主要结论与发现
- MoSA 通过结构生成与外观生成的解耦，能够比现有方法生成更真实、结构一致且物理合理的人体运动视频。
- 在大多数评价指标上，MoSA 显著优于通用视频生成、人类视频生成以及人体动画三类基线方法。
- 证明了引入稠密跟踪约束和接触约束可以有效提升人体运动结构的可控性和人-环境交互的合理性。

## 7. 优点
- **设计创新**：将人类视频生成解耦为结构生成与外观生成，思路清晰，针对性强，能直接对运动结构施加约束。
- **模块有效性**：Human-Aware Dynamic Control 模块与接触约束在机理上分别解决细粒度结构控制与物理交互问题，具有较好的可解释性。
- **数据集贡献**：构建了更大规模、动作更复杂多样的人类视频数据集，弥补现有数据集在复杂运动覆盖上的不足。
- **对比全面**：与通用生成、专用人类生成、人体动画等多类方法对比，体现广泛适用性。

## 8. 不足与局限
- **算力与复现信息不透明**：未报告 GPU 型号、数量、训练时间等关键资源信息，不利于复现与公平的成本评估。
- **实验细节有限**：消融实验的具体结构、指标细节和统计显著性未在摘要中展开，难以判断各部分贡献的量化程度。
- **数据偏差风险**：新数据集虽动作更复杂，但可能仍存在场景、人群、环境多样性的局限性；对外界未知测试集的泛化能力有待验证。
- **应用限制**：模型依赖文本提示作为输入，对复杂文本描述的长时运动生成可能仍有误差累积问题；结构-外观两阶段流程可能增加推理复杂度，实时应用受限。

（完）
