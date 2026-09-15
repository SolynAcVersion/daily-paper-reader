---
title: "FAST-AR: Fast Autoregressive Video Diffusion and World Models with Temporal Cache Compression and Sparse Attention"
title_zh: FAST-AR：基于时序缓存压缩与稀疏注意力的快速自回归视频扩散与世界模型
authors: "Dvir Samuel, Issar Tzachor, Matan Levy, Michael Green, Gal Chechik, Rami Ben-Ari"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f93d6a0d6126da027b65cdcf692c09d9839ed00c.pdf"
tags: ["query:video-gen-rl"]
score: 7.0
evidence: 自回归视频扩散，通过时序缓存压缩提升长程一致性
tldr: 自回归视频扩散支持流式长视频生成，但推理时KV缓存不断增长导致延迟与显存开销上升，限制了可用时序上下文并损害长程一致性。本文分析其冗余来源，包括跨帧近重复键与缓慢演化的查询键等，并提出时序缓存压缩与稀疏注意力方法。实验表明该方法在降低推理成本的同时改善了长程一致性，推动了长视频与世界模型生成。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 自回归视频扩散推理时KV缓存增长，造成高延迟、高显存并损害长程一致性。
method: 识别冗余来源，提出时序缓存压缩与稀疏注意力以降低推理开销。
result: 在降低推理成本的同时改善长程一致性。
conclusion: 为高效长视频与世界模型生成提供了加速方案。
---

## Abstract
Autoregressive video diffusion models enable streaming generation, opening the door to long-form synthesis, video world models, and interactive neural game engines. However, their core attention layers become a major bottleneck at inference time: as generation progresses, the KV cache grows, causing both increasing latency and escalating GPU memory, which in turn restricts usable temporal context and harms long-range consistency. In this work, we study redundancy in autoregressive video diffusion and identify three persistent sources: near-duplicate cached keys across frames, slowly evolving (largely semantic) queries/keys that make many attention computations redundant, and cross-attention over long prompts where only a small subset of tokens matters per frame.
Building on these observations, we propose a unified, training-free attention framework (FAST-AR) for FAST-AutoRegressive diffusion, consisting of three components: TempCache compresses the KV cache via temporal correspondence to bound cache growth; AnnCA accelerates cross-attention by selecting frame-relevant prompt tokens using fast approximate nearest neighbor (ANN) matching; and AnnSA sparsifies self-attention by restricting each query to semantically matched keys, also using a lightweight ANN. Together, these modules reduce attention, compute, and memory and are compatible with existing autoregressive diffusion backbones and world models. Experiments demonstrate up to x5--x10 end-to-end speedups while preserving near-identical visual quality and, crucially, maintaining stable throughput and nearly constant peak GPU memory usage over long rollouts, where prior methods progressively slow down and suffer from increasing memory usage.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 正文抓取失败（仅返回 “no healthy upstream”），以下总结主要依据论文标题、摘要与元数据整理；材料未覆盖的信息均标注为“未说明”，避免臆测。

# FAST-AR 论文中文总结

## 1. 核心问题与整体含义
- **研究背景**：自回归视频扩散模型支持流式生成，可用于长视频合成、视频世界模型和交互式神经游戏引擎。
- **核心瓶颈**：推理时注意力层成为主要瓶颈。随着生成推进，KV 缓存不断增长，导致延迟升高、GPU 显存占用上升。
- **连锁影响**：缓存增长限制了可用时序上下文，进而损害长程一致性，使长视频生成和世界模型难以高效、稳定地扩展。
- **整体含义**：论文旨在通过分析自回归视频扩散中的注意力冗余，提出免训练的高效注意力框架，降低推理成本，同时保持视觉质量与长程稳定性。

## 2. 方法论：核心思想与关键技术
- **核心思想**：研究自回归视频扩散中的冗余，并识别出三类持续存在的冗余来源：
  1. 跨帧存在近重复的缓存键；
  2. 查询/键演化缓慢，很多注意力计算在语义上重复；
  3. 长提示跨注意力中，每帧只有少量 token 真正重要。
- **统一框架**：提出 **FAST-AR**，即 FAST-AutoRegressive diffusion，一个免训练、兼容现有自回归扩散骨干和世界模型的注意力加速框架。
- **三个组件**：
  - **TempCache**：通过时序对应关系压缩 KV 缓存，限制缓存随生成过程无界增长。
  - **AnnCA**：用于跨注意力加速，利用快速近似最近邻匹配选择与当前帧相关的提示 token，只对少量重要 token 做跨注意力。
  - **AnnSA**：用于自注意力稀疏化，将每个查询限制到语义匹配的键上，同样使用轻量级 ANN 完成匹配。
- **算法流程概述**：在逐帧自回归生成中，TempCache 先压缩冗余 KV 缓存；AnnCA 在跨注意力阶段筛选帧相关提示 token；AnnSA 在自注意力阶段为每个 query 选择语义相关的 key 子集。三者联合减少注意力计算量、总体计算量和显存占用。
- **特点**：无需重新训练，可作为现有模型的推理加速模块使用。

## 3. 实验设计
- **数据集/场景**：摘要仅泛泛提到自回归视频扩散、长视频生成和世界模型场景；具体数据集名称、视频分辨率、生成长度等**未说明**。
- **Benchmark**：材料未给出明确 benchmark 或评价协议。
- **对比方法**：摘要称与“prior methods”对比，即先前方法，但**未列出具体基线名称**。
- **评价维度**：摘要提到端到端加速、视觉质量、长 rollout 吞吐稳定性和峰值 GPU 显存使用。
- **实验结论概述**：实现最高 **x5–x10 端到端加速**，同时保持近乎相同的视觉质量，并在长 rollout 中维持稳定吞吐和近乎恒定的峰值 GPU 显存；先前方法则逐渐变慢且显存持续增加。

## 4. 资源与算力
- 材料中**未明确说明**使用的 GPU 型号、数量、训练时长或推理硬件配置。
- 由于方法被描述为 **training-free**，可能不涉及额外训练算力；但推理实验的硬件与耗时细节仍未提供。
- 因此无法评估其算力需求、复现成本或加速比的具体硬件依赖性。

## 5. 实验数量与充分性
- 材料中**未说明**具体实验组数、数据集数量、消融实验数量或统计显著性检验。
- 从摘要可推断至少报告了速度、视觉质量、吞吐、显存等维度的结果，但缺少消融、基线细节和公平性设置。
- 因此**无法判断实验是否充分、客观、公平**；也无法确认 x5–x10 加速是否在多种模型、分辨率、生成长度和硬件上一致成立。

## 6. 主要结论与发现
- 自回归视频扩散的注意力存在三类主要冗余：跨帧近重复键、缓慢演化的查询/键、长提示中少量关键 token。
- FAST-AR 通过 TempCache、AnnCA 和 AnnSA 三个模块，可在免训练条件下显著降低注意力计算、计算量和内存。
- 实验声称最高可实现 **x5–x10 端到端加速**，视觉质量接近不变。
- 在长 rollout 中，方法能保持稳定吞吐和近乎恒定的峰值 GPU 显存，而先前方法会逐步变慢并增加内存。
- 该方案为高效长视频生成和世界模型生成提供了潜在加速路径。

## 7. 优点
- **免训练、即插即用**：不依赖重新训练，便于集成到现有自回归视频扩散模型和世界模型中。
- **问题分析较系统**：明确归纳三类冗余来源，并分别设计对应模块处理 KV 缓存、跨注意力和自注意力。
- **同时优化延迟与显存**：不仅追求速度提升，还关注长 rollout 中峰值显存稳定性。
- **ANN 使用轻量**：通过近似最近邻匹配筛选相关 token/key，思路直接且计算开销较低。
- **面向长程一致性**：针对自回归视频生成中缓存增长损害长程一致性的关键痛点。

## 8. 不足与局限
- **材料严重不足**：正文抓取失败，无法验证数据集、基线、指标、消融和实现细节。
- **实验覆盖未知**：未说明测试了多少模型、数据集、分辨率、视频长度和硬件配置。
- **公平性无法评估**：基线方法未列名，加速比可能依赖特定设置或实现优化。
- **近似误差风险**：ANN 匹配和稀疏注意力可能引入误差，摘要仅称视觉质量“近乎相同”，未量化质量下降边界。
- **泛化性未知**：免训练方法可能依赖预训练骨干的特定性质，跨模型、跨域迁移能力未说明。
- **世界模型/交互场景未详述**：对交互式神经游戏引擎中的实时性、控制一致性和长期稳定性缺乏细节。
- **统计与失败案例缺失**：未报告显著性检验、失败模式或长视频生成中的退化情况。

（完）
