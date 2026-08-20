---
title: "STANCE: Motion Coherent Video Generation Via Sparse-To-dense Anchored Encoding"
title_zh: STANCE：通过稀疏到稠密锚定编码实现运动一致的视频生成
authors: "ZhiFei Chen, Tianshuo Xu, Leyi Wu, Luozhou Wang, Dongyu Yan, Zihan You, Wenting Luo, Guo Zhang, Ying-Cong Chen"
date: 2025-09-08
pdf: "https://openreview.net/pdf?id=FwtKMYHov7"
tags: ["query:phys-video"]
score: 6.0
evidence: 通过稀疏到稠密锚定编码提升视频生成的运动与时间一致性
tldr: 针对视频生成中对象运动不连贯和时间一致性差的问题，STANCE 提出实例提示机制，把用户稀疏的可编辑运动提示转化为稠密2.5D相机相对运动场，并结合单目深度强化实例级运动控制。通过像素级对齐的稠密运动引导，模型在保持外观质量的同时显著提升运动的一致性与交互表现，为可控视频生成提供一种简洁有效的稀疏到稠密控制范式。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频生成难以保持对象运动一致性和交互，运动提示编码后信息不足，外观与运动联合优化导致时间一致性差。
method: 提出实例提示信号，将稀疏可编辑提示转化为稠密2.5D运动场，并结合单目深度增强实例运动信息，引导图像到视频生成。
result: 改善了运动一致性和时间一致性，在图像到视频生成任务上有效。
conclusion: 说明稀疏到稠密运动编码能够有效提升视频生成的运动连贯性。
---

## Abstract
Video generation has recently made striking visual progress, but maintaining coherent object motion and interactions remains difficult. We trace two practical bottlenecks: (i) human-provided motion hints (e.g., small 2D maps) often collapse to too few effective tokens after encoding, weakening guidance; and (ii) optimizing for appearance and motion in a single head can favor texture over temporal consistency. We present STANCE, an image-to-video framework that addresses both issues with two simple components.
First, we introduce Instance Cues—a pixel-aligned control signal that turns sparse, user-editable hints into a dense 2.5D (camera-relative) motion field by averaging per-instance flow and augmenting with monocular depth over the instance mask. This reduces depth ambiguity compared to 2D drag/arrow inputs while remaining easy to user. Second, we preserve the salience of these cues in token space with Dense RoPE, which tags a small set of motion tokens (anchored on the first frame) with time-addressable rotary embeddings. Paired with joint RGB + auxiliary-map prediction (segmentation or depth), our model anchors structure while RGB handles appearance, stabilizing optimization and improving temporal coherence without requiring per-frame trajectory scripts.

---

## 论文详细总结（自动生成）

# STANCE：通过稀疏到稠密锚定编码实现运动一致的视频生成——论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：视频生成在视觉质量上已取得显著进展，但*保持连贯的对象运动与交互*仍是核心难点。
- **两大瓶颈**：
  - **运动提示信息坍缩**：人工提供的运动提示（如小尺寸2D拖拽图/箭头图）在编码后往往坍缩为极少量有效token，导致运动引导信号被稀释，生成时运动弱、错乱。
  - **外观与运动的联合优化冲突**：在单一解码头中同时优化外观与运动，模型容易偏向纹理细节而牺牲时间一致性。
- **研究意义**：提出一种能兼顾“用户可编辑性”和“稀疏到稠密运动引导”的简洁范式，为可控视频生成（尤其是图像到视频）提供新的编码与优化思路。

## 2. 方法论：核心思想、关键技术细节与算法流程

- **总体思想**：将用户提供的稀疏、可编辑运动提示，转化为**像素级对齐的稠密2.5D运动场**，并从token层面增强其显著性，从而在不牺牲外观质量的前提下提升运动一致性。
- **技术细节一：Instance Cues（实例提示）**
  - 输入：用户在各对象实例上标注的稀疏运动提示（类似2D拖拽/箭头）。
  - 处理：在实例掩码内**按实例平均运动**，生成每实例的密集流场。
  - 增强：结合**单目深度**，将2D流场扩展为2.5D（相机相对）运动场，减少深度歧义。
  - 效果：相比纯2D拖拽输入，减少深度模糊；同时保持用户可编辑的简易性。
- **技术细节二：Dense RoPE（稠密旋转位置编码）**
  - 目标：解决“运动token编码后显著性丢失”问题。
  - 做法：为锚定在第一帧的一小组运动token，附加**时间可寻址的旋转位置嵌入**，使模型在后续帧中仍能识别并强化这些运动token的引导作用。
  - 本质：在token空间中保留运动线索的“位置记忆”，防止信息坍缩。
- **技术细节三：联合RGB + 辅助图预测**
  - 模型同时预测RGB图像与辅助图（分割图或深度图）。
  - 作用：辅助图作为结构锚点，RGB负责外观，二者**解耦优化**，稳定训练并提升时间一致性。
- **算法流程（文字描述）**：
  1. 输入首帧图像 + 用户稀疏运动提示；
  2. 计算每实例流场 → 结合单目深度 → 得到稠密2.5D运动场（Instance Cues）；
  3. 将运动场编码为运动token并施加Dense RoPE；
  4. 图像到视频生成，联合优化RGB重建与辅助图预测。

## 3. 实验设计

- **任务**：图像到视频生成（image-to-video generation）。
- **评估重点**：
  - 对象运动一致性；
  - 时间一致性；
  - 交互表现（对象间交互）。
- **数据集与benchmark**：
  - 论文提供的摘要与元数据中**未给出具体数据集名称**，也未列出具体的benchmark（如UCF-101、DAVIS、WebVid等）与评估指标（如FVD、CLIP score、运动轨迹精度等）。
  - 由于仅能获取论文摘要信息，详细实验设置（场景数量、对比方法列表）无法从现有文本中确证。
- **对比方法**：
  - 摘要中**未提及具体基线方法名称**，仅从语义上推断可能对比了现有视频生成方法（如基于拖拽/运动控制的方法）以及无运动引导的baseline。

## 4. 资源与算力

- **明确说明**：论文提供的文本信息中**未提及**使用的GPU型号、数量、训练时长、数据规模等算力相关细节。
- 因此，关于算力资源，目前**无法给出具体数据**，需查阅论文全文实验章节才能获知。

## 5. 实验数量与充分性分析

- **已知实验**：
  - 核心实验：图像到视频生成任务上的运动一致性评估；
  - 方法层面包含多个组件（Instance Cues、Dense RoPE、联合预测），推测有对应的**消融实验**，但摘要中未明确列出；
  - 对“稀疏输入→稠密运动场”的可行性验证（是否做了不同稀疏程度的对照实验尚不清楚）。
- **充分性评估**：
  - **受限**：由于信息不足，无法判断实验覆盖了多少数据集、多少场景类型（如多对象交互、相机运动、遮挡等）。
  - **客观性**：摘要中未提供具体数值指标，难以评估改进幅度。
  - **公平性**：无法判断对照组设置是否对齐（如是否统一运动提示形式、是否控制计算量）。
  - 结论：**实验充分性无法从摘要层面确认**，需要阅读完整论文。

## 6. 主要结论与发现

- **核心结论**：稀疏到稠密的运动编码方式，能够有效提升视频生成中的运动一致性与时间一致性。
- **分项发现**：
  1. 仅将2D拖拽/箭头提示转为**2.5D密集运动场**，即可显著改善运动引导质量；
  2. 通过Dense RoPE在token层面保持运动锚点的显著性，是防止运动提示编码坍缩的关键；
  3. 联合预测结构锚点（分割/深度）与RGB，有助于解耦外观与运动优化，改善时间不稳定性；
  4. 所提方法**无需逐帧轨迹脚本**，仍能实现较好的运动控制，实用性更强。

## 7. 优点（方法与实验亮点）

- **方法角度**：
  - **稀疏到稠密的控制范式**：用户输入成本低（类似2D拖拽），但引导密度高（像素级对齐的2.5D运动场），两者兼顾巧妙。
  - **引入单目深度解决深度歧义**：比纯2D运动输入在物理合理性上更有优势。
  - **Dense RoPE的设计直觉清晰**：专门针对“运动token信息坍缩”这一诊断出的瓶颈对症下药。
  - **联合辅助图预测的优化解耦**：结构锚定与外观生成的分离，符合视频生成中“结构优先、纹理其次”的实际经验。
- **实用角度**：
  - 适用图像到视频任务，接口对创作者友好，无需写脚本或提供序列轨迹。
  - 方法由两个简单组件构成，设计简洁，可扩展性强（辅助图可为分割或深度，灵活适配不同应用）。

## 8. 不足与局限

- **信息缺失的局限**：
  - 摘要中未给出定量结果，无法验证“显著提升”的幅度；
  - 未列出具体数据集和对比方法，无法评估实验的广度与公平性；
  - 无算力、训练成本信息，难以评估部署可行性。
- **方法潜在局限（基于推理）**：
  - 依赖单目深度估计质量：若深度不准，2.5D运动场可能引入误差；
  - 实例掩码质量敏感：自动实例分割误差会影响运动引导的准确性；
  - 多对象复杂交互场景：按实例平均运动可能损失局部运动细节；强交互（如手握物体）下独立实例运动可能不一致；
  - 辅助图预测增加解码负担：若辅助图本身预测不佳，可能带来额外噪声；
  - 时间可寻址ROPE的泛化能力：长视频生成中旋转编码的位置外推表现未知。
- **总体评价**：方法思路有价值、针对性强，但当前文本信息不足以进行完全充分的实验合理性与性能验证评估，需进一步获取论文全文。

（完）
