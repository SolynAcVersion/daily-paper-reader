---
title: Autoregressive Video Generation with Learnable Memory and Consistent Decoding
title_zh: 带可学习记忆与一致性解码的自回归视频生成
authors: "xiaofei wu, Guozhen Zhang, zhiyong xu, Yuan Zhou, Qinglin Lu, Xuming He"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=UoRWYIGeRi"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 长视频生成中的长程依赖建模与时间一致性
tldr: 长视频自回归生成面临长程依赖难以捕捉与误差累积的双重挑战。本文提出MemoryPack可学习上下文检索机制，联合文本与图像信息建模短长期依赖，并引入Direct Forcing单步近似解码策略缓解误差累积。实验实现分钟级时间一致性且保持线性复杂度，为长视频生成的帧间连贯性提供了高效方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 长视频自回归生成难以兼顾长程依赖捕捉与误差累积抑制。
method: 提出MemoryPack可学习上下文检索与Direct Forcing单步解码近似策略。
result: 实现分钟级时间一致性，并保持随视频长度线性扩展的计算效率。
conclusion: 为长视频生成中的帧间连贯性与误差控制提供了可扩展方法。
---

## Abstract
Long-form video generation presents a dual challenge: models must capture long-range dependencies while preventing the error accumulation inherent in autoregressive decoding. To address these challenges, we make two contributions. First, for dynamic context modeling, we propose MemoryPack, a learnable context-retrieval mechanism that leverages both textual and image information as global guidance to jointly model short- and long-term dependencies, achieving minute-level temporal consistency. This design scales gracefully with video length, preserves computational efficiency, and maintains linear complexity. Second, to mitigate error accumulation, we introduce Direct Forcing, an efficient single-step approximating strategy that improves training–inference alignment and thereby curtails error propagation during inference. Together, MemoryPack and Direct Forcing substantially enhance the context consistency and reliability  of long-form video generation, advancing the practical usability of autoregressive video models. Project website: https://anonymous.4open.science/w/ICLR2026-55FF

---

## 论文详细总结（自动生成）

# 带可学习记忆与一致性解码的自回归视频生成：论文总结

> 说明：当前可获取的论文 PDF 正文抓取失败（503），仅有标题、作者、摘要与 OpenReview 元数据。因此以下总结主要依据摘要和元数据；凡正文中可能包含但当前不可见的信息（如数据集、对比方法、算力、实验组数等），均明确标注为“未提供/无法确认”，不做臆测。

## 1. 论文的核心问题与整体含义

- **研究动机**：长视频自回归生成面临双重挑战：
  - 模型需要捕捉**长程依赖**，以保证视频在较长时间跨度上的语义与内容连贯；
  - 自回归解码存在**误差累积**问题，早期帧的偏差会在后续生成中传播和放大。
- **背景**：长视频生成若要在实际应用中可用，必须同时兼顾时间一致性、生成可靠性与计算效率；而传统自回归视频模型在视频变长时容易出现上下文遗忘、漂移和计算复杂度上升。
- **整体含义**：论文试图通过“可学习记忆”和“一致性解码”两条路线，提升长视频生成的上下文一致性与可靠性，使自回归视频模型更接近实用化。摘要声称其方案可实现分钟级时间一致性，并保持随视频长度线性扩展的计算效率。

## 2. 论文提出的方法论

- **核心思想**：分别针对“长程依赖建模”和“误差累积抑制”提出两个组件：
  - **MemoryPack**：用于动态上下文建模；
  - **Direct Forcing**：用于缓解自回归推理中的误差传播。
- **MemoryPack：可学习上下文检索机制**
  - 利用**文本和图像信息作为全局引导**；
  - 联合建模**短期依赖与长期依赖**；
  - 目标是实现**分钟级时间一致性**；
  - 设计上强调随视频长度“优雅扩展”，保持计算效率，并维持**线性复杂度**。
- **Direct Forcing：单步近似解码策略**
  - 是一种高效的**单步近似策略**；
  - 用于改善**训练—推理对齐**；
  - 从而减少推理阶段的误差传播，缓解自回归解码的误差累积问题。
- **文字化算法流程理解**：
  - 在自回归视频生成过程中，模型不仅依赖最近帧，还通过 MemoryPack 从可学习记忆中检索与当前生成相关的上下文信息；
  - 这些上下文由文本和图像信息共同引导，以兼顾局部动态和全局叙事一致性；
  - 在训练与解码阶段，Direct Forcing 通过单步近似目标缩小训练时与推理时的分布差异，使模型在自回归推理时更稳定；
  - 两者结合，共同提升长视频生成的上下文一致性与可靠性。

## 3. 实验设计

- 当前可获取的摘要和元数据**未提供具体实验设计细节**。
- 因此以下内容无法确认：
  - 使用了哪些数据集或场景；
  - benchmark 是什么；
  - 对比了哪些基线方法；
  - 使用了哪些评价指标，如时间一致性、FVD、PSNR、SSIM、用户研究等。
- 可获取信息仅表明：论文声称实现**分钟级时间一致性**，并保持**线性复杂度**。这些属于结果性描述，但缺少实验设置支撑。

## 4. 资源与算力

- 摘要和元数据中**未提及**以下信息：
  - GPU 型号与数量；
  - 训练时长；
  - 显存占用；
  - 模型参数量；
  - 训练数据规模；
  - 推理速度或实际部署成本。
- 因此无法总结该论文的算力资源使用情况。

## 5. 实验数量与充分性

- 当前文本**未列出实验组数**，也未说明是否包含：
  - 不同数据集上的主实验；
  - 消融实验；
  - 与不同基线方法的对比；
  - 长视频长度扩展实验；
  - 人工评价或用户研究。
- 因此无法判断实验是否充分、客观、公平。
- 仅从摘要看，论文给出了较强的结论性声称，但这些声称需要正文中的定量结果、消融分析和统计比较来支撑。

## 6. 论文的主要结论与发现

- MemoryPack 与 Direct Forcing 结合后，可显著增强长视频生成的**上下文一致性与可靠性**。
- MemoryPack 通过文本与图像全局引导和可学习上下文检索，能够联合建模短期与长期依赖，实现**分钟级时间一致性**。
- 该设计在视频长度增加时仍保持**线性复杂度**，具备较好的可扩展性。
- Direct Forcing 通过单步近似改善训练—推理对齐，有助于抑制推理阶段的误差传播。
- 总体而言，论文为长视频生成中的帧间连贯性与误差控制提供了一种可扩展方法，并推进了自回归视频模型的实用可用性。

## 7. 优点

- **问题定位清晰**：将长视频自回归生成的核心困难拆解为长程依赖与误差累积两个维度，并分别设计对应方法。
- **方法设计有针对性**：
  - MemoryPack 强调可学习检索与文本/图像全局引导，兼顾短期和长期依赖；
  - Direct Forcing 针对训练—推理不一致导致的误差传播，思路直接。
- **效率意识较强**：强调线性复杂度，说明作者关注长视频生成的可扩展性，而非只追求短片段质量。
- **潜在实用价值**：若摘要结论成立，分钟级时间一致性和线性复杂度对长视频生成应用具有吸引力。
- 元数据中该论文评审分数为 7.0，说明在 ICLR-2026 公开评审中获得一定认可，但最终判断仍需正文实验支撑。

## 8. 不足与局限

- **信息不完整导致无法验证**：由于 PDF 正文不可获取，无法核实数据集、baseline、指标、消融和统计显著性。
- **实验覆盖未知**：不清楚是否覆盖多种视频领域、不同长度、不同分辨率和不同运动复杂度场景。
- **潜在偏差风险**：当前总结主要依赖摘要和元数据，可能存在选择性报告或结论过度概括的风险。
- **方法潜在局限**：
  - MemoryPack 依赖文本和图像全局引导，若条件信息不足或噪声较大，检索质量可能受影响；
  - Direct Forcing 作为单步近似策略，是否会在生成质量、多样性或细节保真度上带来折衷，尚需实验验证；
  - 线性复杂度虽好，但实际常数、显存占用和推理速度未说明。
- **应用限制未知**：长视频生成通常计算成本高，论文未在可获取文本中讨论实时性、部署成本、长视频极端长度下的稳定性等问题。
- **复现材料未知**：项目网站为匿名链接，代码、模型和训练细节是否公开无法确认。

（完）
