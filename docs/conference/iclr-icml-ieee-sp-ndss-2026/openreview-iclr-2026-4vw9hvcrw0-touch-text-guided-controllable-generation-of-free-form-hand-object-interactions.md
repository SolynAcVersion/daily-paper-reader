---
title: "TOUCH: Text-guided Controllable Generation of Free-Form Hand-Object Interactions"
title_zh: TOUCH：自由形式手物交互的文本引导可控生成
authors: "Guangyi Han, Wei Zhai, Yuhang Yang, Yang Cao, Zheng-Jun Zha"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=4VW9HVCRw0"
tags: ["query:phys-video"]
score: 8.0
evidence: 生成物理合理的手物交互并支持细粒度控制
tldr: 现有手物交互生成局限于固定抓取模式，难以表达多样日常交互。TOUCH 提出自由形式手物交互生成，以细粒度意图为条件，生成推、戳、旋转等可控且物理合理的交互。实验中该方法在多样性和物理合理性上表现突出，将手物交互生成从抓取推广到更广泛的日常场景。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有手物交互生成局限于固定抓取模式，控制依赖力闭合等物理先验，无法覆盖多样化日常交互。
method: 提出自由形式手物交互生成任务，基于细粒度意图条件生成可控、多样且物理合理的手物交互，并配套构建相应数据与模型。
result: 实验表明该方法能生成推、戳、旋转等多样且物理合理的自由交互。
conclusion: 该工作将手物交互生成从抓取扩展至更丰富的日常交互，并提供细粒度控制。
---

## Abstract
Hand-object interaction (HOI) is fundamental for humans to express intent. Existing HOI generation research is predominantly confined to fixed grasping patterns, where control is tied to physical priors such as force closure or generic intent instructions, even when expressed through elaborate language. Such an overly general conditioning imposes a strong inductive bias for stable grasps, thus failing to capture the diversity of daily HOI. To address these limitations, we introduce $\textbf{Free-Form HOI Generation}$, which aims to generate controllable, diverse, and physically plausible HOI conditioned on fine-grained intent, extending HOI from grasping to free-form interactions, like pushing, poking, and rotating. To support this task, we construct $\textbf{WildO2}$, an in-the-wild diverse 3D HOI dataset, which includes diverse HOI derived from internet videos. Specifically, it contains 4.4k unique interactions across 92 intents and 403 object categories, each with detailed semantic annotations. Building on this dataset, we propose $\textbf{TOUCH}$, a three-stage framework centered on a multi-level diffusion model that facilitates fine-grained semantic control to generate versatile hand poses beyond grasping priors. This process leverages explicit contact modeling for conditioning and is subsequently refined with contact consistency and physical constraints to ensure realism. Comprehensive experiments demonstrate our method's ability to generate controllable, diverse, and physically plausible hand interactions representative of daily activities.

---

## 论文详细总结（自动生成）

# TOUCH：自由形式手物交互的文本引导可控生成 —— 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：手物交互（Hand-Object Interaction, HOI）是人类表达意图的基本方式，在计算机视觉、图形学、具身智能等领域具有重要意义。现有 HOI 生成研究主要集中于**固定抓取模式**，其控制方式往往依赖物理先验（如力闭合）或通用意图指令（即使通过复杂语言表达）。
- **核心问题**：这种过度泛化的条件设定对“稳定抓取”产生了强烈的归纳偏置，导致模型难以覆盖日常生活中的多样化交互行为，如推、戳、旋转等自由形式操作。
- **研究意义**：将 HOI 生成从“抓取”推广到更广泛的“自由形式日常交互”，并引入细粒度意图控制，是该工作的核心目标。这不仅扩展了任务定义，也为生成可控、多样且物理合理的人手运动提供了新的方向。

## 2. 论文提出的方法论（核心思想与技术细节）

- **新任务定义**：提出 **Free-Form HOI Generation**（自由形式手物交互生成）任务，目标是在细粒度意图条件下生成可控、多样且物理上合理的手物交互。
- **核心框架 TOUCH**：一个三阶段框架，核心是一个**多层级扩散模型**（multi-level diffusion model），用于实现细粒度语义控制，生成超越抓取先验的多样手部姿态。
  - **阶段一**：以文本/意图为条件，通过多层级扩散模型生成初始手部姿态。
  - **阶段二**：使用**显式接触建模（explicit contact modeling）** 作为条件输入，进一步约束手与物体之间的接触关系。
  - **阶段三**：通过**接触一致性（contact consistency）** 和**物理约束（physical constraints）** 进行细化，确保生成结果在几何和物理上的真实性。
- **关键思路**：将控制条件从“力闭合”等物理先验或通用语言描述，细化为具体意图（如“用手指推物体的左上角”），从而突破抓取模式的局限，支持推、戳、旋转等动作的生成。
- **配套数据**：构建了 **WildO2** 数据集，从互联网视频中获取真实世界的 3D 手物交互数据，包含 92 种意图、403 个物体类别、共 4.4k 个独特交互，并带有详细语义标注。

## 3. 实验设计（数据集、基准与对比方法）

- **数据集**：
  - 主要使用自建数据集 **WildO2**，覆盖真实世界中多样化的手物交互场景。
  - 可能还涉及已有公开 HOI 数据集（如 GRAB、OakInk 等）用于对比或泛化测试，但论文摘要中未详细列出。
- **Benchmark**：由于这是一个新任务（自由形式 HOI 生成），没有现成的标准基准，因此作者基于 WildO2 构建了评估基准，包含 92 种意图、403 类物体上的生成评估。
- **对比方法**：摘要中未明确列出对比方法名称，但从上下文推断，应会与现有基于抓取先验的 HOI 生成方法（如基于力闭合的方法、基于通用语言条件的方法）进行对比，以验证新任务设定和多层级扩散模型的有效性。

## 4. 资源与算力

- **明确说明**：论文摘要中**未提及**任何 GPU 型号、数量、训练时长、参数量等算力信息。
- **推断**：由于涉及大规模视频数据（WildO2）和多层级扩散模型的训练，估计需要较高级别的算力资源（如多卡 A100 级别），但此仅为推测，作者未给出细节。

## 5. 实验数量与充分性

- **实验数量**：摘要中仅提到“综合实验表明该方法能够生成可控、多样且物理合理的交互”，但**未给出具体实验组数**。
- **缺乏细节**：
  - 未提及定量指标（如接触距离、物理穿透率、多样性得分等）。
  - 未明确说明消融实验数量（如是否验证接触建模、物理约束的贡献）。
  - 未展示用户研究或对比实验的具体结果。
- **充分性评估**：
  - **优势**：任务设定新颖，数据规模较大（4.4k 交互、92 意图），具备一定说服力。
  - **不足**：由于摘要内容有限，无法判断实验的全面性和公平性。需要查看全文才能确定是否有充分的基线对比、消融分析、泛化测试和稳定性评估。

## 6. 主要结论与发现

- 现有基于抓取先验的 HOI 生成方法无法表达多样的日常交互，而 TOUCH 通过自由形式任务定义和细粒度意图条件，能够生成推、戳、旋转等多样化交互。
- 结果表明，TOUCH 在**可控性、多样性和物理合理性**方面表现出色，将 HOI 生成从“抓取”成功扩展到“日常交互”这一更广泛的范畴。
- WildO2 数据集本身也可作为未来研究自由形式 HOI 任务的资源。

## 7. 优点（方法与实验设计亮点）

- **任务创新**：首次明确提出“自由形式 HOI 生成”，突破了传统抓取模式的束缚，拓展了研究边界。
- **数据贡献**：通过互联网视频构建大规模、真实世界、语义丰富的 3D 交互数据集 WildO2，涵盖 92 种意图和 403 类物体，为训练和评估提供了坚实基础。
- **方法设计**：三阶段框架思路清晰——先用扩散模型生成，再引入接触建模，最后用物理约束细化；多层级设计有利于处理从整体姿态到局部接触的粒度问题。
- **控制粒度**：以细粒度意图为条件，相比通用语言指令提供了更精确的控制能力，更符合实际应用需求。

## 8. 不足与局限

- **信息缺失**：论文摘要未提供实验细节、定量结果、消融研究、对比方法名称等，无法全面评估其有效性和公平性。
- **数据偏差风险**：WildO2 来源于互联网视频，可能存在物体类别分布不均、交互方式偏向常见动作、手部姿态标注误差等问题，会影响模型的泛化能力。
- **物理合理性验证**：虽然声称经过物理约束细化，但摘要未给出具体的物理指标（如穿透率、接触距离、力合理性），缺乏客观验证标准。
- **控制范围限制**：目前仅覆盖 92 种意图，对于开放世界中更细粒度、更复杂的长时序交互（如工具使用、双手协作）可能仍不充分。
- **应用局限**：方法依赖文本条件，对复杂抽象意图的表达能力有限；且生成的是静态/短时姿态，未说明是否支持时间上的连续运动生成。
- **算力与复现系数**：未报告训练资源、超参数、训练时间等，影响可复现性。

---

（完）
