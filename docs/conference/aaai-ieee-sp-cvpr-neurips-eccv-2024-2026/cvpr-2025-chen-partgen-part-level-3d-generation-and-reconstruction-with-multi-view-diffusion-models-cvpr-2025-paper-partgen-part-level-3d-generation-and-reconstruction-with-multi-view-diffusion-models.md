---
title: "PartGen: Part-level 3D Generation and Reconstruction with Multi-view Diffusion Models"
title_zh: PartGen：基于多视角扩散模型的部件级三维生成与重建
authors: "Chen, Minghao, Shapovalov, Roman, Laina, Iro, Monnier, Tom, Wang, Jianyuan, Novotny, David, Vedaldi, Andrea"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Chen_PartGen_Part-level_3D_Generation_and_Reconstruction_with_Multi-view_Diffusion_Models_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 多视角扩散从二维视图一致地构建三维结构
tldr: 现有三维生成与扫描方法产出的往往是缺乏结构、难以独立编辑的融合整体。该文提出PartGen，先用多视角扩散模型从多个视角提取一致的分部件分割，再用第二个扩散模型对每个部件单独生成与补全，从而得到可独立操作的有意义部件。方法在文本、图像及无结构网格输入下均能生成结构化三维资产。其贡献在于把二维多视角信息转化为结构化三维部件表示，对理解视图到三维的映射具有参考价值。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1785, \"height\": 808, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1745, \"height\": 562, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 775, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1712, \"height\": 689, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 858, \"height\": 509, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1721, \"height\": 912, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 761, \"height\": 776, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1442, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-chen-partgen-part-level-3d-generation-and-reconstruction-with-multi-view-diffusion-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 204, \"label\": \"Table\"}]"
motivation: 现有三维生成与扫描得到的是缺乏结构、无法独立编辑的融合整体，难以满足需要分部件操作的设计流程。
method: 先用多视角扩散模型从多视角提取一致的分部件分割，再用第二个多视角扩散模型对每个部件单独生成与重建。
result: 在文本、图像和无结构三维网格输入下均能生成由有意义部件组成的三维对象。
conclusion: 把多视角二维信息转化为结构化三维部件表示，为视图到三维的映射提供了可迁移思路。
---

## Abstract
Text- or image-to-3D generators and 3D scanners can now produce 3D assets with high-quality shapes and textures, but as single, fused entities lacking meaningful structure. In contrast, most applications and creative workflows require 3D assets to be composed of distinct, meaningful parts that can be independently manipulated. To bridge this gap, we introduce PartGen, a novel approach for generating, from text, images, or unstructured 3D objects, 3D objects composed of meaningful parts. Our method leverages a multi-view diffusion model to extract plausible and view-consistent part segmentations from multiple views of a 3D object, dividing it into meaningful components. A second multi-view diffusion model then processes each part individually, filling in occlusions and generating completed views, which are subsequently passed to a 3D reconstruction network. The completion process ensures that the reconstructed parts integrate cohesively by considering the context of the entire object, compensating for missing information caused by occlusions and, in extreme cases, hallucinating entirely invisible parts based on contextual cues. We evaluate PartGen on both generated and real 3D assets, demonstrating significant improvements over segmentation and part completion baselines. We also showcase downstream applications such as text-guided 3D part editing.

---

## 论文详细总结（自动生成）

# PartGen 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有文本/图像到 3D 的生成方法以及 3D 扫描方法，通常输出高质量但“融合”的单体 3D 资产，缺乏有意义、可独立操作的部件结构。
- **研究动机**：专业 3D 工作流、游戏、动画、机器人和具身 AI 等场景，往往需要将对象拆分为可复用、可编辑、可动画、可替换的部件，而不是一个不可分离的整体。
- **整体含义**：PartGen 试图把现有 3D 生成管线从“生成无结构对象”升级为“生成由有意义部件组成的组合式 3D 对象”。它可从文本、图像或无结构 3D 资产出发，自动完成部件分割、补全和 3D 重建，并支持文本引导的部件编辑。
- **关键挑战**：
  - 部件分割本身具有歧义：不同艺术家对同一对象可能有不同分解方式，不存在唯一“金标准”。
  - 部件补全具有歧义：许多部件被遮挡，甚至完全不可见，需要根据上下文合理“补全”甚至“幻觉”。
  - 3D 重建模型通常是确定性的，难以直接处理遮挡和不可见区域。

## 2. 论文提出的方法论

- **核心思想**：利用多视角扩散模型的多视角一致生成能力，先做多视角部件分割，再做上下文部件补全，最后将补全后的多视角部件图像送入 3D 重建网络。
- **总体流程**：
  1. 从文本、图像或已有 3D 对象获得对象的多视角图像网格 \(I\)，通常为 4 个正交视角组成的 \(2\times2\) 网格。
  2. 多视角扩散分割模型 \(\Phi_{\text{seg}}\) 生成颜色编码的部件分割图。
  3. 多视角扩散补全模型 \(\Phi_{\text{comp}}\) 对每个部件进行补全，生成完整、视角一致的部件图像。
  4. 预训练 3D 重建模型 \(\Psi\) 将补全后的部件图像重建为 3D 部件，并组合成结构化 3D 对象。

### 2.1 多视角部件分割

- 将部件分割建模为**随机多视角一致着色问题**。
- 训练数据中，对象 \(L=(S_1,\dots,S_S)\) 被分解为若干 3D 部件；将 RGB 空间量化为 \(Q\) 个固定颜色 \(c_1,\dots,c_Q\)。
- 对每个训练样本，随机排列颜色并分配给各部件，渲染得到颜色编码的多视角分割图 \(C\)。
- 微调多视角图像生成器 \(\Phi\) 得到 \(\Phi_{\text{seg}}\)，使其条件于多视角图像 \(I\)，采样生成分割图：
  \[
  C \sim p(C \mid \Phi_{\text{seg}}, I)
  \]
- 测试时，对生成的彩色分割图按参考颜色量化，得到部件掩码；丢弃像素过少的部件。
- 由于模型是随机生成式的，多次采样可得到多种合理分割，隐式处理了部件“命名”和分解歧义。

### 2.2 上下文部件补全

- 直接使用掩码图像 \(I\odot M\) 送入重建模型会遇到遮挡和不可见问题。
- 论文微调另一个多视角生成器为补全模型 \(\Phi_{\text{comp}}\)，建模：
  \[
  \hat{J} \sim p(\hat{J} \mid \Phi_{\text{comp}}, I\odot M, I, M)
  \]
  即同时条件于：
  - 被掩码的部件图像 \(I\odot M\)；
  - 完整对象上下文图像 \(I\)；
  - 部件掩码 \(M\)。
- 上下文 \(I\) 帮助补全部件，使其与整体对象和其他部件协调；遮挡越严重，上下文越重要。
- 实现上，使用 VAE 分别编码 masked image 和 context image，得到 \(2\times8\) 通道；再拼接 8 维噪声潜变量和未编码的 mask，共 25 通道输入扩散模型。

### 2.3 部件重建

- 补全后的多视角部件图像 \(\hat{J}\) 已完整且视角一致，可直接送入重建模型：
  \[
  \hat{S} = \Psi(\hat{J})
  \]
- 论文发现重建模型无需针对部件任务微调，使用高质量预训练重建模型即可。
- 实验中重建模型采用 LightplaneLRM。

### 2.4 训练数据构建

- 使用约 140k 个艺术家创建的 3D GLTF 资产，每个资产通常包含多个 watertight mesh，即天然部件。
- 文本条件训练：选取 10k 最高质量资产，用类似 CAP3D 的流程和 LLAMA3 生成文本描述。
- 图像条件训练：使用全部 140k 模型，以随机方向单视角渲染作为条件
