---
title: "VideoPhy-2: A Challenging Action-Centric Physical Commonsense Evaluation in Video Generation"
title_zh: VideoPhy-2：面向视频生成的动作中心物理常识挑战性评估
authors: "Hritik Bansal, Clark Peng, Yonatan Bitton, Roman Goldenberg, Aditya Grover, Kai-Wei Chang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=HA8KSQW7SO"
tags: ["query:phys-video"]
score: 9.0
evidence: 构建4000条提示的数据集，通过人类评估检验生成视频的物理常识
tldr: 大尺度视频生成模型在真实动作上的物理常识遵循情况尚不明确，已有基准存在规模小、无人类评估等局限。为此构建VideoPhy-2，包含4000条多样化详细提示的动作中心数据集，并进行人类评估与物理规则细粒度分析。结果显示模型在动作类物理常识上仍有明显不足，该基准提供了更具挑战性的评测工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 大尺度视频生成模型在真实动作上的物理常识遵循情况尚不明确，现有基准存在规模小、缺少人类评估等问题。
method: 构建VideoPhy-2，一个包含4000条多样详细提示的动作中心数据集，并进行人类评估和物理规则细粒度分析。
result: 人类评估考察语义一致性与物理规则遵循，揭示了模型在动作类物理常识上的不足。
conclusion: VideoPhy-2为评估视频生成模型的物理常识提供了大规模、细粒度的挑战性基准。
---

## Abstract
Large-scale video generative models, capable of creating realistic videos of diverse visual concepts, are strong candidates for general-purpose physical world simulators. However, their adherence to physical commonsense across real-world actions remains unclear (e.g., playing tennis, backflip). Existing benchmarks suffer from limitations such as limited size, lack of human evaluation, sim-to-real gaps, and absence of fine-grained physical rule analysis. To address this, we introduce VideoPhy-2, an action-centric dataset for evaluating physical commonsense in generated videos. We curate 4000 diverse and detailed prompts for video synthesis from modern generative models. We perform human evaluation that assesses semantic adherence, physical commonsense, and grounding of physical rules in the generated videos. Our findings reveal major shortcomings, with even the best model achieving only $47.7\%$ joint performance (i.e., high semantic and physical commonsense adherence) on the hard subset of VideoPhy-2. We find that the models particularly struggle with conservation laws like mass and momentum. Finally, we also train VideoPhy-2-AutoEval, an automatic evaluator for fast, reliable assessment on our dataset. Overall, VideoPhy-2 serves as a rigorous benchmark, exposing critical gaps in video generative models and guiding future research in physically-grounded video generation. The data and code is available at \url{https://videophy2.github.io/}.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大规模视频生成模型能够生成包含多种视觉概念的真实视频，被视为通用物理世界模拟器的有力候选。然而，这些模型在真实世界动作（如打网球、后空翻）中对物理常识的遵循情况尚不明确。
- **现有基准的局限**：已有评估基准存在规模小、缺乏人类评估、模拟到现实差距（sim-to-real gap）以及缺乏细粒度物理规则分析等问题。
- **核心问题**：视频生成模型生成的视频在多大程度上遵守物理常识？特别是在真实动作场景下，模型能否在语义正确的同时满足物理规则约束？
- **整体含义**：该论文通过构建大规模动作中心基准，系统性地揭示视频生成模型在物理常识方面的不足，为构建具身物理世界模拟器提供评估工具和方向指引。

## 2. 论文提出的方法论

- **核心思想**：构建动作中心的基准数据集 VideoPhy-2，通过人类评估和细粒度物理规则分析，全面检验视频生成模型的物理常识遵循能力。
- **数据集构建**：从现代生成模型出发，人工策展了 4000 条多样且详细的视频合成提示（prompts），聚焦于真实世界动作场景。
- **人类评估流程**：评估三个维度：
  - **语义一致性（semantic adherence）**：生成视频是否与提示的语义内容匹配；
  - **物理常识（physical commonsense）**：视频是否符合基本物理直觉；
  - **物理规则落地（grounding of physical rules）**：具体物理定律在视频中的表现是否合理。
- **自动评估器训练**：基于收集的人类评估数据，训练了 VideoPhy-2-AutoEval，用于在数据集上进行快速、可靠的自动评估。

## 3. 实验设计

- **数据集 / 基准**：VideoPhy-2，包含 4000 条多样且详细的提示，并设有困难子集（hard subset）；数据与代码已公开。
- **评估方法**：
  - 人类评估：考察语义一致性、物理常识和物理规则的落地情况；
  - 自动评估：使用 VideoPhy-2-AutoEval 进行大规模自动评测。
- **对比模型**：论文评估了“现代生成模型”（modern generative models），但摘要中未具体列出模型名称或版本，也未给出逐模型的详细对比表。
- **核心指标**：联合性能（joint performance），即同时满足高语义一致性与高物理常识遵循的比例。

## 4. 资源与算力

- 论文摘要和元数据中**未明确说明**训练或评估所使用的 GPU 型号、数量、训练时长、参数量等算力信息。
- 也未提及自动评估器 VideoPhy-2-AutoEval 的训练成本或推理效率数据。
- 如需获得算力细节，需查阅论文正文或附录。

## 5. 实验数量与充分性

- **主要实验**：
  1. 人类评估实验：在 4000 条提示上评估生成模型的语义与物理表现；
  2. 困难子集分析：单独报告模型在困难子集上的联合性能；
  3. 物理规则细粒度分析：单独考察模型在守恒定律（质量、动量等）上的表现；
  4. 自动评估器训练与验证：训练了 VideoPhy-2-AutoEval 作为快速评估工具。
- **充分性评价**：
  - 优点：数据集规模大（4000 条），评估维度覆盖语义和物理，且包含细粒度物理规则分析，比已有基准更全面；
  - 不足：摘要中未展示多模型横向对比的详细结果，也未提及消融实验或自动评估器与人类评估的一致性验证细节；由于缺少模型列表和逐项数据，无法判断实验对比的完整公平性。

## 6. 论文的主要结论与发现

- 视频生成模型在动作类物理常识上存在**明显不足**：即使在最好的模型上，困难子集的联合性能也仅为 **47.7%**，即超过半数生成视频无法同时满足语义正确和物理合理。
- 模型在**守恒定律**（如质量守恒、动量守恒）方面表现尤其糟糕，揭示了模型对基础物理法则的建模能力严重欠缺。
- VideoPhy-2 作为一个大规模、细粒度的基准，能够有效暴露现有视频生成模型与“物理世界模拟器”目标之间的关键差距，为后续研究提供明确方向。

## 7. 优点

- **大规模数据集**：4000 条人工策展提示，显著超越已有基准的规模。
- **动作中心设计**：聚焦真实世界动作（如打网球、后空翻），贴近实际应用场景，填补了现有基准对动作类物理常识评估的空白。
- **人类评估与细粒度分析**：同时评估语义一致性、物理常识和物理规则落地，并单独分析守恒定律等细粒度物理维度，诊断性更强。
- **自动评估器**：提供 VideoPhy-2-AutoEval 实现快速可靠评估，降低了 benchmark 的使用门槛，便于后续研究复现和对比。
- **公开资源**：数据和代码开源，提升可复现性和社区可用性。

## 8. 不足与局限

- **算力信息缺失**：未报告训练/评估的 GPU 资源、耗时等，影响实验可复现性评估。
- **模型对比细节不明确**：摘要中未给出参与评估的模型名单及逐模型结果，难以独立判断评估全貌与公平性。
- **自动评估器验证信息不足**：未说明 AutoEval 与人类评估的一致性程度、误差范围等关键指标。
- **可能的数据偏差**：4000 条提示虽多样，但提示的选取来源为现代生成模型，可能引入与真实动作分布不一致的偏差；动作类型覆盖范围未必完全均衡。
- **物理规则覆盖有限**：论文侧重守恒定律等特定物理规则，其他物理维度（如流体、材料属性、光的传播等）的覆盖未在摘要中说明。
- **应用限制**：基准聚焦于“动作中心”场景，面向通用物理世界模拟器的全面评估仍需进一步扩展任务范围。

（完）
