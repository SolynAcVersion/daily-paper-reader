---
title: Rethinking Video Generation Model for the Embodied World
title_zh: 重新思考具身世界的视频生成模型
authors: "Yufan Deng, Zilin Pan, Hongyu Zhang, Xiaojie Li, Ruoqing Hu, Yufei Ding, Yiming Zou, Yan Zeng, Daquan Zhou"
date: 2026-04-30
pdf: "https://openreview.net/pdf/bf84fb3838c76b82bd85509ccbb2f381ae06f62d.pdf"
tags: ["query:phys-video"]
score: 9.0
evidence: RBench基准评估机器人视频生成的物理真实性与任务正确性
tldr: 视频生成在具身智能中潜力巨大，但现有模型物理真实性不足且缺少标准化评测。RBench包含五个任务领域、四种具身形态，从任务正确性和视觉保真度两个角度度量生成质量。在25个模型上的评测显示模型生成物理上合理的机器人行为能力存在明显缺陷，且基准与人类判断斯皮尔曼相关系数达0.96。这为衡量视频生成的物理真实性提供了可靠且可复现的基准工具。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 机器人视频生成模型缺乏物理真实感和标准化基准。
method: 构建RBench，覆盖多任务多具身，用可复现指标评估任务正确性和视觉保真度。
result: 25个模型表现均暴露物理合理性缺陷，基准与人类判断高度相关。
conclusion: 为具身视频生成提供了标准化物理真实性评测方法。
---

## Abstract
While video generation holds promise for embodied intelligence, current video models struggle with physical realism, and progress is hindered by the lack of standardized benchmarks. To address this gap, we introduce a comprehensive robotics benchmark, RBench, designed to evaluate robot-oriented video generation across five task domains and four distinct embodiments. By assessing task correctness and visual fidelity through reproducible metrics, our evaluation of 25 models reveals significant deficiencies in generating physically realistic robot behaviors. Furthermore, the benchmark achieves a 0.96 Spearman correlation with human judgment, validating its effectiveness. While RBench provides the necessary lens to identify these deficiencies, achieving physical realism requires moving beyond evaluation to address the critical shortage of high-quality training data. Driven by these insights, we introduce a refined four-stage data pipeline, resulting in RoVid-X, the largest open-source robotic dataset for video generation with 4 million annotated video clips, covering thousands of tasks and enriched with physical property annotations. Extensive experiments demonstrate that finetuning on RoVid-X yields consistent performance gains. Collectively, this synergistic ecosystem of evaluation and data establishes a robust foundation for rigorous assessment and scalable training of video models, accelerating the evolution of embodied AI toward physical intelligence. The code and video demos are available in the supplementary materials.

---

## 论文详细总结（自动生成）

好的，我将根据提供的论文信息，为您生成一份详细的中文总结。

---

## 论文总结：重新思考具身世界的视频生成模型

### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：当前视频生成模型在具身智能领域展现出巨大潜力，但其生成的视频普遍缺乏物理真实性（physical realism），无法准确模拟真实世界的物理规律和机器人行为。
- **研究背景**：
  - 具身智能（Embodied AI）的发展依赖于模型对物理世界的理解和交互能力，视频生成被视为一种极具前景的“世界模型”载体。
  - 然而，现有视频模型生成的机器人行为往往不符合物理常识，且该领域缺乏一个标准化、可复现的基准来系统性地评估和量化这些问题。
- **研究意义**：论文旨在通过构建标准化的评测基准和高质量的数据集，弥合视频生成与物理世界之间的鸿沟，为具身智能从“数据驱动”迈向“物理智能”提供坚实基础。

### 2. 方法论：核心思想与关键技术细节
- **核心思想**：构建一个“评测（Evaluation）+数据（Data）”协同发展的生态系统，即先通过严格的基准揭示问题，再通过针对性的数据管线解决问题。
- **技术细节——RBench基准**：
  - 这是一个专为机器人视频生成设计的综合评测基准，覆盖了**五个任务领域**和**四种不同的具身形态**（如机械臂、人形机器人、四足机器人等）。
  - 评测维度：从**任务正确性**（Task Correctness）和**视觉保真度**（Visual Fidelity）两个关键角度进行评估。
  - 评估方法：采用**可复现的指标**（reproducible metrics）进行量化，力求保证评估过程的客观性和可重复性。
- **技术细节——RoVid-X数据集与数据管线**：
  - 基于基准评测暴露出的问题，论文指出高质量训练数据的缺乏是核心瓶颈。
  - 为此，论文提出了一种**四阶段的数据处理管线（four-stage data pipeline）**，旨在系统性地清洗、筛选和标注机器人视频数据。
  - 该管线的产出是**RoVid-X**，是目前最大的开源机器人视频生成数据集，包含**400万个带注释的视频片段**，覆盖数千种任务，并附有**物理属性注释**（如物体材质、力学关系等）。

### 3. 实验设计：数据集、基准与对比方法
- **数据集与基准**：
  - **基准**：使用提出的 **RBench** 作为核心评测工具，涵盖多任务、多具身场景。
  - **训练数据**：使用新构建的 **RoVid-X** 数据集对模型进行微调训练。
- **对比方法**：
  - 论文使用 RBench 对 **25个现有主流视频生成模型** 进行了系统性的横向评测。
  - 此外，通过对比在 RoVid-X 上微调前后的模型性能，验证了新数据集的有效性。
- **评测标准**：
  - **客观指标**：任务正确性相关的判定指标，以及视觉保真度的量化指标。
  - **主观指标**：与人类判断的相关性分析。

### 4. 资源与算力
- 提供的论文原文（摘要及元数据）**未明确提及**训练或评测所使用的具体GPU型号、数量及训练时长等算力信息。这一点在原文中未被详细披露。

### 5. 实验数量与充分性
- **实验数量**：
  - **基准评测**：对25个不同模型进行了大规模横向评测。
  - **数据集验证**：基于RoVid-X进行了微调实验，并验证了性能提升。
  - **相关性分析**：验证了RBench与人类判断的相关性（斯皮尔曼系数达0.96）。
- **充分性与客观性分析**：
  - **充分性**：从“大规模模型评测”和“数据集微调验证”两个维度来看，实验设计较为全面，为结论提供了有力支撑。
  - **客观性**：RBench强调使用“可复现指标”，且与人类判断的高相关性（0.96）表明其评测结果具有良好的可信度和客观性，在一定程度上避免了单一指标带来的偏差。

### 6. 主要结论与发现
- **现状缺陷**：对25个模型的评测显示，现有视频生成模型在生成物理上合理的机器人行为方面存在显著缺陷，物理真实性不足是普遍问题。
- **基准有效性**：RBench不仅能有效识别这些缺陷，且其结果与人类判断高度一致（斯皮尔曼相关系数0.96），证明了其作为评测工具的有效性和可靠性。
- **数据是关键瓶颈**：实现物理真实感的关键不只在于算法或评测，更核心的是**高质量训练数据的严重短缺**。
- **数据集成效显著**：在 RoVid-X 数据集上进行微调后，模型性能取得了**一致的提升**，验证了该数据集和四阶段数据管线在解决数据瓶颈方面的实用价值。

### 7. 优点
- **填补空白**：提出了首个系统性的机器人视频生成基准（RBench），填补了该领域缺乏标准化、可复现评估工具的空白。
- **多维度评估**：RBench同时考量了“任务正确性”和“视觉保真度”，且覆盖多任务、多具身，评估维度全面。
- **可靠性验证**：通过与人类判断进行相关性验证（0.96），有力地确立了该基准的可靠性和生态效度。
- **数据与评测协同**：论文不仅“发现问题”（通过RBench），还“解决问题”（通过RoVid-X数据集），构成一个完整的闭环生态系统，这是其重要的实践贡献。
- **开源贡献**：RoVid-X是当前最大的开源机器人视频数据集，为社区后续研究提供了宝贵资源。

### 8. 不足与局限
- **信息缺失**：论文未提供关于训练算力、模型参数量等关键细节，使复现和成本评估变得困难。
- **物理真实性外延**：虽然RBench侧重物理真实性，但“物理合理”的涵盖范围极广（如刚体力学、流体、接触力等），基准是否涵盖了所有关键物理维度尚待解析原文以获得更详细信息。
- **评测指标局限性**：尽管指标是“可复现”的，但自动指标（如视觉保真度）与人类深层感知之间可能存在偏差，完全依赖这些指标仍可能导致对某些细节的误判。
- **应用限制**：基准和数据集的能力上限受限于已有的任务定义和具身类型，对于超出其覆盖范围的全新机器人形态或交互模式，其适用性有待验证。

---

（完）
