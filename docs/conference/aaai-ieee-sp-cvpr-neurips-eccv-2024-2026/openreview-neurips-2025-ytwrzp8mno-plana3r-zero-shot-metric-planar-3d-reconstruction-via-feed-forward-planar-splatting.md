---
title: "PLANA3R: Zero-shot Metric Planar 3D Reconstruction via Feed-forward Planar Splatting"
title_zh: PLANA3R：基于前馈平面溅射的零样本度量平面三维重建
authors: "Changkun Liu, Bin Tan, Zeran Ke, Shangzhan Zhang, Jiachen Liu, Ming Qian, Nan Xue, Yujun Shen, Tristan Braud"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=YTwRZP8mNO"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 基于平面基元的度量三维重建
tldr: 针对室内场景的度量三维重建，本文利用人造环境中普遍存在的平面规律，提出免位姿的PLANA3R框架。方法用视觉Transformer提取稀疏平面基元，估计相对相机位姿，并通过平面溅射在高分辨率深度与法向图上传播梯度来监督几何学习。该框架无需训练时的三维平面标注即可实现零样本度量重建，为紧凑几何表示提供了新方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 室内场景度量三维重建缺乏紧凑表示且依赖标注。
method: 用ViT提取稀疏平面基元并估计位姿，通过平面溅射监督几何学习。
result: 无需三维平面标注即可实现零样本度量重建。
conclusion: 为免位姿度量重建提供紧凑有效的平面基元方案。
---

## Abstract
This paper addresses metric 3D reconstruction of indoor scenes by exploiting their inherent geometric regularities with compact representations. Using planar 3D primitives -- a well-suited representation for man-made environments -- we introduce PLANA3R, a pose-free framework for metric $\underline{Plana}$r $\underline{3}$D $\underline{R}$econstruction from unposed two-view images. Our approach employs Vision Transformers to extract a set of sparse planar primitives, estimate relative camera poses, and supervise geometry learning via planar splatting, where gradients are propagated through high-resolution rendered depth and normal maps of primitives. Unlike prior feedforward methods that require 3D plane annotations during training, PLANA3R learns planar 3D structures without explicit plane supervision, enabling scalable training on large-scale stereo datasets using only depth and normal annotations. We validate PLANA3R on multiple indoor-scene datasets with metric supervision and demonstrate strong generalization to out-of-domain indoor environments across diverse tasks under metric evaluation protocols, including 3D surface reconstruction, depth estimation, and relative pose estimation. Furthermore, by formulating with planar 3D representation, our method emerges with the ability for accurate plane segmentation. The project page is available at: \url{https://lck666666.github.io/plana3r/}.

---

## 论文详细总结（自动生成）

# PLANA3R 论文中文总结

> 说明：提供的 PDF 提取文本实际为 OpenReview 的 CAPTCHA 验证页，未包含论文正文。以下总结主要依据论文标题、摘要与元数据（NeurIPS 2025 Accepted，score 4.0 等）整理；凡正文未提供的信息，均标注为“未说明/无法确认”，避免过度推断。

## 1. 核心问题与整体含义

- **研究领域**：室内场景的度量三维重建。
- **核心问题**：室内度量三维重建通常缺乏紧凑的几何表示，且部分方法依赖三维平面标注或相机位姿，限制了可扩展性与泛化能力。
- **研究动机**：人造室内环境普遍存在平面规律，平面 3D 基元是适合该类场景的紧凑表示。
- **整体含义**：论文提出 **PLANA3R**，一个免位姿、零样本的度量平面三维重建框架，试图利用平面先验，从无位姿双视图图像中恢复度量三维结构。
- **关键目标**：
  - 从无位姿双视图图像进行度量平面 3D 重建；
  - 使用稀疏平面 3D 基元作为紧凑表示；
  - 训练时无需三维平面标注，仅需深度和法向标注；
  - 支持大规模立体数据集训练，并泛化到域外室内环境。

## 2. 方法论

- **核心思想**：
  - 用平面 3D 基元表示人造环境中的几何规律；
  - 构建免位姿的前馈框架，直接从未标定双视图图像预测度量平面 3D 结构；
  - 通过平面溅射将平面基元渲染为高分辨率深度图和法向图，并借此传播梯度监督几何学习。

- **关键技术细节**：
  - 使用 **Vision Transformers** 提取一组稀疏平面基元；
  - 同时估计两视图之间的相对相机位姿；
  - 采用 **planar splatting** 机制，将平面基元渲染为高分辨率深度与法向图；
  - 梯度通过渲染得到的深度和法向图回传，用于监督平面几何学习；
  - 与先前需要 3D 平面标注的前馈方法不同，PLANA3R 不依赖显式平面监督；
  - 训练可使用仅含深度和法向标注的大规模立体数据集，从而提升可扩展性。

- **算法流程文字描述**：
  1. 输入两张无位姿图像；
  2. ViT 编码并预测稀疏平面基元与相对相机位姿；
  3. 利用平面基元进行平面溅射，渲染高分辨率深度图和法向图；
  4. 以深度和法向监督信号计算损失，并通过渲染过程将梯度传播至平面基元与位姿预测；
  5. 输出度量三维表面、深度、相对位姿，并可涌现平面分割能力。

- **公式说明**：提供的摘要与元数据中未给出具体公式，无法总结数学表达。

## 3. 实验设计

- **数据集/场景**：
  - 摘要提到在多个室内场景数据集上进行验证；
  - 这些数据集带有度量监督；
  - 训练侧提到可使用大规模立体数据集，仅需深度和法向标注；
  - 具体数据集名称未在提供文本中列出。

- **Benchmark/评估协议**：
  - 使用度量评估协议；
  - 任务包括：
    - 3D 表面重建；
    - 深度估计；
    - 相对位姿估计；
    - 平面分割。
  - 强调对域外室内环境的泛化能力。

- **对比方法**：
  - 摘要提到与先前需要 3D 平面标注的前馈方法形成对比；
  - 具体对比方法名称、基线设置、评价指标数值未在提供文本中说明。

## 4. 资源与算力

- 提供的文本中**未说明**以下信息：
  - GPU 型号与数量；
  - 训练时长；
  - 显存、参数量、推理速度等资源开销；
  - 是否使用分布式训练或特定训练框架。
- 因此无法对算力需求和训练成本做出可靠总结。

## 5. 实验数量与充分性

- 从摘要可知，论文至少涉及：
  - 多个室内场景数据集；
  - 多个任务：3D 表面重建、深度估计、相对位姿估计、平面分割；
  - 域外室内环境泛化评估。
- 但提供文本中**未给出**：
  - 具体实验组数；
  - 消融实验数量与设计；
  - 数据集划分、评价指标细节；
  - 统计显著性、公平性分析；
  - 失败案例或边界条件实验。
- 因此，实验覆盖可能较广，但**无法判断是否充分、客观与公平**，需查阅正文确认。

## 6. 主要结论与发现

- PLANA3R 能够在**无需 3D 平面标注**的情况下学习平面 3D 结构。
- 方法可在多个室内场景数据集上实现零样本度量重建，并泛化到域外室内环境。
- 在度量评估协议下，方法覆盖 3D 表面重建、深度估计和相对位姿估计等任务。
- 由于采用平面 3D 表示，方法还表现出**准确的平面分割能力**。
- 总体而言，论文为免位姿度量重建提供了一种紧凑、有效的平面基元方案。

## 7. 优点

- **表示紧凑**：使用稀疏平面 3D 基元，适合人造室内环境。
- **免位姿**：直接从无位姿双视图图像进行重建，减少对相机位姿输入的依赖。
- **零样本与可扩展训练**：无需 3D 平面标注，仅用深度和法向标注即可训练。
- **监督方式新颖**：通过平面溅射渲染高分辨率深度和法向图，并利用其传播梯度监督几何学习。
- **多任务统一**：同时涉及表面重建、深度估计、相对位姿估计和平面分割。
- **泛化目标明确**：强调对域外室内环境的泛化，具有实际应用潜力。

## 8. 不足与局限

- **信息缺失导致无法全面评估**：由于提供文本为 CAPTCHA 页面，正文、实验细节、算力信息均不可得。
- **场景假设限制**：方法依赖人造环境中的平面规律，可能不适用于非平面、杂乱或室外场景。
- **双视图设定限制**：目前描述为双视图输入，是否易扩展到多视图、视频或大规模场景未说明。
- **标注依赖仍存在**：虽然不需要 3D 平面标注，但仍需深度和法向标注，可能受训练数据偏差影响。
- **平面分割能力为“涌现”**：摘要称其可进行准确平面分割，但缺少精度、鲁棒性和失败案例分析。
- **应用限制未知**：实时性、内存占用、部署成本、极端视角变化下的稳定性等未在提供文本中讨论。
- **公平性与充分性未知**：缺少与具体基线方法的定量对比、消融实验和统计检验信息，无法判断实验是否完全客观公平。

（完）
