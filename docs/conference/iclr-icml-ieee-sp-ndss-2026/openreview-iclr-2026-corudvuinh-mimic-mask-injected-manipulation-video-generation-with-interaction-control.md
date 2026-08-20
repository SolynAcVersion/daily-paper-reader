---
title: "MIMIC: Mask-Injected Manipulation Video Generation with Interaction Control"
title_zh: MIMIC：掩码注入的带交互控制的操控视频生成
authors: "Tianxiao Chen, Jintao Rong, Huajin Chen, Jingya Wang, Tao Zhou, Jiming Chen, Qi Ye"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=COrUdVuInH"
tags: ["query:phys-video"]
score: 7.0
evidence: 操控视频生成，捕捉细粒度接触动力学
tldr: 具身智能受限于大规模交互数据匮乏，操控视频生成成为可扩展替代方案，但需捕捉细粒度接触动力学。MIMIC 提出两阶段图像到视频扩散框架，利用参考视频的语义与运动线索，通过交互运动感知模块增强交互控制。实验证明其在操控视频的语义理解与细节保真上均有提升，为交互数据生成提供新途径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 操控视频生成需要捕捉细粒度接触动力学，现有视频扩散模型难以平衡语义理解与视觉细节。
method: 提出两阶段图像到视频扩散框架，引入交互运动感知模块融合参考视频的语义与运动线索，并用掩码控制交互动态。
result: 实验显示该方法能生成更具接触真实感和语义准确性的操控视频。
conclusion: 该方法为具身智能提供可扩展的交互视频生成方案，缓解大规模交互数据稀缺瓶颈。
---

## Abstract
Embodied intelligence faces a fundamental bottleneck from limited large-scale interaction data. Video generation offers a scalable alternative, but manipulation videos remain particularly challenging, as they require capturing subtle, contact-rich dynamics. Despite recent advances, video diffusion models still struggle to balance semantic understanding with fine-grained visual details, restricting their effectiveness in manipulation scenarios. Our key insight is that reference videos provide rich semantic and motion cues that can effectively drive manipulation video generation. Building on this, we propose MIMIC, a two-stage image-to-video diffusion framework. (1) We first introduce an Interaction-Motion-Aware (IMA) module to fuse visual features from the reference video, producing coherent semantic masks that correspond to the target image. (2) then utilize these masks as semantic control signals to guide the video generation process. Moreover, considering the ambiguity of the motion attribution,  we introduce a Pair Prompt Control mechanism to disentangle object and camera motion by adding the reference video as an additional input. Extensive experiments demonstrate that MIMIC significantly outperforms existing methods, effectively preserves manipulation intent and motion details, even when handling diverse and deformable objects. Our findings underscore the effectiveness of reference-driven semantics for controllable and realistic manipulation video generation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心瓶颈**：具身智能（Embodied Intelligence）的发展高度依赖大规模人-物交互数据，然而这类数据的获取成本高昂、规模受限，成为该领域的基础性瓶颈。
- **既有替代方案的不足**：视频生成被视作一种可扩展的替代数据来源，但操控视频（manipulation video）的生成极具挑战——它要求模型捕捉细粒度、富含接触的动态（contact-rich dynamics），而现有视频扩散模型往往难以同时兼顾高层语义理解与低层视觉细节保真，导致生成结果在操控场景中效果受限。
- **关键洞察**：参考视频（reference video）中蕴含着丰富的语义与运动线索，可以有效地驱动操控视频的生成，从而改善上述平衡性问题。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **整体框架**：MIMIC 是一个**两阶段图像到视频（image-to-video）扩散框架**。
- **阶段一：交互运动感知模块（Interaction-Motion-Aware, IMA）**
  - 输入：参考视频 + 目标图像。
  - 作用：融合参考视频中的视觉特征，生成与目标图像语义对齐的、连贯的**语义掩码（coherent semantic masks）**。
- **阶段二：掩码引导的视频生成**
  - 将阶段一生成的语义掩码作为**语义控制信号**，注入视频扩散模型，引导后续的视频生成过程，使生成内容贴合交互语义。
- **配对提示控制机制（Pair Prompt Control）**
  - 动机：运动归因（motion attribution）存在歧义，即生成过程中难以判断运动是来自物体本身还是相机。
  - 做法：将参考视频作为额外输入，引入配对提示控制，从而**解耦物体运动与相机运动**。
- **整体流程总结**：参考视频 → IMA 模块提取交互感知语义 → 生成语义掩码 → 掩码作为控制信号 + 配对提示控制 → 生成最终操控视频。

### 3. 实验设计：数据集、Benchmark 与对比方法

- **数据集与场景**：给定文本中**未明确列出具体数据集名称**，但摘要强调实验覆盖了**多种物体**以及**可变形物体（deformable objects）**场景。
- **Benchmark**：未明确说明评测基准的构建方式（如是否基于现有数据集划分、是否使用特定评估指标等）。
- **对比方法**：论文声称“显著优于现有方法（significantly outperforms existing methods）”，但在提供的文本中**未列出具体对比的基线方法名称**。

### 4. 资源与算力

- 论文 PDF 提取内容（标题、摘要）中**未提及任何算力信息**，包括 GPU 型号、数量、训练时长、参数量等。
- 需要说明：由于可供分析的文本仅为摘要级内容，全文中的实验设置与资源消耗详情无法在此确认。

### 5. 实验数量与充分性：是否充分、客观、公平

- **实验数量**：摘要中使用了“Extensive experiments”（大量实验）的说法，说明实验组数较多，但具体数量（如消融实验组数、跨数据集验证数）**未在提供文本中给出**。
- **充分性评估**：
  - 从摘要看，实验涵盖了多样物体与可变形物体，表明作者有意验证泛化性，方向合理。
  - 但由于缺少对比基线、评估指标、数据规模等细节，无法基于现有信息判断实验是否充分、客观和公平。需要阅读全文才能确认是否存在消融实验、统计显著性检验、人类评估等。

### 6. 论文的主要结论与发现

- MIMIC 在操控视频的**语义理解**与**细节保真**两方面均显著优于现有方法。
- 该方法能够有效保留**操控意图（manipulation intent）**与**运动细节（motion details）**。
- 即使面对**多样化和可变形物体**，仍能生成具有接触真实感的操控视频。
- 总体结论：参考视频驱动的语义控制是一种可行且有效的操控视频生成路径，可为具身智能提供**可扩展的交互视频生成方案**，缓解大规模交互数据稀缺的瓶颈。

### 7. 优点：方法与实验设计的亮点

- **两阶段设计**：先提取交互感知语义掩码、再利用掩码控制生成，思路清晰，将复杂问题分解为语义理解和视觉生成两个可优化的子任务。
- **运动解耦**：通过配对提示控制机制将物体运动与相机运动解耦，直击操控视频生成中“运动归因歧义”的痛点，是方法层面显著创新。
- **参考视频驱动**：充分利用参考视频的语义与运动先验，不依赖额外人工标注，具有较强的实用性与扩展性。
- **适用对象广**：明确验证了可变形物体等困难场景，显示方法对复杂接触动力学的建模能力。

### 8. 不足与局限

- **文本信息不完整**：本总结基于论文摘要与元数据，无法全面考察方法细节、评测协议与复现难度。
- **实验细节缺失**：抽象描述中未给出数据集名称、基线方法、评估指标、消融实验设计等，难以独立验证“显著优于现有方法”这一结论的力度。
- **潜在偏差风险**：若实验主要在某一类物体或特定相机设置下进行，结论可能无法推广至更广泛真实场景；参考视频的质量与多样性也可能直接影响生成效果。
- **应用限制**：操控视频生成仍属生成式方法，生成结果用于具身智能训练时存在物理真实性的上限，不能完全替代真实交互数据；此外计算成本与推理速度也未在摘要中说明。

（完）
