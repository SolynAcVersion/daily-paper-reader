---
title: "JDM: Joint Distribution Modeling for Fine-Grained Text-to-Video Generation"
title_zh: JDM：面向细粒度文本到视频生成的联合分布建模
authors: "Penghui Ruan, Bojia Zi, Xianbiao Qi, Youze Huang, Rong Xiao, Pichao WANG, Jiannong Cao, Yuhui Shi"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=Ug8NyyagOw"
tags: ["query:frame-dist"]
score: 7.0
evidence: 建模视频内容与物体掩码的联合分布
tldr: 文本到视频生成在视觉质量上进步显著，但细粒度文本-视频对齐仍存在属性错配、物体交互错误与组合失败等问题。本文指出其根源在于模型偏重视频重建而非显式学习结构化的文本-视频对应关系，提出联合分布建模框架JDM，通过建模视频内容与物体掩码的联合分布来增强对齐。该框架为细粒度文本到视频生成提供了新的分布建模视角。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 扩散文本到视频模型存在属性错配与组合失败等细粒度对齐问题。
method: 提出联合分布建模框架，显式建模视频内容与物体掩码的联合分布。
result: 增强了文本与视频之间的结构化细粒度对应关系。
conclusion: 以联合分布建模为文本到视频的细粒度对齐提供了新路径。
---

## Abstract
Text-to-video (T2V) generation enables AI systems to create videos from textual descriptions, with applications in entertainment, education, and content creation. Recent advances in video diffusion models have improved visual quality, yet they struggle with fine-grained text-video alignment, often leading to attribute mismatches, incorrect object interactions, and compositional failures. In this paper, we identify that this limitation stem from a predominant focus on video reconstruction rather than explicitly learning structured text-video correspondences. To address this, we propose Joint Distribution Modeling (JDM), a novel framework that enhances fine-grained alignment by modeling the joint distribution of video content and object masks. Unlike prior methods that rely on external constraints, JDM inherently learns structured mappings between textual descriptions and video regions, improving compositional consistency. We theoretically demonstrate that JDM improves text-video alignment by directly optimizing for fine-grained correspondences rather than relying on implicit learning from data. Experimental results show that JDM significantly enhances alignment while maintaining high video quality. Furthermore, JDM unifies video generation and segmentation within a single framework, paving the way for more structured and controllable text-to-video synthesis.

---

## 论文详细总结（自动生成）

# JDM：面向细粒度文本到视频生成的联合分布建模——中文总结

> 说明：目标 PDF 返回 503，正文未成功获取。以下总结主要基于论文摘要与 OpenReview 元数据；凡摘要未披露的具体数据集、基线、算力、公式和实验组数，均标注为“未披露”，不做虚构。概念性推断处已标明。

## 1. 核心问题与整体含义（研究动机与背景）

- **应用背景**：文本到视频（T2V）生成可用于娱乐、教育、内容创作等场景。
- **技术现状**：视频扩散模型显著提升了视觉质量，但在**细粒度文本-视频对齐**上仍存在明显问题。
- **具体失败模式**：
  - 属性错配：文本中的颜色、材质、数量等属性未正确绑定到对应物体。
  - 物体交互错误：物体之间的动作、空间关系或因果关系生成错误。
  - 组合失败：多个物体或复杂组合描述无法被正确还原。
- **作者的核心归因**：现有方法过度关注**视频重建**，而没有显式学习文本与视频之间的**结构化对应关系**。
- **整体含义**：若能在生成框架中显式建模文本描述、视频内容与物体区域之间的结构映射，则有望提升细粒度对齐、组合一致性和可控性；JDM 还尝试统一视频生成与分割。

## 2. 方法论

- **核心思想**：提出**联合分布建模（Joint Distribution Modeling, JDM）**，通过建模**视频内容与物体掩膜的联合分布**来增强文本-视频细粒度对齐。
- **与已有方法的区别**：
  - 不依赖外部约束或后处理控制。
  - 在生成模型内部学习文本描述与视频区域之间的结构化映射。
  - 通过物体掩膜作为结构中介，增强组合一致性。
- **关键技术细节（摘要层面）**：
  - 建模对象：视频内容 + 物体掩膜。
  - 学习目标：文本描述与视频区域之间的结构化对应。
  - 预期效果：改善属性绑定、物体交互和组合生成。
  - 统一框架：将视频生成与分割整合在单一框架中。
- **概念性算法流程（摘要未给具体公式，以下为合理推断）**：
  1. 以文本描述为条件，将视频潜表示与物体掩膜视为联合变量。
  2. 训练时优化视频内容与掩膜的联合分布，使文本中的属性、关系和物体绑定到对应视频区域。
  3. 推理时从联合分布中生成视频，并可同时获得物体掩膜/分割结果。
  4. 掩膜提供结构化监督或结构表示，帮助模型学习细粒度对应，而非仅依赖重建损失隐式学习。
- **理论部分**：作者声称从理论上证明，JDM 通过直接优化细粒度对应关系，比依赖数据隐式学习更能改善文本-视频对齐。
- **注意**：摘要未披露具体网络结构、损失函数、概率分解形式或训练目标公式，因此无法复现算法细节。

## 3. 实验设计

- **数据集 / 场景**：摘要未披露具体数据集、视频领域或应用场景。
- **Benchmark**：摘要未说明使用的 benchmark、评价指标或测试协议。
- **对比方法**：摘要未列出任何对比基线或已有方法。
- **可确认的实验结论**：
  - 实验结果显示 JDM 显著增强文本-视频对齐。
  - 同时保持较高的视频质量。
  - JDM 在单一框架内统一了视频生成与分割。
- **评价**：由于缺少数据集、基线、指标和定量结果，无法从现有信息判断实验设计的具体范围与严格程度。

## 4. 资源与算力

- 摘要与元数据中**未提及**以下信息：
  - GPU 型号与数量；
  - 训练时长；
  - 参数量、模型规模；
  - 训练数据规模；
  - 推理成本或显存需求。
- 因此无法总结资源与算力使用情况。若需评估可复现性和计算开销，需要查看论文正文或附录。

## 5. 实验数量与充分性

- **实验组数**：未披露，无法判断做了多少组实验。
- **消融实验**：未披露，无法判断是否验证了联合分布建模、物体掩膜、理论目标等关键组件的贡献。
- **数据集覆盖**：未披露，无法判断是否覆盖多领域、多物体、复杂交互、长视频等场景。
- **对比公平性**：未披露基线设置、训练预算、评价协议，因此无法判断对比是否客观、公平。
- **元数据信息**：该论文来源标注为 `ICLR-2026-Rejected-Public`，元数据中 `score` 为 7.0。该分数可作为评审侧参考，但不能替代对实验充分性的判断。
- **总体判断**：在仅有摘要的情况下，无法确认实验充分性、统计显著性或可复现性。

## 6. 主要结论与发现

- JDM 通过建模视频内容与物体掩膜的联合分布，能够改善文本到视频的**细粒度对齐**。
- 该方法有助于减少属性错配、物体交互错误和组合失败。
- JDM 在提升对齐的同时，声称保持高视频质量。
- JDM 将**视频生成与分割统一**在一个框架中，为更结构化、更可控的 T2V 合成提供了路径。
- 理论分析表明，直接优化细粒度文本-视频对应关系优于仅依赖数据隐式学习。

## 7. 优点

- **问题定位清晰**：将细粒度对齐失败归因于“重建导向”而非“结构化对应学习”，视角明确。
- **方法思路有结构性**：引入物体掩膜作为结构中介，建模联合分布，比单纯增加外部约束更内生于生成过程。
- **理论支撑**：作者尝试从理论上论证直接优化细粒度对应的优势，而不仅依赖经验结果。

- **统一生成与分割的潜在价值**：将视频生成与物体分割放在同一联合框架中，可能提升生成过程的可解释性，并为后续视频编辑、区域级控制、下游分割任务提供共享表示。不过摘要未说明该统一是否带来额外收益，也未披露分割精度指标。
- **减少外部控制依赖的潜力**：与依赖外部布局、轨迹或分割模型进行后处理控制的方法相比，JDM 若能在生成模型内部学习文本-区域对应，理论上可减少多模型级联带来的误差累积与工程复杂度。但这属于概念性推断，摘要未给出实现细节或对照实验。
- **结构中介的通用性**：以物体掩膜作为文本与视频之间的结构中介，思路可迁移到图像生成、视频编辑、组合式生成等任务；但论文是否验证跨任务泛化，摘要未披露。

## 8. 局限与风险（基于现有信息的审慎判断）

- **可验证信息严重不足**：由于正文未获取，当前总结主要依赖摘要与 OpenReview 元数据。数据集、基线、指标、定量结果、消融实验、算力开销均未披露，因此无法判断方法是否真正优于现有 T2V 模型。
- **掩膜监督成本与来源不明**：JDM 的核心是建模视频内容与物体掩膜的联合分布，但摘要未说明训练时掩膜从何而来：人工标注、现成分割模型伪标签，还是自监督生成。若依赖高质量视频掩膜，数据获取成本可能较高，并限制大规模训练与开放域泛化。
- **联合建模可能引入优化冲突**：视频生成目标与分割目标未必完全一致。联合训练可能导致两者相互妥协，例如生成质量提升但分割退化，或分割精度提高但视频多样性下降。摘要未披露是否存在此类权衡。
- **理论证明的适用条件不明**：作者声称从理论上证明直接优化细粒度对应优于隐式学习，但摘要未给出假设、目标函数、概率分解或证明边界。若理论依赖强假设，其实际指导意义仍需正文检验。
- **评估严谨性无法判断**：没有对比基线、评价协议和统计结果，无法确认 JDM 的提升幅度、显著性以及是否在公平训练预算下取得。元数据中 `ICLR-2026-Rejected-Public` 与 `score: 7.0` 只能作为评审侧参考，不能替代对实验充分性的判断。
- **生成与分割统一的代价未知**：统一框架可能增加模型参数量、训练复杂度和推理开销。若分割分支仅作为辅助训练信号，推理时是否保留、是否增加计算成本，摘要未说明。

## 9. 启发与后续可关注方向

- **若获取正文，应优先核查**：
  - 联合分布的具体概率分解形式；
  - 文本、视频潜变量、物体掩膜之间的条件依赖结构；
  - 训练损失是否包含重建损失、对齐损失、掩膜分割损失及其权重；
  - 掩膜是真实标注、伪标签还是模型内部涌现。
- **实验评估应关注**：
  - 属性绑定、数量、颜色、材质、空间关系、动作交互等细粒度指标；
  - 组合泛化与多物体复杂场景；
  - 视频质量、时序一致性、运动合理性；
  - 分割指标与生成指标的联合表现；
  - 与布局控制、轨迹控制、分割引导生成等方法的公平对比。
- **消融实验应验证**：
  - 联合分布建模是否必要；
  - 物体掩膜作为结构中介的贡献；
  - 理论目标与实际训练目标的一致性；
  - 生成分支与分割分支是否相互促进。
- **可复现性关注点**：
  - 训练数据规模、视频时长与分辨率；
  - GPU 型号、数量、训练时长；
  - 模型参数量与推理成本；
  - 代码、权重与数据预处理流程是否公开。

## 10. 总体评价

JDM 的核心主张具有吸引力：将细粒度文本-视频对齐从“隐式重建学习”转向“显式联合分布建模”，并以物体掩膜作为结构中介，理论上可改善属性绑定、物体交互与组合生成。其统一视频生成与分割的设想也具备潜在应用价值。然而，在正文缺失的情况下，当前只能确认其问题意识与方法方向，无法验证方法有效性、实验充分性、理论严谨性与资源开销。因此，JDM 应被视为一个值得关注但尚待完整证据支持的工作。

（完）
