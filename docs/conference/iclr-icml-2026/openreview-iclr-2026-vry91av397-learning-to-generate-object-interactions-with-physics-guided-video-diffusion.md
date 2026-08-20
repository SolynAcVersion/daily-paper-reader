---
title: Learning to Generate Object Interactions with Physics-Guided Video Diffusion
title_zh: 物理引导的视频扩散：学习生成物体交互
authors: "David Romero, Ariana Bermudez, Hao Li, Fabio Pizzati, Ivan Laptev"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=vrY91av397"
tags: ["query:phys-video"]
score: 9.0
evidence: 物理引导的视频扩散方法，实现真实刚体控制与物理合理的物体交互
tldr: 当前视频生成模型在生成物体交互时仍缺乏物理合理性，且缺少物理接地的控制机制。KineMask提出物理引导的视频生成方法：输入单张图像与指定物体速度，即可生成包含推断运动与未来物体交互的视频。方法实现真实刚体控制与物体间交互效果，为世界模拟器与具身决策提供可用的视频生成工具。实验显示其在物理合理性与可控性上优于现有方法。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频生成模型难以生成物理合理的物体交互，且缺乏基于物理的控制机制。
method: 提出KineMask，通过物理引导的视频扩散在单图和物体速度条件下生成刚体运动与物体交互。
result: 实验表明该方法能生成物理合理且可控的视频，支撑世界模拟与具身决策。
conclusion: 该工作为视频生成提供物理接地控制思路，增强了模型作为世界模拟器的可信度。
---

## Abstract
Recent models for video generation have achieved remarkable progress and are now deployed in film, social media production, and advertising. Beyond their creative potential, such models also hold promise as world simulators for robotics and embodied decision making. Despite strong advances, however, current approaches still struggle to generate physically plausible object interactions and lack physics-grounded control mechanisms. To address this limitation, we introduce KineMask, an approach for physics-guided video generation that enables realistic rigid body control, interactions, and effects. Given a single image and a specified object velocity, our method generates videos with inferred motions and future object interactions. We propose a two-stage training strategy that gradually removes future motion supervision via object masks. Using this strategy we train video diffusion models (VDMs) on synthetic scenes of simple interactions and demonstrate significant improvements of object interactions in real scenes. Furthermore, KineMask integrates low-level motion control with high-level textual conditioning via predictive scene descriptions, leading to effective support for synthesis of complex dynamical phenomena. Extensive experiments show that KineMask achieves strong improvements over recent models of comparable size. Ablation studies further highlight the complementary roles of low- and high-level conditioning in VDMs. Our code, model, and data will be made publicly available

---

## 论文详细总结（自动生成）

# 1. 核心问题与整体含义

- **研究动机**：当前视频生成模型在创意生成方面取得显著进展，但作为**世界模拟器**（用于机器人、具身决策等）时，仍存在两个关键缺陷：
  - 对**物理合理的物体交互**生成能力不足；
  - 缺少**基于物理的控制机制**，无法对物体运动进行显式引导。
- **整体含义**：本文提出了一种名为 **KineMask** 的物理引导视频生成方法，试图为视频扩散模型引入物理接地（physics-grounded）的控制能力，提升生成内容在刚体运动、物体交互和动态效果上的真实性与可控性，从而增强视频生成模型作为世界模拟器的可信度。

# 2. 方法论

- **核心思想**：利用物理信息作为条件，生成具有真实刚体运动和物体交互的未来视频。
- **输入与输出**：
  - 输入：**单张图像** + **指定的物体速度**；
  - 输出：包含**推断运动**和**未来物体交互**的视频。
- **关键机制**：
  - 在视频扩散模型（VDM）中引入**物体掩码（object masks）**；
  - 采用**两阶段训练策略**：
    - 第一阶段：常规监督训练；
    - 第二阶段：通过物体掩码**逐步移除未来运动监督**，迫使模型自行推断物理上合理的运动，而不过度依赖显式的未来轨迹。
- **控制与条件**：
  - **低层控制**：物体速度，用于精确指导刚体运动；
  - **高层语义条件**：通过**预测性场景描述（predictive scene descriptions）** 提供文本级情景，支持复杂动力学现象的合成；
  - 低层与高层条件互补，共同作用于扩散模型。
- **训练数据与迁移**：
  - 在**合成场景**（简单交互）上训练视频扩散模型；
  - 在**真实场景**中测试和验证物体交互能力，表明模型可泛化到真实视频。

# 3. 实验设计

- **数据集 / 场景**：
  - 训练：合成场景，包含简单刚体交互；
  - 测试：真实场景中的物体交互；
  - 具体数据集名称、规模等细节在摘要中未披露。
- **Benchmark**：
  - 任务为视频生成中的物体交互物理合理性与可控性；
  - 未明确列出基准数据集名称。
- **对比方法**：
  - 与多个**规模相近的近期视频生成模型**进行了对比；
  - 通过消融实验分析低层控制、高层文本条件以及两阶段训练各自的作用。

# 4. 资源与算力

- 原文**未明确说明**训练所使用的 GPU 型号、数量、训练时长、能耗等算力信息。
- 仅提及“代码、模型和数据将公开”，未提供训练细节。
- 因此，无法从当前内容评估计算成本和资源需求。

# 5. 实验数量与充分性

- **实验数量**：
  - 摘要中仅概括为“大量实验（Extensive experiments）”，未给出具体实验组数；
  - 明确提及的实验类型包括：
    - 合成场景训练后迁移至真实场景的评估；
    - 与近期相似规模模型的对比；
    - 消融研究（低层控制、高层条件的作用）。
- **充分性评估**：
  - **优点**：训练/测试场景分离、迁移评估、消融设计为结论提供了一定支持；
  - **不足**：由于缺乏具体的数据集规模、量化指标、基线细节和多个真实场景类别，无法判断实验在统计上的充分性与全面性；
  - **公平性**：对比模型“规模相似”表述合理，但未说明是否使用了相同训练数据、粒度和评估协议，因此客观公平性有待文章全文验证。

# 6. 主要结论与发现

- KineMask 能够根据单图和物体速度生成**物理合理且可控**的物体交互视频。
- 两阶段训练策略可以逐步弱化未来运动监督，同时保持物理合理性。
- 低层速度控制与高层文本条件可以**互补**，有效支撑复杂动态场景的生成。
- 该方法在物理合理性、控制能力上显著优于同规模近期模型，为视频生成作为世界模拟器提供了有力支撑。

# 7. 优点

- **物理引导的控制机制**：直接以物体速度为条件，使模型具备显式的刚体控制能力，区别于无控制的生成模型。
- **两阶段掩码训练**：创新的训练策略，逐步释放模型对显式运动监督的依赖，鼓励物理推断能力。
- **低层+高层条件融合**：将精确速度控制与语义化场景描述结合，提升了生成内容的可控性和语义丰富度。
- **合成到真实的迁移验证**：在合成场景训练、真实场景评估，展示了模型泛化能力。
- **开放承诺**：计划公开代码、模型和数据，便于复现和后续研究。

# 8. 不足与局限

- **细节缺失**：摘要中未提供足够信息，如数据集构成、视频长度、分辨率、评估指标、基线具体名称等，难以完全评判方法的工程复杂度与性能上限。
- **场景覆盖有限**：训练数据仅为“简单交互的合成场景”，可能不足以应对现实世界中复杂、多样、多物理规律的物体交互。
- **条件输入简化**：仅依赖单图和物体速度，对于需要接触、摩擦、阻尼等更高阶物理属性的交互来说，控制维度可能不足。
- **泛化风险**：从合成到真实场景的迁移虽有验证，但真实场景中的物体类别、材质、环境光照等复杂因素仍可能造成性能退化。
- **计算资源未披露**：无法判断该方法在资源消耗方面是否具备实用优势。
- **未提及安全与偏差问题**：物理引导的生成模型若部署于实体决策中，可能存在安全隐患；但这些方面文中未讨论。

（完）
