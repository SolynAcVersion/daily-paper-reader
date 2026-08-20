---
title: "STANCE: Motion Coherent Video Generation Via Sparse-To-dense Anchored Encoding"
title_zh: STANCE：基于稀疏到密集锚定编码的运动连贯视频生成
authors: "ZhiFei Chen, Tianshuo Xu, Leyi Wu, Luozhou Wang, Dongyu Yan, Zihan You, Wenting Luo, Guo Zhang, Ying-Cong Chen"
date: 2025-09-08
pdf: "https://openreview.net/pdf?id=FwtKMYHov7"
tags: ["query:phys-video"]
score: 6.0
evidence: 运动连贯视频生成；时间一致性
tldr: 视频生成在视觉上进展迅速，但物体运动与交互连贯性仍是难点。STANCE针对运动提示编码稀疏和单头优化偏向纹理的问题，提出实例线索将稀疏提示变为稠密2.5D运动场，并解耦外观与运动优化。实验表明该方法能显著提升生成视频中物体交互和运动时间一致性。该框架为可控视频生成提供了更稳健的运动引导方式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频生成中物体运动和交互连贯性差，源于运动提示编码稀疏且外观与运动优化互相干扰。
method: 提出实例线索将稀疏用户提示转为稠密2.5D运动场，并解耦外观和运动优化。
result: 实验表明该方法显著提升运动时间一致性和交互质量。
conclusion: 为可控视频生成提供更稳健的运动引导方式。
---

## Abstract
Video generation has recently made striking visual progress, but maintaining coherent object motion and interactions remains difficult. We trace two practical bottlenecks: (i) human-provided motion hints (e.g., small 2D maps) often collapse to too few effective tokens after encoding, weakening guidance; and (ii) optimizing for appearance and motion in a single head can favor texture over temporal consistency. We present STANCE, an image-to-video framework that addresses both issues with two simple components.
First, we introduce Instance Cues—a pixel-aligned control signal that turns sparse, user-editable hints into a dense 2.5D (camera-relative) motion field by averaging per-instance flow and augmenting with monocular depth over the instance mask. This reduces depth ambiguity compared to 2D drag/arrow inputs while remaining easy to user. Second, we preserve the salience of these cues in token space with Dense RoPE, which tags a small set of motion tokens (anchored on the first frame) with time-addressable rotary embeddings. Paired with joint RGB + auxiliary-map prediction (segmentation or depth), our model anchors structure while RGB handles appearance, stabilizing optimization and improving temporal coherence without requiring per-frame trajectory scripts.

---

## 论文详细总结（自动生成）

# STANCE 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：视频生成技术在视觉质量上取得了显著进展，但生成视频中**物体运动的连贯性**以及**物体间的交互一致性**仍然是核心难点。
- **核心问题**：论文指出现有可控视频生成方法存在两大实际瓶颈：
  - **瓶颈一（运动提示编码稀疏）**：用户提供的运动提示（如小型2D运动图）在编码后往往塌缩为过少的有效token，导致运动指导信号被稀释，缺乏足够的约束力。
  - **瓶颈二（单头优化偏向纹理）**：在同一个优化目标或网络头中同时优化外观与运动，模型容易偏向优化纹理细节而忽视时间维度上的一致性。
- **整体含义**：该论文旨在解决以上两个问题，提出一种无需逐帧轨迹脚本、同时易于用户操作的图像到视频（I2V）生成框架，以提升生成视频中物体运动的时间一致性与交互质量。

---

## 2. 论文提出的方法论

- **总体框架**：提出 **STANCE（Sparse-To-dense Anchored Coding Encoding）** ，一个图像到视频生成框架，包含两个核心组件。
- **核心组件一：Instance Cues（实例线索）——将稀疏提示变为稠密2.5D运动场**
  - 思想：将稀疏、用户可编辑的提示（如拖拽、箭头）转化为稠密的、像素级对齐的2.5D运动场。
  - 实现方式：在实例掩码（instance mask）区域内，对每个实例的运动流进行平均（per-instance flow averaging），并结合单目深度（monocular depth）进行增强。
  - 效果：相对于纯2D拖拽/箭头输入，显著**降低深度歧义**，同时保持用户操作的简易性。
- **核心组件二：Dense RoPE（密集旋转位置编码）——在token空间中保持运动提示显著性**
  - 思想：为锚定在首帧上的少量运动token标记**时间可寻址的旋转位置嵌入**（rotary embeddings）。
  - 作用：使得这些运动token在后续帧的注意力计算中保持时间上的显著性和位置敏感性，避免在编码过程中被稀释或忽略。
  - 配合策略：采用**联合RGB + 辅助地图预测**（辅助地图为分割或深度），其中RGB分支负责外观生成，辅助分支负责锚定结构。两者协同优化但在职责上有所分工，从而稳定优化过程，提升时间一致性。
- **关键机制说明**：该方法不依赖per-frame轨迹脚本，而是通过上述两组件，将易用的稀疏提示转化为强力的稠密运动引导，在token空间中显式保持其显著性，并通过联合预测实现结构锚定与外观生成的解耦。

---

## 3. 实验设计

根据提供的文本信息，**摘要中仅简要提及了实验设置的部分信息**，具体细节有限。

- **数据集/场景**：文本未明确列出具体使用哪些数据集，也未说明具体测试的场景类型（如人类动作、物体交互、动物运动等）。
- **Benchmark**：未明确说明使用了哪个标准基准（benchmark）。
- **对比方法**：文本提到与 **2D drag/arrow inputs（2D拖拽/箭头输入）** 进行对比，证明其降低深度歧义的有效性；但未列出其他对比方法（如其他可控视频生成模型、基于轨迹的方法等）。

---

## 4. 资源与算力

- **文中未明确提及**具体的GPU型号、数量、训练时长、计算资源消耗等信息。

---

## 5. 实验数量与充分性

- **实验覆盖面**：从摘要文本来看，实验主要验证了该方法在运动时间一致性和交互质量上的提升。
- **消融实验**：隐含了对于两个核心组件（Instance Cues 和 Dense RoPE）有效性的验证，但未明确显示是否有系统的消融实验（如移除某一组件）。
- **充分性评估**：
  - **局限性**：由于缺乏具体实验数量（如多少个数据集、多少组对比实验）、定量指标（如FVD、CLIP-score、用户研究等）的说明，无法完全评估其实验的充分性和客观性。
  - **客观性与公平性**：仅从文本描述推断，其方法设计有明确动机支撑，但缺乏大规模基准评测和多基线对比的细节，难以全面判断实验的公平性与说服力。

---

## 6. 论文的主要结论与发现

- STANCE提出的两个简单组件——**Instance Cues（稠密2.5D运动场）** 和 **Dense RoPE（时间可寻址token标记）** ——能够有效解决运动提示稀疏和优化偏向纹理两大问题。
- 实验表明：该方法能**显著提升生成视频中物体交互的准确性和运动的时间一致性**。
- 该方法为可控视频生成提供了一种**更稳健、更易用**的运动引导方式，并且无需逐帧轨迹脚本。

---

## 7. 优点

- **问题定位精准**：清楚指出了实际应用中的两个关键瓶颈（稀疏编码问题、单头优化问题），具有较强的针对性。
- **方法简洁高效**：组件设计简单，易于实现和嵌入现有I2V框架。
- **用户体验友好**：输入端仅需稀疏的用户可编辑提示（如拖拽），同时利用密集2.5D运动场弥补控制信号的不足，在易用性和控制力之间取得了较好的平衡。
- **优化解耦思想**：通过联合RGB+辅助预测的分工，缓解了外观与运动优化互相干扰的问题。
- **无需逐帧脚本**：降低了数据标注难度和应用门槛。

---

## 8. 不足与局限

- **实验细节不透明**：摘要中未提供数据集、评测基准、定量指标、对比基线等关键信息，使得方法有效性难以被客观评估和复现验证。
- **应用范围待确认**：未说明该方法在不同场景（如复杂交互、多人/多物体场景、非刚体运动）下的鲁棒性，其泛化能力未知。
- **潜在偏差风险**：Instance Cues依赖于实例分割掩码，模型在掩码不精准时可能受影响；单目深度本身存在深度歧义，该方法只能缓解而无法完全解决。
- **算力信息缺失**：未报告训练和推理的资源需求，不利于其他研究者评估其实用性或进行公平的效率对比。

---

（完）
