---
title: "MotiMotion: Motion-Controlled Video Generation with Visual Reasoning"
title_zh: MotiMotion：具有视觉推理的运动控制视频生成
authors: "Lee Hsin-Ying, Hanwen Jiang, Yiqun Mei, Jing Shi, Ming-Hsuan Yang, Zhixin Shu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b1e8dd22d2dacf67bb57f6b8bfd7cd90fc93e66c.pdf"
tags: ["query:phys-video"]
score: 8.0
evidence: 通过视觉推理实现因果合理、物理可信的运动控制视频生成
tldr: 现有运动控制的图像到视频生成模型往往严格跟随用户提供的稀疏轨迹，导致结果不自然且缺乏因果后果。MotiMotion将运动控制重构为“先推理后生成”框架，利用无训练的视觉语言推理器细化主轨迹并补全合理的次级运动，再通过置信度感知控制机制调节引导强度。实验表明，该方法能够生成具有常识一致性和物理可信度的视频，显著提升运动自然度。这为生成符合物理预期的视频提供了有效手段。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 当前运动控制生成模型过度依赖稀疏或不精确的用户轨迹，容易产生不自然、缺少物理因果的后果。
method: 提出MotiMotion，将运动控制转化为推理后生成，使用视觉语言推理器细化主轨迹并补全次级运动，并引入置信度感知的引导控制。
result: 生成的视频在物理可信度与动作自然度上显著提升，能合理呈现因果相关的次级运动。
conclusion: 通过视觉推理增强运动控制，可以更高效地生成物理上合理、因果连贯的视频。
---

## Abstract
Current motion-controlled image-to-video generation models rigidly follow user-provided trajectories that are often sparse, imprecise, and causally incomplete. 
Such reliance often yields unnatural or implausible outcomes, especially by missing secondary causal consequences. 
To address this, we introduce MotiMotion, a novel framework that reformulates motion control as a reasoning-then-generation problem. 
To encourage causally grounded and commonsense-consistent interactions, we leverage a training-free vision-language reasoner to refine image-space coordinates of primary trajectories and to hallucinate plausible secondary motions. 
To further improve motion naturalness, we propose a confidence-aware control scheme that modulates guidance strength, enabling the model to closely follow high-confidence plans while correcting artifacts under low-confidence inputs with its internal generative priors. 
To support systematic evaluation, we curate a new image-to-video benchmark, MotiBench, consisting of interaction-centric scenes where new events are triggered by motion. 
Both VLM-based evaluation and a human study on MotiBench demonstrate that MotiMotion produces videos with more plausible object behaviors and interaction, and is preferred over existing approaches.

---

## 论文详细总结（自动生成）

# MotiMotion 论文总结

## 1. 核心问题与整体含义

- **研究动机**：当前运动控制的图像到视频生成模型严格跟随用户提供的运动轨迹，但这些轨迹往往是**稀疏、不精确且因果不完整**的，导致生成视频中出现不自然、物理不合理的结果，尤其缺乏由主要动作引发的**次级因果后果**（如碰撞引发的连锁反应、受力后的自然反馈等）。
- **核心问题**：如何让运动控制生成模型不再机械地“执行指令”，而是能够**理解运动背后的物理规律与常识因果**，生成自然、真实、因果连贯的视频。
- **整体含义**：该论文将运动控制从“轨迹拟合”问题重新定义为“**推理后再生成**”问题，标志着运动控制视频生成从低层次坐标拟合向高层次场景理解与物理推理的转变。

## 2. 方法论

### 核心思想
提出 **MotiMotion** 框架，采用 **“推理-生成”两阶段范式**：先利用视觉语言模型进行运动推理，再将推理结果转化为可控的生成信号。

### 关键技术细节
1. **无训练的视觉语言推理器（Training-free Vision-Language Reasoner）**
   - 用于**细化主运动轨迹**的图像空间坐标，修正稀疏或不精确的用户输入。
   - 同时**补全合理的次级运动**（即“脑补”由主运动因果引发的后续动作），使生成视频具备常识一致性和物理可信度。
2. **置信度感知控制方案（Confidence-aware Control Scheme）**
   - 动态调节引导强度（guidance strength）：对于模型高置信度的运动规划，严格跟随；对于低置信度的输入，则更多依赖模型内部的生成先验进行修正，减少伪影和不自然结果。

> 文中未提供具体的数学公式，流程上可概括为：**输入图像 + 主轨迹 → VLM推理（细化主轨迹 + 生成次级运动）→ 置信度评估 → 引导视频生成模型**。

## 3. 实验设计

### 基准与数据集
- 作者构建了新基准 **MotiBench**，专门针对**以交互为中心的场景**（即运动触发新事件的场景），用于系统性评估运动控制生成的效果。

### 评估方式
- **基于VLM的自动化评估**：利用视觉语言模型对生成视频进行打分或判断。
- **人工评估（Human Study）**：由人类标注者对生成视频进行主观偏好判断。

### 对比方法
- 与现有的运动控制图像到视频生成方法进行了对比，但摘要中未具体列出基线方法名称。

## 4. 资源与算力

- **论文中未明确说明**所使用的GPU型号、数量、训练时长等算力信息。
- 值得注意的是，论文强调其视觉语言推理器是**无训练（training-free）** 的，这暗示该方法在推理阶段可能不需要额外的训练成本，但整体生成模型和评估过程的计算开销未披露。

## 5. 实验数量与充分性

- 从摘要可见，实验主要围绕 **MotiBench** 基准展开，包含**VLM评估**和**人工评估**两个维度。
- **充分性评价**：
  - **积极面**：包含自动评估和人工评估双重验证，且使用了专门构建的交互中心基准，针对性较强。
  - **不足面**：摘要未提及消融实验的细节（如置信度控制模块的独立贡献、VLM推理器不同设计的影响）、未明确基线数量，也未展示跨不同场景类型（如非交互场景）的泛化能力。整体来看，实验设计显示出较好的初步验证效果，但公开信息不足以全面判断其广泛适用性。

## 6. 主要结论与发现

- MotiMotion 生成的视频在**物体行为合理性**和**交互自然度**上显著优于现有方法。
- 视觉推理的引入能有效生成**因果合理的次级运动**，使视频呈现更真实的物理交互。
- 置信度感知控制机制能够提升运动自然度，在低质量输入下仍能生成合理的视频。

## 7. 优点

- **问题定义新颖**：将运动控制重新定义为推理-生成问题，切入角度具有创新性。
- **无训练设计**：VLM推理器无需额外训练，即插即用，便于部署和推广。
- **因果感知**：显式建模次级运动，突破了传统方法只关注主轨迹拟合的局限。
- **控制策略精细**：置信度感知的引导方案在人机协同上设计合理——高确信时严格服从用户，低确信时依赖先验纠错。
- **评测基准配套**：构建了专门针对交互场景的 MotiBench，为后续研究提供了评测工具。

## 8. 不足与局限

- **信息缺失**：论文提供的摘要和元数据信息有限，无法评价其技术细节的完整性和方法的可复现性。
- **数据覆盖有限**：MotiBench 聚焦交互中心场景，对非交互或静态场景的生成效果未做说明，泛化能力有待验证。
- **指标偏差风险**：VLM 评估可能受大模型自身偏见影响；人工评估的样本量和标注者构成未披露，存在主观偏差风险。
- **算力不可知**：未公开训练/推理的资源消耗，难以评估其实际应用成本。
- **因果正确性局限**：VLM“脑补”的次级运动仍可能出错，尤其对于复杂物理规则（如流体、弹性碰撞等），缺乏物理约束的推理可能生成看似合理但物理错误的运动。

（完）
