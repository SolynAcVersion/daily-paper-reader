---
title: "DiffuPhyGS: Text-to-Video Generation with 3D Gaussians and Learnable Physical Properties via Diffusion Priors"
title_zh: DiffuPhyGS：基于3D高斯与可学习物理属性的扩散先验文本到视频生成
authors: "Wenqing Wang, Yun Fu"
date: 2025-09-11
pdf: "https://openreview.net/pdf?id=mq43BAAos0"
tags: ["query:phys-video"]
score: 9.0
evidence: 通过扩散先验与3D高斯生成文本到视频，学习物理属性以产生物理感知的运动
tldr: 该论文针对 3D 动态生成中外观质量与物理感知运动难以兼得的问题，提出 DiffuPhyGS。其使用 LLM 链式思考迭代优化提示，获取与提示对齐的 2D 和多视角 3D 扩散先验，引导 3D 高斯生成物体；同时引入可学习物理属性，使运动贴近真实物理规律。实验表明该方法直接由文本生成高质量且物理合理的 3D 物体视频，为文本驱动的物理感知生成提供了新路径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有 3D 动态生成依赖手工输入和既有模型，难以同时保证高质量外观与物理感知运动。
method: 通过 LLM-CoT 迭代提示精炼获得扩散先验，指导高斯溅射生成 3D 物体，并学习物理属性以驱动运动。
result: 能够从文本直接生成高质量、物理可感知的 3D 物体视频，验证了方法的有效性。
conclusion: 将可学习物理属性与扩散先验结合可提升 3D 视频生成的物理合理性与可控性。
---

## Abstract
Generating realistic 3D object videos is crucial for virtual reality and digital content creation. However, existing 3D dynamics generation methods often struggle to achieve high-quality appearance and physics-aware motion, relying on manual inputs and pre-existing models. To address these challenges, we propose DiffuPhyGS, a novel framework that generates high-quality 3D objects with realistic and learnable physical motion directly from text prompts. Our approach features an LLM-Chain-of-Thought-based Iterative Prompt Refinement (LLM-CoT-IPR) method, which obtains prompt-aligned 2D and multi-view 3D diffusion priors to guide Gaussian Splatting (GS) to generate 3D objects. We further enhance 3D generation quality with a Densification-by-Adaptive-Splitting (DAS) mechanism. Next, we employ a material property decoder that utilizes a Mixture-of-Experts Material Constitutive Models (MoEMCMs) to predict the mixed material properties of the 3D object. We then apply the Material Point Method (MPM) to deform 3D Gaussian kernels, ensuring physics-grounded motion guided by implicit and explicit physical priors from the video diffusion model and a velocity loss function. Extensive experiments show DiffuPhyGS outperforms other methods in generating realistic physics-grounded motion across diverse materials.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：生成真实的 3D 物体视频是虚拟现实和数字内容创作的关键需求，但现有 3D 动态生成方法往往难以同时实现高质量外观与物理感知运动。
- **问题背景**：已有方法通常依赖手工输入和预训练模型，限制了自动化程度和生成质量，尤其在物理合理性方面表现不足。
- **核心目标**：提出一种能够直接从文本提示生成高质量、具备可学习且真实物理运动的 3D 物体视频的新框架，以弥合外观质量与物理合理性之间的鸿沟。

## 2. 方法论

- **整体思路**：DiffuPhyGS 框架结合了扩散先验、3D 高斯泼溅（Gaussian Splatting, GS）与物理仿真，实现文本到 3D 动态视频的端到端生成。
- **关键技术细节**：
  - **LLM-CoT-IPR（基于大语言模型链式思考的迭代提示精炼）**：利用 LLM 的链式思考能力，通过迭代优化文本提示，获取与提示对齐的 2D 和多视角 3D 扩散先验，用于引导 GS 生成 3D 物体。
  - **DAS（自适应分裂稠密化）**：通过自适应分裂机制增强 3D 生成质量，改善高斯核的分布与表达。
  - **MoEMCMs（混合专家材料本构模型）**：使用材料属性解码器，结合混合专家结构预测 3D 物体的混合材料属性。
  - **MPM（物质点法）**：应用物质点法形变 3D 高斯核，并借助视频扩散模型中的隐式物理先验和显式速度损失函数，确保运动符合物理规律。
- **公式/算法流程（文字说明）**：文本提示 → LLM-CoT-IPR 精炼 → 获得 2D/多视角扩散先验 → 引导 GS 生成 3D 物体（含 DAS 稠密化）→ 材料解码器预测物理属性 → MPM 驱动高斯核变形 → 视频扩散模型提供物理先验 + 速度损失约束 → 输出物理合理的 3D 动态视频。

## 3. 实验设计

- **数据集/场景**：摘要中未提供具体的数据集名称或场景细节。
- **Benchmark**：未明确说明使用的基准测试或评估协议。
- **对比方法**：摘要仅提及“DiffuPhyGS outperforms other methods”，但未列出具体对比的基线方法。

## 4. 资源与算力

- 提供的论文内容（摘要与元数据）中**未提及**任何关于 GPU 型号、数量、训练时长或计算资源的详细信息。

## 5. 实验数量与充分性

- **实验数量**：摘要仅笼统提到“extensive experiments”，但未给出具体实验组数（如不同数据集、消融测试等）。
- **充分性评价**：由于缺少实验细节，无法客观评估实验的全面性、公平性或统计显著性；当前提供的证据不足以支撑深入的方法比较或消融分析。

## 6. 主要结论与发现

- 实验表明 DiffuPhyGS 在生成跨多种材料的真实物理运动方面优于现有方法。
- 验证了将可学习物理属性与扩散先验结合能有效提升 3D 视频生成的物理合理性和可控性。
- 直接从文本提示即可生成高质量、物理感知的 3D 物体视频，无需人工输入或预训练动态模型。

## 7. 优点

- **创新性**：新颖地将 LLM 驱动的提示精炼、3D 高斯泼溅、混合专家材料模型与 MPM 物理仿真融为一体，形成端到端框架。
- **自动化程度高**：仅需文本提示，摆脱了对手工输入和既有 3D 模型的依赖。
- **物理可学习**：通过可学习的物理属性和显式/隐式物理先验，兼顾外观质量与运动真实性。
- **机制互补**：扩散先验提升外观一致性，DAS 优化几何表达，MPM 保障物理动态，各组件分工明确。

## 8. 不足与局限

- **实验信息缺乏**：未公开数据集、基准、对比方法及消融实验细节，导致可复现性和可信度存疑。
- **资源信息缺失**：未说明算力要求，难以评估部署成本。
- **泛化性未知**：未提及对复杂物体、大规模场景或极端物理条件的测试表现。
- **潜在偏差风险**：若评测仅依赖主观视觉或单一指标，可能不足以全面证明物理真实性。
- **应用限制**：可能受限于文本提示的表达能力与扩散模型先验的覆盖范围，对罕见材料或特殊交互的支持有待验证。

（完）
