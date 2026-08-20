---
title: Benchmarking Physical Reasoning of Video Generative Models with Real Physical Experiments
title_zh: 用真实物理实验评测视频生成模型的物理推理能力
authors: "Chenyu Zhang, Daniil Cherniavskii, Antonios Tragoudaras, Antonios Vozikis, Thijmen Nijdam, Derck W. E. Prinzhorn, Mark Bodracska, Nicu Sebe, Andrii Zadaianchuk, Stratis Gavves"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=1E6pburMKc"
tags: ["query:phys-video"]
score: 10.0
evidence: 提出Morpheus基准，包含130个真实世界物理实验视频，用于评估视频生成模型的物理推理能力
tldr: 该论文与Morpheus基准相同，针对视频生成模型物理推理评估能力不足的问题，构建了一个包含130个真实世界物理现象视频的基准。该基准用于检测生成视频是否遵循物理规律，避免主观判断或轨迹匹配的局限。通过对视频生成模型的系统评测，能够更客观地衡量其对物理世界的理解程度。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有评估依赖主观判断或轨迹匹配，无法准确刻画视频生成模型的物理推理能力。
method: 构建130个真实物理实验视频的Morpheus基准，用于评估视频生成模型的物理合理性。
result: 该基准能够揭示模型在物理推理上的差异，为视频生成模型的世界建模提供可靠评测。
conclusion: 真实世界物理视频基准可有效衡量视频生成模型的物理推理能力，推动物理合理生成研究。
---

## Abstract
Recent advances in image and video generation raise hopes that these models possess world modeling capabilities—the ability to generate realistic, physically plausible videos. This could revolutionize applications in robotics, autonomous driving, and scientific simulation. However, before treating these models as world models, we must ask: Do they adhere to physical laws?  Current evaluation methods rely on subjective judgments or trajectory matching, limiting their usage for physical reasoning estimation, where many generations could be physically plausible. 
Thus, we introduce **Morpheus**, a new benchmark for evaluating video generation models on physical reasoning. It features 130 real-world videos capturing physical phenomena, guided by conservation laws. Using those as conditioning for video generation, we assess physical plausibility using physics-informed metrics evaluated with respect to infallible conservation laws known per physical setting, leveraging advances in physics-informed neural networks and vision-language foundation models.
% Since artificial generations lack ground truth, we assess physical plausibility using physics-informed metrics evaluated with respect to infallible conservation laws known per physical setting, leveraging advances in physics-informed neural networks and vision-language foundation models. 
Our findings reveal that even with advanced prompting and video conditioning, current models struggle to encode physical principles despite generating aesthetically pleasing videos.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **研究动机**：图像和视频生成模型的快速发展使人们期待它们具备“世界建模能力”，即生成符合物理规律的真实视频。这类能力对机器人、自动驾驶、科学模拟等应用至关重要。
- **核心问题**：在将视频生成模型视为世界模型之前，需要验证一个关键问题——**它们的生成结果是否遵守物理定律？**
- **现有评估缺陷**：当前评估方法主要依赖主观视觉判断或轨迹匹配，难以准确衡量物理推理能力。因为许多生成结果在视觉上合理但物理上不一定正确，轨迹匹配也忽略了多解性（多种生成都可能是物理可行的）。
- **整体含义**：需要一个新的基准来客观、可靠地评估视频生成模型对物理世界的理解，从而推动物理合理的视频生成研究。

## 2. 方法论

- **核心思想**：构建一个基于真实物理实验的基准，利用**守恒定律**作为不可违背的物理约束，通过物理启发的量化指标来评估生成视频的物理合理性。
- **基准名称**：**Morpheus**
- **关键组成**：
  - 包含 **130 个真实世界视频**，记录具体物理现象，并以守恒定律（如能量守恒、动量守恒等）为指导。
  - 使用这些视频作为条件（conditioning）来驱动视频生成模型。
  - 评估时，依赖**物理信息神经网络**（Physics-Informed Neural Networks）和**视觉-语言基础模型**（Vision-Language Foundation Models）提取物理特征，并计算与已知守恒定律的一致性指标。
- **技术流程（文字说明）**：
  1. 收集真实物理实验视频，确定每个场景对应的守恒定律。
  2. 将视频作为条件输入，让待测视频生成模型生成新的视频。
  3. 利用物理信息神经网络对生成视频进行物理量分析。
  4. 借助视觉-语言模型理解视频内容，结合已知守恒定律计算物理合理性评分。
  5. 通过该评分比较不同模型的物理推理能力。

## 3. 实验设计

- **数据集/基准**：Morpheus 基准，包含 130 个真实世界物理现象视频，覆盖多种物理场景，由守恒定律引导。
- **评估对象**：视频生成模型（原文未列出具体模型名称，推测包括当前先进生成模型）。
- **对比方法**：摘要中未明确说明对比的具体基线，但提及“advanced prompting and video conditioning”，暗示实验可能对比了不同提示策略和视频条件输入方式。
- **评估方式**：不依赖人工主观判断或轨迹匹配，而是采用基于守恒定律的物理信息指标，衡量生成结果是否与已知物理规律一致。

## 4. 资源与算力

- **明确指出**：提供的论文文本中**未提及**任何关于 GPU 型号、数量、训练时长或推理成本的信息。
- 因此，无法从该摘要和元数据中总结具体算力消耗。

## 5. 实验数量与充分性

- **实验规模**：目前已知基准包含 130 个真实视频，但关于具体做了多少组生成实验、是否包含消融实验、对比了多少个模型等细节，在提供的文本中**没有说明**。
- **充分性评价**：
  - 从摘要结论看，该基准能够揭示模型在物理推理上的差异，但缺少详细的实验列表和统计分析。
  - 由于缺少对基线模型、消融设置、重复实验次数等关键信息的描述，现有信息不足以全面判断实验的充分性、客观性和公平性。
  - 不过，基于真实物理视频和物理信息指标的设计本身有助于减少主观偏差，提高评估客观性。

## 6. 主要结论与发现

- 当前视频生成模型尽管能生成**美观悦目**的视频，但在**编码物理原理**方面存在显著不足。
- 即使采用了高级提示（advanced prompting）和视频条件（video conditioning）技术，模型仍然难以生成符合物理规律的视频。
- 表明现有模型的世界建模能力有限，需要进一步发展物理合理的生成方法。

## 7. 优点

- **针对性强**：直击视频生成模型物理推理评估缺失的问题。
- **客观性**：使用真实物理实验和不可违背的守恒定律作为基准，避免主观判断。
- **创新方法**：结合物理信息神经网络和视觉-语言基础模型，提供可量化的物理合理性指标。
- **现实意义**：为机器人、自动驾驶等物理交互应用提供可信评估工具。
- **多样性**：130 个真实世界视频覆盖多种物理现象，有助于评估泛化能力。

## 8. 不足与局限

- **信息不完整**：受限于提供的论文文本，方法细节（如具体指标公式、神经网络架构、提示设计）未能展现。
- **实验细节缺失**：未列出具体对比模型、消融实验和统计显著性分析，难以判断结果的鲁棒性。
- **物理范围限制**：基准以守恒定律为核心，可能无法覆盖所有物理推理能力（如接触力学、流体动力学中的非守恒过程）。
- **生成条件依赖**：评估依赖视频条件生成，可能受到模型条件控制能力的影响，而非纯粹的物理推理能力。
- **模型选择偏差风险**：未提及是否包含不同架构或规模的模型，可能有代表性不足的问题。
- **应用限制**：真实物理实验视频的采集可能受限于可重复性和实验环境差异，导致基准扩展和维护困难。

---

（完）
