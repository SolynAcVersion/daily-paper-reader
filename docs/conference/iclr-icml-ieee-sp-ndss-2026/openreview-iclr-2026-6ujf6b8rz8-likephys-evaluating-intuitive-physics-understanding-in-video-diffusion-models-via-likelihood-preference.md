---
title: "LikePhys: Evaluating Intuitive Physics Understanding in Video Diffusion Models via Likelihood Preference"
title_zh: LikePhys：通过似然偏好评估视频扩散模型的直观物理理解
authors: "Jianhao Yuan, Fabio Pizzati, Francesco Pinto, Lars Kunze, Ivan Laptev, Paul Newman, Philip Torr, Daniele De Martini"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=6UJf6B8RZ8"
tags: ["query:phys-video"]
score: 9.0
evidence: 基于似然偏好的训练无关物理直觉评估方法
tldr: 视频扩散模型需要具备直观物理理解才能成为物理合理的世界模拟器，但现有评测难以将物理正确性与视觉外观分离。LikePhys提出一种免训练评估方法，利用去噪目标作为ELBO似然代理，在有配对数据上区分物理有效与不可能的生成视频。在涵盖四个物理领域、十二个场景的基准上验证了该指标的有效性。这为视频生成模型的物理合理性提供了无需额外训练的评测新思路。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 难以将物理正确性与视觉外观分离评测视频扩散模型。
method: 用去噪目标作ELBO似然近似，在有效-无效视频对上比较物理合理性。
result: 在十二个物理场景上验证了评测指标的有效性。
conclusion: 提供了无需训练的物理合理性评测方法。
---

## Abstract
Intuitive physics understanding in video diffusion models plays an essential role in building general-purpose physically plausible world simulators, yet accurately evaluating such capacity remains a challenging task due to the difficulty in disentangling physics correctness from visual appearance in generation. To the end, we introduce LikePhys, a training-free method that evaluates intuitive physics in video diffusion models by distinguishing physically valid and impossible videos using the denoising objective as an ELBO-based likelihood surrogate on a curated dataset of valid-invalid pairs. By testing on our constructed benchmark of twelve scenarios spanning over four physics domains, we show that our evaluation metric, Plausibility Preference Error (PPE), demonstrates strong alignment with human
preference, outperforming state-of-the-art evaluator baselines. We then systematically benchmark intuitive physics understanding in current video diffusion models. Our study further analyses how model design and inference settings affect intuitive physics understanding and highlights domain-specific capacity variations across physical laws. Empirical results show that, despite current models struggling with complex and chaotic dynamics, there is a clear trend of improvement in physics understanding as model capacity and inference settings scale up.

---

## 论文详细总结（自动生成）

# LikePhys: 通过似然偏好评估视频扩散模型的直观物理理解——中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：视频扩散模型（Video Diffusion Models）若要成为通用的、物理上合理的世界模拟器，必须具备直观物理理解能力（intuitive physics understanding），即能够生成符合物理规律的视频内容。
- **现有挑战**：如何准确评估这种物理理解能力一直是个难题。主要原因在于，生成视频的**物理正确性**与**视觉外观**高度耦合，难以将二者解耦并对“物理合理性”进行独立、可量化的度量。
- **研究意义**：缺乏可靠的物理合理性评测方法，就难以指导模型能力诊断、对比和改进，也无法回答“当前视频扩散模型到底懂不懂物理”这一关键问题。因此，该论文聚焦于构建一个**无需训练、可分离物理正确性**的评测指标，为物理合理的世界模拟器研究提供基础工具。

## 2. 方法论：核心思想、技术细节与流程

- **核心思想**：利用扩散模型的**去噪目标（denoising objective）**作为**基于ELBO的似然代理（ELBO-based likelihood surrogate）**，通过比较物理有效视频和物理不可能视频之间的“似然偏好”来判断模型是否具备直观物理理解。
- **关键假设**：如果模型真正“理解”物理规律，那么对于同一内容的两段视频（一段符合物理、一段违反物理），模型应赋予物理有效视频更高的似然（即去噪损失更低）。
- **技术细节**：
  - **训练无关（training-free）**：评测时不需要对模型进行任何微调或额外训练，直接使用预训练模型的去噪损失进行评分。
  - **成对比较机制**：在精心构建的“有效-无效视频对”（valid-invalid pairs）上，分别计算模型对两个视频的似然分数，比较其相对偏好，从而消除视觉外观差异的干扰。
  - **评测指标**：提出 **Plausibility Preference Error（PPE）**，用于量化模型偏好与人类偏好的不一致程度，PPE越低表示模型对物理合理性的判断越接近人类。
- **整体流程**（文字描述）：
  1. 构建包含物理有效视频与对应物理无效视频（在相同场景内容下违反特定物理定律）的数据集；
  2. 将每对视频分别输入视频扩散模型，计算去噪目标以近似其ELBO似然；
  3. 比较两个似然分数，判断模型偏好哪个视频；
  4. 将模型偏好与人类标注偏好比对，计算PPE评估指标；
  5. 在多个物理领域和场景上重复该过程，系统评估模型能力。

## 3. 实验设计：数据集、基准与对比方法

- **基准（Benchmark）**：论文构建了覆盖**四个物理领域**、**十二个场景**的评测基准，具体领域和场景在摘要中未详细展开，但暗示包括常见物理规律（如重力、碰撞、流体动力学、刚体运动等，具体以原文为准）。
- **数据集**：采用“有效-无效视频对”的成对数据集，每个场景均包含物理上可能和不可能的视频，用于消除外观混淆。
- **对比方法**：与**最先进（state-of-the-art）的评估器基线**进行比较，证明LikePhys指标在PPE上优于这些基线，并与人类偏好高度对齐。
- **模型评测**：基于该基准，系统评估了当前若干视频扩散模型的直观物理理解能力，并分析了模型设计（如容量、架构）和推理设置（如采样步数等）的影响。

## 4. 资源与算力

- 论文提供的摘要和元数据中**未提及**任何关于GPU型号、数量、训练时长或推理算力的具体信息。
- 由于LikePhys本身是**免训练**方法，其直接评测成本主要是对预训练模型进行多次去噪前向传播，但具体算力需求无法从给定文本中获知。
- 如需了解资源细节，建议查阅论文原文的实验设置部分。

## 5. 实验数量与充分性

- **实验数量**：从摘要可知至少包括：
  - 一个包含12个场景、4个物理领域的新评测基准；
  - 在基准上对LikePhys指标有效性的验证（与人类偏好对齐、对比SOTA基线）；
  - 对当前视频扩散模型的系统benchmark；
  - 对模型设计（容量等）和推理设置影响的额外分析；
  - 对物理领域间能力差异的分析。
- **充分性评价**：
  - **正面**：覆盖多物理领域和多场景，且采用成对设计，能较好地隔离外观影响；与人类偏好对齐的验证增强了指标可信度。
  - **局限**：由于仅提供摘要，无法判断消融实验、统计显著性检验、基线选择是否全面，也无法确认场景覆盖是否均匀、是否存在数据偏差。因此，从现有信息看，实验设计较为系统，但充分性需结合原文进一步评估。

## 6. 主要结论与发现

- **LikePhys指标有效**：通过去噪目标作为ELBO似然代理，能够在成对数据上有效区分物理有效和不可能的视频，其评估结果与人类偏好的一致性优于现有SOTA评估器基线。
- **当前模型存在明显短板**：现有视频扩散模型在处理**复杂和混沌动态**（complex and chaotic dynamics）时仍然吃力，直观物理理解能力有限。
- **能力随规模提升**：随着模型容量增大和推理设置优化（如更多采样步数），物理理解能力呈现**清晰的改善趋势**。
- **领域能力差异**：模型对不同物理规律的掌握程度存在差异，暗示需要针对性地改进。

## 7. 优点

- **免训练评测**：无需微调或额外训练，即插即用，部署成本低，易于推广到任意视频扩散模型。
- **解耦物理与外观**：通过有效-无效视频对比较，有效剥离视觉外观对物理判断的干扰，直击评测核心难题。
- **理论支撑**：采用ELBO似然代理，从扩散模型的生成原理出发，具有明确的统计学动机。
- **与人类偏好对齐**：提出的PPE指标经过人类偏好验证，保证评测结果符合直觉认知。
- **系统化基准**：覆盖多个物理领域和场景，为后续研究提供可复用的评价工具。

## 8. 不足与局限

- **仅适用成对比较**：该指标只能判断相对物理合理性，无法给出绝对物理置信度，也难以用于单视频评分。
- **似然代理的近似误差**：去噪目标只是ELBO的一个代理，可能受扩散模型参数化、噪声调度等因素影响，未必能完全反映真实似然。
- **物理场景覆盖有限**：即使有12个场景，仍无法涵盖真实世界全部物理规律；摘要未提及场景类型细节，可能存在偏向简单物理现象的风险。
- **对人类偏好的依赖**：人类标注本身可能存在主观性或对细微物理违例不敏感，导致偏好标注噪声。
- **评估范围局限**：主要考察生成模型的“判别性”物理理解（即区分有效性），但“生成性”物理一致性（即直接生成物理合理的新内容）是否被充分评估尚不明确。
- **信息透明度限制**：由于未能获取全文，本文总结的内容仅基于摘要和元数据，关于模型列表、消融设计、统计显著性等细节无法确证。

（完）
