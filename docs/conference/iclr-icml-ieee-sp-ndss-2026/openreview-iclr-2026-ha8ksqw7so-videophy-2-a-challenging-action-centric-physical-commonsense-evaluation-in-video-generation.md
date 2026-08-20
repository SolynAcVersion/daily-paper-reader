---
title: "VideoPhy-2: A Challenging Action-Centric Physical Commonsense Evaluation in Video Generation"
title_zh: VideoPhy-2：视频生成中具有挑战性的以动作为中心的物理常识评估
authors: "Hritik Bansal, Clark Peng, Yonatan Bitton, Roman Goldenberg, Aditya Grover, Kai-Wei Chang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=HA8KSQW7SO"
tags: ["query:phys-video"]
score: 10.0
evidence: 面向生成视频物理常识的动作中心基准，包含人类评估
tldr: 为评估视频生成模型的物理常识，提出VideoPhy-2动作中心基准，包含4000个多样化提示。采用人类评估系统考察语义符合度与物理规则细粒度分析，弥补现有基准规模小、缺乏人类评估与模拟到真实差距等问题，是衡量生成视频物理正确性的重要测试集。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 大型视频生成模型是否遵守真实世界物理常识尚不清楚，现有基准存在规模小、缺乏人类评估和细粒度物理分析等不足。
method: 构建包含4000个多样提示的动作中心数据集，并设计人类评估流程与细粒度物理规则分析。
result: 提供了对现代生成模型物理常识的全面人类评估，揭示其在真实动作上的物理遵守程度。
conclusion: 该基准为视频生成的物理正确性评估提供了大规模、细粒度的标准测试平台。
---

## Abstract
Large-scale video generative models, capable of creating realistic videos of diverse visual concepts, are strong candidates for general-purpose physical world simulators. However, their adherence to physical commonsense across real-world actions remains unclear (e.g., playing tennis, backflip). Existing benchmarks suffer from limitations such as limited size, lack of human evaluation, sim-to-real gaps, and absence of fine-grained physical rule analysis. To address this, we introduce VideoPhy-2, an action-centric dataset for evaluating physical commonsense in generated videos. We curate 4000 diverse and detailed prompts for video synthesis from modern generative models. We perform human evaluation that assesses semantic adherence, physical commonsense, and grounding of physical rules in the generated videos. Our findings reveal major shortcomings, with even the best model achieving only $47.7\%$ joint performance (i.e., high semantic and physical commonsense adherence) on the hard subset of VideoPhy-2. We find that the models particularly struggle with conservation laws like mass and momentum. Finally, we also train VideoPhy-2-AutoEval, an automatic evaluator for fast, reliable assessment on our dataset. Overall, VideoPhy-2 serves as a rigorous benchmark, exposing critical gaps in video generative models and guiding future research in physically-grounded video generation. The data and code is available at \url{https://videophy2.github.io/}.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

> 说明：本总结基于论文提供的摘要和元数据编写，因原文信息有限，部分细节无法展开，将如实指出。

### 1. 核心问题与整体含义（研究动机与背景）

- **背景**：大规模视频生成模型能够生成包含多种视觉概念的逼真视频，被视为通用物理世界模拟器的有力候选者。
- **核心问题**：目前尚不清楚这些模型在真实世界动作（如打网球、后空翻）中是否遵守物理常识。
- **现有基准的不足**：
  - 规模有限；
  - 缺乏人类评估；
  - 存在模拟到真实的差距（sim-to-real gap）；
  - 缺乏对物理规则的细粒度分析。
- **整体含义**：需要通过一个大规模、动作中心、细粒度的基准来系统评测生成视频中的物理常识，从而揭示当前模型的物理推理缺陷，并为未来研究提供指导。

### 2. 提出的方法论（核心思想与关键技术细节）

- **核心思想**：构建一个以“真实世界动作”为中心的基准，促使生成模型展示对物理常识（如质量守恒、动量守恒等）的遵守程度。
- **数据集构建**：
  - 整理了 **4000 个多样化且详细的提示词**，用于现代视频生成模型的合成任务。
  - 强调动作中心（action-centric），即每个提示围绕一个具体物理动作展开。
- **评估流程设计**：
  - 设计**人类评估系统**，对生成视频进行多维评价：
    - **语义符合度**（是否按提示执行动作）；
    - **物理常识**（是否符合真实世界物理规律）；
    - **物理规则落地分析**（细粒度地检查具体物理规则是否被遵守）。
- **自动评估器**：
  - 训练了 **VideoPhy-2-AutoEval**，用于快速、可靠地自动评估模型性能，弥补人工评估效率低的不足。

### 3. 实验设计（数据集 / 场景 / Benchmark / 对比方法）

- **Benchmark**：VideoPhy-2，动作中心的物理常识评测基准。
- **数据集规模**：包含 4000 条多样化、细粒度的视频生成提示。
- **评估场景**：真实世界动作（例如运动类、技巧类动作）。
- **人类评估**：对语义符合度、物理常识和物理规则遵守情况进行细粒度分析。
- **对比方法**：论文提到“即使最好的模型在困难子集上仅有 47.7% 的联合性能”，说明对比了多种现代视频生成模型，但摘要中未列出具体模型名称。
- **自动评估验证**：同时训练并使用了自动评估器，以支持大范围评测。

### 4. 资源与算力

- 论文摘要和元数据中**未明确说明**使用了多少算力（如 GPU 型号、数量、训练时长等）。
- 无法获得训练 VideoPhy-2-AutoEval 时的具体计算资源信息。

### 5. 实验数量与充分性

- **实验数量**：信息有限。可见的主要实验包括：
  - 人类评估：在 4000 提示生成视频上进行语义和物理常识的联合评估；
  - 自动评估器训练与评测；
  - 困难子集上的性能报告。
- **充分性/客观性/公平性评估**：
  - **充分性**：数据规模较大（4000 提示），人类评估加入提高了可信度；但摘要中未交代模型数量、提示类型分布、重复实验次数等细节，因此难以完全评价实验充分性。
  - **客观性**：引入人类评估物理规则，有助于避免自动指标的偏差；自动评估器用于快速评测，但需注意其与人类评估的一致性未在摘要中给出。
  - **公平性**：未说明每个模型是否使用相同推理资源和解码策略，所以公平性仍需阅读原文核实。

### 6. 主要结论与发现

- **模型表现**：即使最好的模型在 VideoPhy-2 的困难子集上，联合性能（高语义符合度和高物理常识遵守）仅为 **47.7%**。
- **主要短板**：模型尤其难以遵守**守恒定律**（如质量守恒、动量守恒）。
- **基准价值**：VideoPhy-2 为视频生成模型的物理正确性评估提供了大规模、细粒度的标准测试平台，暴露了现有模型的关键物理常识缺口。
- **自动化工具**：VideoPhy-2-AutoEval 可用于快速可靠的评估，推动未来研究。

### 7. 优点（方法或实验设计亮点）

- **规模优势**：4000 个多样提示，远大于许多现有物理常识基准。
- **动作中心设计**：聚焦真实世界动作，直接考察模型对物理解释性的把握。
- **细粒度物理规则分析**：不只是总体评分，而是细分到质量守恒、动量守恒等具体物理规则。
- **人类评估的引入**：解决了自动评估难以捕捉微妙物理违规的问题。
- **自动评估器配套**：兼顾了人工评测的准确性和大规模评测的效率，形成“人工深度评估 + 自动快速筛选”的双层体系。

### 8. 不足与局限（实验覆盖、偏差风险、应用限制）

- **信息不全**：原摘要未提供模型清单、具体评分标准细节、自动评估器与人类评估的一致性指标等。
- **算力信息缺失**：无法判断训练和推理成本，影响可复现性评估。
- **覆盖范围**：提示词虽多样，但可能偏向特定动作类型，未必涵盖所有物理交互场景（如流体、软体物体、微观物理等）。
- **自动评估器风险**：自动评估器可能继承人类标注的偏差，或对复杂物理违规不敏感，仍需更多验证。
- **模拟到真实差距**：虽然基准意图缩小该差距，但生成视频本身属于模拟输出，与实际物理数据仍有本质区别。
- **应用限制**：评判标准可能基于视觉可观察的物理常识，无法覆盖不可见或隐含的物理过程；对对抗性物理错觉的鲁棒性未知。

---

（完）
