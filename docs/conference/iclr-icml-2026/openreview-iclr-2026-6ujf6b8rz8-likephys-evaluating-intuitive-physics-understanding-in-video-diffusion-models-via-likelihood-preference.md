---
title: "LikePhys: Evaluating Intuitive Physics Understanding in Video Diffusion Models via Likelihood Preference"
title_zh: LikePhys：基于似然偏好评估视频扩散模型的直觉物理理解能力
authors: "Jianhao Yuan, Fabio Pizzati, Francesco Pinto, Lars Kunze, Ivan Laptev, Paul Newman, Philip Torr, Daniele De Martini"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=6UJf6B8RZ8"
tags: ["query:phys-video"]
score: 9.0
evidence: 提出基于似然偏好、免训练的视频扩散模型直觉物理评估基准。
tldr: 视频扩散模型的物理合理性评估常受外观与物理因素混杂的干扰。LikePhys 提出免训练评估方法，利用去噪目标作为ELBO式似然代理，在有效-无效视频对上区分物理是否合理，并构建了覆盖四个物理领域、十二个场景的基准。实验表明该指标能有效反映模型的直觉物理理解能力，为生成视频的物理正确性测评提供了新工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 视频扩散模型物理合理性难评估，因外观与物理因素难以解耦。
method: 使用去噪目标构造ELBO式似然代理，在有效-无效视频对上区分物理有效性。
result: 在十二个场景、四个物理域基准上验证了指标的有效性。
conclusion: 提供免训练的物理评估方法，可成为物理合理视频生成的重要衡量标准。
---

## Abstract
Intuitive physics understanding in video diffusion models plays an essential role in building general-purpose physically plausible world simulators, yet accurately evaluating such capacity remains a challenging task due to the difficulty in disentangling physics correctness from visual appearance in generation. To the end, we introduce LikePhys, a training-free method that evaluates intuitive physics in video diffusion models by distinguishing physically valid and impossible videos using the denoising objective as an ELBO-based likelihood surrogate on a curated dataset of valid-invalid pairs. By testing on our constructed benchmark of twelve scenarios spanning over four physics domains, we show that our evaluation metric, Plausibility Preference Error (PPE), demonstrates strong alignment with human
preference, outperforming state-of-the-art evaluator baselines. We then systematically benchmark intuitive physics understanding in current video diffusion models. Our study further analyses how model design and inference settings affect intuitive physics understanding and highlights domain-specific capacity variations across physical laws. Empirical results show that, despite current models struggling with complex and chaotic dynamics, there is a clear trend of improvement in physics understanding as model capacity and inference settings scale up.

---

## 论文详细总结（自动生成）

# 中文总结

## 1. 论文的核心问题与整体含义

- **研究背景**：视频扩散模型被视为构建通用物理合理世界模拟器的潜在基础，但其是否真正具备“直觉物理理解”能力仍不明确。
- **核心问题**：如何准确评估视频扩散模型对物理规律的直觉理解？难点在于生成视频中的物理正确性与视觉外观高度耦合，难以将物理因素从外观中分离出来进行独立评估。
- **整体含义**：论文尝试提出一种不依赖人工标注、不需要额外训练的评估方法，以区分“物理有效”与“物理不可能”的视频，从而量化模型的物理理解能力，并推动物理合理视频生成的发展。

## 2. 论文提出的方法论

- **核心思想**：利用视频扩散模型的**去噪目标（denoising objective）**作为**ELBO 式似然代理（ELBO-based likelihood surrogate）**，通过比较物理有效与物理无效视频对的似然偏好，来判断模型是否具有物理合理性判断能力。
- **关键技术细节**：
  - 方法名为 **LikePhys**，属于 **免训练（training-free）** 评估方法，不需要额外训练评估器。
  - 构建**有效-无效视频对（valid-invalid pairs）**，成对输入评估指标，利用去噪损失计算模型对视频的似然估计。
  - 若模型更偏好物理有效的视频（即赋予更高似然），则说明其具备较好的直觉物理理解。
- **评估指标**：提出 **Plausibility Preference Error（PPE）**，用于量化模型偏好与人类一致性之间的误差，PPE 越低表示模型的物理判断越接近人类偏好。

## 3. 实验设计

- **基准构建**：论文构建了覆盖 **4 个物理领域、12 个场景** 的评估基准，具体物理领域和场景在摘要中未详细列出，但强调涵盖多样化的物理规则。
- **数据集使用**：基于自建的“有效-无效”视频对数据集，视频对由物理合理与物理不合理版本组成。
- **对比方法**：与 **state-of-the-art evaluator baselines** 进行对比，摘要表明 LikePhys 的 PPE 指标显著优于这些基线。
- **评测对象**：多个当前主流的视频扩散模型，用于系统评估其直觉物理理解能力。
- **额外分析**：
  - 探究模型设计（如架构、规模）对物理理解的影响；
  - 探究推理设置（如采样步数等）的影响；
  - 分析不同物理领域的表现差异。

## 4. 资源与算力

- 论文摘要中 **未明确说明** 使用的 GPU 型号、数量、训练时长或推理算力等信息。
- 由于 LikePhys 本身是免训练方法，其主要计算成本来自在视频对上运行视频扩散模型的去噪过程；但原文未提供具体算力配置，因此无法总结具体资源开销。

## 5. 实验数量与充分性

- **实验数量**：摘要中展示的实验包括：
  - 12 个场景、4 个物理域上的基准评估；
  - 与多个 SOTA 评估基线的对比；
  - 对当前视频扩散模型的系统性基准测试；
  - 模型设计（如规模）与推理设置的影响分析；
  - 物理领域间差异分析。
- **充分性评价**：
  - 从覆盖的物理领域和场景数量来看，实验设计较为扎实，能够初步验证指标的有效性。
  - 但是摘要未提供消融实验的具体细节（如是否验证不同去噪步数、不同视频长度、不同噪声级别等），也未见统计显著性检验、跨数据集泛化实验等，因此在公开信息范围内，实验的“充分性”只能说是中等偏上，具体细节需要完整论文进一步确认。
  - 客观性与公平性方面，与 SOTA 基线的对比以及人类偏好对齐的评估方式，增强了结果的可信度。

## 6. 论文的主要结论与发现

- LikePhys 提出的 PPE 指标与人类偏好高度对齐，优于现有评估基线。
- 当前视频扩散模型在复杂的、混沌的动力学场景中表现不佳，直觉物理理解能力仍有显著缺口。
- 随着模型容量（如参数量、架构规模）和推理设置（如计算量）的提升，模型的物理理解能力呈现明显改善趋势。
- 不同物理领域之间的表现存在差异性，说明模型对某些物理规律（如简单刚体运动）更敏感，而对复杂混沌系统更困难。
- 总体而言，LikePhys 可作为评价和指导物理合理视频生成的有效工具。

## 7. 优点

- **免训练设计**：无需训练额外评估器，直接利用扩散模型的内部似然信号，简单高效且通用。
- **解耦物理与外观**：通过成对视频对比，有效降低外观差异带来的干扰，针对性地测量物理合理性。
- **与人类对齐的指标**：PPE 以人类偏好为参照，使评估更具语义合理性和实用性。
- **系统性基准**：覆盖 4 个物理领域、12 个场景，相比单一场景评估具有更好的覆盖面。
- **可扩展性**：方法不依赖特定模型结构，可推广到不同的视频扩散模型。

## 8. 不足与局限

- **信息缺失**：摘要中未提供详细的方法公式、数据集构建细节、人类标注协议以及算力配置，难以完整复现。
- **可能的选择偏差**：有效-无效视频对的构建方式可能影响结果，若物理无效视频的构造方式单一，模型可能学习到特定伪影而非真正的物理偏好。
- **外观混淆仍未完全消除**：尽管成对设计有助于解耦，但视频对之间仍可能存在细微外观差异，影响似然判断。
- **覆盖范围有限**：4 个物理域 12 个场景虽具多样性，但相比于真实世界丰富的物理现象仍较有限，尤其缺乏交互式、多物体、非刚体等复杂情况。
- **未讨论效率问题**：对于长视频或高分辨率视频，运行多次去噪过程可能带来较高的计算成本，论文未提供优化或实用性讨论。
- **未提供失败案例分析**：未说明该方法在哪些场景下失效，以及其适用范围边界。

（完）
