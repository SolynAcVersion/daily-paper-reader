---
title: Inferring Dynamic Physical Properties from Video Foundation Models
title_zh: 从视频基础模型推断动态物理属性
authors: "Guanqi Zhan, Xianzheng Ma, Weidi Xie, Andrew Zisserman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=DCbQUijwtf"
tags: ["query:phys-video"]
score: 8.0
evidence: 面向动态物理属性推断与评估的新视频数据集
tldr: 从视频中推断动态物理属性（如弹性、粘度、动摩擦）对理解物理世界至关重要。该工作为每种属性收集了新的视频数据集，包含合成训练/测试划分和真实场景划分，并探索了基于经典视觉线索、简单读出机制等方法进行物理属性推断。这些数据集和推断方法可用于评估生成视频的物理正确性，也可为视频模型提供物理动态训练数据，是物理合理性研究的重要资源。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 许多物理属性只能从时序信息中推断，缺乏相应数据集和方法。
method: 收集弹性、粘度、摩擦三类物理属性的视频数据集，并探索基于视觉线索与视频基础模型的属性推断方法。
result: 构建了同时包含合成与真实数据的基准集，并验证了多种推断途径的有效性。
conclusion: 该工作为物理属性推断和视频物理合理性评估提供了数据集与方法支撑。
---

## Abstract
We study the task of predicting dynamic physical properties from videos. More specifically, we consider physical properties that require temporal information to be inferred: elasticity of a bouncing object, viscosity of a flowing liquid, and dynamic friction of an object sliding on a surface. To this end, we make the following contributions: (i) We collect a new video dataset for each physical property, consisting of synthetic training and testing splits, as well as a real split for real world evaluation. (ii) We explore three ways to infer the physical property from videos: (a) an oracle method where we supply the visual cues that intrinsically reflect the property using classical computer vision techniques; (b) a simple read out mechanism using a visual prompt and trainable prompt vector for cross-attention on pre-trained video generative and self-supervised models; and (c) prompt strategies for Multi-modal Large Language Models (MLLMs). (iii) We show that video foundation models trained in a generative or self-supervised manner achieve a similar performance, though behind that of the oracle, and MLLMs are currently inferior to the other models, though their performance can be improved through suitable prompting.

---

## 论文详细总结（自动生成）

好的，我将根据您提供的论文元数据信息，为您生成一份详细的中文总结。

---

### 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：该论文聚焦于**从视频中推断动态物理属性**这一核心任务。与颜色、形状等静态属性不同，许多关键的物理属性（如弹性、粘度、动摩擦）**只能通过物体的时序运动信息来推断**。
- **研究动机**：理解物理世界的动态属性对于人工智能系统（如具身智能、视频理解）至关重要。然而，目前缺乏专门用于推断这些动态属性的数据集和相应的研究方法，这限制了模型对物理世界动态规律的学习与评估能力。
- **整体含义**：该工作旨在填补这一空白，通过构建新数据集和探索多种推断方法，推动视频模型从“看见”向“理解”物理动态的迈进。这项工作不仅为物理属性推断提供了基准，也为评估生成视频的物理正确性提供了重要资源。

### 2. 论文提出的方法论

- **核心思想**：针对弹性、粘度、动摩擦三类动态物理属性，该工作开创性地收集并构建了专门的视频数据集，并探索了三种由浅入深、相互补充的物理属性推断途径。
- **关键技术细节**：论文探索了三种技术路线：
  - **(a) Oracle 方法（基于经典视觉线索）**：采用经典计算机视觉技术，从视频中提取能**内在反映物理属性的视觉线索**（如形变程度、流动速度、位移变化），作为属性推断的强先验或直接依据。
  - **(b) 简单读出机制（基于视频基础模型）**：利用预训练的视频生成模型或自监督模型，通过**视觉提示（visual prompt）** 和**可训练提示向量（trainable prompt vector）** 进行**交叉注意力（cross-attention）**，从而“读出”视频中蕴含的物理属性。这种方法旨在验证视频基础模型是否隐式编码了物理知识。
  - **(c) MLLM 提示策略**：设计不同的**提示词策略（prompt strategies）** 来引导多模态大语言模型（MLLMs）进行物理属性的推断。

### 3. 实验设计

- **数据集 / 场景**：
  - 该工作为每一种物理属性（弹性、粘度、动摩擦）都新收集了**专门的视频数据集**。
  - 数据集包含**合成训练/测试划分**（用于模型训练和受控评估）和**真实场景划分**（用于真实世界评估），形成了一个同时覆盖合成与真实数据的**基准集（benchmark）**。
- **对比方法**：
  - 实验对比了三种方法：**(a) Oracle 方法**、**(b) 基于视频基础模型的简单读出机制**、**(c) MLLM 提示策略**。

### 4. 资源与算力

- 根据提供的元数据信息，该论文的摘要和描述中**未明确说明**其使用的具体算力资源（如 GPU 型号、数量、训练时长等）。

### 5. 实验数量与充分性

- **实验数量**：论文针对三种属性分别构建了数据集的合成/真实划分，并系统性地对比了三种不同范式的推断方法，实验范围覆盖了多种主流技术路线。
- **充分性与客观性**：实验设计包含了合成数据（可控环境）和真实数据（挑战性环境）的评估，能够较为客观地反映模型性能。结论指出视频基础模型性能接近 Oracle 但仍有差距，而 MLLM 表现相对不足，这一对比为不同技术路线提供了清晰的性能定位。整体来看，实验设计具有一定充分性，但其公平性（如不同模型的参数量、训练细节是否对齐）和覆盖度（如真实世界场景的多样性）在摘要中无法完全体现。

### 6. 论文的主要结论与发现

- 视频基础模型（无论是生成式还是自监督式）在推断动态物理属性方面表现**相似**，但性能均**不及**基于视觉线索的 Oracle 方法。
- 多模态大语言模型（MLLMs）在这项任务上的表现**目前逊于**其他模型。
- 然而，通过**合适的提示策略**，MLLMs 的性能可以得到有效**改善**。
- 该工作构建的数据集和推断方法，可用于评估生成视频的物理正确性，并可为视频模型提供物理动态训练数据。

### 7. 优点

- **填补空白**：首次系统性地构建了针对动态物理属性推断的基准数据集，同时包含合成和真实场景，具有重要的资源价值。
- **方法论全面**：探索了从经典视觉技术、视频基础模型到多模态大模型的多种推断路径，通过与 Oracle 方法的对比，能够清晰衡量各方法的当前潜力与瓶颈。
- **应用价值高**：数据集和方法不仅服务于推断任务本身，还可用于生成视频的物理合理性评估，为视频生成领域提供了新的验证工具。

### 8. 不足与局限

- **应用范围限制**：论文仅考虑了弹性、粘度和动摩擦三种物理属性，未覆盖其他动态物理属性（如碰撞、流体湍流、热力学等）。
- **性能差距**：当前表现最好的视频基础模型仍然落后于 Oracle 方法，说明模型对物理动态的隐式理解能力有限；MLLM 的表现更需要进一步提升。
- **信息透明度**：公开信息中未提及算力资源和实验细节，难以对方法的复现成本进行准确评估。
- **潜在偏差风险**：合成数据与真实数据之间可能存在域差距，仅凭摘要无法判断模型在跨域泛化上的表现，真实世界实验的覆盖度和多样性也可能有限。

---

（完）
