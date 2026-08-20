---
title: What Happens Next? Anticipating Future Motion by Generating Point Trajectories
title_zh: 接下来会发生什么？通过生成点轨迹预测未来运动
authors: "Gabrijel Boduljak, Laurynas Karazija, Iro Laina, Christian Rupprecht, Andrea Vedaldi"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=t1vMYl1yhe"
tags: ["query:phys-video"]
score: 5.0
evidence: 通过生成稠密点轨迹预测未来运动，揭示视频生成模型物理动态预测能力的不足
tldr: 该论文关注从单张图像预测未来运动的问题，将任务建模为条件生成稠密点轨迹，并采用类似视频生成器的架构输出轨迹而非像素。该方法能捕捉场景级动态与不确定性，比传统回归器和生成器预测更准确多样。作者还发现当前最先进的视频生成模型在单图运动预测上表现不佳，说明其物理世界模型能力仍有欠缺。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 单图运动预测难以观测速度、受力等参数，现有回归器和生成器预测效果有限。
method: 将未来运动预测建模为稠密轨迹网格的条件生成，利用视频生成器架构输出点轨迹。
result: 生成的轨迹在地图级动态和不确定性上优于以往方法，并发现视频生成模型在此任务上不足。
conclusion: 点轨迹生成可作为物理运动预测的有效工具，同时暴露了视频生成模型物理推理的局限。
---

## Abstract
We consider the problem of forecasting motion from a single image, i.e., predicting how objects in the world are likely to move, without the ability to observe other parameters such as the object velocities or the forces applied to them. We formulate this task as conditional generation of dense trajectory grids with a model that closely follows the architecture of modern video generators but outputs motion trajectories instead of pixels. This approach captures scene-wide dynamics and uncertainty, yielding more accurate and diverse predictions than prior regressors and generators. Although recent state-of-the-art video generators are often regarded as world models, we show that they struggle with forecasting motion from a single image, even in simple physical scenarios such as falling blocks or mechanical object interactions, despite fine-tuning on such data. We show that this limitation arises from the overhead of generating pixels rather than directly modeling motion.

---

## 论文详细总结（自动生成）

# 论文总结：What Happens Next? Anticipating Future Motion by Generating Point Trajectories

## 1. 核心问题与整体含义（研究动机与背景）

- **研究任务**：本文关注的是**单张图像中的未来运动预测（forecasting motion from a single image）**问题，即：仅根据一张静态图像，预测场景中物体接下来如何运动。
- **核心难点**：在单张图像设定下，模型无法观测到决定物体运动的关键物理参数，如**物体速度、质量、受力情况、材料属性**等，这使得运动预测在本质上具有高度不确定性和多解性。
- **背景动机**：随着视频生成模型（Video Generation Models）的发展，业界普遍把它们视作潜在的"世界模型"（World Models）。本文对这一观点提出了系统性检验——**视频生成模型在单图运动预测任务上表现如何？能否借助其架构来解决运动预测问题？**
- **整体含义**：论文将运动预测重新建模为**稠密点轨迹的条件生成**问题，既是为了提出一种更好的运动预测方法，也是在**重新审视"视频生成即世界模型"这一流行论断**，揭示生成像素与直接建模运动之间的根本差异。

## 2. 论文提出的方法论

- **核心思想**：与其通过生成视频像素来隐式地表达运动，不如**直接在运动本身的表征——稠密点轨迹（dense trajectory grids）**——上进行条件生成，从而绕开像素生成带来的巨大开销和无关细节。
- **任务形式化**：
  - 输入：单张静态图像。
  - 输出：覆盖场景的一组稠密点（对应场景中不同物体和表面位置）在未来一段时间内的运动轨迹。
  - 该任务被建模为**条件生成问题**：给定图像条件下，生成轨迹的分布，而非单一确定性的预测结果。
- **模型架构**：
  - 模型**紧密沿用现代视频生成器（video generator）的架构**，但将输出模态从"像素帧序列"替换为"点轨迹"。
  - 即：保留视频生成模型在时序建模、空间推理上的能力，但让模型在低维的轨迹空间中输出，而非高维像素空间。
- **关键优势所在**：轨迹空间比像素空间更直接地对应物理运动本身，降低了生成任务的复杂度，同时能够更好地刻画**场景级别的动态（scene-wide dynamics）**与**多模态不确定性（uncertainty）**。
- **说明**：由于提取到的论文文本仅包含摘要，未包含正文中的公式与具体网络模块细节，因此无法给出更具体的损失函数定义与算法伪代码。

## 3. 实验设计

- **数据与场景**（依据摘要中提及的例子）：
  - **下落方块（falling blocks）**：测试对重力、碰撞等基本物理规律的感知。
  - **机械物体交互（mechanical object interactions）**：测试对齿轮、杠杆等机械传动机制的推理能力。
  - 这些场景属于**简单物理场景**，被用于检验模型对直观物理（intuitive physics）的理解。
- **Benchmark**：摘要中未明确指出具体数据集名称（如 CLEVRER、Physion 等），但从场景描述看，属于**合成物理视频基准**的典型设定。
- **对比方法**：
  - **传统的回归器（prior regressors）**：输出确定性轨迹预测的模型。
  - **生成器（prior generators）**：此前已有的轨迹生成方法。
  - **当前最先进的视频生成模型（state-of-the-art video generators）**：被当作"世界模型"的代表，测试其直接用于单图运动预测的性能。
- **主要对比结论**：本文方法在预测**准确性和多样性**上优于传统回归器和生成器；而视频生成模型在该任务上表现不佳，即使经过微调也如此。

## 4. 资源与算力

- **明确说明**：从可获取的文本内容（摘要、tldr）中，**未提及任何有关GPU型号、数量、训练时长、参数量等计算资源信息**。
- **推断**：考虑到本文使用了现代视频生成器架构并进行微调实验，推测其训练成本不低，但具体细节需查阅论文正文的实验章节才能获知。

## 5. 实验数量与充分性

- **实验数量**：由于仅能获取摘要和元数据，无法得知完整的实验组数量。从摘要信息中可以确认的实验维度包括：
  1. 本文方法 vs. 传统回归器
  2. 本文方法 vs. 先前的生成器
  3. 本文方法 vs. 现成视频生成模型（零样本与微调后）
  4. 在至少两类物理场景（下落方块、机械交互）上的验证
- **充分性评估**：
  - 从摘要透露的信息来看，实验设计**覆盖了方法对比、场景泛化、模型能力诊断**等关键维度，逻辑上是完整且有针对性的。
  - 但**缺少消融实验、轨迹质量量化指标、不同视频生成模型之间的横向比较**等细节，需阅读全文才能判断实验的完备程度。
- **公平性**：摘要中特别指出视频生成模型经过微调后依然表现不佳，这一设计说明作者**给了强基线充分的学习机会**，对比公平性较好。

## 6. 主要结论与发现

1. **轨迹生成优于像素生成**：直接以点轨迹为输出目标的条件生成模型，能比传统方法**更准确、更多样**地预测单图场景的未来运动。
2. **"视频生成=世界模型"的观点被质疑**：最先进的视频生成模型在单图运动预测上，即便经过微调，也无法在**简单的物理场景**（如方块下落、机械交互）中做出正确预测——说明它们作为物理世界模型的能力存在明显局限。
3. **局限性的根源**：作者将视频生成模型的不足归因于**生成像素的巨大开销**——像素层级的生成引入与运动无关的表观细节，分散了模型的建模能力，而**直接建模运动本身（轨迹）才是更高效的路径**。

## 7. 优点

- **问题定义清晰且富有启发性**：用"条件点轨迹生成"来重构运动预测，直接对标前沿的"视频生成=世界模型"论断，问题意识很强。
- **架构选择巧妙**：采用视频生成器架构但替换输出空间，既吸收了生成模型的表达力和时序建模能力，又避开了像素生成的冗余负担，思路简洁有效。
- **诊断价值突出**：通过对比"生成轨迹"与"生成像素"，将运动预测能力从视频生成任务中剥离出来单独考察，形成了对视频生成模型的**能力诊断实验**，具有超出任务本身的方法论价值。
- **对不确定性的处理**：使用生成式方法建模轨迹分布，能输出多种可能的未来，而非单点估计，符合物理预测任务的内在多解特性。

## 8. 不足与局限

- **信息局限**：由于本文被OpenReview的验证（CAPTCHA）页面拦截，能获取的信息仅限摘要和元数据，无法提取实验细节、定量指标、模型参数、公式推导、消融实验等关键内容。以下局限基于摘要本身及领域常识推断：
- **场景覆盖面有限**：摘要仅提及"下落方块"和"机械交互"两类合成物理场景，均属于简单物理范畴。对于流体、非刚体、复杂接触、真实世界视频等更广泛的物理动态，方法是否依然有效尚不明确。
- **对"视频生成模型不行"的结论需谨慎解读**：论文指出视频生成模型在单图运动预测上表现差，但这一结论受限于特定架构、特定微调策略和特定数据规模。不能排除更强的视频生成模型（更大参数、更专门训练）在该任务上表现更好的可能。
- **应用层面的潜在限制**：点轨迹是相对中间层级的表征，下游应用（如视频预测、机器人规划、3D重建）如何利用这些轨迹，论文未在摘录文本中给出说明，实际应用价值有待进一步验证。
- **基线的选择偏差风险**："传统回归器和生成器"是哪些具体方法、是否为其选择了最优超参数，摘要中未给出，若基线调参不充分，可能高估本文方法的相对优势。

---

（完）
