---
title: "MotionStream: Real-Time Video Generation with Interactive Motion Controls"
title_zh: MotionStream：带交互式运动控制的实时视频生成
authors: "Joonghyuk Shin, Zhengqi Li, Richard Zhang, Jun-Yan Zhu, Jaesik Park, Eli Shechtman, Xun Huang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=v1DKz5Vxr7"
tags: ["query:video-gen-rl"]
score: 6.0
evidence: 实时运动控制视频生成
tldr: 当前运动条件视频生成方法存在数分钟级的高延迟与非因果处理，无法支持实时交互。本文提出MotionStream，在单GPU上实现亚秒级延迟、最高29FPS的流式生成。方法先用运动控制增强文本到视频模型，生成符合全局文本与局部运动引导的高质量视频，再通过自强制与分布匹配蒸馏将双向教师模型蒸馏为因果学生模型，支持长时甚至无限时长的实时流式推理。该工作推动了交互式视频生成走向实时实用。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有运动条件视频生成延迟高且非因果处理，无法支持实时交互。
method: 提出MotionStream，先用运动控制增强文本到视频模型，再通过自强制与分布匹配蒸馏将其蒸馏为因果学生。
result: 单GPU上实现亚秒级延迟、最高29FPS的流式生成，支持长时甚至无限时长推理。
conclusion: 推动交互式视频生成走向实时实用。
---

## Abstract
Current motion-conditioned video generation methods suffer from prohibitive latency (minutes per video) and non-causal processing that prevents real-time interaction. We present MotionStream, enabling sub-second latency with up to 29 FPS streaming generation on a single GPU. Our approach begins by augmenting a text-to-video model with motion control, which generates high-quality videos that adhere to the global text prompt and local motion guidance, but does not perform inference on the fly. As such, we distill this bidirectional teacher into a causal student through Self Forcing with Distribution Matching Distillation, enabling real-time streaming inference. Several key challenges arise when generating videos of long, potentially infinite time-horizons -- (1) bridging the domain gap from training on finite length and extrapolating to infinite horizons, (2) sustaining high quality by preventing error accumulation, and (3) maintaining fast inference, without incurring growth in computational cost due to increasing context windows. A key to our approach is introducing carefully designed sliding-window causal attention, combined with attention sinks. By incorporating self-rollout with attention sinks and KV cache rolling during training, we properly simulate inference-time extrapolations with a fixed context window, enabling constant-speed generation of arbitrarily long videos. Our models achieve state-of-the-art results in motion following and video quality while being two orders of magnitude faster, uniquely enabling infinite-length streaming. With MotionStream, users can paint trajectories, control cameras, or transfer motion, and see results unfold in real-time, delivering a truly interactive experience.

---

## 论文详细总结（自动生成）

> 说明：当前可获取的 PDF 文本仅包含标题、作者、元数据与 Abstract，正文链接返回 503（no healthy upstream）。因此以下总结主要依据摘要与元数据；涉及数据集、算力、实验组数、消融等正文细节无法核验，将明确标注为“未说明”。

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：现有“运动条件视频生成”方法通常延迟极高，生成一段视频需要数分钟，并且采用非因果处理，即模型需要访问未来帧或完整序列，难以支持实时交互。
- **研究背景**：文本到视频生成已取得进展，但要让用户通过轨迹、相机控制、运动迁移等方式实时操控视频生成，仍面临速度、因果性和长时稳定性的三重挑战。
- **整体含义**：MotionStream 试图把运动控制视频生成推进到“实时、流式、可交互”的实用阶段。其目标是单 GPU 上实现亚秒级延迟、最高 29 FPS 的流式生成，并支持长时甚至无限时长的视频推理。

## 2. 方法论

- **核心思想**：采用两阶段策略。先构建一个高质量但非实时的“双向教师模型”，再将其蒸馏为可实时流式推理的“因果学生模型”。
- **阶段一：运动控制增强文本到视频模型**
  - 在文本到视频模型基础上加入运动控制能力。
  - 生成的视频需同时满足全局文本提示和局部运动引导。
  - 该教师模型质量高，但不能在推理时实时运行。
- **阶段二：蒸馏为因果学生模型**
  - 通过 **Self Forcing** 与 **Distribution Matching Distillation（分布匹配蒸馏）**，将双向教师蒸馏为因果学生。
  - 因果学生只依赖过去和当前信息，适合流式生成。
- **长时/无限时域生成的关键技术**
  - 使用精心设计的 **滑动窗口因果注意力（sliding-window causal attention）**。
  - 结合 **注意力汇（attention sinks）**，缓解长时外推中的稳定性问题。
  - 训练时引入 **self-rollout with attention sinks** 与 **KV cache rolling**，模拟推理时的外推行为。
  - 通过固定上下文窗口，使生成任意长视频时计算成本不随上下文增长，从而实现恒定速度生成。
- **算法流程文字说明**
  1. 训练一个具备运动控制能力的双向文本到视频教师模型。
  2. 设计因果学生模型，采用滑动窗口因果注意力和注意力汇。
  3. 在训练中让学生模型自回归 rollout，并滚动 KV 缓存，模拟推理时的长时外推。
  4. 使用 Self Forcing 和分布匹配蒸馏，让学生匹配教师分布。
  5. 推理时以固定上下文窗口流式生成，支持实时交互和无限长度。

## 3. 实验设计

- **数据集 / 场景**：未说明。摘要未列出具体训练或评测数据集。
- **Benchmark**：摘要仅声称在 **运动跟随（motion following）** 和 **视频质量（video quality）** 上达到 state-of-the-art。
- **对比方法**：未列出具体基线名称、数量或指标。
- **应用场景**：用户可绘制轨迹、控制相机、进行运动迁移，并实时看到生成结果。
- **速度指标**：单 GPU 上亚秒级延迟，最高 29 FPS 流式生成，比现有方法快“两个数量级”。

## 4. 资源与算力

- **推理资源**：摘要提到“单 GPU”上实现亚秒级延迟和最高 29 FPS 流式生成。
- **GPU 型号 / 数量**：未说明。
- **训练算力**：未说明训练使用的 GPU 型号、数量、训练时长、显存或总计算量。
- **其他资源**：未说明数据集规模、蒸馏训练成本、教师模型规模等。

## 5. 实验数量与充分性

- **实验组数**：无法从给定内容判断。摘要未提供数据集数量、基线数量、消融实验数量或用户研究数量。
- **充分性**：无法评估。仅从摘要看，作者声称在运动跟随和视频质量上达到 SOTA，并快两个数量级，但缺少定量表格、指标定义和实验设置。
- **客观性与公平性**：无法核验。由于未列出对比方法、评测协议、硬件条件和延迟测量方式，公平性无法判断。
- **可能存在的评估风险**：若“29 FPS”“亚秒级延迟”未说明分辨率、视频长度、批大小和 GPU 型号，则跨方法比较可能不充分。

## 6. 主要结论与发现

- MotionStream 可在单 GPU 上实现实时、流式的运动控制视频生成。
- 延迟达到亚秒级，最高 29 FPS。
- 通过将双向教师蒸馏为因果学生，支持长时甚至无限时长视频生成。
- 借助滑动窗口因果注意力、注意力汇、self-rollout 和 KV cache rolling，可在固定上下文窗口下保持恒定速度。
- 作者声称该方法在运动跟随和视频质量上达到 SOTA，同时比现有方法快两个数量级。
- 支持用户交互式绘制轨迹、控制相机和迁移运动，并实时看到结果。

## 7. 优点

- **问题重要且实用**：把运动控制视频生成从离线高延迟推向实时交互。
- **方法设计清晰**：先高质量教师，再蒸馏为因果学生，兼顾质量与速度。
- **长时生成机制有针对性**：滑动窗口因果注意力、注意力汇和 KV 缓存滚动共同应对无限时域外推、误差累积和计算增长。
- **训练模拟推理**：通过 self-rollout 和 KV cache rolling 缩小训练与推理外推之间的差距。
- **应用直观**：轨迹、相机、运动迁移等控制方式适合实时创意工具和交互式内容生成。
- **性能宣称突出**：两个数量级加速、29 FPS、亚秒延迟、单 GPU，若成立则实用价值较高。

## 8. 不足与局限

- **信息可得性不足**：当前仅有摘要，正文 PDF 不可用，无法核验方法细节、公式、实验和结论。
- **实验细节缺失**：未提供数据集、benchmark 细节、对比基线、评价指标、消融实验和用户研究。
- **算力信息缺失**：未说明训练 GPU 型号、数量、时长和成本；单 GPU 仅指推理。
- **性能条件不明确**：29 FPS、亚秒延迟未说明分辨率、帧数、批大小、GPU 型号和测量环境。
- **长时稳定性仍需验证**：虽然提出注意力汇和 KV 缓存滚动，但无限长生成中的误差累积、内容漂移和运动一致性是否完全解决，摘要未给出证据。
- **公平性风险**：若基线未在相同硬件和设置下测量，速度优势的公平性无法判断。
- **应用限制**：实时交互可能受分辨率、控制精度、教师模型能力和蒸馏损失影响；运动迁移、相机控制等场景的泛化性未说明。
- **潜在偏差**：仅凭摘要中的 SOTA 和加速声明，可能存在选择性报告或评测范围有限的风险。

（完）
