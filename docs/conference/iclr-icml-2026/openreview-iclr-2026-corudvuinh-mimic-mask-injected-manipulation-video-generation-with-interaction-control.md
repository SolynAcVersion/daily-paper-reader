---
title: "MIMIC: Mask-Injected Manipulation Video Generation with Interaction Control"
title_zh: MIMIC：掩码注入与交互控制的操控视频生成
authors: "Tianxiao Chen, Jintao Rong, Huajin Chen, Jingya Wang, Tao Zhou, Jiming Chen, Qi Ye"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=COrUdVuInH"
tags: ["query:phys-video"]
score: 4.0
evidence: 生成接触丰富动态的操控视频并进行交互控制，与真实物理交互相关。
tldr: 操控视频生成需要捕捉细微的接触动态，现有模型难以平衡语义理解与细粒度视觉细节。MIMIC 提出两阶段图像到视频扩散框架，引入交互-运动感知模块融合参考视频的语义与运动线索，并通过掩码注入实现交互控制。该方法面向接触丰富的操控场景，提升了视频生成中物理交互动态的真实性，为具身智能提供可扩展的数据生成途径。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 操控视频依赖接触丰富的动态建模，现有视频扩散模型难以兼顾语义与细节。
method: 提出两阶段图像到视频扩散框架，用交互-运动感知模块融合参考视频线索并注入掩码控制。
result: 更好地捕捉接触丰富物理动态，改善操控视频生成质量。
conclusion: 验证了参考视频线索和掩码控制对物理交互视频生成的有效性。
---

## Abstract
Embodied intelligence faces a fundamental bottleneck from limited large-scale interaction data. Video generation offers a scalable alternative, but manipulation videos remain particularly challenging, as they require capturing subtle, contact-rich dynamics. Despite recent advances, video diffusion models still struggle to balance semantic understanding with fine-grained visual details, restricting their effectiveness in manipulation scenarios. Our key insight is that reference videos provide rich semantic and motion cues that can effectively drive manipulation video generation. Building on this, we propose MIMIC, a two-stage image-to-video diffusion framework. (1) We first introduce an Interaction-Motion-Aware (IMA) module to fuse visual features from the reference video, producing coherent semantic masks that correspond to the target image. (2) then utilize these masks as semantic control signals to guide the video generation process. Moreover, considering the ambiguity of the motion attribution,  we introduce a Pair Prompt Control mechanism to disentangle object and camera motion by adding the reference video as an additional input. Extensive experiments demonstrate that MIMIC significantly outperforms existing methods, effectively preserves manipulation intent and motion details, even when handling diverse and deformable objects. Our findings underscore the effectiveness of reference-driven semantics for controllable and realistic manipulation video generation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：具身智能（Embodied Intelligence）的发展长期受限于大规模交互数据的缺乏；视频生成技术为获取交互数据提供了一种可扩展的替代方案。
- **核心问题**：操控（manipulation）视频的生成尤为困难，因为它需要捕捉细微、接触丰富（contact-rich）的动态过程。现有视频扩散模型在操控场景中难以同时兼顾**高层语义理解**与**细粒度视觉细节**，导致生成的视频在物理交互动态和语义一致性上表现不佳。
- **整体含义**：如果能利用参考视频中的语义与运动线索驱动操控视频生成，并实现对交互过程的显式控制，则有望为具身智能提供更真实、可控、可扩展的数据生成途径。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：参考视频（reference videos）蕴含着丰富的语义和运动线索，可以有效地驱动操控视频生成，并支持交互控制。
- **总体框架**：提出 **MIMIC**，一个**两阶段图像到视频（image-to-video）扩散框架**：
  1. **第一阶段**：通过 **Interaction-Motion-Aware（IMA）交互-运动感知模块**，融合参考视频中的视觉特征，生成与目标图像对齐的、连贯的语义掩码（semantic masks）。
  2. **第二阶段**：将上述掩码作为**语义控制信号**，引导视频扩散模型的生成过程，使生成结果与操控意图保持一致。
- **交互控制机制**：针对运动归因（motion attribution）的模糊性问题，引入 **Pair Prompt Control（配对提示控制）** 机制——将参考视频作为额外输入，从而**解耦物体运动与相机运动**，使生成过程更可控。
- **流程要点（文字说明）**：输入为目标图像 + 参考视频 → IMA 模块提取并融合交互/运动特征 → 生成语义掩码 → 掩码注入扩散生成管线（与 Pair Prompt Control 配合）→ 输出符合操控意图、物理细节丰富的视频。

> 说明：所提供的摘要中未给出具体数学公式，以上流程均为对摘要中方法描述的提炼。

## 3. 实验设计：数据集、基准与对比方法

- **数据集 / 场景**：摘要中仅提到方法在处理“多样化且可变形物体”（diverse and deformable objects）时表现良好，但**未具体列出数据集名称**（如 Epic-Kitchens、Something-Something 等是否使用，无法确认）。
- **Benchmark**：未在摘要中明确说明使用了何种标准基准（benchmark）。
- **对比方法**：摘要仅称“significantly outperforms existing methods”（显著优于现有方法），但**未列举具体的对比方法名称**。

> 由于此总结仅基于论文摘要，关于数据集、基准与对比方法的详细信息在摘要中缺失，需查看正文才能确认。

## 4. 资源与算力

- **文中未明确说明**任何算力信息，包括 GPU 型号、数量、训练时长、参数量等。
- 摘要和元数据中均未涉及计算资源相关内容，因此无法总结。

## 5. 实验数量与充分性

- 从摘要看，实验至少覆盖了：
  - 操控视频生成质量的整体评估（对比现有方法）；
  - 对多样化与可变形物体的验证；
  - 操控意图保持与运动细节保留的评估。
- **是否充分、客观、公平**：
  - **充分性**：仅凭摘要无法判断。缺少数据集规模、评估指标、定量结果、消融实验数量等信息；
  - **客观性**：摘要中声称“显著优于现有方法”，但未给出指标数据，尚无法核验；
  - **公平性**：未说明对比方法的设置与可控变量，无法判断是否存在不公平比较。

## 6. 论文的主要结论与发现

- **主要结论**：MIMIC 相比现有方法能显著提升操控视频生成质量，有效保持操控意图和运动细节，即使面对多样与可变形物体也能生成接触丰富的物理交互动态。
- **更广泛的意义**：验证了参考视频驱动的语义线索（参考视频融合 + 掩码控制）对可控、逼真的操控视频生成的有效性，为具身智能数据扩充提供了可行的生成方向。

## 7. 优点：方法或实验设计上的亮点

- **任务靶向性强**：直指操控视频生成中“接触丰富动态”这一难点，而非泛化的视频生成。
- **两阶段设计清晰**：语义掩码生成与视频生成分离，便于控制与解释。
- **多模态线索融合**：IMA 模块同时利用参考视频的语义与运动信息，解决了单图像输入信息不足的问题。
- **新颖的交互控制**：Pair Prompt Control 机制显式解耦物体运动与相机运动，缓解运动归因模糊性，提升可控性。
- **方法通用性**：声称可处理多样化及可变形物体，扩展了适用场景。

## 8. 不足与局限

- **信息透明度不足（以摘要为限）**：未提供数据集、基准、对比方法、评估指标与定量结果，难以独立验证其声称的优势。
- **计算资源缺失**：未报告 GPU 使用情况与训练成本，影响可复现性评估。
- **可能存在的偏差风险**：
  - 仅凭摘要无法判断实验是否覆盖足够多样化的场景与物体类型；
  - 若对比方法未充分调参或未采用相同输入条件，则“显著优于”结论可能受限；
  - 参考视频依赖本身可能限制实际部署（需要额外提供参考视频，并非完全“零样本”生成）。
- **应用限制**：生成操控视频的真实物理一致性（如力、接触摩擦等）是否真正符合物理规律，摘要中未给出证明；其在真实具身系统数据增强中的有效性仍需进一步验证。

（完）
