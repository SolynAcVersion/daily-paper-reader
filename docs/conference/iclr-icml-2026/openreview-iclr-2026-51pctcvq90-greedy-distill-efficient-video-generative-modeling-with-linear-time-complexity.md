---
title: "Greedy Distill: Efficient Video Generative Modeling with Linear Time Complexity"
title_zh: 贪婪蒸馏：线性时间复杂度的高效视频生成建模
authors: "Dingcheng Zhen, Qian Qiao, Tan Yu, Ruixin Zhang, Yutian Yan, Siyuan Liu, Shunshun Yin, Ming Tao, Xu Zheng"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=51pcTCVQ90"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 视频生成的局部帧间时序依赖
tldr: 由于双向注意力依赖，视频生成模型面临O(n^2)计算复杂度。本文发现局部帧间信息冗余现象，表明视频生成中存在强局部时序依赖，而对远距离帧的全局注意力贡献甚微。据此提出GREEDY DISTILL蒸馏训练范式，并设计流式扩散解码器（SDD），仅利用第0帧与最后一帧生成下一帧，避免冗余计算，实现线性时间复杂度的高效视频生成。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 双向注意力依赖使视频生成模型面临O(n^2)计算复杂度，效率低下。
method: 发现局部帧间信息冗余现象，提出GREEDY DISTILL蒸馏范式与流式扩散解码器SDD。
result: 仅用首尾帧即可生成下一帧，避免冗余计算，实现线性时间复杂度。
conclusion: 揭示了视频生成的强局部时序依赖，为高效视频生成提供新路径。
---

## Abstract
Due to bidirectional attention dependencies, video generation models generally suffer from $O(n^2)$ computational complexity. In this work, we find the “local inter-frame information redundancy" phenomenon which indicates strong local temporal dependencies in video generation, with global attention to distant frames contributing only marginally. Built upon this finding, we introduce a novel distillation training paradigm for video diffusion models, namely GREEDY DISTILL. 
Specifically, to generate the next frame using only the 0-th and the last frames, we propose the Streaming Diffusion Decoder (SDD) as the “Greedy Decoder" to avoid redundant computational costs from the other frames. 
Meanwhile, to our knowledge, we introduce Efficient Temporal Module (ETM) to capture the global temporal information across frames.
These two modules achieve the computational complexity reduction from $O(n^2)$ to linear. Moreover, we make the first attempt to apply RL fine-tuning to address the error accumulation during streaming generation.
Our method achieves an overall score of 84.60 on the VBench benchmark, surpassing previous state-of-the-art methods by large margins(+4.18%). Qualitative results also demonstrate superior performance. 
Leveraging its efficient model structure and KV cache, it is able to rapidly generate high-quality video streams at 24 FPS (nearly 50% faster) on a single H100 GPU.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 正文提取失败（503，no healthy upstream），以下总结主要依据论文摘要与元数据；未在摘要中出现的训练细节、数据集细节和消融实验无法确认。

## 1. 核心问题与整体含义
- **研究动机**：视频生成模型通常依赖双向注意力，导致计算复杂度随帧数增长呈 \(O(n^2)\)，长视频生成效率低、成本高。
- **关键观察**：作者发现“局部帧间信息冗余”现象，即视频生成中存在强局部时序依赖，而对远距离帧的全局注意力贡献很小。
- **整体含义**：若远距离全局注意力可被大幅压缩，则视频生成可转向更高效的流式/自回归式生成，实现线性时间复杂度，同时保持生成质量。

## 2. 方法论：核心思想与关键技术
- **核心思想**：基于局部时序依赖，提出蒸馏训练范式 **GREEDY DISTILL**，将原本依赖全帧双向注意力的视频扩散模型，蒸馏为只需局部条件即可逐帧生成的模型。
- **Streaming Diffusion Decoder（SDD）**：
  - 作为“Greedy Decoder”，生成下一帧时仅使用第 0 帧和当前最后一帧作为条件。
  - 避免对其余历史帧进行冗余计算，从而降低计算开销。
- **Efficient Temporal Module（ETM）**：
  - 作者声称引入 ETM 来捕获跨帧的全局时序信息。
  - 在局部贪心生成的同时，补偿可能丢失的全局时序依赖。
- **复杂度降低**：
  - 通过 SDD 与 ETM 的组合，将计算复杂度从 \(O(n^2)\) 降至线性复杂度。
- **RL 微调**：
  - 作者称首次尝试将强化学习微调用于流式视频生成，以缓解逐帧生成中的误差累积问题。
- **推理加速**：
  - 结合高效模型结构与 KV cache，实现快速视频流生成。

## 3. 实验设计
- **Benchmark**：使用 **VBench** 评估视频生成质量。
- **主要结果**：
  - VBench 总体得分为 **84.60**。
  - 相比此前 state-of-the-art 方法提升 **+4.18%**。
- **定性结果**：摘要称定性结果也展示出优越性能。
- **效率评估**：
  - 在单张 **H100 GPU** 上生成高质量视频流，速度达 **24 FPS**，比此前方法快近 **50%**。
- **对比方法**：
  - 摘要仅说明对比“previous state-of-the-art methods”，未列出具体方法名称。
- **数据集/场景**：
  - 摘要未说明训练数据集、测试集构成或具体视频生成场景。

## 4. 资源与算力
- **推理资源**：明确提到单张 **H100 GPU**，达到 **24 FPS**，并称比之前方法快近 50%。
- **训练资源**：摘要未提及训练使用的 GPU 型号、数量、训练时长、参数量或总计算量。
- **KV cache**：提到利用 KV cache 加速流式生成，但未给出缓存大小、显存占用等细节。

## 5. 实验数量与充分性
- **可确认实验**：
  - VBench 总体定量评估。
  - 定性结果展示。
  - 单 H100 推理效率评估。
- **未确认信息**：
  - 不同数据集或场景下的实验数量。
  - 消融实验数量及具体设置。
  - 与哪些具体基线方法对比。
  - 训练稳定性、误差累积、长视频一致性等专项实验。
- **充分性与公平性判断**：
  - VBench 是视频生成领域常用 benchmark，具备一定客观性。
  - 但仅凭摘要无法判断实验是否充分、对比是否公平，也无法确认是否覆盖长视频、复杂运动、多对象交互等困难场景。

## 6. 主要结论与发现
- 视频生成中存在强局部时序依赖，远距离帧的全局注意力贡献有限。
- 基于该发现，GREEDY DISTILL、SDD 与 ETM 可将视频生成复杂度从 \(O(n^2)\) 降至线性。
- 仅用第 0 帧与最后一帧即可生成下一帧，避免大量冗余计算。
- RL 微调可被用于缓解流式生成中的误差累积。
- 方法在 VBench 上达到 84.60，超过此前 SOTA 约 4.18%，并在单 H100 上实现 24 FPS 的高效视频流生成。

## 7. 优点
- **问题重要**：针对视频生成中 \(O(n^2)\) 注意力瓶颈，具有明确效率和实际部署价值。
- **观察新颖**：提出“局部帧间信息冗余”现象，为高效视频生成提供经验依据。
- **方法组合清晰**：SDD 负责贪心流式解码，ETM 补偿全局时序，KV cache 加速推理。
- **引入 RL 微调**：尝试解决流式生成误差累积，这是视频生成中较有价值的方向。
- **性能与效率兼顾**：VBench 提升明显，同时单 H100 达到 24 FPS，近 50% 加速。
- **面向流式生成**：适合实时或长视频流式生成场景。

## 8. 不足与局限
- **正文信息缺失**：当前 PDF 提取失败，只有摘要和元数据，无法验证方法细节与实验完整性。
- **训练算力未说明**：未报告训练 GPU 数量、时长、数据规模，难以评估总成本与可复现性。
- **实验覆盖有限**：摘要仅提及 VBench 总分、定性和推理效率，缺少消融、长视频、泛化性等实验。
- **对比方法不明确**：未列出具体 SOTA 方法，公平性需正文确认。
- **局部贪心假设风险**：若某些场景依赖长程时序一致性，仅保留第 0 帧和最后一帧可能导致信息丢失或误差累积。
- **RL 微调细节未知**：奖励设计、稳定性、训练开销等未说明。
- **应用限制**：流式生成可能更适合局部连续性强的视频，对复杂叙事、大幅场景切换等任务仍需验证。
- **元数据提示**：来源标记为 ICLR-2026-Rejected-Public，评审分 7.0，说明论文可能尚未正式接收，方法价值与争议需结合全文判断。

（完）
