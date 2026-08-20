---
title: "VisPhyWorld: Probing Physical Reasoning via Code-Driven Video Reconstruction"
title_zh: VisPhyWorld：通过代码驱动视频重构探测物理推理
authors: "Jiarong Liang, Max Ku, Ka-Hei Hui, Ping Nie, Wenhu Chen"
date: 2026-01-18
pdf: "https://openreview.net/pdf/0a041130b4503b2422b603bc0a4617b1557077ed.pdf"
tags: ["query:phys-video"]
score: 6.0
evidence: 基于代码执行的物理推理评测基准，将物理推理与渲染分离
tldr: 现有物理推理基准多采用识别式问答或违背预期范式，难以验证模型真正理解物理动态。VisPhyWorld提出基于代码执行的评测框架，要求模型从视觉观察生成可运行模拟器代码，使推断的世界模型可检验、可编辑。构建的VisPhyBench包含209个测评单元，将物理推理与渲染分离，能更可靠地评估模型对物理动态的推理能力。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有物理推理基准多为识别式协议，无法验证模型是否真正做出可检验的物理假设。
method: 提出基于代码执行的评测框架，要求模型生成可运行的模拟器代码，将物理推理与渲染分离。
result: 构建VisPhyBench基准，包含209个评测单元，实现更可靠的物理动态推理评估。
conclusion: VisPhyWorld提供了可检验、可编辑的物理推理评测方式，为多模态模型物理理解研究提供新工具。
---

## Abstract
Evaluating whether Multimodal Large Language Models (MLLMs) genuinely reason about physical dynamics remains challenging.
Most existing benchmarks rely on recognition-style protocols such as Visual Question Answering (VQA) and Violation of Expectation (VoE), which can often be answered without committing to an explicit, testable physical hypothesis. We propose VisPhyWorld, an execution-based framework that evaluates physical reasoning by requiring models to generate executable simulator code from visual observations. By producing runnable code, the inferred world representation is directly inspectable, editable, and falsifiable. This separates physical reasoning from rendering. Building on this framework, we introduce VisPhyBench, comprising 209 evaluation scenes derived from 108 physical templates and a systematic protocol that evaluates how well models reconstruct appearance and reproduce physically plausible motion. Our pipeline produces valid reconstructed videos in 97.7\% on the benchmark. Experiments show that while state-of-the-art MLLMs achieve strong semantic scene understanding, they struggle to accurately infer physical parameters and to simulate consistent physical dynamics.

---

## 论文详细总结（自动生成）

好的，我已经仔细阅读了您提供的论文信息，包括题目、元数据、摘要和简要总结。根据您的要求，我将对这篇论文进行结构化、深入且客观的中文总结。

---

### 论文总结：VisPhyWorld：通过代码驱动视频重构探测物理推理

#### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：如何真正评估多模态大语言模型对物理世界动态的理解能力，而不仅仅是表面上的视觉模式匹配。
- **现有基准的局限**：
    - 目前主流基准采用**识别式协议**，如视觉问答或违背预期范式（Violation of Expectation）。这些协议存在关键缺陷：模型可以通过物体识别、场景标签或语言先验来回答，而无需形成**显式的、可检验的**物理假设。这导致无法可靠地判断模型是否真正理解了物理规律。
- **整体含义**：研究旨在推动物理推理评测从“感知识别”向“生成与验证”转变，要求模型不仅能“看见”物理现象，还要能“重建”和“运行”物理过程，以此区分真正的物理理解和表面上的模式识别。

#### 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：提出一种**基于代码执行的评测框架**——VisPhyWorld。该框架的理念是“**将物理推理与渲染分离**”。
- **关键流程（如何实现这一思想）**：
    1. **视觉输入**：向模型提供一段包含特定物理动态（如碰撞、摆动、滚动）的视频作为视觉观察。
    2. **代码生成**：模型需要根据这段视频，生成一段**可执行的模拟器代码**（例如Python脚本）。这段代码必须能够复现视频中观察到的物体的外观、运动轨迹和物理交互。
    3. **代码执行与验证**：框架运行该代码，生成一个新的重建视频。
    4. **评判与检验**：通过比较重建视频与原始视频，评估模型生成的代码是否准确抓住了物理世界的核心属性。由于代码是可运行的，生成的“世界表示”是**可直接检查的、可编辑的、可证伪的**。
- **对比现有方法**：与VQA或VoE等“隐性”评估不同，这个框架要求模型做出“显式的”物理承诺，即生成可以运行的物理模拟，这使得模型的行为可以被客观地评判。

#### 3. 实验设计：数据集、基准与对比方法

- **提出的基准**：基于VisPhyWorld框架，研究者构建了**VisPhyBench**。
- **数据集规模**：包含**209个评测场景**，这些场景是由**108个物理模板**派生而来。这允许在可控的背景下生成多样化的物理情境。
- **评估协议**：基准包含一个系统性协议，通过两个维度对模型进行评分：
    - **外观重建**：评估模型重建视频中对物体外观（颜色、形状）的编码能力。
    - **运动重建**：评估模型生成的代码是否能够模拟出**物理上合理的运动轨迹**（如速度、加速度、碰撞反应）。
- **评测方法**：为了评估，默认要求模型生成代码，然后运行代码，将生成的新视频与原始视频进行对比。这种“生成-执行-比对”的流程提供了一种客观的评估方式。

#### 4. 资源与算力

- **无明确说明**：所提供的内容（摘要、结论）中**并未提及**任何关于实验所需算力的具体信息，如GPU型号、数量、训练时长或推理成本。因此，无法从该文本中总结这部分内容。

#### 5. 实验数量与充分性

- **实验数量**：基于摘要可以推断，研究者对多个当前最先进的多模态大语言模型（MLLMs）进行了测试，以对比其结果。文中未明确报告具体模型名称和实验组数，但提到“state-of-the-art MLLMs”在测试中表现出语义理解强、物理推理弱的趋势。
- **充分性评估**：
    - **客观性**：强调基于代码执行的评估是客观的，因为模型预测的物理参数与真实动态对比是可量化的，削弱了识别式基准中可能存在的作弊风险。
    - **公平性**：VisPhyBench的多样性（209个场景/108个模板）试图提升统计可靠性，但在所给文本中缺乏对具体消融实验（如不同模型规模的影响、代码生成错误容忍度）的描述。整体来看，实验设计思路是充分的，但需要查看完整论文才能评估其结论的稳健性。

#### 6. 主要结论与发现

- **核心结论**：当今最先进的多模态大语言模型在**语义场景理解**上表现优秀，但在**精确推理物理参数**（如质量、摩擦系数、速度）和**模拟连贯的物理运动**方面仍然面临巨大困难。
- **方法论价值**：VisPhyWorld提供的评测方式成功地揭示了这种“语义理解”与“物理推理”之间的鸿沟，证明了它作为一种更可靠的物理动态推理评估工具的价值。
- **数据有效性**：构建的流水线本身是有效的，能够在97.7%的情况下生成有效的重建视频，说明该基准本身是可行的且能有效执行。

#### 7. 优点与方法亮点

- **创新性**：将物理推理评测从“被动识别”转向“主动生成”，是一种强有力的范式创新。
- **可检验性**：通过要求生成可执行代码，将模型对物理世界的“外部表征”（代码）与“内部认知”分离，使得物理推理可以被直接检查、编辑和证伪。
- **物理推理与渲染解耦**：这是一个关键亮点，它避免了模型通过生成看似合理但物理错误的图片来欺骗评估，确保了评估的公正性。
- **高生成成功率**：97.7%的有效视频生成率，证明该基准本身是健壮且可行的，为后续实验提供了坚实基础。

#### 8. 不足与局限

- **信息缺失**：受限于提供的文本，关于实验的具体覆盖范围（模型种类）、消融实验（如是否分析过代码生成长度的影响）以及统计检验的细节信息不明。
- **代码生成偏差风险**：模型的性能可能受到其**编程能力**（而非物理推理）的影响。如果一个模型有很好的物理直觉但编码能力差，它也可能在VisPhyWorld上表现不佳。摘要未探讨这种潜在的混淆变量。
- **模拟器覆盖度**：该框架依赖于生成的模拟器代码是否能够覆盖所有物理现象。当涉及复杂的流体、材料变形等物理行为时，代码的生成和验证可能面临困难，限制了该基准的普适性。
- **应用限制**：该评测方法主要用于评估模型基本的物理动态理解，对于需要常识或复杂因果推理的新型交互可能不够灵敏，且无法评估模型对摄像头视角变化（渲染）的适应能力。

---

（完）
