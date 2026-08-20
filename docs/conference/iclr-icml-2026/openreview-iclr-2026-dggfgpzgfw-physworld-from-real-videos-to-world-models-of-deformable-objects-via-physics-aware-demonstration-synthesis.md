---
title: "PhysWorld: From Real Videos to World Models of Deformable Objects via Physics-Aware Demonstration Synthesis"
title_zh: PhysWorld：通过物理感知演示合成从真实视频构建可变形物体世界模型
authors: "Yu Yang, Zhilu Zhang, Xiang Zhang, Yihan Zeng, Hui Li, Wangmeng Zuo"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=dggfgPzGFW"
tags: ["query:phys-video"]
score: 7.0
evidence: 从真实视频合成物理感知演示以学习物理一致的动力学
tldr: 该论文解决真实视频数据不足导致可变形物体物理动力学模型难以学习的问题。PhysWorld先在MPM模拟器中通过本构模型选择和全局-局部优化构建物理一致的数字孪生，再施加部分感知扰动合成多样化的物理合理演示。实验显示该合成数据显著提升了世界模型对可变形物体动力学的预测能力，为从真实视频学习物理一致模型提供了有效方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 真实视频数据稀缺导致难以从有限数据学习物理一致的可变形物体动力学模型。
method: 利用MPM模拟器为真实视频构建物理一致的数字孪生，并通过本构模型选择和物理属性优化合成多样演示。
result: 合成的物理合理演示有效提升了世界模型在可变形物体上的动力学预测性能。
conclusion: 该方法缓解了真实数据稀缺问题，为学习物理一致的世界模型提供了一种数据合成范式。
---

## Abstract
Interactive world models that simulate object dynamics are crucial for robotics, VR, and AR. However, it remains a significant challenge to learn physics-consistent dynamics models from limited real-world video data, especially for deformable objects with spatially-varying physical properties. To overcome the challenge of data scarcity, we propose PhysWorld, a novel framework that utilizes a simulator to synthesize physically plausible and diverse demonstrations to learn efficient world models. Specifically, we first construct a physics-consistent digital twin within MPM simulator via constitutive model selection and global-to-local optimization of physical properties. Subsequently, we apply part-aware perturbations to the physical properties and generate various motion patterns for the digital twin, synthesizing extensive and diverse demonstrations. Finally, using these demonstrations, we train a lightweight GNN-based world model that is embedded with physical properties. The real video can be used to further refine the physical properties. PhysWorld achieves accurate and fast future predictions for various deformable objects, and also generalizes well to novel interactions. Experiments show that PhysWorld has competitive performance while enabling inference speeds 47 times faster than the recent state-of-the-art method, i.e., PhysTwin. The code and pre-trained models will be publicly available.

---

## 论文详细总结（自动生成）

# PhysWorld 论文总结

## 1. 核心问题与整体含义

- **研究动机**：交互式世界模型（用于模拟物体动力学）对机器人、VR、AR 等领域至关重要。然而，从有限的真实世界视频数据中学习物理一致的动力学模型非常困难，尤其是对于具有**空间变化物理属性**的**可变形物体**而言，真实数据稀缺问题尤为突出。
- **核心问题**：如何在不依赖大规模真实视频数据的前提下，学习能够准确、快速预测可变形物体未来状态，并且具有物理一致性的世界模型？
- **整体含义**：论文提出了一种“以模拟器为数据源”的范式，通过构建物理一致的数字孪生并合成多样化演示，将真实视频的稀缺问题转化为可用仿真数据的大规模生成问题，为学习物理一致的世界模型提供了一条可扩展的路径。

## 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：利用 MPM（Material Point Method，物质点法）模拟器为真实视频中的可变形物体构建“物理一致的数字孪生”，然后通过可控的扰动合成大量物理合理的演示数据，用于训练一个轻量级、内嵌物理属性的 GNN 世界模型。
- **关键技术细节**：
  - **本构模型选择（Constitutive Model Selection）**：从候选本构模型中为每个物体选出最能描述其材料行为的模型，确保数字孪生的物理结构正确。
  - **全局到局部优化（Global-to-Local Optimization）**：先全局粗调物理参数，再在局部空间上精细优化空间变化的物理属性，使数字孪生与真实视频中的动力学行为高度一致。
  - **部分感知扰动（Part-Aware Perturbations）**：在已构建的数字孪生上，针对不同部位施加有物理意义的属性扰动（如局部刚度、密度变化），从而生成多种具有不同运动模式但依然物理合理的演示。
  - **轻量级 GNN 世界模型**：模型以图神经网络为基础，并在其中显式嵌入物理属性信息，利用合成演示进行训练，使模型不仅学会运动规律，还能感知物体的内在物理状态。
  - **真实视频微调**：真实视频数据可以用来进一步修正模型中所嵌入的物理属性，实现从仿真到真实的领域适应。
- **算法流程（文字描述）**：
  1. 输入真实视频，提取可变形物体的运动轨迹与形态变化；
  2. 在 MPM 模拟器中重建物体的几何与材料模型；
  3. 通过本构模型选择 + 全局-局部优化，拟合物理属性，构建物理一致的数字孪生；
  4. 对数字孪生施加部分感知扰动，生成大量多样且物理合理的演示序列；
  5. 利用合成演示训练内嵌物理属性的 GNN 世界模型；
  6. 可选：使用真实视频进一步优化物理属性嵌入，提升真实世界泛化能力。

## 3. 实验设计

- **数据集/场景**：论文摘要未详细列出具体数据集名称，但实验对象为多种可变形物体（如布料、弹性体等），场景涉及真实视频中的动力学预测与新型交互泛化测试。
- **Benchmark**：主要与近期 SOTA 方法 **PhysTwin** 进行对比，衡量未来预测的准确性与推理速度。
- **对比方法**：摘要中明确提到 PhysTwin；未提及更多基线，但可推测实验中应包含若干视频预测/物理模拟基线，具体方法列表在论文正文中，未在提取文本中体现。
- **评估指标**：包括动力学预测准确性（具体数值未给出）和推理速度（相对加速比 47 倍）。

## 4. 资源与算力

- **未明确说明**：论文摘要和元数据中没有提及 GPU 型号、数量、训练时长、模拟器运行资源等具体算力信息。
- **间接信息**：GNN 世界模型为轻量级设计，且推理速度比 PhysTwin 快 47 倍，暗示其在实际部署中对算力要求较低；但训练阶段的资源消耗（如 MPM 模拟、参数优化、合成数据生成）未给出量化数据。

## 5. 实验数量与充分性

- **实验数量**：从摘要看，至少包含以下实验类别：
  - 多种可变形物体的动力学预测实验；
  - 与 PhysTwin 的对比实验（准确性与速度）；
  - 对“新型交互”（novel interactions）的泛化实验；
  - 真实视频微调物理属性的实验（隐含于方法描述中）。
- **充分性分析**：
  - **正面**：实验覆盖了核心性能对比、泛化能力和速度优势，能基本支撑论文“有效且高效”的结论。
  - **不足**：提取信息中缺少消融实验细节（如本构模型选择、全局-局部优化、部分感知扰动各自的贡献）、多组真实视频场景的统计结果、不同物体类别/材料的多维度评估。因此，从现有可见信息看，实验的充分性和客观性无法完整评估；需要阅读论文全文确认是否有更详细的基准与消融。

## 6. 主要结论与发现

- 合成得到的物理合理演示数据能够有效提升世界模型对可变形物体动力学的预测能力，缓解真实数据稀缺问题。
- 通过在 GNN 中嵌入物理属性，模型不仅预测准确，还具备对新交互行为的泛化能力。
- 提出的 PhysWorld 在预测性能上与当前最先进方法 PhysTwin 相当或更有竞争力，但**推理速度快 47 倍**，具备实时应用的潜力。

## 7. 优点

- **数据稀缺问题的高效解法**：不依赖大规模真实视频，而是用物理模拟器生成高质量、多样性数据，思路新颖且工程可行。
- **物理一致性保障**：通过本构模型选择和全局-局部优化，确保数字孪生与真实视频的物理行为一致，合成数据具有可信度。
- **可控数据多样性**：部分感知扰动机制允许在物理合理范围内生成多样化运动模式，避免数据单一，增强模型泛化。
- **高效轻量模型**：GNN 世界模型体积小、推理速度快，适合机器人/AR/VR 等需要实时响应的场景。
- **真实数据融合**：支持利用真实视频微调物理属性，兼顾仿真效率与真实准确性。

## 8. 不足与局限

- **实验细节缺失**：从提取内容中无法看到具体数据集、评估指标数值、消融实验和统计显著性分析，难以全面判断方法的稳健性。
- **依赖 MPM 模拟器精度**：数字孪生的物理一致性很大程度上取决于本构模型库和优化算法的覆盖范围，对于复杂材料（如黏弹性、非均质生物组织）可能不适用。
- **合成域到真实域的偏差**：即使有真实视频微调，合成数据与真实物理之间仍可能存在系统偏差，尤其对于罕见交互或极端形变场景。
- **应用范围有限**：目前主要针对可变形物体，对刚体、流体耦合或涉及多物体复杂接触的场景未在摘要中体现。
- **算力成本未透明**：训练阶段需进行 MPM 模拟与参数优化，其计算开销可能较大，论文未披露相关成本。
- **对比方法单一**：仅提及 PhysTwin，缺少与其他视频预测模型（如基于 NeRF/RF 的方法）或纯学习方法的对比，说服力不足。

（完）
