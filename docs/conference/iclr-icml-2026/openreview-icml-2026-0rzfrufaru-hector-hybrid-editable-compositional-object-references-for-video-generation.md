---
title: "HECTOR: Hybrid Editable Compositional Object References for Video Generation"
title_zh: HECTOR：用于视频生成的混合可编辑组合对象参照
authors: "Guofeng Zhang, Angtian Wang, Jacob Zhiyuan Fang, Liming Jiang, Haotian Yang, Alan Yuille, Chongyang Ma"
date: 2026-04-30
pdf: "https://openreview.net/pdf/66df44bb768f2a363e9e52325e8afe2797de9a9e.pdf"
tags: ["query:phys-video"]
score: 6.0
evidence: 可对每个物体指定轨迹、位置、尺度和速度，支持组合式视频生成中的物理路径控制
tldr: 真实视频通常包含多个物理对象的复杂交互，但现有生成模型整体合成场景，难以组合操控。HECTOR提出混合参照条件生成流程，能够同时使用静态图和动态视频进行引导，并允许用户显式指定每个参照要素的轨迹、位置、尺度和速度。这让模型可以精细控制物体动态，为编排符合物理直观的运动提供了可行机制。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视频生成模型缺乏对多物体动态组合的显式控制，难以精确编排对象运动。
method: 提出支持图像和视频混合参照条件的生成流程，可逐对象指定轨迹、尺度、位置和速度。
result: 实现了对视频中对象运动的细粒度组合控制，可生成指定的复合动态。
conclusion: 为视频生成提供了可编辑的对象级动态控制，有助于实现物理上合理的运动编排。
---

## Abstract
Real-world videos naturally portray complex interactions among distinct physical objects, effectively forming dynamic compositions of visual elements. However, most current video generation models synthesize scenes holistically and therefore lack mechanisms for explicit compositional manipulation. To address this limitation, we propose HECTOR, a generative pipeline that enables fine-grained compositional control. In contrast to prior methods, HECTOR supports hybrid reference conditioning, allowing generation to be simultaneously guided by static images and/or dynamic videos. Moreover, users can explicitly specify the trajectory of each referenced element, precisely controlling its location, scale, and speed (see Figure1). This design allows the model to synthesize coherent videos that satisfy complex spatiotemporal constraints while preserving high-fidelity adherence to references. Extensive experiments demonstrate that HECTOR achieves superior visual quality, stronger reference preservation, and improved motion controllability compared with existing approaches.

---

## 论文详细总结（自动生成）

# HECTOR：用于视频生成的混合可编辑组合对象参照

## 1. 核心问题与整体含义

- **研究动机**：真实世界视频通常包含多个物理对象之间的复杂交互，本质上构成视觉元素的动态组合。然而，当前大多数视频生成模型倾向于整体性地合成整个场景，缺乏显式的组合式操控机制，用户难以独立控制场景中每个物体的运动与外观。
- **核心问题**：如何在视频生成过程中实现对多个对象的细粒度、可编辑的组合控制，同时保持生成视频的视觉质量和对参照内容的高保真度。
- **整体含义**：该研究旨在填补视频生成中“对象级动态控制”的空白，使模型不再只能生成“整体场景”，而能按照用户意图分别驱动每个对象的轨迹、位置、尺度与速度，进而支持更符合物理直观的运动编排。

## 2. 方法论

- **核心思想**：提出一种名为 HECTOR 的生成流程，通过“混合参照条件”实现组合式视频生成。与只能使用静态图像或动态视频作为条件的方法不同，HECTOR 允许同时使用静态图像和/或动态视频来引导生成，从而兼顾外观保真与运动参考。
- **关键技术细节**：
  - **混合参照条件**：用户可以提供一个或多个静态图像作为对象外观参照，同时提供一个或多个动态视频作为运动/行为参照；模型在生成时同时受这两类条件约束。
  - **逐对象属性指定**：用户能够对每个被参照的元素显式指定其轨迹（trajectory）、位置（location）、尺度（scale）和速度（speed）。这些参数构成细粒度的时空控制信号。
  - **统一生成框架**：模型将上述参照条件与时空控制参数整合到一个条件生成管线中，输出满足复杂时空约束且与参照高度一致的连续视频。
- **算法流程（文字描述）**：输入静态参照图与动态参照视频片段的特征，结合用户为每个对象指定的轨迹、位置、尺度和速度，经过条件编码与时空注意力融合，在生成过程中逐帧约束对象的外观一致性和运动轨迹，最终输出完整视频。具体公式与网络结构细节在提供的文本中未展开。

## 3. 实验设计

- **数据集 / 场景**：论文摘要未明确列出具体使用的数据集名称，也未详细说明测试场景类型（如自然场景、物体交互场景等）。仅提及实验涉及“复杂时空约束”和“对象级动态控制”的合成视频任务。
- **Benchmark**：未在可用文本中说明采用了哪个基准数据集或评估协议（如 VBench、UCF101 等）。
- **对比方法**：摘要提到“与现有方法相比”（compared with existing approaches），但未列出具体对比模型名称。从“混合参照”与“逐对象属性控制”的定位看，对比方法可能包括基于文本/图像/视频条件的可控视频生成模型，但具体信息缺失。

## 4. 资源与算力

- **未明确说明**：提供的论文文本（摘要与元数据）中没有提及任何算力信息，例如 GPU 型号、数量、训练时长、显存消耗等。因此无法总结计算资源情况。

## 5. 实验数量与充分性

- **实验数量**：文本中仅提到“大量实验”（Extensive experiments）这一概括性描述，未给出具体实验组数、数据集数量或消融实验细节。
- **充分性评估**：由于缺乏具体实验内容，无法判断实验的充分性与公平性。仅从摘要声明看，作者声称在视觉质量、参照保持和运动可控性三方面优于现有方法，但缺少定量指标、对比设置和消融分析的公开信息，因此客观性存疑。

## 6. 主要结论与发现

- HECTOR 能够同时利用静态图像和动态视频作为参照条件，实现对视频中多个对象的外观与运动进行组合控制。
- 用户可以显式指定每个对象的轨迹、位置、尺度和速度，从而使模型生成满足复杂时空约束的连贯视频。
- 实验结果表明，HECTOR 在视觉质量、参照保真度和运动可控性上均优于现有方法，为可编辑的对象级视频生成提供了可行方案。

## 7. 优点

- **新颖的混合条件机制**：同时支持图像和视频作为参照，扩展了视频生成条件表达的灵活性，能更好地分离“外观”与“运动”两个维度。
- **细粒度对象控制**：允许对每个对象的轨迹、位置、尺度和速度进行独立指定，相比整体场景生成具有更高的编辑自由度和可解释性。
- **物理合理性的潜在支持**：通过精确控制对象动态，有助于生成符合物理直觉的复合运动（如遮挡、碰撞、跟随等），切合“物理视频查询”这一应用需求。

## 8. 不足与局限

- **信息透明度不足**：摘要及可用元数据未提供数据集、基准、对比方法、评测指标或消融实验等关键细节，难以评估方法的可复现性与实验充分性。
- **实验覆盖未知**：未说明是否涵盖多种视频类型（人物、物体、自然场景）、不同对象数量、长时间生成或罕见运动模式等情况，泛化能力不明。
- **推理与训练成本未报告**：缺少算力、参数量、推理速度等信息，无法评估实用性和资源需求。
- **潜在偏差风险**：若实验只在有限数据集上做主观或单一指标评测，可能存在选择偏好；混合参照的可用性也依赖用户提供高质量参照，实际应用门槛可能较高。
- **物理约束的深度有限**：虽然支持指定轨迹和速度，但并未在文本中展示如何保证物体间碰撞、重力等物理规律的自动满足，可能仍依赖用户手动设置。

（完）
