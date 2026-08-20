---
title: Rethinking Video Generation Model for the Embodied World
title_zh: 反思具身世界中的视频生成模型
authors: "Yufan Deng, Zilin Pan, Hongyu Zhang, Xiaojie Li, Ruoqing Hu, Yufei Ding, Yiming Zou, Yan Zeng, Daquan Zhou"
date: 2026-04-30
pdf: "https://openreview.net/pdf/bf84fb3838c76b82bd85509ccbb2f381ae06f62d.pdf"
tags: ["query:phys-video"]
score: 9.0
evidence: 提出RBench，面向机器人视频生成，评估生成视频的物理真实感
tldr: 当前视频生成模型在物理真实性上存在明显不足，且缺乏标准化评测基准。为此提出机器人视频生成基准RBench，覆盖五个任务域和四种具身形态，通过可复现指标评估任务正确性与视觉保真度。在25个模型上的评测显示，模型生成物理真实机器人行为的能力显著不足，且基准与人类判断的Spearman相关系数达0.96，验证了其有效性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频生成模型在物理真实性上存在明显不足，且缺乏标准化的评测基准。
method: 提出了面向机器人视频生成的综合基准RBench，覆盖五个任务域和四种具身形态，用可复现指标评估任务正确性与视觉保真度。
result: 对25个模型的评测显示其生成物理真实机器人行为的能力明显不足，基准与人类判断的Spearman相关系数达0.96。
conclusion: RBench为检测物理真实性缺陷提供了有效工具，并提示实现物理真实仍需进一步研究。
---

## Abstract
While video generation holds promise for embodied intelligence, current video models struggle with physical realism, and progress is hindered by the lack of standardized benchmarks. To address this gap, we introduce a comprehensive robotics benchmark, RBench, designed to evaluate robot-oriented video generation across five task domains and four distinct embodiments. By assessing task correctness and visual fidelity through reproducible metrics, our evaluation of 25 models reveals significant deficiencies in generating physically realistic robot behaviors. Furthermore, the benchmark achieves a 0.96 Spearman correlation with human judgment, validating its effectiveness. While RBench provides the necessary lens to identify these deficiencies, achieving physical realism requires moving beyond evaluation to address the critical shortage of high-quality training data. Driven by these insights, we introduce a refined four-stage data pipeline, resulting in RoVid-X, the largest open-source robotic dataset for video generation with 4 million annotated video clips, covering thousands of tasks and enriched with physical property annotations. Extensive experiments demonstrate that finetuning on RoVid-X yields consistent performance gains. Collectively, this synergistic ecosystem of evaluation and data establishes a robust foundation for rigorous assessment and scalable training of video models, accelerating the evolution of embodied AI toward physical intelligence. The code and video demos are available in the supplementary materials.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：视频生成模型有望为具身智能（Embodied Intelligence）提供训练与决策支持，但现有模型在生成内容的**物理真实性**上存在明显缺陷，例如动作不符合真实物理规律、机器人行为不自然等。
- **核心痛点**：缺乏标准化、可复现的评测基准，导致不同模型之间的物理真实性差距难以量化，也阻碍了该领域的系统性进步。
- **整体含义**：论文试图构建一个“评测 + 数据”的协同生态系统，一方面通过基准准确暴露模型缺陷，另一方面通过高质量数据集弥补训练数据不足，从而推动视频生成模型从“视觉上合理”走向“物理上真实”，加速具身人工智能向物理智能进化。

## 2. 论文提出的方法论

- **核心思想**：将视频生成模型的评估从传统视觉质量指标转向**物理真实性**和**任务正确性**，并针对机器人视频生成场景专门设计评测体系。
- **关键方法：RBench 基准**
  - 覆盖 **5 个任务域**（task domains）和 **4 种不同的具身形态**（embodiments），用于评估机器人视频生成模型的多场景适应能力。
  - 评估维度包括：
    - **任务正确性（task correctness）**：生成视频是否完成指定任务、动作序列是否符合目标。
    - **视觉保真度（visual fidelity）**：画面质量、细节真实性等。
  - 使用**可复现的自动指标**，保证评测结果可比、可验证。
- **数据构建：RoVid-X 数据集**
  - 提出一套**四阶段数据流水线**（refined four-stage data pipeline），用于清洗、筛选、标注和增强机器人视频数据。
  - 产出 **RoVid-X**：当前最大的开源机器人视频生成数据集，包含 **400 万个带标注的视频片段**，覆盖数千个任务，并额外标注了**物理属性信息**（如物体材质、接触关系、运动轨迹等）。
- **没有给出具体公式或算法流程图**，但文字描述了从数据构建到评测的完整方法链条。

## 3. 实验设计

- **评测基准**：RBench，涵盖多任务域、多形态，强调物理真实性与任务完成度。
- **评测对象**：**25 个现有视频生成模型**，包括通用视频生成模型和机器人视频生成模型（具体模型名称未在摘要中列出）。
- **评测方式**：在 RBench 上运行各模型生成机器人视频，自动计算任务正确性与视觉保真度指标；同时请人类标注者评分，用于验证自动指标的有效性。
- **数据实验**：使用 RoVid-X 对部分模型进行微调（finetuning），对比微调前后的性能变化，验证数据集的训练价值。
- **结果对比**：未在摘要中列出各模型的详细排名，但明确指出模型整体表现不足，且微调 RoVid-X 后一致获得性能提升。

## 4. 资源与算力

- **未明确说明**：论文摘要在提供的文本中没有给出任何具体的算力信息（如 GPU 型号、数量、训练时长、数据集处理耗时等）。
- 仅能确认使用了较大规模数据（400 万视频片段），实际训练与评测所需的计算资源未知，需要查看论文正文或附录才能获取。

## 5. 实验数量与充分性

- **模型评测数量**：对 25 个模型进行了系统评测，覆盖多个任务域和形态，规模较大，具有较强的比较意义。
- **数据集实验**：在 RoVid-X 上进行了微调实验，并报告了“一致的性能提升”（consistent performance gains），表明数据有效性得到验证。
- **消融实验**：摘要中未明确提到消融实验（如仅评测不同组件的影响），但四阶段数据流水线的有效性可能包含内部对比（无法从摘要确认）。
- **客观性与公平性**：
  - 使用可复现指标，并验证了与人类判断的 Spearman 相关系数达 **0.96**，说明自动指标高度接近人类评价，评测结果具有较强可信度。
  - 不足之处在于：摘要未提供不同模型的具体评测细节和统计显著性分析，无法独立判断实验的公平性完全性。

## 6. 论文的主要结论与发现

- 现有视频生成模型在生成**物理真实的机器人行为**方面能力显著不足。
- 缺乏标准化基准是导致该问题难以被发现和解决的重要原因；RBench 弥补了这一空白。
- RBench 自动指标与人类判断高度一致（Spearman ρ = 0.96），可以作为可靠的评测工具。
- 仅靠评测无法解决物理真实性问题，**高质量训练数据的短缺**才是根本瓶颈之一。
- 通过四阶段数据流水线构建的 RoVid-X（400 万标注视频片段）能显著改善模型性能，微调后获得一致提升。
- 评测基准 + 数据集的协同生态，为视频模型在具身智能中的应用提供了坚实基础。

## 7. 优点

- **问题精准**：直接聚焦物理真实性这一视频生成用于具身智能的关键难点。
- **基准全面**：RBench 覆盖 5 个任务域和 4 种具身形态，适用范围广。
- **指标可复现**：使用自动指标并通过人类相关性验证（0.96），兼顾效率与可靠性。
- **数据贡献大**：RoVid-X 是当前最大的开源机器人视频生成数据集（400 万片段），并附带物理属性标注，具有高实用价值。
- **评测与数据闭环**：不仅指出问题，还提供解决方案，形成“评估-发现不足-数据补足-再评估”的完整链条。

## 8. 不足与局限

- **算力细节缺失**：论文未披露训练/评测的 GPU 资源和时间成本，不利于复现和成本评估。
- **模型细节未展开**：25 个模型的具体构成、参数量、生成设置等未在摘要中透露，影响横向对比的透明度。
- **物理真实性的定义**：摘要未明确物理真实性的具体评判标准（如接触力、动力学约束等），可能存在主观偏差。
- **任务域和形态的覆盖面有限**：虽含 5 个任务域和 4 种形态，但真实世界任务千差万别，能否泛化到更复杂场景仍有待验证。
- **数据流水线细节缺失**：四阶段流水线的具体筛选规则、标注质量校验方法未说明，可能存在噪声或标注不一致风险。
- **微调实验的泛化性**：仅报告“一致提升”，但提升幅度、在不同模型上的稳定性、过拟合风险未提及。
- **潜在偏差风险**：人类判断可能与数据分布相关，高相关（0.96）也可能源于评分维度设计覆盖不够全面。

（完）
