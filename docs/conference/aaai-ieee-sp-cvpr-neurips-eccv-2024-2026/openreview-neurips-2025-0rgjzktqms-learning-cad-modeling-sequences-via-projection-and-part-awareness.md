---
title: Learning CAD Modeling Sequences via Projection and Part Awareness
title_zh: 基于投影与部件感知学习CAD建模序列
authors: "Yang Liu, Daxuan Ren, Yijie Ding, Jianmin Zheng, Fang Deng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=0rGJzKTqMs"
tags: ["query:cad-spatial"]
score: 8.0
evidence: 三平面投影引导的CAD生成
tldr: 针对从点云重建可编辑CAD模型时结构不连贯、设计意图缺失的问题，本文提出PartCAD框架。方法先用自回归方式将点云分解为部件感知的隐表示，再通过三平面投影模块注入显式设计意图线索，最后用非自回归解码器一次性生成拉伸草图参数。实验表明该框架能高效、结构一致地合成CAD指令序列，为连接几何信号与语义理解提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 从点云重建可编辑CAD模型时，现有方法难以保持结构连贯并捕捉设计意图。
method: 用部件感知隐表示分解点云，借助三平面投影提供设计意图线索，并用非自回归解码器生成拉伸草图参数。
result: 框架能高效、结构一致地合成CAD建模指令序列。
conclusion: 为几何信号与语义理解之间搭建桥梁，推进可编辑CAD模型重建。
---

## Abstract
This paper presents PartCAD, a novel framework for reconstructing CAD modeling sequences directly from point clouds by projection-guided, part-aware geometry reasoning. It consists of (1) an autoregressive approach that decomposes point clouds into part-aware latent representations, serving as interpretable anchors for CAD generation; (2) a projection guidance module that provides explicit cues about underlying design intent via triplane projections; and (3) a non-autoregressive decoder to generate sketch-extrusion parameters in a single forward pass, enabling efficient and structurally coherent CAD instruction synthesis. By bridging geometric signals and semantic understanding, PartCAD tackles the challenge of reconstructing editable CAD models—capturing underlying design processes—from 3D point clouds. Extensive experiments show that PartCAD significantly outperforms existing methods for CAD instruction generation in both accuracy and robustness. The work sheds light on part-driven reconstruction of interpretable CAD models, opening new avenues in reverse engineering and CAD automation.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页面，未包含论文正文。以下总结主要基于论文元数据、摘要及 TLDR/方法/结论字段；凡正文未提供的细节，均明确标注为“未说明”或“无法确认”。

## 1. 核心问题与整体含义
- **研究动机**：从 3D 点云重建**可编辑 CAD 模型**时，现有方法往往难以保持结构连贯性，也容易丢失底层**设计意图**。
- **核心问题**：如何从点云中恢复不仅几何合理、而且结构一致、可解释、可编辑的 CAD 建模序列。
- **整体含义**：论文提出 **PartCAD** 框架，试图连接**几何信号**与**语义理解**，把点云反向工程为 CAD 指令序列，推动逆向工程与 CAD 自动化。
- **任务定位**：不是只重建静态 3D 形状，而是生成 CAD 建模指令，尤其是**拉伸草图参数**，从而得到可编辑 CAD 模型。

## 2. 方法论：核心思想与关键技术
- **核心思想**：采用“**投影引导 + 部件感知**”的几何推理，将点云分解为部件级表示，再注入设计意图线索，最后生成 CAD 指令序列。
- **三阶段流程**：
  1. **自回归点云分解**：以自回归方式将点云分解为**部件感知隐表示**，这些隐表示作为 CAD 生成的可解释锚点。
  2. **投影引导模块**：通过**三平面投影**提供关于底层设计意图的显式线索，弥补纯几何表示中语义与设计意图不足的问题。
  3. **非自回归解码器**：在一次前向传播中生成**拉伸草图参数**，即 sketch-extrusion parameters，实现高效且结构连贯的 CAD 指令合成。
- **算法流程文字描述**：
  - 输入：3D 点云。
  - 步骤一：自回归模型逐步推断部件级隐表示，形成结构化、可解释的中间表示。
  - 步骤二：利用三平面投影对几何/部件信息进行投影编码，注入显式设计意图线索。
  - 步骤三：非自回归解码器并行生成 CAD 指令参数，输出可编辑 CAD 建模序列。
- **未提供细节**：论文摘要和元数据中未给出具体网络结构、损失函数、公式、训练目标或推理算法伪代码。

## 3. 实验设计
- **任务场景**：根据摘要，实验围绕从点云生成 CAD 指令、重建可编辑 CAD 模型展开。
- **评价维度**：摘要声称在 **accuracy** 和 **robustness** 上显著优于现有方法。
- **数据集 / Benchmark**：可获取文本中**未列出具体数据集、场景或 benchmark 名称**。
- **对比方法**：可获取文本中**未给出具体对比方法名称**。
- **指标**：仅提到准确率与鲁棒性，**未说明具体评价指标**，如 Chamfer Distance、IoU、序列匹配指标、参数误差等。
- **结论**：因此，实验设计的具体覆盖范围无法从当前材料确认。

## 4. 资源与算力
- 提供的摘要与元数据中**未提及 GPU 型号、数量、训练时长、参数量、训练成本**等信息。
- 因此无法总结算力资源，也无法判断该方法在实际训练与推理中的资源需求。

## 5. 实验数量与充分性
- 摘要仅称进行了 **extensive experiments**，并声称显著优于现有方法。
- 但当前材料**未提供实验组数、数据集数量、消融实验、跨数据集测试、鲁棒性测试设置、统计显著性检验**等细节。
- 因此：
  - **充分性无法验证**：无法判断是否覆盖主流 CAD 重建基准、是否包含消融和泛化实验。
  - **客观性与公平性无法验证**：缺少对比方法、训练配置、评价协议和数据划分信息。
  - 只能认为作者在摘要中主张实验充分且效果显著，但外部读者无法仅凭摘要复核。

## 6. 主要结论与发现
- PartCAD 能从点云中高效、结构一致地合成 CAD 建模指令序列。
- 在 CAD 指令生成任务上，PartCAD 在准确性和鲁棒性方面显著优于现有方法。
- 部件感知隐表示和三平面投影引导有助于捕捉设计意图，提高可解释性。
- 非自回归解码器支持一次前向生成拉伸草图参数，提升生成效率。
- 该工作为几何信号与语义理解之间搭建桥梁，推进可编辑 CAD 模型重建与 CAD 自动化。

## 7. 优点
- **部件感知建模**：将点云分解为部件级隐表示，有助于保持 CAD 结构连贯性，并提升中间表示的可解释性。
- **显式设计意图注入**：三平面投影模块为几何推理提供设计意图线索，针对“纯几何到 CAD 语义”的鸿沟提出解决思路。
- **生成效率较高**：非自回归解码器一次前向生成拉伸草图参数，相比逐步自回归生成可能更快。
- **任务价值明确**：面向可编辑 CAD 模型重建，而非仅静态形状拟合，更贴近逆向工程和 CAD 自动化需求。
- **方法组合有层次**：自回归部件分解负责结构理解，投影模块负责意图引导，非自回归解码负责高效生成，分工较清晰。

## 8. 不足与局限
- **材料限制**：提供的 PDF 文本为 CAPTCHA 验证页，无法获取正文，因此无法核实方法、实验与结论细节。
- **实验信息缺失**：未说明数据集、benchmark、对比方法、评价指标、训练配置和消融实验，难以判断实验充分性与公平性。
- **算力未报告**：未提供 GPU 型号、数量、训练时长等，无法评估可复现性与资源门槛。
- **方法覆盖范围可能有限**：摘要强调生成“拉伸草图参数”，可能主要覆盖 sketch-extrusion 类 CAD 操作，对旋转、倒角、扫掠、放样等复杂 CAD 操作是否适用尚不明确。
- **潜在依赖风险**：部件感知分解可能依赖点云质量、部件分割质量或部件定义方式；三平面投影对复杂拓扑、遮挡和细粒度结构的表达能力也需正文验证。
- **泛化与偏差风险未知**：若训练数据分布有限，模型对真实扫描噪声、跨类别 CAD 模型和不同建模风格的泛化能力无法从当前材料判断。
- **结论需外部验证**：摘要声称“显著优于现有方法”，但缺少可复核的实验细节，因此该结论目前只能视为作者主张。

（完）
