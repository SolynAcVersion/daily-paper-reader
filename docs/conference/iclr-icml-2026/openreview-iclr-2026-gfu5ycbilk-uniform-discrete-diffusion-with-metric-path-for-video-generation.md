---
title: Uniform Discrete Diffusion with Metric Path for Video Generation
title_zh: 面向视频生成的度量路径均匀离散扩散
authors: "Haoge Deng, Ting Pan, Fan Zhang, Yang Liu, Zhuoyan Luo, Yufeng Cui, Wenxuan Wang, Chunhua Shen, Shiguang Shan, Zhaoxiang Zhang, Xinlong Wang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=GFU5yCbILk"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 面向可扩展长视频生成的离散扩散框架
tldr: 连续空间视频生成进展迅速，而离散方法因误差累积与长上下文不一致而落后。本文重新审视离散生成建模，提出带度量路径的均匀离散扩散框架URSA，将视频生成建模为离散时空令牌的迭代全局精炼，并引入线性化度量路径与分辨率相关时间步偏移两个设计。该框架可高效扩展到高分辨率图像合成与长时长视频生成，显著缩小了与连续方法的差距。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 离散视频生成因误差累积与长上下文不一致而落后于连续方法。
method: 提出URSA框架，用线性化度量路径与分辨率相关时间步偏移对离散时空令牌迭代精炼。
result: 可高效扩展到高分辨率与长时长视频生成，缩小与连续方法的差距。
conclusion: 为可扩展离散视频生成提供了简洁而有力的新范式。
---

## Abstract
Continuous-space video generation has advanced rapidly, while discrete approaches lag behind due to error accumulation and long-context inconsistency. In this work, we revisit discrete generative modeling and present Uniform discRete diffuSion with metric pAth (URSA), a simple yet powerful framework that bridges the gap with continuous approaches for the scalable video generation. At its core, URSA formulates the video generation task as an iterative global refinement of discrete spatiotemporal tokens. It integrates two key designs: a Linearized Metric Path and a Resolution-dependent Timestep Shifting mechanism. These designs enable URSA to scale efficiently to high-resolution image synthesis and long-duration video generation, while requiring significantly fewer inference steps. Additionally, we introduce an asynchronous temporal fine-tuning strategy that unifies versatile tasks within a single model, including interpolation and image-to-video generation. Extensive experiments on challenging video and image generation benchmarks demonstrate that URSA consistently outperforms existing discrete methods and achieves performance comparable to state-of-the-art continuous diffusion methods. Code and models are available at https://github.com/baaivision/URSA.

---

## 论文详细总结（自动生成）

# 论文总结：Uniform Discrete Diffusion with Metric Path for Video Generation（URSA）

> **信息可得性说明**：目标 PDF 链接返回 503，正文提取结果为“no healthy upstream”。因此以下总结主要依据论文标题、摘要和 Markdown 元数据；正文中的公式、实验表格、数据集细节、算力配置等无法确认，相关部分将明确标注为“未说明”或“无法判断”。

## 1. 核心问题与整体含义
- **研究背景**：连续空间视频生成进展迅速，而离散生成方法明显落后。
- **核心问题**：离散视频生成存在两大瓶颈：
  - 误差累积；
  - 长上下文不一致。
- **整体含义**：论文重新审视离散生成建模，提出 **URSA**（Uniform discRete diffuSion with metric pAth），试图缩小离散方法与连续方法在可扩展视频生成上的差距。
- **定位**：ICLR 2026 接收论文，评审分数为 7.0，属于视频生成与离散扩散交叉方向的工作。

## 2. 方法论
- **核心思想**：将视频生成建模为对 **离散时空令牌** 的 **迭代全局精炼**，而不是一次性生成或局部修补。
- **框架名称**：URSA，即“带度量路径的均匀离散扩散”。
- **两个关键设计**：
  - **Linearized Metric Path / 线性化度量路径**：用于构建离散扩散过程中的度量路径，改善离散生成中的误差累积与一致性问题。
  - **Resolution-dependent Timestep Shifting / 分辨率相关时间步偏移**：根据分辨率调整时间步，使模型能高效扩展到高分辨率图像合成与长时长视频生成。
- **推理效率**：摘要声称该设计使 URSA 需要显著更少的推理步数。
- **异步时间微调策略**：引入 asynchronous temporal fine-tuning，将多种任务统一到单一模型中，包括：
  - 视频插值；
  - 图像到视频生成。
- **算法流程的文字描述**：从离散时空令牌出发，通过带度量路径的均匀离散扩散过程进行迭代全局精炼；在时间维度和分辨率维度上采用特定调度与微调策略，最终统一支持视频生成、图像合成和条件生成任务。
- **未说明部分**：具体损失函数、扩散转移公式、时间步调度公式、网络结构等未在可得内容中给出。

## 3. 实验设计
- **实验场景**：摘要称在“挑战性视频和图像生成基准”上进行实验。
- **任务覆盖**：
  - 高分辨率图像合成；
  - 长时长视频生成；
  - 视频插值；
  - 图像到视频生成。
- **对比方法**：
  - 现有离散生成方法；
  - 当前最先进的连续扩散方法。
- **主要实验结果**：URSA 持续优于现有离散方法，并达到与 SOTA 连续扩散方法相当的性能。
- **未说明部分**：具体数据集名称、benchmark 名称、评价指标、对比方法列表、实验设置等均未提供，无法进一步核实。

## 4. 资源与算力
- 摘要与元数据中 **未提及** GPU 型号、GPU 数量、训练时长、参数量、训练数据规模等算力信息。
- 因此无法总结其资源消耗，也无法判断其训练成本是否具有实际可扩展性。
- 论文提供了代码与模型链接：`https://github.com/baaivision/URSA`，但当前未验证其可用性。

## 5. 实验数量与充分性
- 摘要声称进行了 “Extensive experiments”，但未给出具体实验组数。
- 从可得信息看，实验至少覆盖：
  - 视频生成；
  - 图像生成；
  - 插值；
  - 图像到视频。
- 但以下内容无法判断：
  - 使用了多少个数据集；
  - 做了多少组消融实验；
  - 是否比较了推理步数、计算成本、长视频一致性等关键指标；
  - 对比是否在相同数据、相同算力、相同推理预算下进行。
- **公平性评估**：由于正文不可得，无法确认对比是否完全公平。开源代码和模型有助于复现，但仅凭摘要不能判断实验的客观性与充分性。

## 6. 主要结论与发现
- URSA 能显著缩小离散视频生成与连续视频生成之间的差距。
- 线性化度量路径与分辨率相关时间步偏移，使模型可高效扩展到高分辨率图像和长时长视频。
- 异步时间微调策略可将插值、图像到视频等任务统一在一个模型中。
- 在挑战性视频和图像生成基准上，URSA 优于现有离散方法，并达到与 SOTA 连续扩散方法可比的性能。
- 论文将自身定位为“可扩展离散视频生成的简洁而有力的新范式”。

## 7. 优点
- **问题选择有价值**：针对离散视频生成中的误差累积与长上下文不一致，切入明确。
- **方法设计简洁**：以线性化度量路径和分辨率相关时间步偏移为核心，目标直接。
- **可扩展性**：同时面向高分辨率图像与长时长视频，强调推理步数更少。
- **任务统一**：通过异步时间微调统一插值、图像到视频等任务，减少多模型需求。
- **开源可复现**：提供代码与模型链接，有利于后续验证。
- **学术认可**：ICLR 2026 接收，评审分数 7.0。

## 8. 不足与局限
- **信息不完整**：PDF 正文未能获取，无法验证方法公式、实验细节和算力配置。
- **实验覆盖未知**：具体数据集、benchmark、指标、消融实验数量均未说明，难以判断实验充分性。
- **公平性待确认**：与连续扩散方法的比较是否在相同推理步数、相同算力、相同数据条件下进行，无法判断。
- **量化结论不足**：摘要只给出“优于离散方法、与 SOTA 连续方法相当”的定性结论，缺少具体提升幅度。
- **长上下文一致性**：虽然动机提到该问题，但是否彻底解决、提升多少，未在可得内容中量化。
- **应用限制**：视频生成的显存、计算成本、长视频稳定性和离散令牌表达能力等潜在限制，需正文进一步确认。
- **偏差风险**：仅凭摘要可能只呈现成功结果；是否存在失败案例、负结果或选择性报告，无法评估。

（完）
