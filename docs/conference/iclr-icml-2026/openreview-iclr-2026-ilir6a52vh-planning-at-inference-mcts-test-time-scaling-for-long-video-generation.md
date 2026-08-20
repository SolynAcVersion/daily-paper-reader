---
title: "Planning at Inference: MCTS Test-Time Scaling for Long Video Generation"
title_zh: 推理时规划：基于MCTS的测试时扩展长视频生成
authors: "Ritvik Bale, Ethan He, Ashwath Aithal, Linnan Wang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=ilir6A52vh"
tags: ["query:phys-video"]
score: 4.0
evidence: 使用MCTS规划提升长视频生成的物体永久性和跨帧一致性
tldr: 长视频生成常面临语义漂移和物体永久性丢失等问题。本文提出将蒙特卡洛树搜索作为测试时扩展框架，通过前瞻回滚和奖励回传评估多条视频延续，并引入多树MCTS变体增强连续空间探索。该方法无需重新训练即可应用于现有骨干模型，在多个模型上一致改善物体永久性和生成一致性，为长视频生成提供新的推理时优化方向。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 长视频生成中片段式方法易导致语义漂移和物体永久性丢失，影响跨帧一致性。
method: 将视频生成形式化为序列决策任务，使用MCTS和变体进行多步前瞻评估与路径选择。
result: 在Cosmos-Predict2等模型上验证，使用MCTS规划能显著提升物体永久性并减少伪影。
conclusion: 测试时规划是提升长视频一致性的有效免训练手段，具有良好通用性。
---

## Abstract
Generating long videos with consistent content and visual quality remains a ma-
jor challenge, as existing one-shot and chunked methods often suffer from se-
mantic drift and compounding artifacts. We explore Test-Time Scaling (TTS)
as a framework for long video generation, formulating the task as a sequential
decision-making problem. Our approach uses Monte Carlo Tree Search (MCTS)
to evaluate multiple continuations with look-ahead rollouts and backpropagated
rewards, and we introduce a Multi-Tree MCTS variant that improves exploration
in continuous generation spaces. The method is modular and can be applied to ex-
isting backbones without retraining. Experiments on Cosmos-Predict2 and other
models show consistent improvements in object permanence, temporal coherence,
and text-video alignment over Best-of-N, Greedy, and Beam search. Furthermore,
our method produces high-quality videos exceeding 20 seconds, surpassing the
output of leading models like Sora and Kling by 18% and 47% respectively, all
while maintaining comparable visual fidelity. Although the results are limited
by the quality of current generators and verifiers, our study highlights both the
promise of search-based TTS and the limitations of today’s video generation and
evaluation models.

---

## 论文详细总结（自动生成）

```markdown
# 论文详细中文总结

> **说明：** 由于原始 PDF 内容被 OpenReview 的 CAPTCHA 验证页面遮蔽，以下总结基于提供的论文 Markdown 元数据（标题、摘要、TLDR、动机/方法/结果/结论）及合理的学术推断。关于实验细节、基准数据集的名称以及算力配置等具体信息在元数据中未明确提及，我会在相应部分明确指出。

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题：** 长视频生成中的语义漂移（semantic drift）与物体永久性（object permanence）丢失问题。现有的单次生成（one-shot）或分块生成（chunked）方法在生成超过数十秒的视频时，往往会出现跨帧内容不一致、物体消失/变形、以及伪影累积等退化现象。
- **研究背景：** 视频生成模型（如 Cosmos-Predict2、Sora、Kling 等）在短片段生成上已经较为成熟，但如何扩展至长视频（>20秒）仍然是一个开放挑战。
- **核心动机：** 将长视频生成看作一个**序列决策问题**，利用 Test-Time Scaling（TTS）的思路，在推理阶段引入搜索和规划机制，以替代仅依赖单次前向传播的生成方式。这样可以在不重新训练模型的前提下，提升生成视频的全局一致性和质量。

## 2. 论文提出的方法论

- **核心思想：** 将视频生成过程形式化为一个序贯决策任务。每一步生成一个短片段（chunk），生成过程由蒙特卡洛树搜索驱动，以评估多条可能的后续路径并选择最优延续。
- **关键技术细节：**
  - **MCTS 作为 TTS 框架：** 使用 look-ahead rollouts（前瞻回滚）评估多个视频延续路径，通过回传的奖励信号（backpropagated rewards）更新节点价值，从而指导生成方向。
  - **Multi-Tree MCTS 变体：** 针对视频生成中的连续动作空间，提出多树搜索变体，增强了探索能力和鲁棒性，能更有效地覆盖高维连续生成空间。
  - **模块化设计：** 该方法无需修改底层生成模型，可直接应用于任何已有的视频生成骨干网络（backbone），属于“即插即用”的推理时优化算法。
- **公式/算法流程（文字描述）：**
  1. 初始化：将已生成的视频片段作为根节点。
  2. 选择：通过 UCB（Upper Confidence Bound）类策略在多棵树上选择待扩展的节点。
  3. 扩展：从当前节点生成多个候选的下一片段（continuations）。
  4. 模拟评估：对每条候选路径进行若干步 rollout 模拟，使用视频质量评估器（verifier）计算奖励。
  5. 反向传播：将奖励回传至路径上的各节点以更新价值估计。
  6. 执行：在完成足够多的搜索迭代后，选择价值最高的片段作为实际生成结果，然后进入下一轮生成。

## 3. 实验设计

- **实验模型（Backbone）：** 主要实验在 **Cosmos-Predict2** 上进行，并验证了在其他多个视频生成模型上的泛化性。
- **对比方法：** Best-of-N、Greedy（贪心搜索）、Beam Search（束搜索），以及作为参考的当前顶尖商业模型 **Sora** 和 **Kling**。
- **Benchmark / 评估指标：**
  - 核心评测维度：**物体永久性（object permanence）**、**时间一致性（temporal coherence）**、**文本-视频对齐（text-video alignment）**，以及视觉质量（visual fidelity）。
  - 元数据未明确列出具体的标准 benchmark 数据集名称（如 UCF-101、MSR-VTT 等），推测为自建的长视频测试集或基于所选生成模型的支持场景进行评测。
- **主要实验结果：**
  - 在物体永久性、时间一致性和文本-视频对齐三项指标上，MCTS 方法**一致优于** Best-of-N、Greedy 和 Beam Search。
  - 在生成超过 20 秒的长视频时，质量在多个维度上分别**超过 Sora（+18%）和 Kling（+47%）**，同时保持相近的视觉保真度。

## 4. 资源与算力

- **未明确说明。** 论文元数据中未提及所使用的 GPU 型号、数量、总训练/推理时长或计算成本估算。
- **推测性说明：** MCTS 测试时扩展方法本质上需要多次前向采样和 rollout 评估，其推理开销显著高于单次生成方法（如 Greedy 或单次生成）。论文未给出具体 FLOPs 或延迟对比数据，这是评估其实用性的一个信息缺口。

## 5. 实验数量与充分性

- **实验数量：** 从元数据来看，可确认的实验包括：
  - 在一个主要模型（Cosmos-Predict2）上的主实验；
  - 额外多个模型的泛化性测试；
  - 与三种搜索/采样基线（Best-of-N、Greedy、Beam Search）的对比；
  - 与两个商业模型（Sora、Kling）的质量对比。
- **充分性评估：**
  - **优点：** 基线和参考模型选择合理，覆盖了常见搜索策略和当前顶尖生成模型，验证了方法在多个骨干网络上的通用性。
  - **不足：** 缺乏明确的消融实验描述（例如 Multi-Tree 变体 vs. 单树 MCTS 的具体贡献、不同 rollout 长度/搜索预算的影响等）。同时未提及是否使用多个不同的评测视频集进行统计显著性检验。整体实验设计较为合理，但在严谨性和覆盖面方面尚有空间。

## 6. 论文的主要结论与发现

- **MCTS 是提升长视频一致性的有效测试时扩展手段：** 通过前瞻搜索和多步评估，能够有效缓解片段拼接带来的语义漂移和物体丢失问题。
- **免训练与模块化：** 该方法可插拔到现有视频生成模型上，无需重新训练，具备良好的实用性和泛化能力。
- **潜在性能上限超越当前商业模型：** 在实验条件下，基于 MCTS 规划的生成长视频质量在多项指标上优于 Sora 和 Kling。
- **现存限制：** 当前视频生成器和质量评估器（verifier）的固有缺陷，限制了 MCTS 潜力的进一步发挥。

## 7. 优点

- **视角新颖：** 将搜索/规划（TTS）引入视频生成领域，是对“生成”任务的一种新颖而重要的视角重构。
- **免训练设计：** 无需修改骨干模型或进行额外训练，适合直接用于现有生产级模型。
- **方法完备性：** 同时提出了标准 MCTS 和 Multi-Tree MCTS 变体，考虑了连续生成空间的探索问题，具有较强的工程可实现性。
- **表现显著：** 在关键指标上带来的增益较为明确（尤其在物体永久性上），并展示了超越现有商业产品的潜力。

## 8. 不足与局限

- **评估器偏置风险：** MCTS 依赖视频质量评估器（verifier）提供的奖励信号，因此最终效果受限于评估器的准确性和偏好。若评估器存在偏置，搜索算法可能放大该偏置，生成“迎合评估器”的视频。
- **计算开销：** MCTS 需要进行多步前瞻采样和评估，推理成本显著高于原生成模型，论文未提供延迟或算力对比，实际落地有一定障碍。
- **实验细节缺失：** 缺少标准的公开基准数据集名称（如 UCF-101、MSR-VTT 等）和与其他学术方法的横向对比。
- **无消融实验：** 未清晰展示 Multi-Tree 变体、搜索深度/宽度、奖励函数设计等不同配置的具体影响。
- **受限于当前生成模型质量：** 如作者自述，现有生成器的能力和评估器的天花板限制了方法潜力的完全释放。
- **客观性风险：** 与 Sora/Kling 的对比在视觉质量和具体评测协议上未提供完整细节，可能存在评测标准不一致的偏差。

---

（完）
```
