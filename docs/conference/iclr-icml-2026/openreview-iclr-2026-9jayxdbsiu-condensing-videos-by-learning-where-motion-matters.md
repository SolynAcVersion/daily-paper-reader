---
title: Condensing Videos by Learning Where Motion Matters
title_zh: 通过学习运动关键位置进行视频压缩
authors: "Jaehyun Choi, Jiwan Hur, Gyojin Han, Jaemyung Yu, Junmo Kim"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=9JAYXdBsIU"
tags: ["query:video-gen-rl"]
score: 4.0
evidence: 时序连贯的视频帧合成
tldr: 视频数据集压缩需在缓解巨大计算开销的同时，保留空间内容与时序动态之间复杂的相互依赖，而先前工作常将二者不当解耦。本文提出动态帧合成DFS，从少量关键帧出发，通过梯度错位定位高运动复杂度、简单插值失效的时刻，自适应地合成新帧。该方法仅在复杂度高的位置分配新帧，从而构建高效且时序连贯的合成数据集。这为视频数据的时空耦合建模与高效压缩提供了新思路。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频数据集压缩需缓解巨大计算开销，同时保留空间内容与时序动态的相互依赖，现有方法常将其不当解耦。
method: 提出动态帧合成DFS，从少量关键帧出发，通过梯度错位定位高运动复杂度时刻，自适应合成新帧。
result: 仅在复杂度高处分配新帧，构建高效且时序连贯的合成数据集。
conclusion: 在保留时空耦合的前提下实现了高效视频数据集压缩。
---

## Abstract
Video dataset condensation aims to mitigate the immense computational cost of video processing, but faces the unique challenge of preserving the complex interplay between spatial content and temporal dynamics. Prior work often unnaturally disentangles these elements, overlooking their essential interdependence. We introduce Dynamic Frame Synthesis (DFS), a novel approach that preserves this critical coupling. DFS begins with a minimal set of key frames and dynamically synthesizes new ones by identifying moments of high motion complexity, where simple interpolation fails, through gradient misalignments. This adaptive process allocates new frames only where such complexity exists, creating highly efficient and temporally coherent synthetic datasets. Extensive experiments show DFS outperforms prior methods on standard action recognition benchmarks, creating powerful representations with significantly less storage.

---

## 论文详细总结（自动生成）

**说明**：给定材料中的 PDF 正文提取失败（返回 503 / “no healthy upstream”），因此以下总结主要依据论文标题、元数据与摘要；凡正文未提供的信息，均标注为“未说明/无法确认”，避免过度推断。

### 1. 核心问题与整体含义
- **研究领域**：视频数据集压缩（video dataset condensation），目标是在降低视频处理巨大计算开销的同时，构建仍具强表征能力的压缩数据集。
- **核心挑战**：视频数据同时包含空间内容与时序动态，二者存在复杂相互依赖；压缩时不能简单割裂。
- **现有问题**：先前工作常将空间内容与时序动态“不自然地解耦”，忽视其本质耦合，导致压缩后的视频数据难以保留真实时空关系。
- **整体含义**：论文提出 **Dynamic Frame Synthesis（DFS，动态帧合成）**，尝试在保留时空耦合的前提下，自适应地选择并合成关键帧，为高效视频数据集压缩提供新思路。

### 2. 方法论
- **核心思想**：
  - 从极少量关键帧出发，不采用均匀采样或静态压缩，而是动态合成新帧。
  - 通过识别“高运动复杂度、简单插值失效”的时刻，决定在哪里增加新帧。
  - 仅在运动复杂处分配新帧，从而在压缩率与时空保真度之间取得更好平衡。
- **关键技术细节**：
  - 使用 **梯度错位（gradient misalignments）** 定位高运动复杂度时刻。
  - 当简单插值无法维持时序连贯或动态一致性时，说明该位置需要新帧。
  - 自适应过程只在复杂度高的位置分配新帧，形成高效且时序连贯的合成数据集。
- **算法流程（文字描述）**：
  1. 初始化少量关键帧。
  2. 在关键帧之间尝试插值或动态建模。
  3. 计算梯度错位，检测简单插值失效、运动复杂度高的时刻。
  4. 在这些时刻合成并加入新帧。
  5. 迭代更新帧集合，直到达到帧预算、压缩率或复杂度阈值。
  6. 输出压缩后的合成视频数据集，用于后续动作识别等任务。
- **公式与伪代码**：给定摘要与元数据未提供具体公式、损失函数或完整算法伪代码，无法确认细节。

### 3. 实验设计
- **场景/任务**：标准动作识别 benchmark。
- **对比对象**：与先前视频数据集压缩方法进行比较。
- **评价维度**：
  - 动作识别性能：验证压缩数据能否训练出强表征。
  - 存储开销：强调“significantly less storage”。
  - 时序连贯性：摘要提到生成“temporally coherent synthetic datasets”。
- **具体数据集与 benchmark**：给定文本未列出具体数据集名称、划分方式或评价协议，无法确认。
- **对比方法**：仅说明“prior methods”，未列出具体方法名称。

### 4. 资源与算力
- 给定文本**未说明**使用的 GPU 型号、数量、训练时长、参数量或总计算开销。
- 因此无法评估其训练成本、可复现性与算力门槛。

### 5. 实验数量与充分性
- 摘要称进行了 **extensive experiments**，但给定材料未给出具体实验组数。
- 无法确认是否包含：
  - 多个动作识别数据集；
  - 不同压缩率/帧预算下的实验；
  - 关键帧数量、梯度错位阈值等消融实验；
  - 与不同 baseline 的完整对比。
- **公平性**：若所有方法均在相同标准动作识别 benchmark 和相同协议下比较，则设计方向合理；但由于缺少数据集、指标、超参搜索、训练预算等细节，无法验证公平性与统计显著性。
- **充分性判断**：从摘要看有实验支撑，但仅凭给定材料无法认定实验充分。

### 6. 主要结论与发现
- DFS 在标准动作识别 benchmark 上**优于先前方法**。
- DFS 能用**显著更少的存储**构建强表征。
- 通过梯度错位定位高运动复杂度区域，并仅在必要位置合成新帧，可生成高效且时序连贯的合成视频数据集。
- 保留空间内容与时序动态的耦合，比简单解耦更有利于视频数据集压缩。
- 该工作为视频数据时空耦合建模与高效压缩提供了新方向。

### 7. 优点
- **问题诊断清晰**：明确指出先前方法不当解耦空间与时序信息的问题。
- **方法有针对性**：用梯度错位检测“简单插值失效”的高运动复杂度时刻，思路直观且具创新性。
- **自适应压缩**：只在运动复杂处增加帧，避免均匀分配帧带来的冗余。
- **兼顾效率与连贯性**：目标同时包括低存储和时序连贯的合成数据集。
- **实验信号积极**：声称在标准动作识别 benchmark 上超越 prior methods，说明压缩数据仍具实用表征能力。

### 8. 不足与局限
- **正文缺失导致验证困难**：当前材料仅有摘要和元数据，无法核实方法公式、算法细节与实验设置。
- **实验覆盖未知**：仅提到动作识别 benchmark，未说明是否覆盖检测、分割、视频生成、长视频等任务。
- **代理指标局限**：梯度错位是否总能等价于语义重要运动，仍需验证；对遮挡、相机运动、非刚性运动、噪声等复杂情况可能不稳健。
- **超参敏感性未知**：关键帧数量、错位阈值、合成策略等对性能的影响未说明。
- **公平性与可复现性不足**：未报告算力、训练时长、超参搜索预算，难以判断对比是否完全公平。
- **应用限制**：对大规模视频、长时序视频、多模态视频或实时场景的扩展性尚未在给定文本中体现。
- **潜在权衡**：压缩率提升是否会在某些细粒度动作或长尾类别上带来性能损失，无法从现有信息判断。

（完）
