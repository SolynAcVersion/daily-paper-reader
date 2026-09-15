---
title: "Temporal Saliency-Guided Distillation: A Scalable Framework for Distilling Video Datasets"
title_zh: 时间显著性引导蒸馏：可扩展的视频数据集蒸馏框架
authors: "Xulin Gu, Xinhao Zhong, Zhixing Wei, Yimin Zhou, Shuoyang Sun, Bin Chen, Hongpeng Wang, Yuan Luo"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=vYqAuAuV1v"
tags: ["query:frame-dist"]
score: 4.0
evidence: 跨帧时间动态的保持
tldr: 针对视频数据集蒸馏因高维与时间复杂而计算昂贵、直接套用图像方法会损失时间动态的问题，作者提出单层视频数据集蒸馏框架，直接优化合成视频并引入时间显著性引导以保留时间动态。实验表明该方法在降低计算成本的同时更好地保持时间动态，性能优于朴素扩展的图像蒸馏方法，为视频数据压缩提供了更可扩展的方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视频数据集蒸馏因高维与时间复杂而困难，直接套用图像方法会损失时间动态且计算昂贵。
method: 提出单层视频数据集蒸馏框架，直接优化合成视频并引入时间显著性引导以保留时间动态。
result: 该方法在降低计算成本的同时更好地保持视频时间动态，性能优于朴素扩展的图像方法。
conclusion: 为视频数据集蒸馏提供了更可扩展且保留时间动态的框架。
---

## Abstract
Dataset distillation (DD) has emerged as a powerful paradigm for dataset compression, enabling the synthesis of compact surrogate datasets that approximate the training utility of large-scale ones. While significant progress has been achieved in distilling image datasets, extending DD to the video domain remains challenging due to the high dimensionality and temporal complexity inherent in video data. Existing video distillation (VD) methods often suffer from excessive computational costs and struggle to preserve temporal dynamics, as naïve extensions of image-based approaches typically lead to degraded performance. In this paper, we propose a novel uni-level video dataset distillation framework that directly optimizes synthetic videos with respect to a pre-trained model. To address temporal redundancy and enhance motion preservation, we introduce a temporal saliency-guided filtering mechanism that leverages inter-frame differences to guide the distillation process, encouraging the retention of informative temporal cues while suppressing frame-level redundancy. Extensive experiments on standard video benchmarks demonstrate that our method achieves state-of-the-art performance, bridging the gap between real and distilled video data and offering a scalable solution for video dataset compression.

---

## 论文详细总结（自动生成）

## 重要说明

- 提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页面，未包含论文正文。
- 因此以下总结主要依据论文元数据、标题、摘要、TLDR 等可得信息；凡摘要未明确提及的内容，均标注为“未说明”或“无法确认”，不做臆测。
- 论文题目：**Temporal Saliency-Guided Distillation: A Scalable Framework for Distilling Video Datasets**  
  中文：**时间显著性引导蒸馏：可扩展的视频数据集蒸馏框架**  
  来源元数据：ICLR-2026-Rejected-Public，score 4.0。

---

## 1. 论文的核心问题与整体含义

- **研究背景**：数据集蒸馏（Dataset Distillation, DD）旨在合成紧凑的代理数据集，使其在训练模型时近似大规模原始数据集的效用。该方向在图像领域已有较多进展。
- **核心问题**：将 DD 扩展到视频领域仍然困难，主要原因是：
  - 视频数据具有高维度；
  - 视频包含复杂的时间动态；
  - 直接套用图像蒸馏方法往往导致性能退化；
  - 现有视频蒸馏方法计算成本过高，且难以保留时间动态。
- **整体含义**：论文试图提出一种更可扩展的视频数据集蒸馏框架，在降低计算成本的同时更好地保留视频中的时间信息，从而缩小真实视频数据与蒸馏视频数据之间的训练效用差距。

---

## 2. 论文提出的方法论

- **核心思想**：
  - 提出一种 **单层视频数据集蒸馏框架**（uni-level video dataset distillation framework）。
  - 直接针对一个预训练模型优化合成视频，而不是依赖传统图像蒸馏中常见的复杂嵌套优化流程。
- **关键技术：时间显著性引导过滤机制**：
  - 引入 **temporal saliency-guided filtering mechanism**。
  - 利用 **帧间差异**（inter-frame differences）来指导蒸馏过程。
  - 目标是：
    - 保留有信息量的时间线索；
    - 抑制帧级冗余；
    - 增强运动信息的保持。
- **算法流程概述**：
  - 初始化合成视频数据；
  - 使用预训练模型作为优化目标/评估器；
  - 计算帧间差异，得到时间显著性信息；
  - 用该显著性引导过滤或加权蒸馏过程，使合成视频更关注运动变化显著的区域；
  - 直接更新合成视频，使其在预训练模型上近似真实视频数据的训练效用；
  - 最终得到紧凑、可扩展的合成视频代理数据集。
- **公式与细节**：提供内容中未给出具体公式、损失函数、优化器、显著性计算方式或网络结构，无法进一步确认。

---

## 3. 实验设计

- **数据集 / 场景**：
  - 摘要仅说明使用了 **standard video benchmarks**（标准视频基准）。
  - 具体数据集名称、视频任务类型、输入分辨率、帧数、类别数等均未说明。
- **Benchmark**：
  - 未明确给出 benchmark 协议、评价指标或训练/测试划分。
- **对比方法**：
  - 摘要提到与以下方向比较：
    - 现有视频蒸馏方法；
    - 朴素扩展的图像蒸馏方法。
  - 具体对比方法名称未列出。
- **实验结论性描述**：
  - 论文声称在标准视频基准上取得 **state-of-the-art performance**；
  - 缩小了真实视频数据与蒸馏视频数据之间的差距；
  - 为视频数据集压缩提供了可扩展方案。

---

## 4. 资源与算力

- 提供内容中 **没有提及**：
  - GPU 型号；
  - GPU 数量；
  - 训练时长；
  - 显存消耗；
  - 总计算量或碳排放等信息。
- 摘要仅强调方法在概念上降低计算成本，但没有给出可核实的算力报告。
- 因此无法评估其实际资源需求、训练效率或可复现成本。

---

## 5. 实验数量与充分性

- 摘要仅称进行了 **extensive experiments on standard video benchmarks**，但未说明：
  - 使用了多少个数据集；
  - 进行了多少组对比实验；
  - 是否包含消融实验；
  - 是否验证时间显著性模块、过滤机制、单层框架等组件的贡献；
  - 是否报告方差、置信区间或统计显著性。
- 因此，从提供内容看：
  - **无法判断实验数量是否充分**；
  - **无法判断比较是否客观、公平**；
  - 元数据显示该论文来自 ICLR-2026-Rejected-Public，score 为 4.0，但这只能说明评审结果，不能替代对实验充分性的独立判断。
- 若要评估实验充分性，需要获取论文正文、附录、开源代码和完整实验表格。

---

## 6. 论文的主要结论与发现

- 提出了一种 **单层视频数据集蒸馏框架**，可直接优化合成视频。
- 引入 **时间显著性引导过滤机制**，利用帧间差异保留时间动态并抑制冗余。
- 在标准视频基准上，该方法据称：
  - 达到 SOTA；
  - 优于朴素扩展的图像蒸馏方法；
  - 在降低计算成本的同时更好地保持时间动态；
  - 为视频数据集压缩提供了更可扩展的解决方案。
- 总体结论：时间显著性引导对视频蒸馏中的运动保持和时间动态保留具有关键作用。

---

## 7. 优点

- **问题选择有价值**：视频数据集蒸馏相比图像蒸馏更具挑战性，也具有实际压缩与加速训练的意义。
- **方法思路清晰**：
  - 单层框架可能简化优化流程，降低传统双层蒸馏的计算负担；
  - 直接优化合成视频，与预训练模型对齐，符合数据集蒸馏的基本目标。
- **针对视频特性设计**：
  - 使用帧间差异构建时间显著性，直接面向视频中的时间冗余与运动保持问题；
  - 相比简单迁移图像蒸馏方法，更有视频领域针对性。
- **可扩展性定位明确**：论文强调 scalable solution，适合视频数据压缩场景。
- **性能主张较强**：摘要声称在标准视频基准上达到 SOTA，并缩小真实数据与蒸馏数据的差距。

---

## 8. 不足与局限

- **正文不可得导致的信息局限**：
  - 当前提供内容仅为验证页面，无法核实方法公式、网络结构、训练细节和实验配置。
- **实验细节不足**：
  - 未列出具体数据集、对比方法、评价指标、消融实验和超参数设置；
  - 无法判断 SOTA 结论是否在公平条件下取得；
  - 无法判断是否覆盖不同视频任务、不同规模数据集和不同预训练模型。
- **算力与效率报告缺失**：
  - 虽声称降低计算成本，但没有 GPU 型号、数量、训练时长等数据；
  - 无法验证其实际效率优势。
- **潜在方法限制**：
  - 时间显著性依赖帧间差异，可能对帧率、运动速度、场景切换、长视频依赖等敏感；
  - 对静态或低运动视频、复杂多模态视频、长时序视频的泛化能力未知；
  - 单层直接优化是否会导致过拟合预训练模型，摘要未讨论。
- **评审与偏差风险**：
  - 元数据显示该论文来自被拒公开投稿，score 4.0，提示其创新性或实验说服力可能存在争议；
  - 但最终判断仍需完整论文和评审意见支持。
- **应用限制**：
  - 视频数据集蒸馏本身仍面临存储、优化稳定性、跨架构泛化等问题；
  - 论文未在提供内容中讨论伦理、隐私、版权或真实部署限制。

---

（完）
