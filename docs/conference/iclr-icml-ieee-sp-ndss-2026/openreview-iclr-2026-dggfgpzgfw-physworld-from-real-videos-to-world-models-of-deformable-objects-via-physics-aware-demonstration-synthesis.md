---
title: "PhysWorld: From Real Videos to World Models of Deformable Objects via Physics-Aware Demonstration Synthesis"
title_zh: PhysWorld：从真实视频到可变形物体世界模型的物理感知演示合成
authors: "Yu Yang, Zhilu Zhang, Xiang Zhang, Yihan Zeng, Hui Li, Wangmeng Zuo"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=dggfgPzGFW"
tags: ["query:phys-video"]
score: 7.0
evidence: 合成物理合理的演示数据，用于学习物理一致的动力学
tldr: 学习可变形物体的物理一致动力学常受限于真实视频数据不足。PhysWorld 在 MPM 仿真器中通过本构模型选择与全局-局部物理属性优化构建数字孪生，并施加操纵扰动来合成多样且有物理合理性的演示。利用这些演示可高效学习交互世界模型，为机器人、VR/AR 等应用提供支持。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 从有限的真实视频学习可变形物体的物理一致动力学模型面临严重的数据稀缺挑战。
method: 利用 MPB 仿真器构建物理一致的数字孪生，通过本构模型选择和物理属性全局-局部优化，并施加部位感知扰动合成多样物理合理的演示。
result: 实验表明合成演示能高效训练世界模型，并实现对可变形物体动态的物理一致模拟。
conclusion: 该方法为机器人、VR/AR 提供物理可信的交互世界模型学习途径，缓解了数据瓶颈。
---

## Abstract
Interactive world models that simulate object dynamics are crucial for robotics, VR, and AR. However, it remains a significant challenge to learn physics-consistent dynamics models from limited real-world video data, especially for deformable objects with spatially-varying physical properties. To overcome the challenge of data scarcity, we propose PhysWorld, a novel framework that utilizes a simulator to synthesize physically plausible and diverse demonstrations to learn efficient world models. Specifically, we first construct a physics-consistent digital twin within MPM simulator via constitutive model selection and global-to-local optimization of physical properties. Subsequently, we apply part-aware perturbations to the physical properties and generate various motion patterns for the digital twin, synthesizing extensive and diverse demonstrations. Finally, using these demonstrations, we train a lightweight GNN-based world model that is embedded with physical properties. The real video can be used to further refine the physical properties. PhysWorld achieves accurate and fast future predictions for various deformable objects, and also generalizes well to novel interactions. Experiments show that PhysWorld has competitive performance while enabling inference speeds 47 times faster than the recent state-of-the-art method, i.e., PhysTwin. The code and pre-trained models will be publicly available.

---

## 论文详细总结（自动生成）

# 论文总结：PhysWorld：从真实视频到可变形物体世界模型的物理感知演示合成

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：从有限的真实世界视频中学习物理一致的物体动力学模型，尤其是具有空间变化物理属性的可变形物体，面临严重的数据稀缺挑战。
- **研究背景**：交互式世界模型（interactive world models）对机器人操作、VR/AR 等应用至关重要，但真实视频数据难以覆盖丰富、多样的交互与变形模式。
- **整体含义**：PhysWorld 提出一种利用物理仿真器**合成物理合理且多样化的演示数据**来训练高效世界模型的框架，从而缓解真实数据不足的瓶颈，实现对可变形物体未来动态的准确、快速预测。

## 2. 方法论（核心思想、关键技术细节、流程）
- **核心思想**：先用仿真器构建物理一致的数字孪生，再通过扰动生成多样化演示，最后用这些演示训练轻量级图神经网络（GNN）世界模型。
- **关键技术步骤**：
  - **构建物理一致的数字孪生**：在 MPM（Material Point Method，物质点法）仿真器中，通过**本构模型选择**与**物理属性的全局-局部优化**，使数字孪生尽可能匹配真实物体的形变行为。
  - **合成多样化演示**：对数字孪生的物理属性施加**部位感知（part-aware）扰动**，生成多种运动模式，从而合成大量且富有差异性的交互演示。
  - **训练世界模型**：使用这些演示数据训练一个**轻量级、嵌入物理属性的 GNN 世界模型**；后续真实视频可进一步细化物理属性。
- **公式与算法流程**：摘要中未给出具体公式，算法流程可概括为：仿真器数字孪生构建 → 物理属性扰动与演示合成 → GNN 世界模型训练 → 真实视频微调。

## 3. 实验设计（数据集 / 场景、Benchmark、对比方法）
- **数据集与场景**：摘要未明确列出具体真实数据集名称，但实验涉及“多种可变形物体”以及“新颖交互”的泛化测试；真实视频用于细化物理属性。
- **Benchmark**：主要与最新的 SOTA 方法 **PhysTwin** 进行对比。
- **评价指标**：包括未来预测的准确性、推理速度（PhysWorld 的推理速度比 PhysTwin 快 47 倍），以及对新交互的泛化能力。
- **对比方法**：仅提及 PhysTwin；未提及更多基线或消融实验。

## 4. 资源与算力（GPU、训练时长等）
- **文中未明确说明**：摘要中未提及使用的 GPU 型号、数量、训练时长、显存等具体算力资源。
- 因此，无法从该摘要判断训练成本或硬件需求；需要查看论文正文补充信息。

## 5. 实验数量与充分性
- **公开的实验信息有限**：摘要仅提到在多种可变形物体上进行了准确性和速度测试，并验证了对新交互的泛化，但**未列出具体的实验组数、消融实验、定量结果表格**。
- **充分性评估**：
  - 由于只有摘要，无法全面判断实验的完整性和公平性。
  - 从已知信息看，与 PhysTwin 的对比能体现速度优势，但缺乏详细误差分析、消融各模块贡献、仿真与真实域差距的量化验证。
  - 实验覆盖范围可能不够充分：未报告失败案例、极端物体、不同扰动幅度的影响等。

## 6. 主要结论与发现
- PhysWorld 能够对多种可变形物体实现**准确且快速的未来预测**，并**泛化到新交互**。
- 其推理速度比 PhysTwin **快 47 倍**，同时保持有竞争力的性能。
- 合成演示数据可有效训练高效世界模型，并将公开代码与预训练模型，便于复现和应用。

## 7. 优点（方法与实验亮点）
- **创新解决数据稀缺**：利用物理仿真器合成演示，绕开大规模真实数据采集困难。
- **物理一致性**：通过本构模型选择和物理属性全局-局部优化，赋予数字孪生物理合理性。
- **数据多样性与可控性**：部位感知扰动可系统生成多种运动模式，增强演示覆盖度。
- **高效轻量模型**：GNN 世界模型体积小、推理速度快，适合实时应用。
- **可结合真实视频微调**：支持利用真实数据进一步优化物理属性，兼顾仿真与真实数据。
- **开放资源**：计划公开代码和预训练模型，促进复现和社区研究。

## 8. 不足与局限
- **仿真与真实域差距**：合成数据基于 MPM 仿真器，存在仿真近似误差，数字孪生无法完全模拟真实物体的复杂物理行为。
- **物理属性优化复杂度**：全局-局部优化在空间变化属性下可能计算代价高，且需要足够的观测数据支撑优化。
- **实验信息不足**：摘要缺少详细实验设置、定量结果、消融研究和多基线对比，难以充分验证方法的普适性和公平性。
- **泛化范围有限**：只提到“新颖交互”，但未明确交互类型范围；对极端变形、断裂、粘连等复杂情况可能未覆盖。
- **真实世界验证缺失**：未具体说明真实视频微调后的提升幅度，以及是否在真实机器人/VR/AR 环境中部署测试。
- **算力成本未知**：由于未报告训练资源，可能限制了可复现性。

（完）
