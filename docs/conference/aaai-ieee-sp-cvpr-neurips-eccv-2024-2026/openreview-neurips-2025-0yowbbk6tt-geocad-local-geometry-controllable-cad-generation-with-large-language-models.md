---
title: "GeoCAD: Local Geometry-Controllable CAD Generation with Large Language Models"
title_zh: GeoCAD：基于大语言模型的局部几何可控CAD生成
authors: "Zhanwei Zhang, kaiyuan liu, Junjie Liu, Wenxiao Wang, Binbin Lin, Liang Xie, Chen Shen, Deng Cai"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=0yowBBK6tT"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 按几何指令进行局部可控的CAD生成
tldr: 局部几何可控的CAD生成旨在自动修改模型的局部部件并遵循用户给定的几何指令，但现有方法要么无法遵循文本指令，要么无法聚焦局部。该文提出GeoCAD，设计互补的标注描述策略为局部部件生成几何指令，从而支持文本驱动的局部可控CAD生成。方法在保持局部几何精度方面优于已有方案。其贡献在于提升CAD生成的几何可控性与设计效率，与CAD几何建模理解相关。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 局部几何可控的CAD生成需要修改局部部件并遵循用户几何指令，但现有方法难以兼顾指令遵循与局部聚焦。
method: 提出互补的标注描述策略为局部部件生成几何指令，实现文本驱动的局部可控CAD生成。
result: 在保持局部几何精度和指令遵循方面优于现有方法，提升设计效率。
conclusion: 为CAD模型的几何可控生成提供了有效方案。
---

## Abstract
Local geometry-controllable computer-aided design (CAD) generation aims to modify local parts of CAD models automatically, enhancing design efficiency. 
It also ensures that the shapes of newly generated local parts follow user-specific geometric instructions (e.g., an isosceles right triangle or a rectangle with one corner cut off).
However, existing methods encounter challenges in achieving this goal.
Specifically, they either lack the ability to follow textual instructions or are unable to focus on the local parts.
To address this limitation, we introduce GeoCAD, a user-friendly and local geometry-controllable CAD generation method. 
Specifically, we first propose a complementary captioning strategy to generate geometric instructions for local parts.
This strategy involves vertex-based and VLLM-based captioning for systematically annotating simple and complex parts, respectively.
In this way, we caption $\sim$221k different local parts in total.
In the training stage, given a CAD model, we randomly mask a local part.
Then, using its geometric instruction and the remaining parts as input, we prompt large language models (LLMs) to predict the masked part.
During inference, users can specify any local part for modification while adhering to a variety of predefined geometric instructions.
Extensive experiments demonstrate the effectiveness of GeoCAD in generation quality, validity and text-to-CAD consistency.

---

## 论文详细总结（自动生成）

> 说明：给定的 PDF 提取文本仅为 OpenReview 的浏览器验证/CAPTCHA 页面，不包含论文正文。以下总结主要依据论文摘要与元数据字段；凡需要正文才能确认的细节，均明确标注为“未提供/无法确认”。

## 1. 核心问题与整体含义
- **核心问题**：局部几何可控的 CAD 生成，即自动修改 CAD 模型的局部部件，并让新生成的局部形状遵循用户给定的几何指令，例如“等腰直角三角形”或“切掉一个角的矩形”。
- **研究动机**：现有方法存在两类不足：
  - 要么**缺乏遵循文本指令的能力**；
  - 要么**无法聚焦到局部部件**，难以做到只修改指定局部。
- **整体含义**：该工作试图提升 CAD 生成中的几何可控性与设计效率，使 LLM 能参与局部 CAD 部件修改，并与 CAD 几何建模理解相关。

## 2. 方法论：核心思想与关键技术
- **方法名称**：GeoCAD，一个用户友好、局部几何可控的 CAD 生成方法。
- **核心思想**：通过“几何指令 + 剩余部件”来预测被遮蔽的局部部件，从而支持文本驱动的局部 CAD 修改。
- **关键细节一：互补标注描述策略**
  - 针对**简单部件**：使用基于顶点的标注方法生成几何指令。
  - 针对**复杂部件**：使用基于 VLLM 的标注方法生成几何指令。
  - 该策略系统性地标注了约 **221k 个不同局部部件**。
- **训练阶段流程**：
  - 给定一个 CAD 模型；
  - 随机遮蔽一个局部部件；
  - 将该局部部件的几何指令与剩余部件作为输入；
  - 提示大语言模型预测被遮蔽的局部部件。
- **推理阶段流程**：
  - 用户可以指定任意局部部件进行修改；
  - 修改需遵循多种预定义几何指令。
- **可概括为条件生成/掩码部件补全**：模型根据剩余部件和几何指令生成目标局部部件，但论文未在可用文本中给出具体公式或网络结构。

## 3. 实验设计
- **评估目标**：摘要称实验覆盖生成质量、有效性和 text-to-CAD 一致性。
- **对比结论**：元数据指出 GeoCAD 在保持局部几何精度和指令遵循方面优于已有方案。
- **数据集与 benchmark**：未提供具体名称，无法确认。
- **对比方法**：未列出具体 baseline 方法，无法确认。
- **场景**：可推断为 CAD 局部部件修改、文本几何指令遵循等场景，但缺少正文细节支撑。

## 4. 资源与算力
- 论文可用内容中**未明确说明**使用的 GPU 型号、数量、训练时长、参数量或训练成本。
- 仅可推测：标注约 221k 局部部件可能涉及 VLLM 推理资源，但具体算力开销无法确认。

## 5. 实验数量与充分性
- 摘要称进行了 “extensive experiments”，但给定文本中**无法统计具体实验组数**。
- 未提供数据集划分、消融实验、基线数量、评价指标细节。
- 从摘要看，评估维度覆盖生成质量、有效性和文本-CAD 一致性，方向较全面。
- 但由于正文不可访问，**无法客观判断实验是否充分、公平，是否包含严格消融与统计显著性分析**。

## 6. 主要结论与发现
- GeoCAD 在生成质量、有效性和 text-to-CAD 一致性方面表现有效。
- 在局部几何精度和文本指令遵循方面优于已有方法。
- 互补标注策略能够支持简单与复杂局部部件的几何指令生成。
- 使用 LLM 根据剩余部件和几何指令预测被遮蔽局部部件是可行路径。
- 该方法为 CAD 模型的几何可控生成提供了有效方案，有助于提升设计效率。

## 7. 优点
- **问题定义有价值**：同时强调“局部修改”和“文本几何指令遵循”，贴近实际 CAD 设计需求。
- **互补标注策略**：区分简单部件与复杂部件，分别用顶点方法和 VLLM 方法标注，思路合理。
- **数据规模较大**：标注约 221k 个局部部件，为训练提供支撑。
- **训练与推理设计直观**：训练时随机遮蔽局部部件，推理时允许用户指定局部部件修改。
- **评估维度较全面**：关注生成质量、有效性和文本到 CAD 一致性。

## 8. 不足与局限
- **信息可验证性不足**：提供的 PDF 文本不是正文，无法核实数据集、benchmark、baseline、指标、消融和算力。
- **指令范围可能受限**：摘要提到“预定义几何指令”，说明可能不支持完全开放的自由文本几何描述。
- **标注误差风险**：VLLM 与顶点标注可能引入噪声或误差传播，尤其对复杂 CAD 部件。
- **复杂 CAD 场景未知**：未确认对拓扑有效性、装配约束、长程几何依赖的处理能力。
- **应用限制**：用户需要指定局部部件，非专家使用门槛、交互成本未知。
- **公平性与泛化性未知**：缺少具体实验细节，难以判断方法在不同 CAD 数据分布上的稳健性。

（完）
