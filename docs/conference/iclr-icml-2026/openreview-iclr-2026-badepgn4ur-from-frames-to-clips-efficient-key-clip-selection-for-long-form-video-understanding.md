---
title: "From Frames to Clips: Efficient Key Clip Selection for Long-Form Video Understanding"
title_zh: 从帧到片段：面向长视频理解的高效关键片段选择
authors: "Guangyu Sun, Archit Singhal, Burak Uzkent, Mubarak Shah, Chen Chen, Garin N. Kessler"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=BAdePgN4uR"
tags: ["query:frame-dist"]
score: 4.0
evidence: 帧级选择丢失时间动态与事件连续性
tldr: 视频大模型受限于海量视觉token，需稀疏选择帧以压缩上下文。本文指出逐帧选择孤立关键帧会丢弃时间动态，损害对运动与事件连续性的推理。为此作者将选择单位从关键帧扩展到时间连贯的关键片段。实验表明关键片段选择能更好保留帧间时间信息，提升长视频理解效果。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频大模型受困于海量视觉token，帧级选择丢失时间动态。
method: 将选择从孤立关键帧扩展到时间连贯的关键片段。
result: 关键片段选择改善了对运动和事件连续性的推理。
conclusion: 保留帧间时间连贯性可提升长视频理解效果。
---

## Abstract
Video Large Language Models (VLMs) have achieved remarkable results on a variety of vision language tasks, yet their practical use is limited by the "needle in a haystack" problem: the massive number of visual tokens produced from raw video frames exhausts the model’s context window. Existing solutions alleviate this issue by selecting a sparse set of frames, thereby reducing token count, but such frame-wise selection discards essential temporal dynamics, leading to suboptimal reasoning about motion and event continuity. In this work we systematically explore the impact of temporal information and demonstrate that extending selection from isolated key frames to key clips, which are short, temporally coherent segments, improves video understanding.
To maintain a fixed computational budget while accommodating the larger token footprint of clips, we propose an adaptive resolution strategy that dynamically balances spatial resolution and clip length, ensuring a constant token count per video. Experiments on three long-form video benchmarks demonstrate that our training-free approach, F2C, outperforms uniform sampling up to 8.1%, 5.6%, and 10.3% on Video-MME, LongVideoBench and MLVU benchmarks, respectively. These results highlight the importance of preserving temporal coherence in frame selection and provide a practical pathway for scaling Video LLMs to real world video understanding applications.

---

## 论文详细总结（自动生成）

# 论文总结：From Frames to Clips: Efficient Key Clip Selection for Long-Form Video Understanding

> **资料范围说明**：提供的“PDF 提取文本”实际为 OpenReview 的 CAPTCHA 验证页面，未包含论文正文。以下总结主要依据论文标题、作者、摘要与元数据，因此方法细节、实验设置和算力信息无法完全核实。

## 1. 核心问题与整体含义

- **研究背景**：视频大语言模型（Video LLMs）在多种视觉语言任务上表现优异，但实际应用受限于“大海捞针”问题：原始视频帧产生海量视觉 token，容易耗尽模型上下文窗口。
- **现有方案的问题**：常见做法是稀疏选择一组关键帧来减少 token 数，但这种**逐帧选择**会丢弃关键的时间动态信息，导致对运动、事件连续性的推理效果不佳。
- **整体含义**：本文系统探索时间信息的影响，提出将选择单位从孤立关键帧扩展到**时间连贯的关键片段（key clips）**，即短小、时间上连贯的片段，以更好保留帧间时间信息，提升长视频理解。
- **核心主张**：保留时间连贯性比单纯选帧更重要；在固定计算预算下，关键片段选择是扩展 Video LLMs 到真实视频理解应用的实用路径。

## 2. 方法论

- **核心思想**：提出 **F2C（From Frames to Clips）**，一种**免训练（training-free）**方法，将视频上下文选择从“关键帧”推进到“关键片段”。
- **关键定义**：关键片段是短小、时间连贯的视频段，而非孤立帧；其优势在于保留运动与事件连续性。
- **关键技术细节**：
  - 为应对片段带来的更大 token footprint，提出**自适应分辨率策略（adaptive resolution strategy）**。
  - 该策略动态平衡**空间分辨率**与**片段长度**，确保每个视频的 token 数保持恒定。
  - 在固定计算预算下，将稀疏的关键片段输入 Video LLM，从而缓解上下文窗口限制。
- **算法流程（文字说明）**：
  1. 输入长视频，并设定固定 token 预算；
  2. 将选择单位从单帧扩展为时间连贯的短片段；
  3. 在预算约束下选择关键片段；
  4. 根据片段长度动态调整空间分辨率，使总 token 数恒定；
  5. 将所选片段组成稀疏视觉上下文，供 Video LLM 推理。
- **注意**：摘要未给出具体选择评分函数、片段长度范围、分辨率调节公式或超参数设置，因此无法进一步还原算法细节。

## 3. 实验设计

- **数据集 / 场景**：三个长视频理解基准：
  - **Video-MME**
  - **LongVideoBench**
  - **MLVU**
- **对比方法**：主要与**均匀采样（uniform sampling）**对比。
- **主要结果**：
  - 在 Video-MME 上，F2C 相比均匀采样最高提升 **8.1%**；
  - 在 LongVideoBench 上最高提升 **5.6%**；
  - 在 MLVU 上最高提升 **10.3%**。
- **场景侧重**：长视频理解，尤其是运动与事件连续性推理。
- **未说明信息**：摘要未给出具体评价指标、所用 Video LLM 骨干、输入帧数 / token 预算、片段长度设置、推理成本等。

## 4. 资源与算力

- 论文摘要与元数据中**未提及** GPU 型号、数量、训练时长或推理算力。
- 由于方法被描述为 **training-free**，可能不需要训练阶段算力；但实验评测所需的推理 / 计算资源同样未说明。
- 因此，无法从现有材料判断其实际计算开销与可扩展性。

## 5. 实验数量与充分性

- 从摘要看，实验覆盖 **3 个长视频基准**，并与 **uniform sampling** 对比。
- 未提及消融实验，例如：
  - 不同片段长度的影响；
  - 自适应分辨率策略的贡献；
  - 不同选择策略的对比；
  - 不同 Video LLM 骨干或模型规模的验证。
- **充分性评价**：跨三个基准的一致提升提供了方向性证据，但缺少全文和详细实验设置，无法判断是否充分。
- **客观性与公平性**：与均匀采样对比较直接，但若仅对比均匀采样，则未覆盖其他帧选择、token 压缩或长视频理解方法，外部有效性有限。

## 6. 主要结论与发现

- 逐帧选择会丢弃必要的时间动态，损害对运动和事件连续性的推理。
- 将选择单位扩展到时间连贯的关键片段，能更好保留帧间时间信息，提升长视频理解效果。
- 在固定 token 预算下，通过自适应分辨率平衡空间分辨率与片段长度是可行的。
- 关键片段选择为 Video LLMs 在真实世界长视频理解中的扩展提供了实用路径。

## 7. 优点

- **问题定位准确**：抓住 Video LLMs 的视觉 token 爆炸与逐帧选择丢失时间动态这一核心矛盾。
- **思路简洁有效**：从“关键帧”到“关键片段”的单位转换直观且具有启发性。
- **免训练方法**：F2C 为 training-free，便于集成到现有 Video LLM 流程中。
- **预算可控**：自适应分辨率策略在引入片段的同时保持每视频 token 数恒定，兼顾计算约束。
- **实验信号积极**：在三个长视频基准上均报告了相对均匀采样的提升。

## 8. 不足与局限

- **全文不可得**：当前材料仅为摘要和元数据，无法核实方法细节、公式、实验严谨性和结果可复现性。
- **实验覆盖有限**：仅摘要提到三个 benchmark 和 uniform sampling 对比，缺少与其他先进长视频理解 / token 压缩方法的比较。
- **消融不足**：未说明片段长度、分辨率平衡策略、选择策略等各组件的独立贡献。
- **算力与效率未报告**：缺少 GPU 资源、推理延迟、吞吐量等实际应用关键指标。
- **潜在偏差风险**：结果可能受特定 benchmark、模型骨干和视频类型影响；固定 token 预算下降低空间分辨率可能影响细粒度识别。
- **应用限制**：关键片段选择可能引入额外计算或选择开销；在极长视频和复杂场景下的鲁棒性尚不明确。

（完）
