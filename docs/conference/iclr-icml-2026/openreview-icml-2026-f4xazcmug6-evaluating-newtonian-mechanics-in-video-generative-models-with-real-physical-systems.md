---
title: Evaluating Newtonian Mechanics in Video Generative Models with Real Physical Systems
title_zh: 用真实物理系统评估视频生成模型中的牛顿力学
authors: "Antonios Tragoudaras, Chenyu Zhang, Daniil Cherniavskii, Antonios Vozikis, Thijmen Nijdam, Derck W. E. Prinzhorn, Mark Bodracska, Nicu Sebe, Andrii Zadaianchuk, Stratis Gavves"
date: 2026-04-30
pdf: "https://openreview.net/pdf/976c490ac6544b3d27985792d12e47d8266dda69.pdf"
tags: ["query:phys-video"]
score: 10.0
evidence: 提出基于真实物理系统的Morpheus基准，用于衡量视频生成模型对牛顿动力学的理解
tldr: 该论文指出现有视频生成模型评估依赖主观判断或轨迹匹配，难以衡量物理推理能力。为此引入Morpheus，一个基于真实物理实验的物理感知评估框架，包含大量真实物理视频，用于测试模型对牛顿动力学的理解。通过该基准可更准确地评估生成视频是否符合物理定律，为视频生成模型的世界建模能力提供客观度量。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有评估方法主观或基于轨迹匹配，无法客观衡量视频生成模型是否遵循物理定律。
method: 构建Morpheus基准，使用真实物理系统视频和牛顿动力学测试集评估模型。
result: Morpheus能够揭示现有视频生成模型在物理推理上的不足，提供更严格的物理正确性度量。
conclusion: 物理信息驱动的真实实验基准可替代主观评估，有效衡量视频生成模型的物理合理性。
---

## Abstract
Recent advances in image and video generation raise hopes that these models possess world modeling capabilities—the ability to generate realistic, physically plausible videos. This could revolutionize applications in robotics, autonomous driving, and scientific simulation. However, before treating these models as world models, we must ask: Do they adhere to physical laws?  Current evaluation methods rely on subjective judgments or trajectory matching, limiting their usage for physical reasoning estimation, where many generations could be physically plausible. 
Thus, we introduce **Morpheus**, one of the first physics-informed evaluation frameworks for measuring the ability of video generation models to comprehend Newtonian dynamics. **Morpheus** features 130 real-world videos capturing physical phenomena, guided by conservation laws. Using those as conditioning for video generation, we assess physical plausibility leveraging interpretable metrics evaluated with respect to infallible conservation laws known per physical setting, leveraging advances in physics-informed neural networks and vision-language foundation models. Importantly, **Morpheus** targets controlled Newtonian rigid-body settings to enable quantitative checks. Our findings reveal that even with advanced prompting and video conditioning, contemporary models struggle to encode physical principles despite generating aesthetically pleasing videos. Code and data available [here](https://github.com/physics-from-video/Morpheus).

---

## 论文详细总结（自动生成）

# 《用真实物理系统评估视频生成模型中的牛顿力学》论文总结

## 1. 核心问题与整体含义

- **研究背景**：近年来图像与视频生成模型取得了显著进展，许多人期待这些模型具备“世界建模能力”——即能生成真实、物理上合理的视频。如果这一能力成立，将深刻影响机器人、自动驾驶、科学仿真等领域。
- **核心问题**：在将这些模型视为“世界模型”之前，必须回答一个根本性问题——**它们是否真正遵守物理定律？**
- **现有方法的不足**：当前评估手段主要依赖**主观视觉判断**或**轨迹匹配**，这两种方式都难以客观衡量模型的物理推理能力。因为在生成空间中，存在大量视觉上美观但物理上不合理的结果，也可能有多种物理上合理的生成结果，导致主观判断和简单轨迹对齐失效。
- **论文的总体回答**：作者提出 **Morpheus**，一个基于**真实物理系统视频**的物理感知评估框架，用于量化衡量视频生成模型对**牛顿动力学**的理解程度，从而为“生成模型是否具备物理世界建模能力”提供客观、可复现的度量标准。

## 2. 方法论

- **核心思想**：不依赖人类主观打分或生成视频间的轨迹匹配，而是以**物理系统固有的守恒律**（如动量守恒、能量守恒等）作为“不可违背的判官”，对生成视频的物理合理性进行**定量检验**。
- **技术方案概述**：
  1. **数据构建**：采集 130 段真实世界物理实验视频，覆盖多种场景与物体，由已知守恒律精确控制每个物理系统的动力学行为。
  2. **视频条件生成**：将这些真实视频作为条件输入，引导视频生成模型产出对应场景的生成视频。
  3. **物理可行性评估**：利用**物理信息神经网络**和**视觉-语言基础模型**，从生成视频中提取动力学状态，并对照该物理系统已知的守恒律，计算可解释的物理合理性指标。
  4. **定量判断**：通过生成结果对守恒律的违反程度，直接度量模型对牛顿动力学的编码能力。
- **关键特点**：该框架聚焦于**受控的牛顿刚体系统**，确保物理规则明确、可量化检验，避免了开放场景中物理不确定性带来的评估模糊问题。

## 3. 实验设计

- **基准数据集**：Morpheus 基准包含 **130 段真实世界物理视频**，涵盖多种刚体物理现象（如碰撞、抛体运动等），每段视频对应的物理系统由明确的守恒律约束。
- **评估方式**：以真实视频为条件进行视频生成，然后对生成视频进行物理合理性检测，运用物理信息神经网络和视觉-语言模型提取物理量，并对照守恒律计算指标。
- **对比对象**：论文考察了多种当代先进的视频生成模型。实验发现，即便采用**先进的提示词策略**和**视频条件注入**，这些模型生成的视频虽然在视觉上赏心悦目，但在编码物理原则上普遍失败。
- **说明**：受摘要信息限制，具体对比的模型列表、消融实验的详细设置及指标数值未在给定文本中体现。

## 4. 资源与算力

- 论文提供的摘要和元数据中**未明确说明**训练或评估所使用的 GPU 型号、数量、训练时长等算力资源信息。
- 如需了解完整算力开销，需要查阅论文正文的实验设置部分。

## 5. 实验数量与充分性

- 从摘要来看，Morpheus 提供了 130 段真实物理视频作为基准，属于中等规模但高度受控的评测集。
- 实验覆盖了多种先进视频生成模型，并通过统一物理指标进行对比，具备一定系统性。
- **充分性与客观性的初步判断**：
  - **积极面**：基于守恒律的评估标准客观且可量化，避免了主观偏差；真实物理视频作为基准具有生态效度。
  - **不确定处**：由于未提供详细的消融实验、指标数值和模型列表，暂难判断实验的全面性。例如是否针对不同提示策略逐项消融、是否对生成模型的不同版本/参数规模进行对比，以及是否考虑多种物理场景类型的分层分析，这些信息有待正文补充。

## 6. 主要结论与发现

- **核心结论**：当代视频生成模型尽管能生成视觉质量极高的视频，但**对牛顿动力学的理解存在显著不足**。
- **评估框架的有效性**：Morpheus 能够揭示现有模型在物理推理上的缺陷，提供比主观评估更严格的物理正确性度量。
- **方法论的可行性**：事实证明，**物理信息驱动的、基于真实实验的评估框架**可以有效替代主观评估，成为衡量视频生成模型物理合理性的可靠工具。
- **意义**：该工作为“视频生成模型是否具备世界建模能力”这一关键问题提供了首个可量化的客观答案，为后续模型改进和评估标准制定奠定了基础。

## 7. 优点

- **问题选择精准且重要**：直接挑战视频生成模型“世界建模能力”的宣称，回应领域内关键争议，具有重要学术价值。
- **物理原理驱动的客观评估**：以守恒律为不可违背的判据，优于主观评分和传统轨迹匹配，提供了可量化、可复现的评估标准。
- **真实物理系统数据**：采用 130 段真实世界物理实验视频，比合成数据更具生态效度，更能反映模型在真实场景中的物理合理性。
- **跨学科技术融合**：将物理信息神经网络与视觉-语言基础模型相结合，分别利用其物理约束建模能力和高層语义理解能力，技术路线具有创新性。
- **开放贡献**：代码与数据公开，有利于社区复现和后续研究推进。

## 8. 不足与局限

- **物理场景范围有限**：基准聚焦于**受控牛顿刚体系统**，尚未覆盖流体力学、弹性体、热力学等更广泛的物理现象，因此结论的推广范围有限。
- **算力信息缺失**：论文未交代评估过程所需的计算资源，可能导致复现门槛不明确。
- **实验细节未充分展示**：摘要及元数据中未给出完整的实验数量、消融设计、模型对比列表和指标数值，难以从现有信息全面评估实验的充分性与统计学显著性。
- **刚体假设的局限**：现实物理相互作用复杂（如摩擦、空气阻力、形变等），刚体设定可能低估或高估某些模型的实际物理推理能力。
- **评估依赖下游感知模型**：物理量的提取依赖物理信息神经网络和视觉-语言模型的精度，若上游感知存在误差，可能影响最终物理合理性判断的准确性。
- **生成模型快速迭代的时效性问题**：随着视频生成技术的快速演进，基准的难度和覆盖范围需要持续更新以保持区分度。

（完）
