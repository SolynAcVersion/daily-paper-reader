---
title: Can Text-to-Video Models Generate Realistic Human Motion?
title_zh: 文生视频模型能否生成真实的人体运动？
authors: "Zhengqing Yuan, Yunhong He, Xiaoyu Ma, Zixuan Weng, Rong Zhou, Weixiang Sun, Mengyu Wang, Lifang He, Lichao Sun, Yanfang Ye"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=LUXsDBYTkp"
tags: ["query:phys-video"]
score: 8.0
evidence: 系统评测文生视频中人体运动的物理真实性与合理性
tldr: 该研究系统考察了Pika、Gen-3、Sora等文生视频模型能否生成真实人体运动，发现生成人物常出现脚滑、关节过伸、肢体不同步等“看似正常但动起来不对”的物理不合理现象。作者指出这些运动学伪影不仅影响视觉体验，还会造成安全、临床分析和仿真训练方面的风险，并呼吁将人体运动物理合理性作为重要评估维度。该工作为视频模型的人体运动评测与改进提供了依据。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 文生视频生成的人体动作常出现脚滑、关节过伸等物理上不合理的运动伪影，影响安全与下游应用。
method: 系统性评估现有T2V模型生成人体运动的真实性与物理合理性，分析运动学伪影及其危害。
result: 发现生成的人体运动普遍存在非物理的关节运动和时间不一致问题。
conclusion: 强调评估和改进T2V模型人体运动物理合理性的必要性。
---

## Abstract
Recent advances in text-to-video (T2V) generation have yielded impressive progress in resolution, duration, and prompt fidelity, with models such as Pika, Gen-3, and Sora producing clips that appear compelling at first glance. Yet, in everyday use and public demos, generated people often “look right but move wrong,” exhibiting artifacts like foot sliding, joint hyperextension, and desynchronized limbs. Such failures are not cosmetic: 1) unsafe motions can be copied by viewers, especially juveniles, raising injury risks; 2) in clinical and sports contexts, implausible kinematics corrupt analytics for angle, cadence, and phase, causing misdiagnosis and unsafe return-to-play; and 3) in simulation pipelines, non-physical motion distributions contaminate training and evaluation, degrading sim-to-real transfer. However, existing benchmarks remain inadequate: 1) they lack kinematics awareness, rewarding visual resemblance while joint trajectories violate physiological ranges; 2) they lack rhythm- and body-level temporal metrics, overlooking gait-cycle timing, symmetry, and inter-limb coordination; and 3) they fail to disentangle camera from body motion, letting pans and zooms mask biomechanical errors. To address these gaps, we present \textbf{Movo}, the first kinematics-centric benchmark for T2V motion realism. Movo unifies three components: 1) a posture-focused dataset with camera-aware prompts that isolate representative upper- and lower-body actions; 2) skeletal-space metrics, Joint Angle Change (JAC), Dynamic Time Warping (DTW), and Motion Consistency Metric (MCM), that operationalize biomechanical plausibility across joints, rhythms, and constraints; and 3) human validation studies that calibrate thresholds and show strong correlation between skeletal scores and perceived realism. Evaluating 14 leading T2V models reveals persistent gaps: some excel in specific motions but struggle with cross-action consistency, and performance varies widely between open-source and proprietary systems. Movo provides a rigorous, interpretable foundation for improving human motion generation and for integrating biomechanical realism checks into model development, selection, and release workflows. The code and scripts are available at Supplementary Material.

---

## 论文详细总结（自动生成）

## 论文总结：Can Text-to-Video Models Generate Realistic Human Motion?

### 1. 论文的核心问题与整体含义

- **研究背景**：文本到视频（T2V）生成技术近年来发展迅猛，Pika、Gen-3、Sora 等模型在分辨率、时长和提示词遵循度上取得了显著进步，生成的视频初看极具吸引力。
- **核心问题**：尽管视频观感良好，生成人物却普遍存在"看似正常、动起来不对"的问题，典型伪影包括：
  - 脚部滑动（foot sliding）
  - 关节过伸（joint hyperextension）
  - 肢体不同步（desynchronized limbs）
- **问题严重性**：作者强调这类缺陷并非单纯的视觉瑕疵，而是具有实质性的现实影响：
  - **安全隐患**：不安全的运动模式可能被观众（尤其是青少年）模仿，增加受伤风险；
  - **临床与运动分析风险**：不符合物理规律的关节运动（角度、节奏、相位）会污染分析数据，导致误诊和不安全的恢复训练决策；
  - **仿真训练风险**：非物理的运动分布会污染仿真管线中的训练和评估，降低sim-to-real迁移效果。
- **现有基准的不足**：
  1. 缺乏运动学感知，只奖励视觉相似性，而关节轨迹可能违反生理学范围；
  2. 缺乏节奏级和身体级时间指标，忽略了步态周期节奏、对称性和肢体间协调性；
  3. 未将相机运动与身体运动分离，镜头的平移和缩放可能掩盖生物力学错误。

### 2. 论文提出的方法论

- **核心思想**：提出 **Movo**——首个以运动学为中心（kinematics-centric）的 T2V 运动真实性基准，将生物力学合理性纳入视频生成模型的评估框架。
- **三大核心组件**：
  1. **姿态聚焦数据集（Posture-focused dataset）**
     - 包含具有相机感知提示词的视频样本；
     - 特意设计以隔离具有代表性的上肢和下肢动作。
  2. **骨架空间指标（Skeletal-space metrics）**——三个关键指标：
     - **JAC（Joint Angle Change，关节角度变化）**：衡量各关节在时间序列上的角度变化是否符合生物力学规律；
     - **DTW（Dynamic Time Warping，动态时间规整）**：用于评估运动节奏和时序对齐，检测步态周期定时是否正确；
     - **MCM（Motion Consistency Metric，运动一致性指标）**：衡量运动约束的一致性，包括关节限制、肢体间协调和对称性。
  3. **人工验证研究（Human validation studies）**：
     - 用于校准各指标的阈值；
     - 验证骨架评分与人类感知真实性之间的强相关性。
- **技术流程**：提取生成视频中的人物骨架 → 在骨架空间计算上述三类运动学指标 → 与人类感知标注进行相关性分析和阈值校准 → 最终输出可解释的运动真实性评分。

### 3. 实验设计

- **评估对象**：共评估 **14 个领先的 T2V 模型**，涵盖开源和专有系统。
- **任务类型**：覆盖代表性的上肢和下肢动作，测试模型在不同动作类型下的运动生成能力。
- **Benchmark 构成**：
  - 姿态聚焦数据集 + 相机感知提示词；
  - 三类骨架空间指标（JAC、DTW、MCM）作为自动评价标准；
  - 人类感知实验用于校准和验证指标的有效性。
- **分析方法**：不仅比较模型的总分，还分析不同模型在不同动作类型上的表现差异，考察跨动作一致性。

### 4. 资源与算力

- **文中未见明确说明**：论文摘要中未提及使用的 GPU 型号、数量、训练时长或评估所需的算力资源。
- 推测：由于本文主要是评估基准（benchmark）而非训练新模型，算力需求主要体现在对 14 个 T2V 模型的推理和骨架提取上，但具体数据无法从摘要中获得。

### 5. 实验数量与充分性

- **实验规模**：覆盖 14 个主流 T2V 模型，规模较为可观；包含多种上下肢动作类型和三类互补的量化指标，外加人工验证实验。
- **充分性评估**：
  - **优点**：多模型对比 + 多维指标 + 人工校准，形成了相对完整的评估闭环；
  - **潜在不足**：摘要中未明确说明具体动作类别数量、视频样本量、人工评估者人数及统计显著性检验细节，实验完整性难以完全判定；
  - **公平性**：分为开源和专有系统对比，表明考虑了模型来源差异，但在提示词选择和评估环境标准化方面未给出细节。

### 6. 论文的主要结论与发现

- **持续存在明显缺陷**：即使是最先进的 T2V 模型，生成的人体运动仍然普遍存在非物理的关节运动和时间不一致问题。
- **模型间差异显著**：某些模型在特定动作上表现优异，但跨动作的泛化一致性不足。
- **开源 vs 专有差异明显**：性能在开源和专有系统之间存在显著差异。
- **现有评估指标严重缺失**：传统视觉相似性指标无法捕捉运动学错误，必须引入骨架层面的运动学度量。
- **Movo 的有效性**：Movo 的骨架评分与人类感知真实性高度相关，可作为开发、选择和发布 T2V 模型时的自动化筛查工具。

### 7. 优点

- **视角新颖且重要**：首次系统地将生物力学/运动学合理性引入 T2V 模型评估，弥补了现有视觉质量评估的盲区。
- **指标设计有理论支撑**：JAC、DTW、MCM 分别从关节角度、时序节奏和运动约束三个互补维度刻画运动真实性，覆盖面广。
- **人类验证闭环**：引入人工感知实验校准阈值，避免了纯自动指标与实际体验脱节的问题。
- **实际应用导向**：明确指出运动学伪影在安全、医疗和仿真领域的实际危害，增强研究的社会价值。
- **可复现性**：提供代码和脚本（Supplementary Material）。

### 8. 不足与局限

- **数据集范围**：聚焦于代表性的上下肢动作，是否覆盖复杂全身协调运动、多人互动、物体交互等更复杂场景尚不清楚。
- **指标覆盖**：虽然涵盖关节角度、节奏和一致性，但对接触力、重力效应、动力学（kinetics）层面的物理真实性未作深入衡量。
- **评估模型范围**：14 个模型虽多，但具体版本和时间点未知，部分闭源模型（如 Sora）的评估条件可能受限。
- **算力与资源报告缺失**：未报告评估所需的计算资源，不利于其他研究者复现评估成本估算。
- **实验细节不足**：人工验证的规模、评估者背景、统计方法等信息未在摘要中呈现，无法全面评估研究的稳健性。
- **提示词设计**："相机感知提示词"的具体设计策略和可能引入的偏差未被讨论。

---

（完）
