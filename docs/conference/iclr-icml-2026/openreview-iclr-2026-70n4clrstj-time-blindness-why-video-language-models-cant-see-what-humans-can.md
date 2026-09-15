---
title: "Time Blindness: Why Video-Language Models Can’t See What Humans Can?"
title_zh: 时间盲区：视频语言模型为何看不到人类能看到的东西？
authors: "Ujjwal Upadhyay, Mukul Ranjan, Zhiqiang Shen, Mohamed Elhoseiny"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=70n4clRSTj"
tags: ["query:frame-dist"]
score: 4.0
evidence: 基于帧序列时序模式编码的基准
tldr: "针对视频语言模型在空间信息被遮挡时难以捕捉纯时序模式的问题，本文提出SpookyBench基准，将信息仅编码在类似噪声帧的时间序列中。实验发现人类识别形状、文字和图案的准确率超过98%，而最先进视频语言模型准确率为0%。该差距揭示了模型对帧级空间特征的过度依赖和从时序线索中提取意义的无能，对理解视频时间维度建模的局限有警示意义。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频语言模型在空间信息被遮挡时难以捕捉纯时序模式。
method: 提出SpookyBench，将信息仅编码在噪声帧的时间序列中。
result: "人类准确率超98%，而视频语言模型准确率为0%。"
conclusion: 揭示模型过度依赖空间特征，难以从时序线索中提取意义。
---

## Abstract
Recent advances in vision–language models (VLMs) have made impressive strides in understanding spatio-temporal relationships in videos. However, when spatial information is obscured, these models struggle to capture purely temporal patterns. We introduce $\textbf{SpookyBench}$, a benchmark where information is encoded solely in temporal sequences of noise-like frames, mirroring natural phenomena from biological signaling to covert communication. Interestingly, while humans can recognize shapes, text, and patterns in these sequences with over 98\% accuracy, state-of-the-art VLMs achieve 0\% accuracy. This performance gap highlights a critical limitation: an over-reliance on frame-level spatial features and an inability to extract meaning from temporal cues. Overcoming this limitation will require novel architectures or training paradigms that decouple spatial dependencies from temporal processing. Our systematic analysis shows that this issue persists across model scales and architectures. We release SpookyBench to catalyze research in temporal pattern recognition and bridge the gap between human and machine video understanding. Dataset is available at this anonymous link: https://tinyurl.com/spooky-bench

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本实际为 OpenReview 验证/CAPTCHA 页面，未包含论文正文；以下总结主要依据论文摘要与 Markdown 元数据，部分方法细节、实验设置与算力信息无法从给定材料中确认。

## 1. 核心问题与整体含义
- **研究动机**：当前视觉-语言模型（VLM）在视频时空关系理解上取得显著进展，但当视频中的**空间信息被遮挡或单帧本身不提供有效空间线索**时，模型难以捕捉**纯时序模式**。
- **核心问题**：视频语言模型是否真正具备从时间维度中提取意义的能力？还是主要依赖帧级空间特征？
- **整体含义**：论文提出 **SpookyBench**，将信息仅编码在类似噪声帧的时间序列中，模拟生物信号、隐蔽通信等自然现象。人类识别形状、文字和图案的准确率超过 **98%**，而最先进 VLM 准确率为 **0%**。这一差距揭示了模型对帧级空间特征的过度依赖，以及从时序线索中提取意义的无能。
- **更广泛影响**：该问题跨模型规模和架构持续存在，说明要克服这一限制，可能需要新的架构或训练范式，将空间依赖与时序处理解耦。

## 2. 方法论
- **核心思想**：构建一个基准 **SpookyBench**，其中每一帧单独看起来都接近噪声，无法提供可识别的空间信息；只有按时间顺序观察帧序列，才能识别出形状、文字或图案。
- **关键设计**：将类别或语义信息编码在**时间维度的变化模式**中，而非单帧空间内容中。这样可强制模型依赖纯时序线索，排除帧级空间捷径。
- **形式化概括**（非原文公式，仅概念描述）：
  - 给定视频帧序列 \(\{F_1, F_2, ..., F_T\}\)，单帧 \(F_t\) 近似噪声；
  - 标签 \(y\) 由帧间时序模式决定；
  - 模型预测 \(\hat{y} = f(F_1, ..., F_T)\)；
  - 人类通过时间整合识别 \(y\)，而 VLM 被测试能否同样从序列中恢复 \(y\)。
- **技术细节缺失**：提供文本未说明具体帧生成方式、帧率、视频长度、类别数量、噪声类型、图案编码算法等。因此无法进一步总结其生成流程或训练目标。

## 3. 实验设计
- **数据集 / 场景**：使用 **SpookyBench**。该基准包含仅靠噪声样帧的时间序列编码的信息，任务涉及识别**形状、文字和图案**。
- **对比对象**：
  - 人类被试；
  - 最先进的视频语言模型（SOTA VLMs）。
- **评估指标**：准确率。
- **主要结果**：人类准确率超过 **98%**，而 SOTA VLM 准确率为 **0%**。
- **系统性分析**：摘要称该问题在**不同模型规模和架构**上持续存在，说明并非单一模型或单一规模的特例。
- **未明确信息**：具体测试了哪些 VLM、多少个人类被试、数据集规模、任务类别数、是否进行消融实验等，均未在给定材料中说明。

## 4. 资源与算力
- 提供的论文内容中**未提及** GPU 型号、GPU 数量、训练时长、推理成本、参数量或计算资源规模。
- 由于正文缺失，无法判断该工作是否主要进行评估而非训练，也无法总结算力开销。
- 因此，关于资源与算力的结论是：**信息不足，无法总结**。

## 5. 实验数量与充分性
- 从可见信息看，实验至少包括：
  - 人类基线实验；
  - 多个 SOTA VLM 的评估；
  - 跨模型规模和架构的比较；
  - 可能覆盖形状、文字、图案等不同任务类型。
- 但具体实验组数、模型数量、被试数量、统计显著性和消融实验均未提供，因此**无法准确判断实验总量**。
- **充分性与公平性**：
  - 人类 >98% 与 VLM 0% 的对比非常强烈，具有警示意义；
  - 但需确认模型是否接收与人类相同的完整帧序列，是否受帧采样、上下文长度、分辨率或视频编码方式限制；
  - 若模型因输入接口或采样策略无法访问关键时序信息，0% 可能部分反映评估设置限制，而非完全代表模型时序理解能力。
  - 因此，结论方向有启发性，但实验细节不足以完全支持对所有视频语言模型的普遍性判断。

## 6. 主要结论与发现
- SOTA 视频语言模型在**纯时序信息任务**上表现极差，SpookyBench 上准确率为 **0%**。
- 人类在同一任务上准确率超过 **98%**，表明信息在时间序列中是可识别的。
- 该差距说明 VLM **过度依赖帧级空间特征**，难以从时序线索中提取语义。
- 问题跨模型规模和架构存在，可能是一个**结构性局限**，而非个别模型缺陷。
- 要解决该问题，需要新的架构或训练范式，**解耦空间依赖与时序处理**。
- SpookyBench 的发布旨在推动时序模式识别研究，弥合人类与机器视频理解之间的差距。

## 7. 优点
- **问题新颖且尖锐**：直接挑战视频模型“理解时间”的能力，而非仅关注空间识别或短视频问答。
- **基准设计简洁有力**：通过让单帧接近噪声，剥离空间捷径，强制模型依赖时序信息。
- **人类 vs 模型对比鲜明**：98% 与 0% 的差距极具冲击力，易于引发后续研究。
- **跨模型规模和架构分析**：增强了结论的普适性，表明问题不局限于单一模型。
- **公开数据集**：提供匿名链接，有助于社区复现和进一步研究。

## 8. 不足与局限
- **方法细节不足**：给定材料未说明 SpookyBench 的具体生成机制、任务难度控制和数据规模。
- **实验覆盖不明确**：未列出具体模型、人类被试数量、任务类别数、消融实验和统计检验。
- **0% 结果需谨慎解释**：可能受模型帧采样、输入长度、视频编码、上下文窗口等工程因素影响，未必等同于模型完全不具备任何时序能力。
- **生态效度待验证**：SpookyBench 使用类似噪声的合成帧序列，与真实视频中的时序模式仍有差距，结论外推到自然视频需谨慎。
- **公平性风险**：若模型与人类获得的信息形式或采样率不同，直接比较可能不完全公平；需确认实验控制。
- **未提出具体解决方案**：论文主要揭示问题并发布基准，未给出可落地的架构或训练方法。
- **算力信息缺失**：无法评估计算成本与可复现性。
- **应用限制**：若模型无法从纯时序线索中学习，则在遮挡、低光、隐蔽通信、生物信号等场景中的视频理解能力可能受限。

（完）
