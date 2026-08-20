---
title: "TOUCH: Text-guided Controllable Generation of Free-Form Hand-Object Interactions"
title_zh: TOUCH：文本引导的自由形式手-物交互可控生成
authors: "Guangyi Han, Wei Zhai, Yuhang Yang, Yang Cao, Zheng-Jun Zha"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=4VW9HVCRw0"
tags: ["query:phys-video"]
score: 4.0
evidence: 生成物理合理的手-物交互，受意图文本控制
tldr: 现有手-物交互生成局限于固定抓取模式，缺乏日常交互多样性。该工作提出自由形式手-物交互生成，将交互从抓取扩展到推、戳、旋转等，并利用细粒度意图文本进行可控条件生成。实验证明该方法能生成多样且物理合理的手-物交互，拓宽了交互生成的范围与应用潜力。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有手-物交互生成局限于固定抓取模式，难以表现多样化的日常交互。
method: 提出自由形式手-物交互生成任务，并基于细粒度意图文本条件生成可控制且物理合理的手-物交互。
result: 方法支持推、戳、旋转等丰富交互，扩展了从抓取到自由操作的范围。
conclusion: 细粒度意图控制能提升生成手-物交互的多样性与物理合理性。
---

## Abstract
Hand-object interaction (HOI) is fundamental for humans to express intent. Existing HOI generation research is predominantly confined to fixed grasping patterns, where control is tied to physical priors such as force closure or generic intent instructions, even when expressed through elaborate language. Such an overly general conditioning imposes a strong inductive bias for stable grasps, thus failing to capture the diversity of daily HOI. To address these limitations, we introduce $\textbf{Free-Form HOI Generation}$, which aims to generate controllable, diverse, and physically plausible HOI conditioned on fine-grained intent, extending HOI from grasping to free-form interactions, like pushing, poking, and rotating. To support this task, we construct $\textbf{WildO2}$, an in-the-wild diverse 3D HOI dataset, which includes diverse HOI derived from internet videos. Specifically, it contains 4.4k unique interactions across 92 intents and 403 object categories, each with detailed semantic annotations. Building on this dataset, we propose $\textbf{TOUCH}$, a three-stage framework centered on a multi-level diffusion model that facilitates fine-grained semantic control to generate versatile hand poses beyond grasping priors. This process leverages explicit contact modeling for conditioning and is subsequently refined with contact consistency and physical constraints to ensure realism. Comprehensive experiments demonstrate our method's ability to generate controllable, diverse, and physically plausible hand interactions representative of daily activities.

---

## 论文详细总结（自动生成）

## 1. 论文核心问题与整体含义

- **研究动机**：手-物交互（HOI）是人类表达意图的基本方式。然而，现有 HOI 生成研究大多局限于**固定抓取模式**，控制条件通常绑定到物理先验（如力闭合）或泛化的意图指令，即使使用复杂语言描述，也难以摆脱“稳定抓取”的归纳偏置，导致无法覆盖日常交互的多样性。
- **核心问题**：如何突破“抓取”这一单一模式，生成**自由形式、多样化且物理合理**的手-物交互，并实现**细粒度意图控制**。
- **整体含义**：该工作将手-物交互生成从“抓取”扩展为“自由操作”（如推、戳、旋转等），旨在让生成模型理解并响应更具体的人类意图，从而推动交互生成在机器人操作、虚拟现实、具身智能等领域的应用潜力。

## 2. 论文提出的方法论

- **核心任务**：提出 **Free-Form HOI Generation（自由形式手-物交互生成）**，以细粒度意图为条件，生成可控、多样、物理合理的手-物交互。
- **数据集构建**：构建 **WildO2**，一个从互联网视频中提取的多样化 3D HOI 数据集，包含：
  - 4.4k 个独特交互；
  - 92 种意图；
  - 403 个物体类别；
  - 每种交互均配有详细语义标注。
- **生成框架**：提出 **TOUCH**，一个三阶段框架，核心是**多层级扩散模型**：
  - **细粒度语义控制**：利用多层级扩散模型，将意图文本映射到手部姿态生成，超越抓取先验；
  - **显式接触建模**：将接触信息作为条件，引导生成过程；
  - **接触一致性与物理约束优化**：通过后处理或约束项，确保生成结果满足接触一致性和物理合理性。

> 注：论文内容中未给出具体的公式或详细算法流程（如扩散模型的具体损失函数、三阶段各自细节），上述为基于摘要的关键技术要点概括。

## 3. 实验设计

- **数据集**：使用论文自建的 **WildO2** 数据集，该数据集来自互联网视频，覆盖 92 种意图、403 个物体类别、4.4k 个独特交互，属于“in-the-wild”场景数据。
- **Benchmark**：由于该任务（自由形式 HOI 生成）是首次提出，因此 WildO2 本身很可能作为该任务的标准基准；评估指标可能涉及多样性、物理合理性、控制准确性等（原文未详述）。
- **对比方法**：摘要未明确列出对比基线，但推测会与现有手-物交互生成方法（尤其是基于固定抓取模式的方法）进行比较，以证明其在多样性、可控性和物理合理性上的优势。

## 4. 资源与算力

- 论文提供的文本中**未提及**任何算力信息，如 GPU 型号、数量、训练时长等。
- 因此，无法评估其训练成本或资源消耗。若需了解，需查阅论文正文或附录。

## 5. 实验数量与充分性

- 从摘要中只能确认**一项主要实验**：在 WildO2 上进行的方法评估，验证了生成结果的可控性、多样性和物理合理性。
- 未提及具体实验组数、消融实验数量或与基线的详细对比次数。
- **充分性判断**：
  - 由于信息有限，无法全面判断实验是否充分。
  - 从任务新颖性看，至少验证了核心主张；但缺少对三阶段框架中接触建模、物理约束、多层级扩散设计等模块的系统消融分析（原文未明确说明），可能削弱对方法各组件贡献的证明力。
  - 未提及其他公开基准或跨数据集泛化实验，因此客观性和公平性尚需在全文验证。

## 6. 论文的主要结论与发现

- 细粒度意图文本可以显著提升自由形式手-物交互生成的**多样性**与**物理合理性**。
- TOUCH 方法能够生成推、戳、旋转等丰富的日常交互，突破固定抓取模式的限制。
- 结合显式接触建模与物理约束，可以在可控生成的同时保持交互的真实感。
- WildO2 数据集可为后续自由形式 HOI 生成研究提供有力支撑。

## 7. 优点

- **任务创新**：首次提出“自由形式手-物交互生成”，将范围从抓取扩展到多种日常操作，具有较强学术价值。
- **数据丰富**：WildO2 数据集规模较大（4.4k 交互、92 意图、403 类物体），且来自互联网视频，具有真实世界多样性。
- **条件控制精细**：利用细粒度意图文本作为条件，比通用“抓取”指令更具表达能力，能更好满足实际应用需求。
- **物理合理性保障**：引入显式接触建模、接触一致性和物理约束，兼顾生成多样性与物理可信度。
- **框架完整性**：三阶段扩散框架（语义控制 → 接触条件 → 物理优化）逻辑清晰，集成技术较完备。

## 8. 不足与局限

- **文本信息有限**：基于当前提供的 PDF 提取内容，缺乏方法细节、实验设置、对比方法与定量指标的完整描述。
- **实验充分性存疑**：未展示消融实验细节，无法确认每个组件（如接触建模、物理约束、多层级扩散）的独立贡献；也未提及跨数据集泛化测试。
- **评估维度不完整**：摘要只提及“可控、多样、物理合理”，但缺少用户研究、交互质量客观指标、失败案例分析等。
- **物理约束的适用性**：自由形式交互（如推、戳）可能涉及更复杂的动力学（滑动、摩擦），仅靠接触一致性和静态物理约束可能不足以处理动态场景。
- **数据偏差风险**：互联网视频来源可能存在类别不均衡、意图分布偏斜等问题，进而影响模型泛化能力。
- **应用限制**：生成结果是否可直接用于机器人执行或 VR 体验，还需后续的实物验证或仿真测试。

（完）
