---
title: "CADMorph: Geometry‑Driven Parametric CAD Editing via a Plan–Generate–Verify Loop"
title_zh: CADMorph：基于几何驱动参数化CAD编辑的计划-生成-验证循环
authors: "Weijian Ma, Shizhao Sun, Ruiyu Wang, Jiang Bian"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=jCuEeQF7uP"
tags: ["query:cad-spatial"]
score: 5.0
evidence: 保持形状保真度的几何驱动参数化CAD编辑
tldr: CAD模型由参数化构造序列与可见几何形状耦合表示，几何修改需同步编辑参数序列，但编辑数据稀缺。该文提出CADMorph，采用计划-生成-验证循环，在推理时协调预训练领域基础模型完成几何驱动的参数化编辑。实验表明该方法在保持结构、语义有效与形状保真方面具有优势。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 几何驱动的参数化CAD编辑需同步修改参数序列，但编辑三元组数据稀缺。
method: 提出CADMorph，用计划-生成-验证循环在推理时编排预训练领域基础模型。
result: 在保持原序列结构、语义有效性与目标形状保真度方面表现良好。
conclusion: 为稀缺数据下的参数化CAD编辑提供了可验证的迭代框架。
---

## Abstract
A Computer-Aided Design (CAD) model encodes an object in two coupled forms: a \emph{parametric construction sequence} and its resulting \emph{visible geometric shape}.
During iterative design, adjustments to the geometric shape inevitably require synchronized edits to the underlying parametric sequence, called \emph{geometry-driven parametric CAD editing}.
The task calls for 1) preserving the original sequence’s structure, 2) ensuring each edit's semantic validity, and 3) maintaining high shape fidelity to the target shape, all under scarce editing data triplets.
We present \emph{CADMorph}, an iterative \emph{plan–generate–verify} framework that orchestrates pretrained domain-specific foundation models during inference: a \emph{parameter-to-shape} (P2S) latent diffusion model and a \emph{masked-parameter-prediction} (MPP) model.
In the planning stage, cross-attention maps from the P2S model pinpoint the segments that need modification and offer editing masks. 
The MPP model then infills these masks with semantically valid edits in the generation stage. 
During verification, the P2S model embeds each candidate sequence in shape-latent space, measures its distance to the target shape, and selects the closest one. 
The three stages leverage the inherent geometric consciousness and design knowledge in pretrained priors, and thus tackle structure preservation, semantic validity, and shape fidelity respectively. 
Besides, both P2S and MPP models are trained without triplet data, bypassing the data-scarcity bottleneck.
CADMorph surpasses GPT-4o and specialized CAD baselines, and supports downstream applications such as iterative editing and reverse-engineering enhancement.

---

## 论文详细总结（自动生成）

# CADMorph 论文总结

> 说明：提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页面，未包含论文正文。以下总结主要依据论文摘要、题录元数据与已有信息；凡涉及具体实验设置、数据集、算力等未披露内容，均会明确标注“未说明/无法确认”。

## 1. 核心问题与整体含义
- **研究背景**：CAD 模型通常由两部分耦合表示：一是**参数化构造序列**，二是该序列生成的**可见几何形状**。
- **核心问题**：在迭代设计中，用户调整几何形状时，必须同步修改底层参数化序列，这类任务称为**几何驱动的参数化 CAD 编辑**。
- **关键挑战**：
  - 保持原参数序列的**结构**；
  - 保证每次编辑在 CAD 语义上**有效**；
  - 保持编辑结果与目标形状的**高保真度**；
  - 同时面临编辑三元组数据**稀缺**的问题。
- **整体含义**：论文提出 CADMorph，试图在缺少大量编辑标注数据的情况下，利用预训练领域基础模型和推理时闭环验证，实现可迭代、可验证的参数化 CAD 编辑。

## 2. 方法论
- **核心思想**：提出 **CADMorph**，采用“**计划–生成–验证**”（plan–generate–verify）循环，在推理阶段编排两个预训练领域基础模型：
  - **P2S**：parameter-to-shape latent diffusion model，参数到形状的潜扩散模型；
  - **MPP**：masked-parameter-prediction model，掩码参数预测模型。
- **三阶段流程**：
  - **计划阶段**：利用 P2S 模型的**交叉注意力图**定位参数序列中需要修改的片段，并生成编辑掩码。
  - **生成阶段**：由 MPP 模型对被掩码的参数片段进行填充，生成语义有效的编辑候选。
  - **验证阶段**：P2S 模型将每个候选序列嵌入形状潜空间，计算其与目标形状的距离，选择距离最近的候选。
- **迭代机制**：上述计划–生成–验证过程可循环执行，逐步逼近目标几何形状。
- **训练策略**：P2S 和 MPP 均**不依赖编辑三元组数据**训练，从而绕过编辑数据稀缺瓶颈。
- **分工逻辑**：
  - 结构保持：依赖原序列与掩码机制；
  - 语义有效：依赖 MPP 的参数填充能力；
  - 形状保真：依赖 P2S 的形状潜空间距离验证。
- **算法流程文字描述**：输入原始参数序列与目标几何形状 → P2S 交叉注意力定位需修改段并给出掩码 → MPP 填充掩码生成候选参数序列 → P2S 验证候选与目标形状距离 → 选择最优候选 → 可迭代继续编辑。

## 3. 实验设计
- 摘要声称 CADMorph **超过 GPT-4o 和专用 CAD 基线方法**。
- 支持下游应用，包括：
  - **迭代编辑**；
  - **逆向工程增强**。
- 但提供的文本中**未给出具体数据集名称、benchmark 设置、评价指标、对比方法清单**。
- 因此，无法确认实验场景是合成 CAD 数据、真实 CAD 模型库，还是特定逆向工程任务。
- 元数据标签为 `query:cad-spatial`，证据描述强调“保持形状保真度的几何驱动参数化 CAD 编辑”，但不足以还原完整实验设计。

## 4. 资源与算力
- 提供的摘要和元数据中**未说明 GPU 型号、数量、训练时长、参数量或推理成本**。
- 仅可知：方法使用预训练的 P2S 与 MPP 模型，且两者训练**不需要编辑三元组数据**。
- 因此，无法评估其训练算力需求或推理效率；需要正文补充。

## 5. 实验数量与充分性
- 提供文本中**没有实验组数、消融实验、数据集数量、用户研究或统计显著性信息**。
- 从摘要可推断至少包含：
  - 与 GPT-4o 的对比；
  - 与专用 CAD 基线的对比；
  - 下游应用展示，如迭代编辑和逆向工程增强。
- 但无法判断实验是否充分、是否覆盖多种 CAD 操作、是否进行公平的消融与误差分析。
- 由于缺少正文，**客观性与公平性无法验证**。

## 6. 主要结论与发现
- CADMorph 在以下方面表现良好：
  - 保持原参数序列结构；
  - 保证编辑语义有效；
  - 维持目标形状高保真度。
- 方法在摘要所述范围内**超越 GPT-4o 和专用 CAD 基线**。
- 该框架为稀缺编辑数据下的参数化 CAD 编辑提供了**可验证、可迭代**的解决思路。
- 可扩展到迭代编辑与逆向工程增强等下游任务。

## 7. 优点
- **数据效率高**：P2S 和 MPP 无需编辑三元组训练，直接利用预训练先验，缓解数据稀缺问题。
- **闭环可验证**：计划–生成–验证循环使编辑结果可在形状潜空间中筛选，提升可靠性。
- **多目标对应清晰**：三个阶段分别对应结构保持、语义有效和形状保真，设计逻辑明确。
- **模块化编排**：复用 P2S 与 MPP 两个领域基础模型，避免从零训练统一编辑模型。
- **下游扩展性好**：支持迭代编辑和逆向工程增强，具备实际设计流程应用潜力。

## 8. 不足与局限
- **正文缺失导致无法验证**：由于 PDF 提取内容为验证页，无法核实实验细节、数据集、指标、算力与消融。
- **依赖预训练模型能力**：P2S 和 MPP 的质量直接决定编辑上限，若基础模型覆盖不足，可能影响泛化。
- **推理成本可能较高**：计划–生成–验证循环涉及多次 P2S/MPP 调用与候选验证，实际延迟和计算开销未说明。
- **验证标准相对单一**：摘要中验证阶段主要依据形状潜空间距离选择候选，可能无法完全覆盖工程约束、参数合法性、可制造性等设计意图。
- **公平性待确认**：与 GPT-4o 和专用 CAD 基线的比较设置、提示设计、数据划分等未披露。
- **应用限制未知**：跨 CAD 软件、跨参数化建模范式、复杂装配体或工业级模型上的表现尚无信息。

（完）
