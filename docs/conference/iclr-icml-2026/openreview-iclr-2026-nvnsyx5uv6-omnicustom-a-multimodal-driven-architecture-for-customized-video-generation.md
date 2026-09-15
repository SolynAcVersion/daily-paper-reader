---
title: "OmniCustom: A Multimodal-Driven Architecture for Customized Video Generation"
title_zh: OmniCustom：面向定制化视频生成的多模态驱动架构
authors: "Teng Hu, Zhentao Yu, Zhengguang Zhou, Sen Liang, Qin Lin, Yuan Zhou, Ran Yi, Qinglin Lu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=nvNSyX5uV6"
tags: ["query:video-gen-rl"]
score: 6.0
evidence: 多模态定制化视频生成模型
tldr: 定制化视频生成需在灵活用户条件下生成特定主体视频，但现有方法面临身份一致性差与输入模态有限的问题。本文提出OmniCustom，基于HunyuanVideo构建多模态定制视频生成模型，引入基于LLaVA的身份增强文本-图像条件模块与图像ID增强模块，并支持音频、视频驱动的定制注入。该模型在保持主体一致性的同时扩展了可控模态，推进了定制化视频生成能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 定制化视频生成存在身份一致性差与支持输入模态有限的问题。
method: 基于HunyuanVideo引入LLaVA身份增强文本-图像条件模块与图像ID增强模块。
result: 支持图像、音频、视频、文本多模态条件，并强化主体身份一致性。
conclusion: 为灵活可控且保持主体一致的多模态视频生成提供了新架构。
---

## Abstract
Customized video generation aims to produce videos featuring specific subjects under flexible user-defined conditions, yet existing methods often struggle with identity consistency and limited input modalities. In this paper, we propose OmniCustom, a multi-modal customized video generation model that emphasizes subject consistency while supporting image, audio, video, and text conditions. Built upon HunyuanVideo, OmniCustom introduces an identity-enhanced text-image conditioning module based on LLaVA for improved multi-modal understanding, and an image ID enhancement module that leverages temporal concatenation to reinforce identity features. To enable flexible audio- and video-driven customization, we further propose modality-specific injection modules. Our identity-disentangled AudioNet injects temporally aligned audio features into video latents via spatial cross-attention, enabling precise audio control. For video-driven generation, we design an identity-disentangled video injection module that projects conditional video into the latent space and efficiently aligns video features with latents for seamless integration. Extensive experiments on single- and multi-subject scenarios show that OmniCustom significantly outperforms state-of-the-art methods in ID consistency, realism, and text-video alignment. We further demonstrate its robustness on downstream tasks such as audio- and video-driven customized video generation, highlighting the effectiveness of our multi-modal conditioning and identity-preserving strategies for customized video generation.

---

## 论文详细总结（自动生成）

> **说明**：提供的 PDF 链接返回 503，实际提取文本仅为元数据与摘要，正文、实验细节、算力信息均未给出。以下总结严格基于可见信息，缺失处已明确标注。

## 1. 核心问题与整体含义
- **研究动机**：定制化视频生成旨在根据用户定义的灵活条件，生成包含特定主体的视频；但现有方法普遍存在两个问题：
  - 主体身份一致性差；
  - 支持的输入模态有限。
- **整体含义**：论文提出 **OmniCustom**，一个多模态驱动的定制化视频生成架构，在强调主体一致性的同时，支持图像、音频、视频、文本等多种条件输入，推进灵活可控的定制视频生成能力。

## 2. 方法论
- **核心思想**：基于 **HunyuanVideo** 构建多模态定制视频生成模型，通过身份增强与模态特定注入模块，在保持主体身份一致的同时扩展可控模态。
- **关键技术细节**：
  - **基于 LLaVA 的身份增强文本-图像条件模块**：提升多模态理解能力，并将文本与图像条件用于身份增强。
  - **图像 ID 增强模块**：利用**时间拼接（temporal concatenation）**强化身份特征。
  - **身份解耦的 AudioNet**：将时间对齐的音频特征通过**空间交叉注意力（spatial cross-attention）**注入视频 latent，实现精确音频控制。
  - **身份解耦的视频注入模块**：将条件视频投影到 latent 空间，并高效对齐视频特征与 latent，实现无缝集成。
- **算法流程（文字描述）**：
  - 以 HunyuanVideo 为视频生成骨干；
  - 文本与图像条件经 LLaVA 增强理解，并经图像 ID 增强模块强化身份；
  - 音频、视频条件分别通过身份解耦的模态注入模块，在 latent 空间中对齐并融合；
  - 最终生成同时满足多模态条件与主体一致性的定制视频。
- **公式**：可见摘要未给出具体公式。

## 3. 实验设计
- **场景**：
  - 单主体（single-subject）定制视频生成；
  - 多主体（multi-subject）定制视频生成；
  - 下游任务：音频驱动、视频驱动的定制化视频生成。
- **Benchmark**：摘要未明确给出具体 benchmark 名称；从描述看，评估围绕定制视频生成中的身份一致性、真实感与文本-视频对齐。
- **对比方法**：声称与 **state-of-the-art methods** 对比，但摘要未列出具体基线方法。
- **评估指标**：
  - ID consistency（身份一致性）；
  - realism（真实感）；
  - text-video alignment（文本-视频对齐）。
- **数据集**：未明确说明。

## 4. 资源与算力
- 摘要与元数据中**未提及** GPU 型号、数量、训练时长、参数量或训练成本。
- 由于正文不可得，无法确认其实际算力开销；仅能推断其基于 HunyuanVideo 与 LLaVA，可能涉及大规模预训练模型适配或微调，但具体资源未知。

## 5. 实验数量与充分性
- 摘要称进行了 **extensive experiments**，至少覆盖：
  - 单主体场景；
  - 多主体场景；
  - 音频驱动下游任务；
  - 视频驱动下游任务。
- **具体实验组数、消融实验数量、数据集数量、基线数量均未提供**，因此无法准确判断“多少组实验”。
- **充分性与公平性**：
  - 从摘要看，实验方向较全面，覆盖主任务与下游任务；
  - 但缺少定量结果、基线配置、指标实现、随机种子、统计显著性等信息，无法核验实验是否充分、客观、公平。

## 6. 主要结论与发现
- OmniCustom 在 **身份一致性、真实感、文本-视频对齐** 上显著优于现有 state-of-the-art 方法。
- 模型能够支持图像、音频、视频、文本多模态条件，并保持主体身份一致性。
- 在音频驱动与视频驱动的定制视频生成下游任务上表现出鲁棒性。
- 多模态条件策略与身份保持策略对定制视频生成有效。

## 7. 优点
- **多模态统一**：同时支持图像、音频、视频、文本条件，扩展了定制视频生成的可控模态。
- **身份保持设计**：引入 LLaVA 增强的文本-图像条件模块与图像 ID 增强模块，强化主体身份。
- **解耦注入机制**：音频与视频注入模块采用身份解耦设计，有助于在引入新模态时减少对主体身份的干扰。
- **强骨干基础**：基于 HunyuanVideo 与 LLaVA，具备较好的生成与多模态理解基础。
- **下游任务拓展**：展示音频驱动、视频驱动定制生成的可行性。

## 8. 不足与局限
- **信息不完整**：PDF 提取失败，无法评估全文方法、实验与实现细节。
- **实验细节缺失**：未给出具体数据集、benchmark、基线方法、定量指标、消融实验与用户研究。
- **算力与复现性未知**：未报告 GPU 型号、数量、训练时长、参数量等，复现难度无法判断。
- **公平性无法核验**：缺少基线配置与实验协议，难以确认对比是否完全公平。
- **应用限制未讨论**：摘要未涉及计算成本、输入质量依赖、长视频/复杂场景身份一致性、伦理与深度伪造风险等。
- **潜在偏差风险**：单/多主体场景覆盖有限，音频与视频驱动效果可能受条件输入质量影响。

（完）
