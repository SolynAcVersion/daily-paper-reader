---
title: "Populate-A-Scene: Affordance-Aware Human Video Generation"
title_zh: 填充场景：可供性感知的人类视频生成
authors: "Mengyi Shan, Zecheng He, Haoyu Ma, Felix Juefei-Xu, Peizhao Zhang, Tingbo Hou, Ching-Yao Chuang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=hg0lpcHdWk"
tags: ["query:video-gen-rl"]
score: 5.0
evidence: 文本到视频的人类视频生成
tldr: 本文探索文本到视频模型的可供性感知潜力，研究其能否被改造为交互式世界模拟器。给定场景图像与描述人类动作的提示，方法微调模型将人物插入场景，同时保证行为连贯、外观协调、场景和谐与可供性，并从单张场景图像推断人类可供性，无需边界框或人体姿态等显式条件。对交叉注意力热图的深入分析揭示了预训练视频模型内在的可供性感知能力，展示了其作为世界模拟器的潜力。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 探索文本到视频模型能否被改造为交互式世界模拟器，并具备可供性感知能力。
method: 给定场景图像与动作提示，微调模型将人物插入场景，从单图推断可供性，无需边界框或姿态条件。
result: 生成行为连贯、外观协调且符合场景可供性的视频，交叉注意力热图揭示模型内在可供性感知。
conclusion: 展示了预训练视频模型作为交互式世界模拟器的可供性潜力。
---

## Abstract
Can a video generation model be repurposed as an interactive world simulator? We explore the affordance perception potential of text-to-video models by teaching them to predict human-environment interaction. Given a scene image and a prompt describing human actions, we fine-tune the model to insert a person into the scene, while ensuring coherent behavior, appearance, harmonization, and scene affordance. Unlike prior work, we infer human affordance for video generation (i.e., where to insert a person and how they should behave) from a single scene image, without explicit conditions like bounding boxes or body poses. An in-depth study of cross-attention heatmaps demonstrates that we can uncover the inherent affordance perception of a pre-trained video model without labeled affordance datasets.

---

## 论文详细总结（自动生成）

## 说明

- 提供的论文 PDF 正文提取失败：目标 URL 返回 503，Markdown 内容为 “no healthy upstream”。因此，以下总结主要依据论文元数据与摘要，无法覆盖正文中的公式、实验表格、消融细节和算力信息。
- 论文标题：**Populate-A-Scene: Affordance-Aware Human Video Generation**（填充场景：可供性感知的人类视频生成）。
- 作者：Mengyi Shan, Zecheng He, Haoyu Ma, Felix Juefei-Xu, Peizhao Zhang, Tingbo Hou, Ching-Yao Chuang。
- 元数据来源标注：ICLR-2026-Rejected-Public，score 5.0。

## 1. 核心问题与整体含义

- **核心问题**：视频生成模型能否被改造为交互式世界模拟器？具体而言，文本到视频模型是否具备可供性感知能力，能否预测人与环境的交互。
- **研究背景**：传统视频生成多关注外观真实性与运动连贯性；本文进一步要求模型理解场景“可供性”（affordance），即场景中哪里适合插入人物、人物应如何行动。
- **整体含义**：给定一张场景图像和描述人类动作的提示，模型需要将人物插入场景，并保证行为连贯、外观协调、场景和谐以及符合场景可供性。
- **关键挑战**：不依赖边界框、人体姿态等显式条件，而是从单张场景图像中推断人类可供性。这意味着模型需要内化场景功能与交互可能性。
- **目标愿景**：探索预训练视频模型作为交互式世界模拟器的潜力。

## 2. 方法论

- **核心思想**：
  - 将文本到视频模型微调为“人物插入 + 行为生成”的视频生成器。
  - 输入为单张场景图像和描述人类动作的文本提示。
  - 模型需自行推断“人在哪里出现”以及“人应如何行动”，无需边界框、人体姿态或可供性标注。
- **关键技术细节**（据摘要）：
  - 微调模型以将人物插入场景。
  - 同时约束生成结果的行为连贯性、外观协调性、场景和谐性与可供性。
  - 从单张场景图像推断人类可供性，而非依赖显式几何或姿态条件。
  - 通过交叉注意力热图分析，挖掘预训练视频模型内在的可供性感知能力。
  - 无需标注的可供性数据集。
- **算法流程（文字说明）**：
  1. 输入一张场景图像与一段人类动作提示。
  2. 微调文本到视频模型，使其在场景中生成/插入人物。
  3. 优化生成视频，使其满足行为连贯、外观协调、场景和谐与可供性要求。
  4. 生成符合人类-环境交互的视频。
  5. 分析交叉注意力热图，观察模型对可交互区域与动作的注意力分布，从而揭示其内在可供性感知。
- **公式与损失函数**：提供内容中未给出，无法总结。

## 3. 实验设计

- **数据集 / 场景**：
  - 提供内容未列出具体数据集名称、场景类别或数据规模。
  - 摘要仅说明实验基于“单张场景图像”和“描述人类动作的提示”。
- **Benchmark**：
  - 未披露标准 benchmark、评价指标或定量评测协议。
- **对比方法**：
  - 未披露与哪些基线方法、已有视频生成模型或人物插入方法进行比较。
- **实验类型（据摘要可推断）**：
  - 微调后的人类视频生成实验。
  - 交叉注意力热图分析，用于验证预训练视频模型的内在可供性感知。
- **结论**：由于正文不可用，无法确认实验设计的具体细节与公平性。

## 4. 资源与算力

- 提供内容中**未提及** GPU 型号、数量、训练时长、显存、数据规模或微调成本。
- 因此无法总结算力资源与训练开销。
- 这一点也影响对方法可复现性和可扩展性的判断。

## 5. 实验数量与充分性

- 从摘要可见至少包含两类工作：
  - 微调模型进行可供性感知的人类视频生成。
  - 交叉注意力热图分析。
- 是否包含消融实验、用户研究、定量指标、跨数据集测试、不同场景类别测试、失败案例分析等，均未披露。
- 因此无法判断实验数量是否充分，也无法判断对比是否客观、公平。
- 元数据标注 score 为 5.0，来源为 ICLR-2026-Rejected-Public，但这只能作为评审状态的参考，不能替代对实验充分性的分析。

## 6. 主要结论与发现

- 预训练视频模型可能具有内在的可供性感知能力。
- 通过微调，模型可以从单张场景图像和动作提示出发，将人物插入场景并生成交互视频。
- 生成结果在摘要层面被描述为：行为连贯、外观协调、场景和谐且符合可供性。
- 交叉注意力热图可揭示模型内在的可供性感知，而无需标注的可供性数据集。
- 研究展示了视频生成模型作为交互式世界模拟器的潜力。

## 7. 优点

- **任务新颖**：将视频生成从外观/运动合成推进到可供性感知的人-环境交互。
- **条件依赖少**：无需边界框、人体姿态或可供性标注，仅从单张场景图像和文本提示推断。
- **多目标约束**：同时考虑行为连贯、外观协调、场景和谐与可供性，贴近真实交互生成需求。
- **可解释性分析**：利用交叉注意力热图研究模型内在可供性，为理解视频模型提供新视角。
- **应用潜力**：对交互式世界模拟器、具身智能、虚拟内容创作等方向有启发意义。

## 8. 不足与局限

- **正文缺失导致的信息不完整**：PDF 提取失败，无法验证方法、公式、实验与结论细节。
- **实验覆盖未知**：未披露数据集、benchmark、baseline、指标、消融、用户研究等，难以评估泛化性与鲁棒性。
- **可复现性受限**：未提供算力、训练配置、模型架构细节与数据来源。
- **单图可供性推断存在歧义**：单张场景图像可能不足以唯一确定人物位置与行为，复杂场景中尤其如此。
- **物理与交互合理性风险**：摘要未说明是否引入显式物理约束，生成视频可能视觉合理但物理不一致。
- **偏差与伦理风险**：数据未披露，可能存在人体、场景、文化或可供性偏差；人物插入与行为生成也可能带来隐私、安全与滥用风险。
- **应用限制**：目前描述依赖场景图像与动作提示，对多人物、动态场景、长时交互、复杂工具使用等场景的表现未知。
- **评审状态参考**：元数据标注为 ICLR-2026-Rejected-Public，提示该工作可能尚未获得完整同行认可，但具体原因需结合全文判断。

（完）
