---
title: "HECTOR: Hybrid Editable Compositional Object References for Video Generation"
title_zh: HECTOR：用于视频生成的混合可编辑组合式对象引用
authors: "Guofeng Zhang, Angtian Wang, Jacob Zhiyuan Fang, Liming Jiang, Haotian Yang, Alan Yuille, Chongyang Ma"
date: 2026-04-30
pdf: "https://openreview.net/pdf/66df44bb768f2a363e9e52325e8afe2797de9a9e.pdf"
tags: ["query:phys-video"]
score: 5.0
evidence: 视频生成中组合对象轨迹控制
tldr: 真实视频中多个物理对象会形成动态组合，但多数视频生成模型缺少显式的组合操作机制。HECTOR提出混合参考条件化生成管线，可同时利用静态图像和动态视频进行引导，并允许用户为每个参考元素指定位置、尺度和速度轨迹，实现细粒度组合控制。该方法提升了对复杂场景中对象运动和交互的可控性，为生成符合物理直觉的动态视频提供了基础。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 真实世界视频由多个物理对象动态组合而成，现有生成模型缺少显式组合操作机制。
method: 支持静态图像和动态视频混合参考条件化，并让用户指定每个对象的位置、尺度和速度轨迹。
result: 实现对复杂场景中对象运动和交互的细粒度控制。
conclusion: 为物理直觉动态视频生成提供了组合控制基础。
---

## Abstract
Real-world videos naturally portray complex interactions among distinct physical objects, effectively forming dynamic compositions of visual elements. However, most current video generation models synthesize scenes holistically and therefore lack mechanisms for explicit compositional manipulation. To address this limitation, we propose HECTOR, a generative pipeline that enables fine-grained compositional control. In contrast to prior methods, HECTOR supports hybrid reference conditioning, allowing generation to be simultaneously guided by static images and/or dynamic videos. Moreover, users can explicitly specify the trajectory of each referenced element, precisely controlling its location, scale, and speed (see Figure1). This design allows the model to synthesize coherent videos that satisfy complex spatiotemporal constraints while preserving high-fidelity adherence to references. Extensive experiments demonstrate that HECTOR achieves superior visual quality, stronger reference preservation, and improved motion controllability compared with existing approaches.

---

## 论文详细总结（自动生成）

## HECTOR：用于视频生成的混合可编辑组合式对象引用

### 1. 核心问题与整体含义

- **研究动机**：真实世界视频本质上由多个物理对象在时空中动态交互所构成，可视为视觉元素的动态组合。然而，现有主流视频生成模型倾向于以整体化（holistic）方式合成场景，缺乏对单个对象进行显式组合操作（compositional manipulation）的机制。
- **核心问题**：如何在视频生成过程中实现对多个参考对象的细粒度控制，包括位置、尺度和运动速度，同时保持对参考内容的高保真还原，并满足复杂时空约束。
- **整体意义**：该工作为“物理直觉”视频生成提供了组合控制基础，填补了显式组合式视频生成方法的空白，是迈向可编辑、可交互视频生成的重要一步。

### 2. 方法论

- **核心思想**：提出名为 HECTOR 的生成管线，核心设计为**混合参考条件化（hybrid reference conditioning）**。
- **关键技术细节**：
  - **混合参考输入**：与先前方法不同，HECTOR 允许生成过程同时受静态图像和/或动态视频的引导，即用户可自由组合不同类型的参考元素。
  - **显式轨迹控制**：用户可为每个被参考的对象元素显式指定其轨迹，精细控制其在生成视频中的位置（location）、尺度（scale）和速度（speed）。
  - **时空一致性**：通过将上述对象级控制信息注入生成过程，模型能够在满足复杂时空约束的条件下合成连贯视频，同时维持与参考内容的高保真对齐。
- **算法流程（以文字说明）**：模型接收静态图像/动态视频中的参考元素提取特征，结合用户给定的每对象轨迹参数（位置、尺度、速度），在条件化生成框架内联合优化视觉保真度和时空约束满足度，最终输出具有组合结构且运动可控的视频序列。
- **注**：原文提供的文本未给出明确的公式或伪代码，方法描述以架构层面为主。

### 3. 实验设计

- **数据集与场景**：原文未明确披露使用的具体数据集名称，实验（如图1所示）涵盖多对象动态场景，侧重验证对象运动和交互的可控性。
- **Benchmark**：未明确说明具体的基准测试集或评估协议；评价维度包括视觉质量（visual quality）、参考保真度（reference preservation）和运动可控性（motion controllability）。
- **对比方法**：原文提到“existing approaches”，但未列出具体基线方法名称。由于可获取文本仅为摘要，实验细节缺失。

### 4. 资源与算力

- 原文在提供的文本范围内**未说明**所使用的 GPU 型号、数量、训练时长等信息。
- 也未提及数据规模、训练策略或推理开销等相关细节。

### 5. 实验数量与充分性

- 原文仅以“Extensive experiments”概括实验规模，**未给出具体实验数量**（如不同数据集上的组数、消融实验项数等）。
- **充分性评估**：从摘要表述看，实验覆盖了三个关键维度（视觉质量、参考保真、运动可控性），方向合理；但因缺少消融实验细节（如去除轨迹控制、单类型参考 vs 混合参考等），无法判断其充分性。
- **客观性与公平性**：由于未披露对比方法名单和评估指标细节，公平性难以全面核验。

### 6. 主要结论与发现

- HECTOR 在视觉质量、参考保持能力和运动可控性三个维度上均优于现有方法。
- 证明了静态图像与动态视频混合参考引导的有效性，扩展了条件化视频生成的能力边界。
- 实现了对多对象复杂场景中运动与交互的细粒度控制，为符合物理直觉的动态视频生成提供了可行的组合控制范本。

### 7. 优点

- **混合参考条件化**：同时支持静态图和动态视频作为引导来源，灵活性强，优于仅支持单一参考类型的现有方法。
- **对象级轨迹控制**：首次在组合式视频生成中实现位置、尺度、速度的联合显式可控，为用户提供直观的编辑接口。
- **兼顾保真与可控**：在满足复杂时空约束的同时保持高保真参考一致性，解决了可控性与质量难以兼得的常见问题。
- **应用前景明确**：面向物理直觉视频生成，具备较强的实际应用价值（如内容创作、智能体仿真等）。

### 8. 不足与局限

- **实验细节缺失**：原文仅提供摘要，未见数据集、指标、基线方法、消融实验等关键信息，难以独立验证结论的可靠性和可复现性。
- **偏差风险**：当参考元素过多或轨迹复杂时，HECTOR 的表现尚不明确；对遮挡、物体交互等复杂物理场景的泛化能力未知。
- **应用限制**：轨迹控制依赖用户提供的对象级标注或轨迹输入，可能限制其在全自动生成场景中的可用性。
- **评估维度有限**：摘要中未涉及时序一致性、物理合理性、长时间生成稳定性等关键指标的评估。
- **信息不完整**：算力消耗、训练时长、推理效率等工程细节未披露，不利于实际应用中的资源预估。

（完）
