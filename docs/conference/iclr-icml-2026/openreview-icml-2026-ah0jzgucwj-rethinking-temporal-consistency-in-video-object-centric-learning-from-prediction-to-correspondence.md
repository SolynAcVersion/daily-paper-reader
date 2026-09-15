---
title: "Rethinking Temporal Consistency in Video Object-Centric Learning: From Prediction to Correspondence"
title_zh: 重思视频对象中心学习中的时序一致性：从预测到对应
authors: "Zhiyuan Li, Rongzhen Zhao, Wenyan Yang, Wenshuai Zhao, Pekka Marttinen, Joni Pajarinen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/dcd77eaaefe18894b3c15cb1bd0feb33d94061de.pdf"
tags: ["query:frame-dist"]
score: 5.0
evidence: 维持帧到帧的身份与时序一致性
tldr: 针对视频对象中心学习中依赖学习到的动力学模块预测未来对象表示来维持时序一致性的做法，本文指出这些预测器只是离散对应问题的昂贵近似。方法提出Grounded Correspondence框架，用确定性二分匹配替代学习到的转移函数，从冻结骨干特征的显著区域初始化槽，从而维持帧到帧的身份一致。该工作质疑了预测式建模帧间关系的必要性，为帧间对应与时序一致性提供了新视角。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 学习到的动力学预测器只是离散对应问题的昂贵近似。
method: 提出Grounded Correspondence，用确定性二分匹配替代学习转移函数。
result: 从冻结骨干特征初始化槽并维持帧到帧身份一致。
conclusion: 质疑预测式建模帧间关系的必要性，提供对应视角。
---

## Abstract
The de facto approach in video object-centric learning maintains temporal consistency through learned dynamics modules that predict future object representations, called slots. We demonstrate that these predictors function as expensive approximations of discrete correspondence problems. Modern self-supervised vision backbones already encode instance-discriminative features that distinguish objects reliably. Exploiting these features eliminates the need for learned temporal prediction. We introduce Grounded Correspondence, a framework that replaces learned transition functions with deterministic bipartite matching. Slots initialize from salient regions in frozen backbone features. Frame-to-frame identity is maintained through Hungarian matching on slot representations. The approach requires zero learnable parameters for temporal modeling yet achieves competitive performance on MOVi-D, MOVi-E, and YouTube-VIS. Project page: https://magenta-sherbet-85b101.netlify.app/

---

## 论文详细总结（自动生成）

> 说明：由于给定 PDF 提取失败（返回 503 / “no healthy upstream”），以下总结主要依据论文摘要与元数据；未在提供内容中出现的信息，将明确标注为“未说明”。

# 论文总结：Rethinking Temporal Consistency in Video Object-Centric Learning: From Prediction to Correspondence

## 1. 核心问题与整体含义
- **研究领域**：视频物体中心学习（video object-centric learning），通常用“槽位”（slots）表示视频中的物体。
- **主流做法**：通过学习到的动力学模块预测未来物体表示，从而在帧间维持时间一致性。
- **核心质疑**：作者认为，这类学习到的预测器本质上只是离散对应问题的高成本近似。
- **关键观察**：现代自监督视觉骨干网络已经能够编码具有实例判别性的特征，可较可靠地区分不同物体。
- **整体含义**：如果冻结骨干特征已足够好，则不必学习昂贵的时序预测；时间一致性可以从“预测”重新表述为“对应”。这为该领域提供了更简洁的建模路径。

## 2. 方法论：Grounded Correspondence
- **核心思想**：用确定性二分匹配替代学习到的转移函数，从而在帧间维持物体身份。
- **框架名称**：Grounded Correspondence。
- **关键流程**：
  1. 使用**冻结的自监督视觉骨干**提取每帧特征。
  2. 槽位从冻结骨干特征中的**显著区域**初始化。
  3. 在槽位表示上执行**匈牙利匹配**（Hungarian matching），建立帧与帧之间的物体对应。
  4. 通过匹配结果维持物体身份，时间建模部分**零可学习参数**。
- **算法流程文字说明**：
  - 对相邻帧，将上一帧槽位与当前帧候选槽位/显著区域表示构建匹配代价。
  - 使用匈牙利算法求全局最优的一对一对应关系。
  - 根据对应关系传递槽位身份，避免训练动力学预测器。
- **公式细节**：摘要未给出具体公式、代价函数形式或匹配矩阵定义，因此无法进一步展开。

## 3. 实验设计
- **数据集 / 场景**：
  - MOVi-D
  - MOVi-E
  - YouTube-VIS
- **任务背景**：
  - MOVi-D、MOVi-E 通常用于合成视频中的物体中心学习。
  - YouTube-VIS 通常用于真实视频中的视频实例分割/实例级理解。
- **Benchmark**：摘要未明确说明具体评价指标、协议或 benchmark 名称。
- **对比方法**：摘要仅称达到“competitive performance”，但未列出具体基线方法；可推断对比对象主要是依赖学习动力学模块维持时间一致性的物体中心学习方法。
- **消融实验**：摘要未提及。

## 4. 资源与算力
- 提供的摘要与元数据中**未说明** GPU 型号、数量、训练时长、参数量或推理成本。
- 因此无法总结算力使用情况。
- 仅能确认该方法强调时间建模部分“零可学习参数”，但这不等于整体训练或推理不需要算力。

## 5. 实验数量与充分性
- 可确认的实验：在 MOVi-D、MOVi-E、YouTube-VIS 三个数据集上报告了主结果。
- 未说明的内容：
  - 具体做了多少组实验；
  - 是否有消融实验；
  - 是否比较不同骨干、不同匹配代价、不同初始化策略；
  - 是否评估长期一致性、遮挡、物体出现/消失等场景；
  - 是否有统计显著性检验。
- **充分性判断**：仅凭摘要无法判断实验是否充分。缺少量化指标、基线列表和消融细节，难以评估其客观性与公平性。
- **公平性风险**：若与基线使用相同骨干、相同槽位设置和相同训练预算，则比较较公平；但摘要未说明这些控制条件。

## 6. 主要结论与发现
- 视频物体中心学习中的学习型动力学预测器并非必要。
- 离散对应问题可以用确定性二分匹配有效替代。
- 冻结的自监督视觉骨干已能提供可靠的实例判别特征。
- 所提 Grounded Correspondence 在 MOVi-D、MOVi-E 和 YouTube-VIS 上取得有竞争力的性能。
- 时间一致性建模可以从“预测未来表示”转向“帧间对应匹配”。

## 7. 优点
- **方法简洁**：用确定性匹配替代学习到的转移函数，减少时序建模的复杂性。
- **参数高效**：时间建模部分零可学习参数，避免训练昂贵的动力学模块。
- **利用现代自监督特征**：顺应自监督视觉骨干的发展，避免重复学习实例判别能力。
- **可解释性较强**：匈牙利匹配提供明确的帧间对应关系。
- **跨数据集验证**：同时在合成数据 MOVi-D/MOVi-E 和真实数据 YouTube-VIS 上评估，具备一定泛化信号。
- **概念贡献**：重新审视领域默认假设，提出“从预测到对应”的新视角。

## 8. 不足与局限
- **信息不完整**：PDF 提取失败，无法核验全文；当前总结仅基于摘要和元数据。
- **缺少量化结果**：未提供具体指标、提升幅度或失败案例。
- **缺少算力与效率分析**：未说明训练/推理成本，虽然时间建模零参数，但逐帧骨干特征和匹配仍可能带来开销。
- **依赖冻结骨干质量**：若骨干特征在遮挡、运动模糊、外观剧变或拥挤场景下不稳定，匹配可能出错。
- **初始化敏感**：槽位由显著区域初始化，显著区域检测失败可能影响后续对应。
- **匹配机制限制**：匈牙利匹配需要定义代价矩阵和槽位数量，可能对超参数、物体数量变化和长期视频敏感。
- **错误传播风险**：确定性匹配一旦发生错误，可能缺少学习型动力学模块的纠错能力。
- **实验覆盖未知**：未说明消融、长期一致性、新物体出现/消失、复杂交互等挑战场景。
- **公平比较风险**：具体基线、训练预算和实现细节未给出，无法完全判断结论的普适性。

（完）
