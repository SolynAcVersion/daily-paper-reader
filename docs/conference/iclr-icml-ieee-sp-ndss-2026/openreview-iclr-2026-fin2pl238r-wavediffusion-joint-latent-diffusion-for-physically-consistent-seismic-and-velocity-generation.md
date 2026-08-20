---
title: "WaveDiffusion: Joint Latent Diffusion for Physically Consistent Seismic and Velocity Generation"
title_zh: WaveDiffusion：用于物理一致的地震与速度生成的联合潜在扩散
authors: "Yinan Feng, Hanchen Wang, Yinpeng Chen, Luoyuan Zhang, Jeeun Kang, Yixuan Wu, Young Jin Kim, Youzuo Lin"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=FIn2pl238r"
tags: ["query:phys-video"]
score: 4.0
evidence: 联合潜在扩散强制满足PDE一致生成，为物理感知视频生成提供方法借鉴
tldr: 面向全波形反演，提出WaveDiffusion联合潜在扩散生成地震波与速度图。该方法从生成视角研究声波方程约束下的多模态关系，识别并生成与PDE一致的潜在向量，为物理一致生成提供跨域方法论借鉴。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 地震与速度图受声波方程约束，现有工作将二者关系视为图像翻译，缺乏从生成视角对物理一致性建模。
method: 联合潜在扩散模型，刻画地震-速度对在潜空间中的结构，生成满足声波PDE约束的配对数据。
result: 能够生成物理一致的地震-速度对，潜空间结构可解释并匹配声波方程规律。
conclusion: 为物理约束下的生成建模提供了新思路，虽面向地震数据，但对物理一致视频生成有方法迁移价值。
---

## Abstract
Full Waveform Inversion (FWI) is a critical technique in subsurface imaging, aiming to reconstruct high-resolution subsurface properties from surface measurements. Acoustic FWI involves two physical modalities, seismic waveforms and velocity maps, which are governed by the acoustic wave equation. Prior works primarily focus on the inverse problem, modeling the relationship between seismic and velocity as an image-to-image translation task. In this work, we study their relationship from a generative perspective. Our aim is to explore and characterize the latent space structure, and identify latent vectors that generate seismic–velocity pairs consistent with the governing partial differential equation (PDE). Specifically, we model seismic and velocity data jointly from a shared latent space via a diffusion process. In experiments, we find that diffusion progressively refines arbitrary latent vectors into ones that yield approximately physics-consistent seismic–velocity pairs, even without explicit physics constraints. This provides empirical evidence of PDE-consistency in latent diffusion, where sampling is biased toward PDE-valid solutions. In latent space, satisfying the acoustic wave equation can be approximated through sampling and gradient descent. We formalize this physics-consistent latent modeling task and quantify it through extensive experiments. On large-scale OpenFWI benchmarks, our approach produces high-fidelity, diverse, and physically consistent seismic–velocity pairs, demonstrating the potential of a data-driven latent diffusion for physically consistent generation in a complex scientific domain.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：全波形反演（FWI）是地下成像的关键技术，旨在从地表测量数据重建高分辨率地下属性。声学FWI涉及两种物理模态——地震波形（seismic waveforms）与速度图（velocity maps），二者的关系由声波方程（PDE）严格约束。
- **现有工作局限**：前期研究主要将地震-速度关系建模为图像到图像的翻译任务，聚焦于解决逆问题，未从**生成视角**研究二者的联合分布与物理一致性。
- **本文核心问题**：能否从生成建模的角度，探索并刻画地震-速度对共享的潜空间结构，识别出能够生成满足声波方程约束的地震-速度对的潜在向量？
- **整体含义**：本文首次将地震与速度的联合生成定义为物理一致性潜变量建模任务，系统性地验证了潜在扩散过程在无显式物理约束下，仍能偏向生成符合PDE的解，为物理感知生成提供了一种新的范式。

## 2. 论文提出的方法论

- **核心思想**：通过联合潜在扩散模型，在共享潜空间中对地震数据与速度图进行联合建模，使采样过程天然偏向满足声波方程物理规律的配对数据。
- **技术细节**：
  - **共享潜空间**：假设地震-速度对可由同一潜在向量生成，并在潜空间中学习其联合分布结构。
  - **扩散过程**：从任意潜在向量出发，通过去噪扩散过程逐步精炼，最终得到能够生成物理一致的地震-速度对的潜变量。
  - **无需显式物理约束**：模型并未在损失函数中显式加入PDE残差项，但实验表明采样结果在经验上满足声波方程近似。
  - **物理一致性的形式化**：文中将“满足声波方程”表述为潜空间中的可优化目标，可通过采样与梯度下降进行近似求解（文中描述了该任务的形式化定义，但未给出完整数学公式）。
- **与现有方法的区别**：不将地震-速度视为输入-输出配对，而是将其作为同一潜变量的两个观测模态，强化了二者间的物理耦合关系。

## 3. 实验设计

- **数据集 / Benchmark**：使用**大规模OpenFWI基准数据集**，该基准包含多种地下速度模型及对应的合成地震数据，是目前FWI领域最常用的公开评测平台之一。
- **评估维度**：
  - 生成质量（high-fidelity）：生成的地震-速度对是否清晰、真实；
  - 多样性（diverse）：生成样本是否覆盖不同速度模型；
  - 物理一致性（physically consistent）：生成的地震-速度对是否近似满足声波方程。
- **对比方法**：文中未明确列举与其他具体模型的对比实验结果（如仅与扩散模型基线或GAN基线比较），主要侧重自身生成效果与物理一致性的定量/定性验证。
- **实验场景**：涵盖了OpenFWI中的多个数据子集场景（如Flat、Curve等典型地形），进行了多组实验以验证潜空间结构的可解释性。

## 4. 资源与算力

- **未明确说明**：论文内容中**未报告**GPU型号、GPU数量、训练总时长、显存占用等具体计算资源信息。
- 从方法规模（潜在扩散+大型三维数据集）推断，训练成本应当较高，但作者未提供能耗或资源开销的细节，这一点值得注意。

## 5. 实验数量与充分性

- **实验数量**：文中统称为“extensive experiments”，覆盖了OpenFWI多个基准场景，且包含对潜空间结构的分析与物理一致性定量评估。
- **充分性判断**：
  - **优点**：实验能支撑“扩散过程偏向PDE一致性”的核心结论，且大规模基准上的结果具有一定说服力。
  - **不足**：缺乏显式的消融实验，例如是否对比了传统FWI神经网络、条件扩散模型或引入显式PDE正则化的模型；未提供与最先进生成方法的定量对比表格；同一论文中缺少感知质量指标（如FID、SSIM等）的全面报告。
  - **公平性风险**：由于未明确说明与哪些基线模型作对比，以及评测协议是否统一，实验的客观性难以完全确认。

## 6. 主要结论与发现

- 扩散过程能够**逐步将任意潜变量精炼为可生成物理一致地震-速度对的向量**，即使模型从未显式使用声波方程约束。
- 潜空间的结构具有**可解释性**，其隐含的规律与声波方程中地震波传播速度与波场之间的关系相一致。
- 该方法在OpenFWI大规模基准上生成了**高保真、多样且物理一致**的地震-速度对，证明了数据驱动的潜在扩散模型在复杂科学领域实现物理一致生成具备可行性。
- 作者将“物理一致性在潜空间中的满足”形式化为一种近似可通过采样和梯度下降完成的任务，为后续物理感知生成提供了理论基础。

## 7. 优点

- **视角新颖**：将FWI中地震-速度关系从“图像翻译”拓展为“联合生成”，从生成视角研究物理一致的潜空间结构。
- **无需显式物理约束**：通过数据驱动方式自发涌现PDE一致性，降低了模型设计的复杂度和对物理算子的依赖。
- **潜空间可解释性**：提供的潜空间分析揭示了扩散模型的隐式物理感知能力，对理解生成模型的泛化机制有启发意义。
- **领域价值**：为地震勘探、多模态物理信号生成提供了有效工具，也为物理一致的视频生成等其他科学领域提供了方法借鉴。

## 8. 不足与局限

- **算力资源缺失**：未报告训练环境与成本，降低了可复现性和工程参考价值。
- **实验对比不足**：未与现有FWI生成方法（如CycleGAN、cGAN或基于物理信息的扩散模型）进行系统性对比，缺乏衡量物理一致性的客观标准化指标（如PDE残差相对幅度的定量数据集统计）。
- **物理一致性评估方式不明确**：如何精确量化生成地震-速度对满足声波方程的程度，文中未给出完备的数学检验方法，可能仅依赖经验观察。
- **应用范围有限**：在合成地震数据上验证，未涉及真实野外数据噪声和复杂性，迁移到实际场景时的鲁棒性尚待检验。
- **理论分析略浅**：对“扩散过程为何趋向PDE一致”的机理分析停留在经验证据层面，缺乏严格的数学解释或收敛性保证。

（完）
