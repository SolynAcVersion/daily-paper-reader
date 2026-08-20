---
title: Physics-Grounded Motion Forecasting via Equation Discovery for Trajectory-Guided Image-to-Video Generation
title_zh: 基于方程发现的物理基运动预测与轨迹引导的图像到视频生成
authors: "Tao Feng, Xianbing Zhao, Zhenhua Chen, Tien-Tsin Wong, Hamid Rezatofighi, Gholamreza Haffari, Lizhen Qu"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=dDvLeDjBOa"
tags: ["query:phys-video"]
score: 9.0
evidence: 通过符号回归发现运动方程，将轨迹引导的图生视频建立在物理规律之上
tldr: 该论文指出视频生成模型虽视觉逼真却缺乏物理对齐，难以复现真实物体动态。作者提出将符号回归与轨迹引导的图像到视频（I2V）模型相结合的框架：先从输入视频提取运动轨迹，再用检索式预训练增强符号回归，发现运动方程并进行物理基底的视频预测。实验显示该方法能提升生成视频的物理规律符合度，为物理感知视频生成提供了新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频生成模型仅学习统计相关性，缺少物理机制刻画，导致物体运动不合真实物理规律。
method: 提取视频运动轨迹，利用检索式预训练增强符号回归，发现运动方程并引导图像到视频生成。
result: 发现运动方程并用于轨迹引导的视频预测，提升了生成视频的物理对齐度与运动准确性。
conclusion: 融合方程发现与视频生成能显著改善物理一致性，为物理可解释的视频生成奠定基础。
---

## Abstract
Recent advances in video generation models have achieved remarkable visual realism. However, these models typically lack accurate physical alignment, failing to replicate real-world dynamics in object motion. This limitation arises primarily from their reliance on learned statistical correlations rather than capturing mechanisms adhering to physical laws. To address this issue, we introduce a novel framework that integrates symbolic regression (SR) and trajectory-guided image-to-video (I2V) models for physics-grounded video forecasting. Our approach extracts motion trajectories from input videos, uses a retrieval-based pre-training mechanism to enhance symbolic regression, and discovers equations of motion to forecast physically accurate future trajectories. These trajectories then guide video generation without requiring fine-tuning of existing models. We evaluate our framework on scenarios from classical mechanics, including spring-mass, pendulums, and projectile motions. In these settings, our method successfully recovers ground-truth analytical equations and improves the physical alignment of generated videos compared to baseline methods. This work provides a first step toward integrating equation discovery with video generation.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：当前视频生成模型虽然能够生成高度逼真的视觉画面，但在物理层面的表现存在显著缺陷，物体运动常常不符合真实世界的物理规律。
- **根源分析**：作者认为这一局限性主要源于视频生成模型依赖的是从数据中学到的统计相关性，而非对物理机制的直接建模——模型“看到”物体运动模式，却不“理解”支配运动背后的物理定律。
- **整体含义**：该工作旨在为视频生成赋予“物理可解释性”，让生成过程不仅仅满足视觉相似性，还能在运动学层面遵循真实物理法则，从而弥合视觉生成与物理仿真之间的鸿沟。

### 2. 方法论：核心思想、关键技术细节与算法流程

- **核心思想**：将**符号回归**（Symbolic Regression, SR）与**轨迹引导的图像到视频生成**（Trajectory-Guided Image-to-Video, I2V）相结合，用“发现出来的方程”替代纯粹的统计模式，使视频预测具备物理基础。
- **整体算法流程**（按文字描述分解如下）：
  1. **轨迹提取**：从输入视频中提取物体的运动轨迹（如位置随时间变化的序列数据）；
  2. **检索式预训练增强**：引入基于检索的预训练机制，辅助符号回归模型更高效、更准确地搜索符号表达式空间；
  3. **方程发现**：利用增强后的符号回归从运动轨迹中发现解析的运动方程（如微分方程或闭式表达式）；
  4. **轨迹预测**：基于发现的运动方程，外推出物理上准确的未来轨迹；
  5. **引导视频生成**：将预测得到的未来轨迹作为条件信号，引导 I2V 模型生成后续视频帧。
- **关键优势**：整个过程**无需对现有视频生成模型进行任何微调**（fine-tuning-free），符号回归与生成模型之间以轨迹为接口，实现即插即用式的模块化集成。

### 3. 实验设计：数据集 / 场景、Benchmark 与对比方法

- **评估场景**：仅涉及**经典力学**领域，具体包括三类物理系统：
  - 弹簧-质量系统（spring-mass）
  - 摆运动（pendulums）
  - 抛体运动（projectile motions）
- **Benchmark**：以这些物理系统是否能够恢复“真值解析方程”（ground-truth analytical equations）作为符号回归模块的核心评估标准，同时以生成视频的**物理对齐度**（physical alignment）作为视频生成模块的评估指标。
- **对比方法**：论文提到与基线方法进行了对比，但摘要中未明确列出具体的基线方法名称（如通用视频生成模型或纯数据驱动的轨迹预测方法是否被用作baseline，需要查阅全文才能确认）。

### 4. 资源与算力

- **未明确披露**：当前提供的摘要与元数据中**没有提及**任何关于 GPU 型号、GPU 数量、训练时长、显存占用或总体计算开销的具体信息。
- 仅能推断的是：由于方法无需微调现有 I2V 模型，符号回归部分的计算成本相对可控，但具体的算力需求仍需查阅论文全文中的实验设置章节。

### 5. 实验数量与充分性评估

- **实验数量**：从摘要来看，实验覆盖了三个经典力学场景，且各场景均验证了“方程恢复能力”和“生成视频物理对齐度”两个维度。
- **充分性分析**（客观评价）：
  - **优点**：三个场景覆盖了不同类型的动力系统（周期性振动、非线性摆动、二维轨迹运动），具备一定的物理多样性；且同时验证了“方程发现”与“视频生成”两个环节，形成闭环评估。
  - **不足**：实验覆盖范围较窄，仅限于理想化的解析可解系统，未涉及真实世界视频（如野外场景、流体、碰撞、多物体交互等）；在摘要中未提及消融实验（如检索式预训练的有效性、轨迹质量对方程恢复的影响等），实验的完整性和深度有限。

### 6. 主要结论与发现

- 该方法在弹簧-质量、摆运动、抛体运动等经典力学场景中，能够**成功恢复真值解析方程**，验证了符号回归与检索式预训练结合的有效性。
- 基于发现的方程进行轨迹预测，并引导 I2V 视频生成，显著**提升了生成视频的物理对齐度**，优于基线方法，使生成物体的运动更符合真实物理规律。
- 作者将这项工作定位为“将方程发现与视频生成相结合的第一步”，具有探索性和开创性意义。

### 7. 优点

- **创新性强**：首次将符号回归（可解释的物理建模工具）与大规模视频生成模型衔接，开辟了“物理可解释视频生成”的新方向。
- **模块化设计**：方程发现与视频生成通过轨迹解耦，解耦设计使得该方法**无需微调现有生成模型**，工程落地成本低、兼容性好。
- **可解释性**：相比于黑盒式的物理约束（如物理信息神经网络），发现显式运动方程提供了人类可读、可验证的物理解释，增强了模型的可信度与泛化潜力。
- **方法逻辑自洽**：“提取轨迹→发现方程→预测轨迹→引导生成”这一链条逻辑清晰，每一步都有明确的物理意义。

### 8. 不足与局限

- **实验覆盖有限**：仅验证了理想化的经典力学系统，未测试复杂场景（如流体、弹性体、多物体碰撞、非刚体运动等），对真实世界复杂动态的泛化能力尚未得到验证。
- **轨迹提取的误差风险**：从视频中提取轨迹的质量直接影响方程发现的准确性，但摘要中未讨论轨迹提取误差的鲁棒性及噪声敏感性问题。
- **SDE表达能力的边界**：符号回归对可发现方程的复杂度有固有限制——若真实动力学过程无法用简洁的解析式刻画，该方法可能失效。
- **对比基线未披露**：摘要中未列出具体基线方法，导致难以判断性能提升的幅度与公平性。
- **算力与效率信息缺失**：未披露训练/推理资源消耗，难以评估方法在大规模实际应用中的可行性。
- **应用限制**：当前框架主要面向以物体运动为主体的视频，对于摄像机运动、光影变化、多智能体复杂交互等场景的支持尚不明确。

（完）
