---
title: Benchmarking Physical Reasoning of Video Generative Models with Real Physical Experiments
title_zh: 用真实物理实验评测视频生成模型的物理推理能力
authors: "Chenyu Zhang, Daniil Cherniavskii, Antonios Tragoudaras, Antonios Vozikis, Thijmen Nijdam, Derck W. E. Prinzhorn, Mark Bodracska, Nicu Sebe, Andrii Zadaianchuk, Stratis Gavves"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=1E6pburMKc"
tags: ["query:phys-video"]
score: 9.0
evidence: Morpheus基准用130个真实物理实验评估视频生成模型的物理推理
tldr: 视频生成模型是否遵循物理定律仍缺少严谨评测。现有方法依赖主观判断和轨迹匹配，难以刻画物理推理能力。Morpheus构建了包含130个真实物理现象视频的基准，系统评估模型对物理规律的理解。该基准为衡量视频生成模型的物理常识和动力学期望提供了更客观的依据。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有评测依赖主观判断或轨迹匹配，无法评估物理推理。
method: 构建130个真实世界物理视频的Morpheus基准。
result: 提供了更客观的物理推理评测，识别了模型不足之处。
conclusion: 为视频生成模型的物理推理评估建立了新基准。
---

## Abstract
Recent advances in image and video generation raise hopes that these models possess world modeling capabilities—the ability to generate realistic, physically plausible videos. This could revolutionize applications in robotics, autonomous driving, and scientific simulation. However, before treating these models as world models, we must ask: Do they adhere to physical laws?  Current evaluation methods rely on subjective judgments or trajectory matching, limiting their usage for physical reasoning estimation, where many generations could be physically plausible. 
Thus, we introduce **Morpheus**, a new benchmark for evaluating video generation models on physical reasoning. It features 130 real-world videos capturing physical phenomena, guided by conservation laws. Using those as conditioning for video generation, we assess physical plausibility using physics-informed metrics evaluated with respect to infallible conservation laws known per physical setting, leveraging advances in physics-informed neural networks and vision-language foundation models.
% Since artificial generations lack ground truth, we assess physical plausibility using physics-informed metrics evaluated with respect to infallible conservation laws known per physical setting, leveraging advances in physics-informed neural networks and vision-language foundation models. 
Our findings reveal that even with advanced prompting and video conditioning, current models struggle to encode physical principles despite generating aesthetically pleasing videos.

---

## 论文详细总结（自动生成）

基于提供的论文元数据与摘要，以下是对论文《Benchmarking Physical Reasoning of Video Generative Models with Real Physical Experiments》的结构化总结：

---

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：视频生成模型在生成流畅、美观的视频时，是否真正理解并遵循物理定律？能否被视为具备“世界模型”能力？
- **背景动因**：近年来图像与视频生成模型的快速发展，使得人们对其在机器人、自动驾驶、科学模拟等领域作为世界模型的潜力寄予厚望。但在将其用于物理推理之前，必须严格检验其生成内容是否符合物理规律。
- **现有评测的缺陷**：当前评估方法主要依赖**主观视觉判断**或**轨迹匹配**。这两类方法无法有效刻画模型的物理推理能力——因为对于同一物理场景，可能存在多种在物理上都合理的生成结果，而主观判断与轨迹匹配都难以覆盖这种多样性。

## 2. 论文提出的方法论

- **核心思想**：构建一个以**真实物理实验视频**为依据、以**守恒定律**为客观判据的评测基准（Morpheus），用物理规律本身来检验视频生成模型输出的物理合理性。
- **技术细节**：
  - 基准包含 130 段真实世界物理现象视频，这些现象由守恒定律（如动量守恒、能量守恒等）所支配。
  - 评测流程：以这些真实视频作为条件输入，引导视频生成模型进行生成。
  - 评估方式：利用**物理信息神经网络**与**视觉语言基础模型**的进展，设计**物理信息指标**，对照每个物理场景已知的守恒定律来评估生成视频的物理合理性。
  - 由于生成视频没有真实标注的 ground truth，该评测方法不依赖人工标注，而是直接以守恒定律作为“不可违背”的客观参照。
- **说明**：文中未提供具体的数学公式或算法伪代码，方法描述停留在高层设计层面。

## 3. 实验设计

- **Benchmark**：提出了名为 **Morpheus** 的新基准，包含 130 个真实世界物理实验视频，覆盖由守恒定律支配的多种物理现象。
- **数据集/场景**：以真实物理实验视频为条件进行视频生成评测，场景由守恒定律驱动。
- **对比方法**：摘要未明确列出对比的生成模型或基线方法，但提到使用**先进的提示词（advanced prompting）与视频条件（video conditioning）** 进行测试。具体对比了哪些模型（如 Sora、GenVideo 等）在文中未作说明。
- **评估维度**：物理合理性（physical plausibility），而非仅图像质量或运动轨迹相似度。

## 4. 资源与算力

- 本文提供的元数据和摘要中**未提及任何具体算力信息**，包括 GPU 型号、数量、训练时长、推理成本等。
- 因此无法对算力开销作总结，需要查阅论文正文或附录以获取相关信息。

## 5. 实验数量与充分性

- 实验规模：摘要仅提到 Morpheus 基准包含 130 个真实物理视频。具体生成实验组数、模型数量、消融实验（如不同评测指标、不同条件设置）等细节未在摘要中披露。
- 充分性与客观性：
  - **优点**：以守恒定律作为客观判据，相比主观判断和轨迹匹配，评测立场更客观。
  - **不足**：从摘要无法判断实验覆盖的模型种类是否全面，也无法确认是否针对不同物理现象类型作了分层分析；消融实验与对比实验的规模未知，故对实验充分性难以作完整评估。

## 6. 主要结论与发现

- **核心发现**：尽管当前视频生成模型能生成**美学上令人满意**的视频，但在**编码物理原理**方面存在明显不足。
- 即便使用了**先进的提示策略**和**视频条件输入**，模型依然难以在生成中体现正确的物理规律。
- 该结论提示：现有模型在多大程度上具备“世界模型”能力，应持审慎态度；Morpheus 为量化这种差距提供了新工具。

## 7. 优点

- **评测视角创新**：用守恒定律作为客观不可违背的判据，避免了主观评价的不稳定性，也比轨迹匹配更适应物理上多解的情况。
- **数据来源真实**：基于 130 个真实物理实验视频，而非合成数据或模拟器输出，增强了评测结果的可信度。
- **跨学科方法融合**：将物理信息神经网络与视觉语言基础模型结合起来用于评测，方法上具有前沿性和集成性。
- **意义明确**：为视频生成模型能否作为世界模型这一关键问题提供了可量化的评测手段，填补了现有评测体系的空白。

## 8. 不足与局限

- **实验细节缺失**：摘要与元数据中未列出具体评测的模型清单、生成参数设置、实验重复次数等，不利于完全复现或横向比较。
- **覆盖范围有限**：130 个视频虽涵盖守恒定律类现象，但物理世界极为多样，未必能覆盖力学以外的电磁学、热力学、流体力学等更复杂场景。
- **条件生成的有效性未知**：视频条件输入是否能在多大程度上约束生成过程，文中未做深入分析。
- **评估指标的内部一致性**：物理信息神经网络和视觉语言模型本身也有误差，其用于判定的可靠性尚需验证。
- **应用限制**：作为一个评测基准，Morpheus 依赖对每个物理场景的守恒定律的预先设定，对于未包含的或复合的物理现象，其评测适用性可能降低。
- **未说明算力与成本**：对使用大规模生成模型进行评测的实际计算开销未加说明，可能影响基准在资源受限场景下的可用性。

---

（完）
