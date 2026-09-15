---
title: Improving Autoregressive Video Modeling with History Understanding
title_zh: 通过历史理解改进自回归视频建模
authors: "Wenyang Luo, Haina Qin, Bing Li, Jiwen Lu, Xin Tao, Pengfei Wan, Kun Gai"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=kd2V5Bkw1D"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 以历史帧为条件顺序预测未来帧
tldr: 自回归视频生成以历史帧为条件顺序预测未来帧，但历史帧条件表示的作用长期被忽视。本文系统分析后发现历史表示质量与生成性能正相关，且改进历史表示带来的增益无法仅靠优化未来帧表示获得。基于此作者提出MiMo，通过掩码历史增强历史帧内部表示。结果验证了强化历史表示能有效提升视频自回归生成质量，为条件建模提供新视角。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 自回归视频生成中历史帧条件表示的作用未被充分探索。
method: 提出MiMo，通过掩码历史增强历史帧的内部表示。
result: 历史表示质量与生成性能正相关，改进其表示带来显著增益。
conclusion: 强化历史帧表示可有效提升视频自回归生成。
---

## Abstract
Video autoregressive generation (VideoAR) sequentially predicts future frames conditioned on history frames. Despite the advance of recent diffusion-based VideoAR, the role of conditioning signal—internal representations of history frames—remains underexplored. Inspired by the success of strong condition representations in text-conditioned generation, we investigate: \textit{Can better internal representations of history frames improve VideoAR performance?} Through systematic analysis, we show that history representation quality positively correlates with VideoAR, and that enhancing these representations provides gains that cannot be achieved by refining future frames representations alone. Based on these insights, we propose \textbf{MiMo} (Masked History Modeling), a novel framework that seamlessly integrates representation learning into diffusion-based VideoAR. MiMo applies masks to history frame tokens and trains the model to predict masked tokens of current and future frames alongside the diffusion objective, yielding predictive and robust history representations without relying on vision foundation models (VFMs) or heavy architectural changes. Extensive experiments demonstrate that MiMo achieves competitive performance in video prediction and generation tasks while substantially improving training efficiency. Our work underscores the importance of history representations in VideoAR.

---

## 论文详细总结（自动生成）

## 材料说明

- 给定 PDF 提取文本实际仅包含标题、元数据与 Abstract；PDF 链接返回 503，未提供全文。
- 因此以下总结严格基于现有材料；未出现的数据集、算力、消融数量等信息将明确标注为“未说明”，不作编造。

## 1. 核心问题与整体含义

- 论文关注 **视频自回归生成（Video Autoregressive Generation, VideoAR）**：模型按时间顺序，基于历史帧预测未来帧。
- 尽管近期基于扩散模型的 VideoAR 取得进展，但作为条件信号的 **历史帧内部表示** 的作用仍未得到充分研究。
- 受文本条件生成中“强条件表示”成功的启发，作者提出核心研究问题：**更好的历史帧内部表示能否提升 VideoAR 性能？**
- 整体含义：论文将研究重点从“只优化未来帧表示”转向“提升条件信号质量”，强调历史表示在自回归视频建模中的关键作用。

## 2. 方法论：MiMo

- 核心思想：提出 **MiMo（Masked History Modeling，掩码历史建模）**，将表示学习无缝集成到基于扩散的 VideoAR 中。
- 关键观察：
  - 历史表示质量与 VideoAR 性能正相关。
  - 增强历史表示可带来仅优化未来帧表示无法获得的增益。
- 技术流程（基于摘要）：
  - 对历史帧 token 施加掩码。
  - 训练模型在原有扩散目标之外，额外预测当前帧和未来帧中被掩码的 token。
  - 通过这种掩码预测任务，使历史表示同时具备 **预测性** 和 **鲁棒性**。
- 方法特点：
  - 不依赖视觉基础模型（VFMs）。
  - 不需要重型架构改动。
  - 可与扩散式 VideoAR 训练目标结合，属于表示学习增强而非完全替换生成框架。
- 具体细节限制：掩码比例、损失权重、tokenizer 设计、训练调度等未在给定材料中说明。

## 3. 实验设计

- 摘要称进行了 **大量实验（extensive experiments）**，覆盖 **视频预测** 和 **视频生成** 任务。
- 结果声称：
  - MiMo 在视频预测与生成任务上达到有竞争力的性能。
  - 显著提升训练效率。
- 未说明的信息：
  - 具体数据集 / 场景：未列出。
  - Benchmark：未列出。
  - 对比方法：未列出。
  - 是否与现有 VideoAR 方法、扩散基线、仅优化未来帧表示的变体进行系统比较：摘要暗示存在相关对照，但细节未披露。

## 4. 资源与算力

- 给定材料中 **未提及** GPU 型号、数量、训练时长、参数量、训练数据规模等算力信息。
- 因此无法评估其训练成本、可复现性和实际资源门槛。

## 5. 实验数量与充分性

- 从摘要可见，实验至少涉及：
  - 历史表示质量与 VideoAR 性能关系的系统分析。
  - 增强历史表示与仅优化未来帧表示的对比或消融。
  - MiMo 在视频预测与生成任务上的整体评估。
  - 训练效率评估。
- 但具体实验组数、数据集数量、消融维度、统计显著性等均未提供。
- 公平性无法判断：缺少 baseline 配置、训练预算、评价指标和实现细节。
- 因此，仅凭摘要不能确认实验是否充分、客观、公平；只能说作者声称实验广泛且结果积极。

## 6. 主要结论与发现

- 历史帧内部表示质量与 VideoAR 性能呈正相关。
- 增强历史表示带来的收益，不能仅通过优化未来帧表示获得。
- MiMo 通过掩码历史建模，可在不依赖 VFM 和重架构改动的情况下提升 VideoAR。
- MiMo 在视频预测和生成任务上取得有竞争力的表现，并提升训练效率。
- 总体结论：**条件信号质量对自回归视频生成至关重要**，历史表示应成为 VideoAR 建模的重要优化对象。

## 7. 优点

- 研究视角有价值：关注长期被忽视的“历史帧内部表示”而非仅未来帧生成。
- 动机清晰：从文本条件生成的成功迁移到视频自回归条件建模。
- 方法较简洁：MiMo 以掩码历史建模增强表示，避免依赖 VFM 和复杂架构。
- 潜在通用性：可作为扩散式 VideoAR 的辅助训练目标。
- 兼顾性能与效率：摘要强调竞争性能和训练效率提升。
- 结论具有启发性：强调条件信号质量，对后续 VideoAR 研究有方向性意义。

## 8. 不足与局限

- 材料不完整：缺少全文，无法核实方法细节、实验设置与结果真实性。
- 实验信息缺失：未给出数据集、benchmark、指标、baseline、消融数量和算力。
- 公平性风险：无法确认是否在相同 backbone、训练预算和数据条件下比较。
- 方法细节未知：掩码策略、损失设计、超参数敏感性、推理开销均未说明。
- 应用限制未知：长视频生成、误差累积、高分辨率、实时性等关键问题未在摘要中讨论。
- 偏差风险：摘要呈正面结论，缺少失败案例、负面结果或边界条件分析。
- 可复现性受限：由于资源与实验细节未披露，复现和独立评估困难。

（完）
