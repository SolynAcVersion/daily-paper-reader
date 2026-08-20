---
title: "Dreamland: Hybrid World Creation with Simulator and Generative Models"
title_zh: Dreamland：模拟器与生成模型混合的世界创建
authors: "Sicheng Mo, Ziyang Leng, Leon Liu, Weizhen Wang, Honglin He, Huizhi Zhang, Bolei Zhou"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=I9pQJJWKn3"
tags: ["query:phys-video"]
score: 8.0
evidence: 基于物理模拟器与生成模型的混合框架
tldr: 大规模视频生成模型能生成多样逼真的动态世界，但缺乏元素级可控性，难以用于编辑场景和训练具身智能体。Dreamland提出混合世界生成框架，将基于物理的模拟器的精确控制与预训练生成模型的照片级内容输出结合，通过分层世界抽象同时编码像素级和对象级语义几何作为中间表示，增强可控性并降低适应成本。该方法为物理仿真与生成模型的融合提供了有效范例。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视频生成模型缺乏元素级可控性，难以用于场景编辑和训练具身智能体。
method: 混合物理模拟器与生成模型，用分层世界抽象桥接像素级和对象级语义几何。
result: 增强可控性，同时降低与真实分布对齐的适应成本。
conclusion: 为物理仿真与生成模型融合提供了有效范例。
---

## Abstract
Large-scale video generative models can synthesize diverse and realistic visual content for dynamic world creation, but they often lack element-wise controllability, hindering their use in editing scenes and training embodied AI agents. We propose Dreamland, a hybrid world generation framework that combines the granular control of a physics-based simulator with the photorealistic content output of large-scale, pretrained generative models. In particular, we design a layered world abstraction that encodes both pixel-level and object-level semantics and geometry as an intermediate representation to bridge the simulator and the generative model. This approach enhances controllability, minimizes adaptation cost through early alignment with real-world distributions, and supports the off-the-shelf use of existing and future pretrained generative models. We further construct a D3Sim dataset to facilitate the training and evaluation of hybrid generation pipelines. Experiments demonstrate that Dreamland outperforms existing baselines with 50.8% improved image quality, 17.9% stronger controllability, and has great potential to enhance embodied agent training. Code and data will be made available.

---

## 论文详细总结（自动生成）

## 论文总结：Dreamland（模拟器与生成模型混合的世界创建）

> 注：本次提供的材料仅包含论文标题、作者、摘要及少量元数据，未包含正文细节。以下总结主要基于摘要内容，并在相应位置标注信息缺失情况。

### 1. 核心问题与整体含义（研究动机和背景）
- **背景**：大规模视频生成模型能够合成多样化、逼真的动态世界内容，但**缺乏元素级（element-wise）可控性**，导致难以用于场景编辑和训练具身智能体（embodied AI agents）。
- **核心问题**：如何同时获得生成模型的照片级真实感与物理模拟器的精确控制能力，构建一个既可编辑、又可用于智能体训练的世界生成框架。
- **整体含义**：论文提出“混合世界生成”思路，将物理模拟器与生成模型优势互补，为动态世界创建提供新的范式，对视觉生成、仿真到现实迁移、具身智能训练等领域具有潜在价值。

### 2. 方法论
- **核心思想**：提出 **Dreamland** 混合框架，结合基于物理的模拟器（提供精细控制）与大规模预训练生成模型（提供照片级内容输出）。
- **关键技术**：设计了一种**分层世界抽象（layered world abstraction）**，同时编码**像素级和对象级语义、几何信息**，作为连接模拟器和生成模型的中间表示。
- **工作流程（按摘要推断）**：
  1. 物理模拟器生成具有精确控制和物理一致性的场景状态（对象位置、运动、几何等）；
  2. 分层世界抽象将模拟器输出转换为生成模型可理解的中间表示（融合像素级外观与对象级语义）；
  3. 预训练生成模型基于该表示生成最终逼真图像/视频。
- **优势描述**：
  - 增强可控性；
  - 通过与真实世界分布的早期对齐，降低适应成本；
  - 支持即插即用地使用现有及未来的预训练生成模型。
- **公式或算法流程**：摘要中未提供具体数学表达或伪代码，仅有高层框架描述。

### 3. 实验设计
- **数据集**：论文构建了 **D3Sim 数据集**，用于训练和评估混合生成流程。数据集的具体内容、规模、场景类型在摘要中未说明。
- **Benchmark**：未明确说明使用了何种标准 benchmark，但通过自建数据集及与基线对比来评估。
- **对比方法**：摘要仅笼统提到“existing baselines”，未列出具体方法名称。
- **主要评估指标**：图像质量（改进 50.8%）、可控性（提升 17.9%），以及具身智能体训练潜力。
- **实验场景**：未具体说明（可能涉及仿真场景的图像生成和智能体训练环境）。

### 4. 资源与算力
- **未明确说明**：摘要和元数据中**没有提供**任何关于 GPU 型号、数量、训练时长、参数量、能耗等信息。
- 因此无法从当前材料评估该方法的计算成本或工程可复现性。

### 5. 实验数量与充分性
- **实验数量**：摘要未给出具体实验组数、消融研究或不同数据集上的测试情况。
- **充分性评估**：
  - **信息不足**：由于缺少正文，无法判断实验是否覆盖多样化场景、是否进行消融（如去掉分层抽象或不同生成模型版本）等。
  - **客观性风险**：仅报告相对提升百分比（50.8%、17.9%），缺少基线细节、误差范围、显著性检验等信息，难以判断结果是否稳健。
  - **公平性**：未说明基线训练配置、是否使用相同计算资源等，无法确认对比的公平性。
- **说明**：该论文在元数据中被标注为 **ICLR-2026-Rejected-Public**，可能暗示实验或贡献存在某些不足，但具体评审意见未提供。

### 6. 主要结论与发现
- Dreamland 混合框架相比基线在**图像质量上提升 50.8%**，在**可控性上提升 17.9%**。
- 该方法能有效结合物理模拟器的控制与生成模型的逼真度，并显著降低与真实世界分布对齐的适应成本。
- 具有增强**具身智能体训练**的潜力。
- 作者认为该工作为物理仿真与生成模型的融合提供了有效范例，并承诺开源代码与数据。

### 7. 优点
- **范式创新**：不是简单用生成模型做视频，也不是传统纯物理仿真，而是构建“模拟器 + 生成模型”的混合框架，思想新颖。
- **中间表示设计**：分层世界抽象同时编码像素级和对象级语义几何，解决模拟器与生成模型之间的“翻译”问题，具有较强的通用性。
- **实用导向**：明确面向场景编辑和具身智能体训练，应用价值清晰。
- **兼容性**：支持即插即用现有及未来的预训练生成模型，具有扩展性。
- **贡献数据**：构建 D3Sim 数据集，便于后续研究。

### 8. 不足与局限
- **摘要信息有限**：缺少具体方法细节（分层抽象如何学习、损失函数、网络结构等）、实验设置和定量表格，无法深入评估。
- **实验覆盖不明**：未说明评测场景多样性、不同生成模型 backbone、不同模拟器泛化性等。
- **对比公平性存疑**：未列出基线方法、基线训练配置，51% 和 18% 的提升幅度可能存在特定条件下的夸大风险。
- **可控性定义模糊**：摘要未明确“元素级可控性”的量化方式（如编辑成功率、轨迹误差、属性控制精度等）。
- **具身智能体训练部分**：仅提到“有潜力”，缺少具体实验证据。
- **可复现性**：虽承诺开源代码和数据，但当前材料未提供任何复现所需信息。
- **论文被拒**：该工作被标注为 ICLR-2026 拒稿，可能意味着在理论贡献、实验完整性或写作方面仍有待加强。

（完）
