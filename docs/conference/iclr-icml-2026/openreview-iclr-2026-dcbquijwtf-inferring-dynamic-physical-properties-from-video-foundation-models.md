---
title: Inferring Dynamic Physical Properties from Video Foundation Models
title_zh: 从视频基础模型中推断动态物理属性
authors: "Guanqi Zhan, Xianzheng Ma, Weidi Xie, Andrew Zisserman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=DCbQUijwtf"
tags: ["query:phys-video"]
score: 6.0
evidence: 收集了弹力、粘度、摩擦等动态物理属性的视频数据集，用于从视频推断物理属性；有助于物理感知视频理解
tldr: 该论文研究从视频中推断动态物理属性，针对弹性、粘度和动态摩擦等需要时间信息才能推断的属性，收集了包含合成和真实场景的新视频数据集。作者探索了三种推断方式，从经典视觉提示到视频基础模型的读出机制，并在真实数据上评估其泛化能力。这项工作为物理属性推断提供了数据和方法基础，可用于物理感知的视频理解和生成评估。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法难以从视频中推断需要时间动态的物理属性，缺乏相应数据集和系统研究。
method: 构建弹性、粘度、摩擦力三类物理属性的合成与真实视频数据集，并对比经典视觉、读出机制等三种推断方案。
result: 在合成与真实数据上评测了各方法的推断效果，验证了视频基础模型在物理属性推断上的潜力。
conclusion: 提供了物理属性推断的数据集与方法框架，对物理合理的视频理解与生成有重要价值。
---

## Abstract
We study the task of predicting dynamic physical properties from videos. More specifically, we consider physical properties that require temporal information to be inferred: elasticity of a bouncing object, viscosity of a flowing liquid, and dynamic friction of an object sliding on a surface. To this end, we make the following contributions: (i) We collect a new video dataset for each physical property, consisting of synthetic training and testing splits, as well as a real split for real world evaluation. (ii) We explore three ways to infer the physical property from videos: (a) an oracle method where we supply the visual cues that intrinsically reflect the property using classical computer vision techniques; (b) a simple read out mechanism using a visual prompt and trainable prompt vector for cross-attention on pre-trained video generative and self-supervised models; and (c) prompt strategies for Multi-modal Large Language Models (MLLMs). (iii) We show that video foundation models trained in a generative or self-supervised manner achieve a similar performance, though behind that of the oracle, and MLLMs are currently inferior to the other models, though their performance can be improved through suitable prompting.

---

## 论文详细总结（自动生成）

# 论文总结：从视频基础模型中推断动态物理属性

> **说明**：本次总结基于提供的论文元数据（标题、作者、摘要、结构化字段）进行撰写；由于原始 PDF 提取页面为 OpenReview 的验证页面，未包含论文全文或具体图表细节，以下总结以摘要和元数据信息为准，并明确标注信息缺失之处。

## 1. 核心问题与整体含义（研究动机与背景）

- **研究问题**：从视频中推断物体的**动态物理属性**，具体包括三类需要时间动态才能推断的属性：
  - 弹性（elasticity）：如弹跳物体的弹性系数；
  - 粘度（viscosity）：如流动液体的黏稠程度；
  - 动态摩擦（dynamic friction）：如物体在表面滑动时的摩擦特性。
- **研究动机**：
  - 静态图像只能反映物体的形状、颜色等表观属性，而弹性、粘度、摩擦等物理属性**只有通过观察物体随时间变化的动态过程**才能被准确推断。
  - 现有方法缺乏针对这类**时间依赖型物理属性**的系统研究和相应数据集。
  - 该研究希望为物理感知的视频理解与物理合理的视频生成提供数据和方法基础。

## 2. 方法论：核心思想与关键技术细节

作者提出了**三种推断动态物理属性的方法**，并以对比的方式进行探索：

- **(a) Oracle 方法（经典视觉方法）**
  - 核心思想：先验地知道哪些**视觉线索**与目标物理属性直接相关，然后使用经典计算机视觉技术提取这些线索来推断属性。
  - 本质上是“作弊式”的基准方法，用于衡量任务的理论上限。
- **(b) 基于视频基础模型的读出机制**
  - 使用**视觉提示（visual prompt）** + **可训练的提示向量（trainable prompt vector）**；
  - 通过**交叉注意力（cross-attention）**机制，从预训练视频生成模型（video generative models）或自监督视频模型（self-supervised models）中“读出”物理属性。
  - 该方法代表了一种“轻量级”微调方案——冻结基础模型，仅训练提示向量。
- **(c) 多模态大语言模型（MLLMs）的提示策略**
  - 直接在多模态大语言模型上设计不同的**提示文本（prompting strategies）**，让其回答物理属性。
  - 该类方法不需要额外训练，但依赖模型的固有物理常识。

> **注**：原文未给出具体的公式细节、损失函数或算法流程图，仅从摘要中可获得上述方法层面的描述。

## 3. 实验设计：数据集、Benchmark 与对比方法

- **数据集构建**（论文的核心贡献之一）：
  - 针对**每一种物理属性**（弹性、粘度、动态摩擦）分别收集了独立的数据集；
  - 每个数据集包含：
    - **合成训练集（synthetic training split）**；
    - **合成测试集（synthetic testing split）**；
    - **真实场景测试集（real split）**——用于评估模型的真实世界泛化能力。
- **Benchmark 结构**：整体构成了一个“合成训练 → 合成测试 → 真实测试”的标准评测流程。
- **对比方法**：
  1. Oracle 经典视觉方法；
  2. 基于视频基础模型的读出机制（两种基础模型类型：生成式 vs. 自监督式）；
  3. 多模态大语言模型（含不同提示策略）。

## 4. 资源与算力

- **原文未明确提及**具体的算力信息，例如：
  - GPU 型号与数量；
  - 训练时长；
  - 参数量或显存占用。
- 因此，无法从本摘要中获取训练成本或算力规模的相关说明。

## 5. 实验数量与充分性

- **实验维度**：
  - 3 类物理属性（弹性、粘度、摩擦） × 3 类方法（Oracle / 基础模型读出 / MLLM）；
  - 合成测试与真实场景测试两个评测层次；
  - 视频基础模型内部还有生成式 vs. 自监督式的对比；
  - MLLM 内部还有提示策略的对比。
- **充分性评估**：
  - 从摘要来看，实验设计**覆盖了多个方法家族**，具有较好的对比广度；
  - 真实场景测试的引入增强了结论的可信度；
  - 但摘要中**未披露具体数值结果、消融实验细节、以及各实验的重复次数**，因此无法定量评估实验的统计充分性；
  - 整体而言，实验设计在“方法对比”和“领域覆盖”上是合理的，但在细节透明度上有待完善。

## 6. 主要结论与发现

- **视频基础模型的有效性**：无论是生成式还是自监督式预训练的视频基础模型，均能较好地完成动态物理属性推断任务，两者性能相近。
- **与 Oracle 的差距**：基础模型的推断性能仍低于使用经典视觉线索的 Oracle 方法，说明该任务仍有提升空间。
- **MLLM 的现状**：多模态大语言模型目前在该任务上的表现**逊于**其他两类方法；但通过**合适的提示设计**可以改善其性能。
- **总体价值**：该工作为动态物理属性推断提供了**数据集基础和多样化的方法框架**，对物理合理的视频理解与视频生成评估具有重要意义。

## 7. 优点

- **填补空白**：首次系统性地针对需要时间信息推断的动态物理属性构建数据集，填补了该方向的数据缺失。
- **真实场景评测**：每个属性均包含真实场景测试集，注重模型的泛化能力验证。
- **方法覆盖面广**：同时对比了经典视觉方法、视频基础模型（生成式+自监督式）和 MLLM，涵盖了从传统到前沿的完整方法谱系。
- **轻量级设计**：基于提示向量的交叉注意力读出机制，无需微调整个基础模型，计算效率较高。
- **任务定义清晰**：明确限定在弹性、粘度、动态摩擦三类典型属性上，问题聚焦、便于后续扩展。

## 8. 不足与局限

- **物理属性种类有限**：仅涉及三类属性，未覆盖更广泛的物理量（如质量、密度、刚度、韧性等）。
- **方法细节披露不足**：摘要中缺少具体的模型架构、训练策略、提示文本设计和数值实验细节。
- **算力信息缺失**：未报告训练所需的计算资源，不利于后续研究者复现和评估成本。
- **基础模型与 Oracle 存在差距**：说明当前视频基础模型对物理属性的隐式表征仍不够精确，实际应用中可能需要额外的物理约束或监督信号。
- **MLLM 性能较弱**：多模态大语言模型在该任务上仍不成熟，适用范围有限。
- **真实场景规模与多样性未知**：摘要未说明真实测试集的规模、场景覆盖范围及标注精度，可能存在数据偏差风险。

---

（完）
