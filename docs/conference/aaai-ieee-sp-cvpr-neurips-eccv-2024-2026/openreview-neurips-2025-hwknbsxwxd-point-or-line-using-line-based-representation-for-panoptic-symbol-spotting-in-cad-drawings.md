---
title: Point or Line? Using Line-based Representation for Panoptic Symbol Spotting in CAD Drawings
title_zh: 点还是线？面向CAD图纸全景符号识别的线基表示
authors: "Xingguang Wei, Haomin Wang, Shenglong Ye, Ruifeng Luo, Yanting Zhang, Lixin Gu, Jifeng Dai, Yu Qiao, Wenhai Wang, Hongjie Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=hwKnBsXwXd"
tags: ["query:cad-spatial"]
score: 5.0
evidence: 面向CAD图纸理解的线基表示
tldr: CAD图纸中的全景符号识别需同时识别可数实例与不可数语义区域，但现有基于栅格化、图或点的方法计算昂贵且丢失几何结构信息。该文提出VecFormer，采用图元的线基表示以保留几何连续性。实验表明该方法在CAD图纸符号识别上兼顾效率与通用性，提升了结构信息利用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有CAD图纸符号识别方法依赖栅格化或点表示，计算昂贵且丢失几何结构信息。
method: 提出VecFormer，用线基表示CAD图元，保留原始图元的几何连续性。
result: 在CAD图纸全景符号识别任务上兼顾计算效率与几何结构保持。
conclusion: 为CAD图纸的矢量图元理解提供了更通用高效的表示方式。
---

## Abstract
We study the task of panoptic symbol spotting, which involves identifying both individual instances of countable \textit{things} and the semantic regions of uncountable \textit{stuff} in computer-aided design (CAD) drawings composed of vector graphical primitives.
Existing methods typically rely on image rasterization, graph construction, or point-based representation, but these approaches often suffer from high computational costs, limited generality, and loss of geometric structural information. In this paper, we propose \textit{VecFormer}, a novel method that addresses these challenges through \textit{line-based representation} of primitives. This design preserves the geometric continuity of the original primitive, enabling more accurate shape representation while maintaining a computation-friendly structure, making it well-suited for vector graphic understanding tasks. To further enhance prediction reliability, we introduce a \textit{Branch Fusion Refinement} module that effectively integrates instance and semantic predictions, resolving their inconsistencies for more coherent panoptic outputs. Extensive experiments demonstrate that our method establishes a new state-of-the-art, achieving 91.1 PQ, with Stuff-PQ improved by 9.6 and 21.2 points over the second-best results under settings with and without prior information, respectively—highlighting the strong potential of line-based representation as a foundation for vector graphic understanding.

---

## 论文详细总结（自动生成）

## 说明
由于 OpenReview PDF 页面触发 CAPTCHA，当前可依据的内容仅为论文元数据与 Abstract。以下总结会显式标注摘要未披露的信息，避免编造实验细节。

## 1. 核心问题与整体含义
- **研究任务**：CAD 图纸中的全景符号识别（panoptic symbol spotting）。
- **任务目标**：同时识别两类目标：
  - 可数的 **things**：单个实例；
  - 不可数的 **stuff**：语义区域。
- **背景问题**：CAD 图纸由矢量图元构成，但现有方法多依赖：
  - 图像栅格化；
  - 图构建；
  - 点基表示。
- **核心痛点**：这些方法常导致：
  - 计算成本高；
  - 通用性有限；
  - 丢失原始图元的几何结构信息。
- **整体含义**：论文提出用“线基表示”替代点或栅格表示，试图在保留几何连续性的同时保持计算友好，为矢量图形理解提供更通用的表示基础。

## 2. 方法论
- **核心方法**：提出 **VecFormer**。
- **核心思想**：对 CAD 图元采用 **line-based representation**，即线基表示。
- **关键作用**：
  - 保留原始图元的几何连续性；
  - 实现更准确的形状表示；
  - 避免栅格化、图或点表示带来的结构信息损失；
  - 维持计算友好的结构，适合矢量图形理解任务。
- **辅助模块**：提出 **Branch Fusion Refinement** 模块。
  - 用于融合实例预测与语义预测；
  - 解决实例分支和语义分支之间的不一致；
  - 生成更连贯的全景输出。
- **可概括流程**：
  - 输入 CAD 矢量图元；
  - 将图元转换为线基表示；
  - 进行实例预测与语义区域预测；
  - 通过 Branch Fusion Refinement 融合与精炼；
  - 输出全景符号识别结果。
- **公式/算法细节**：摘要未给出具体公式、网络结构或伪代码。

## 3. 实验设计
- **数据集/场景**：摘要未披露具体数据集名称、场景规模或数据划分。
- **Benchmark**：任务为 CAD 图纸全景符号识别，主要报告指标包括：
  - **PQ**；
  - **Stuff-PQ**。
- **对比设置**：
  - 有先验信息（with prior information）；
  - 无先验信息（without prior information）。
- **对比对象**：
  - 摘要仅提到与“第二好结果”比较；
  - 未列出具体 baseline 方法名称。
- **主要实验结果**：
  - 达到 **91.1 PQ**；
  - Stuff-PQ 相比第二好结果：
    - 有先验信息时提升 **9.6** 点；
    - 无先验信息时提升 **21.2** 点。

## 4. 资源与算力
- 摘要与元数据中**未提及**以下信息：
  - GPU 型号；
  - GPU 数量；
  - 训练时长；
  - 参数量；
  - 推理速度或显存消耗。
- 因此无法总结算力资源与训练成本。

## 5. 实验数量与充分性
- 摘要称进行了 **Extensive experiments**，但未说明具体实验组数。
- 可确认至少包含：
  - 有先验信息设置；
  - 无先验信息设置；
  - PQ 与 Stuff-PQ 指标比较。
- **是否包含消融实验**：摘要未明确说明。
- **是否跨多个数据集验证**：摘要未说明。
- **充分性判断**：仅凭摘要无法判断实验覆盖是否充分。
- **公平性判断**：论文声称与第二好结果比较，但缺少 baseline 细节、数据划分和评价协议，无法完全判断公平性。
- **客观性风险**：正文不可获取，当前只能依赖作者摘要中的结论。

## 6. 主要结论与发现
- **线基表示有效**：VecFormer 通过线基表示 CAD 图元，在保持几何连续性的同时实现计算友好。
- **融合模块有效**：Branch Fusion Refinement 能缓解实例预测与语义预测的不一致，提升全景输出连贯性。
- **性能达到 SOTA**：方法取得 **91.1 PQ**。
- **Stuff 区域提升显著**：Stuff-PQ 在有/无先验信息下分别提升 **9.6** 和 **21.2** 点。
- **更广泛意义**：线基表示有潜力成为矢量图形理解的基础表示方式。

## 7. 优点
- **表示创新**：从点/栅格转向线基表示，更贴合 CAD 矢量图元的几何本质。
- **信息保留**：保留原始图元几何连续性，减少结构信息损失。
- **计算友好**：在保留几何结构的同时兼顾计算效率。
- **模块设计合理**：Branch Fusion Refinement 针对实例与语义预测不一致问题，有助于提升全景一致性。
- **结果提升明显**：尤其在 Stuff-PQ 上提升幅度大，说明对不可数语义区域识别有优势。
- **通用潜力**：方法面向矢量图形理解，可能扩展到更广泛的 CAD/矢量图任务。

## 8. 不足与局限
- **信息不完整**：OpenReview PDF 触发 CAPTCHA，正文无法获取，当前仅能依据摘要和元数据。
- **实验细节缺失**：
  - 未说明数据集名称与规模；
  - 未列出具体对比方法；
  - 未说明评价协议与训练细节；
  - 未提供 Thing-PQ、推理速度、参数量等关键指标。
- **消融与泛化未知**：无法判断线基表示和 Branch Fusion Refinement 各自贡献，也无法判断跨数据集泛化能力。
- **算力与复现性未知**：未提及训练资源，复现难度无法评估。
- **应用限制**：方法面向 CAD 矢量图元，若输入为纯栅格图像或非矢量格式，适用性可能受限。
- **偏差风险**：元数据中的 `score: 5.0` 可能是检索或相关性评分，不应直接视为论文评审质量分。
- **结论验证受限**：摘要中的 SOTA 与大幅提升需要正文实验细节支撑，当前无法进一步核验。

（完）
