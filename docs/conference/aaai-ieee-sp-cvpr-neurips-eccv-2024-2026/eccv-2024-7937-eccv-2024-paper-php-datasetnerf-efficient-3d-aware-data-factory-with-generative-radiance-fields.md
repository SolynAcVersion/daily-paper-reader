---
title: "DatasetNeRF: Efficient 3D-aware Data Factory with Generative Radiance Fields"
title_zh: DatasetNeRF：基于生成辐射场的高效三维感知数据工厂
authors: "Yu Chi*, Fangneng Zhan, Sibo Wu, Christian Theobalt, Adam Kortylewski ;"
date: 2024-10-01
pdf: "https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/07937.pdf"
tags: ["query:cad-spatial"]
score: 4.0
evidence: 生成三维一致标注与分割作为训练数据
tldr: 针对三维视觉任务中多视角标注与点云分割数据获取耗时费力的问题，本文提出DatasetNeRF数据工厂。方法利用三维生成模型中的语义先验训练语义解码器，仅需少量精细标注即可在潜空间中泛化并生成无限数据。生成的标注可用于多种计算机视觉任务，降低了三维监督数据的构建成本。
source: ECCV-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1202, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1249, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 666, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1257, \"height\": 960, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1246, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1252, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1255, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1249, \"height\": 327, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1251, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1273, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 824, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1081, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/eccv-2024-accepted/eccv-2024-7937-eccv-2024-paper-php/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1245, \"height\": 278, \"label\": \"Table\"}]"
motivation: 三维视觉任务需要大量多视角一致标注与点云分割，人工标注代价高昂。
method: 利用三维生成模型的语义先验训练语义解码器，仅需少量标注即可生成无限三维一致数据。
result: 可生成高质量的二维一致标注与三维点云分割，适用于多种视觉任务。
conclusion: 为三维监督数据的自动化构建提供了高效途径。
---

## Abstract
"Progress in 3D computer vision tasks demands a huge amount of data, yet annotating multi-view images with 3D-consistent annotations, or point clouds with part segmentation is both time-consuming and challenging. This paper introduces DatasetNeRF, a novel approach capable of generating infinite, high-quality 3D-consistent 2D annotations alongside 3D point cloud segmentations, while utilizing minimal 2D human-labeled annotations. Specifically, we leverage the semantic prior within a 3D generative model to train a semantic decoder, requiring only a handful of fine-grained labeled samples. Once trained, the decoder generalizes across the latent space, enabling the generation of infinite data. The generated data is applicable across various computer vision tasks, including video segmentation and 3D point cloud segmentation in both synthetic and real-world scenarios. Our approach not only surpasses baseline models in segmentation quality, achieving superior 3D-Consistency and segmentation precision on individual images, but also demonstrates versatility by being applicable to both articulated and non-articulated generative models. Furthermore, we explore applications stemming from our approach, such as 3D-aware semantic editing and 3D inversion. Code can be found at /GenIntel/DatasetNeRF."

---

## 论文详细总结（自动生成）

# DatasetNeRF 论文总结

## 1. 核心问题与整体含义

- **研究动机**：三维计算机视觉任务（如视频分割、点云部件分割）依赖大量高质量标注数据，但多视角图像的 3D 一致标注与点云部件分割标注耗时且困难。
- **背景趋势**：大模型/基础模型训练需要海量 2D 或 3D 标注数据；已有工作（如 DatasetGAN、DatasetDM）利用 2D 生成模型的语义先验，以少量人工标注生成大量数据，但主要局限于 2D 任务。
- **关键机会**：几何感知 3D GAN（如 EG3D、pi-GAN）将潜码与相机位姿解耦，为 3D 感知数据生成提供了新途径。
- **整体含义**：本文提出 **DatasetNeRF**，一个基于生成辐射场的 3D 感知数据工厂，仅需少量 2D 人工标注，即可生成无限量、高质量的 3D 一致 2D 标注与 3D 点云部件分割，并可迁移至真实场景。

## 2. 方法论

### 核心思想

- 以预训练 3D GAN（EG3D）为骨干，附加语义分割分支，利用生成器 backbone 中的语义先验训练语义解码器。
- 仅需少量精细标注样本，训练后的解码器可在潜空间中泛化，随机采样潜码即可生成对应的高质量 3D 一致标注。
- 利用预训练模型的深度先验，将 2D 语义掩码反投影为 3D 点云部件分割。

### 关键技术细节

- **增强 Tri-plane 构建**：
  - 取生成器连续 synthesis block 的全部输出特征 {S₀, S₁, …, S_k}。
  - 上采样至最高输出分辨率后拼接为 [N, N, C] 特征张量，再 reshape 为增强 tri-plane。
  - 与 EG3D 仅使用单一特征不同，该设计显著提升分割质量（消融验证）。

- **语义解码与渲染**：
  - 对任意 3D 位置 x，投影到三个特征平面，双线性插值得 (F_xy, F_xz, F_yz)，求和聚合。
  - 聚合特征输入语义解码器，输出 32 通道语义特征。
  - 复用预训练 RGB 解码器在相同 tri-plane 点的密度 σ 作为密度先验，增强 3D 一致性。
  - 语义体渲染在 128² 分辨率下得到原始语义图 Î_s ∈ R^{128×128×C} 与语义特征图 Î_φ ∈ R^{128×128×32}。
  - 语义超分模块 U_s 将其精炼为高分辨率分割：  
    **Î⁺_s = U_s(Î_s, Î_φ)**，其中 Î⁺_s ∈ R^{512×512×C}。

- **训练损失**：  
  **L_CE(I_s, Î⁺_s) = − Σ_{c=1}^{C} I_{s,c} log(Î⁺_{s,c})**  
  其中 I_{s,c} 为真实类别标签的二值指示，Î⁺_{s,c} 为预测概率。

- **3D 点云分割生成**：
  - 用预训练 RGB 分支通过体渲染 ray marching 渲染深度图（沿射线加权平均深度）。
  - 深度图上采样至语义掩码尺寸，将语义掩码反投影到 3D 空间。
  - 融合多视角反投影结果，形成完整点云部件分割（图 3）。

- **扩展至 Articulated 生成辐射场**：
  - 以 GNARF 生成器为骨干，结合 tri-plane 与模板形状引导的显式特征变形。
  - 语义分支训练于变形感知特征 tri-plane 之上，训练集含 150 个标注（30 个人体样本、60 个训练姿态），可泛化到新人体姿态。

- **应用扩展**：
  - **3D RGB Inversion**：对任意位姿 RGB 图像，联合优化潜码 z 与位姿，用 MSE 损失 + Adam 优化，可多视角渲染分割。
  - **3D Segmentation Inversion**：对任意位姿语义掩码进行 GAN inversion，联合优化 z 与位姿，用交叉熵损失 + Adam。
  - **3D-aware Semantic Editing**：编辑输入标签图，通过 GAN inversion 更新潜码，损失函数结合标签交叉熵、RGB MSE、VGG 感知损失，FFHQ 上额外加入身份损失。

## 3. 实验设计

### 数据集与场景

| 数据集 | 用途 | 标注量 |
|---|---|---|
| AFHQ-Cat | 猫脸 2D 分割 + 点云分割 | 90 个精细标注（30 主体 × 3 视角） |
| FFHQ | 人脸 2D 分割 | 90 个精细标注（30 主体 × 3 视角） |
| AIST++ | 人体姿态分割（articulated） | 150 个标注（60 姿态） |
| ShapeNet-Car | 点云部件分割 | 90 个标注（30 样本 × 1 视角），标签：hood、roof、wheels、other |
| Nersemble | 真实世界人脸点云分割 | 无训练标注，用于测试泛化 |

### Benchmark 与对比方法

- **2D 分割网络**：Deeplab-V3 + ResNet101 骨干。
- **基线方法**：
  - **Transfer Learning**：微调 ImageNet 预训练网络最后一层。
  - **DatasetGAN**：用标注数据训练，生成 10K 图像-标注对训练 Deeplab-V3。
  - **DatasetNeRF**：生成 10K 均匀角度图像训练。
- **测试集**：90 个任意位姿个体图像标注 + 61 帧视频序列。
- **3D 点云**：PointNet 为骨干；AFHQ-Cat 从 1200 生成样本中固定 100 点云为测试集；ShapeNet-Car 原始 1825 点云（500 测试 / 1325 训练），对比多种训练配置。

### 主要实验组

- 2D 分割：AFHQ-Cat 与 FFHQ 上个体（Ind.）与视频（Vid.）测试，对比 3 种方法。
- 3D 点云分割：
  - AFHQ-Cat：400/600/800/1100 生成样本训练对比。
  - ShapeNet-Car：600(ShapeNet)、600(ShapeNet)+725(Generated)、1325(ShapeNet)、1325(ShapeNet)+1325(Generated)。
  - Nersemble 真实人脸：1200 生成点云训练，定性评估。
- 消融实验：多尺度特征、密度先验（个体与视频）、训练样本量（30/45/90）。
- 应用演示：3D RGB Inversion、3D Segmentation Inversion、3D-aware Semantic Editing。

## 4. 资源与算力

- **论文未明确说明**所使用的 GPU 型号、数量、训练时长或总计算量。
- 仅提及增强 tri-plane 的拼接特征在**内存效率与计算需求**上面临挑战，未来需优化最具代表性的语义特征以降低开销。
- 由于缺乏算力细节，复现成本与可扩展性评估受限。

## 5. 实验数量与充分性

- **实验数量**：约 10 余组定量实验，覆盖 4 个数据集、2D/3D 任务、多种训练配置与消融项。
- **充分性**：
  - 覆盖合成（AFHQ-Cat、FFHQ、AIST++、ShapeNet-Car）与真实（Nersemble）场景。
  - 同时评估 2D 分割、3D 点云分割、articulated 人体姿态、应用演示。
  - 消融实验验证了多尺度特征与密度先验的有效性，并分析了训练样本量影响。
- **客观性与公平性**：
  - 与 DatasetGAN 对比时调整特征尺寸以匹配，确保公平。
  - 使用相同标注数据训练基线。
  - 但缺少与更多 3D 感知分割方法（如 Pix2pix3D、Semantic-NeRF 等）的定量对比。
  - 真实世界仅做定性评估，缺少定量指标。

## 6. 主要结论与发现

- DatasetNeRF 仅需少量 2D 标注即可生成无限量 3D 一致 2D 标注与 3D 点云部件分割。
- 在 AFHQ-Cat 和 FFHQ 视频测试集上，分割质量超越 Transfer Learning 与 DatasetGAN；个体测试集上 AFHQ-Cat 更优，FFHQ 相当。
- 生成的点云数据可作为 ShapeNet-Car 的替代或增强：1325(ShapeNet)+1325(Generated) 取得最佳 mIoU 0.7571 与 Accuracy 0.9104。
- 模型可泛化至真实世界人脸点云（Nersemble），在颈部、鼻梁、眼睛、脸颊、额头等区域分割合理，但耳朵易误分类。
- 方法兼容 articulated（GNARF）与非 articulated（EG3D）生成模型，支持人体姿态一致性分割。
- 支持 3D 感知语义编辑、3D RGB/语义 inversion 等下游应用。

## 7. 优点

- **标注效率极高**：仅需 90–150 个精细标注即可生成无限数据，大幅降低人工成本。
- **3D 一致性**：利用 3D GAN 几何先验与密度先验，生成多视角一致的分割掩码，视频测试集提升显著。
- **增强 Tri-plane 设计**：融合多尺度生成器特征，消融显示 mIoU 从 0.4014 提升至 0.4796，效果显著。
- **密度先验复用**：直接复用预训练 RGB 解码器密度，无需额外监督即可增强 3D 一致性。
- **点云生成无需额外标注**：利用深度先验反投影与多视角融合，自动获得点云部件分割。
- **架构通用性**：兼容 articulated 与非 articulated 生成模型，可扩展至人体姿态。
- **应用广泛**：支持 3D inversion、语义编辑，且可作为现有 3D 基准的增强数据源。
- **真实场景泛化**：在 Nersemble 真实人脸点云上展示合理分割能力。

## 8. 不足与局限

- **依赖预标注数据**：方法依赖可用且合适的预标注数据，限制其在室内场景分割等更通用语境的应用。
- **骨干模型限制**：仅使用 3D GAN（EG3D、GNARF），擅长单类别数据分布；未来需扩展至扩散模型以利用更广的生成多样性。
- **计算与内存开销**：拼接多尺度特征为 tri-plane 虽提升质量，但带来内存效率与计算需求的挑战。
- **真实场景精度有限**：在 Nersemble 上耳朵区域误分类，真实世界泛化仍有提升空间。
- **算力信息缺失**：未报告 GPU 型号、数量与训练时长，影响可复现性与成本评估。
- **实验覆盖有限**：数据集集中在人脸、猫、汽车、人体，类别较少；缺少与更多 3D 感知分割方法的定量对比。
- **真实世界仅定性**：Nersemble 实验为定性展示，缺乏定量指标，说服力受限。
- **编辑与 inversion 依赖 GAN inversion 质量**：3D 编辑与 inversion 的效果受潜码优化质量影响，可能存在 2D-to-3D 歧义。

（完）
