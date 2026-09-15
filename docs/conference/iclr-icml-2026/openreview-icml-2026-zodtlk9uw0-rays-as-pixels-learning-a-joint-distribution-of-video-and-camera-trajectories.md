---
title: "Rays as Pixels: Learning A Joint Distribution of Video and Camera Trajectories"
title_zh: 以像素为光线：学习视频与相机轨迹的联合分布
authors: "Wonbong Jang, Shikun Liu, Soubhik Sanyal, Juan Camilo Perez, Kam Woh Ng, Sanskar Agrawal, Juan-Manuel Perez-Rua, Yiannis Douratsos, Tao Xiang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/c0a4677a69a2b0522f6d321e1f3ee53bad83072c.pdf"
tags: ["query:video-gen-rl"]
score: 6.0
evidence: 视频扩散模型联合建模视频帧与相机轨迹分布
tldr: 相机参数恢复与新视角渲染长期被分开处理，在图像覆盖稀疏或相机位姿模糊时容易失败。本文提出Rays as Pixels，一种专用视频扩散模型，联合学习视频与相机轨迹的分布。作者将相机表示为密集光线像素，并通过解耦自交叉注意力与视频帧同步去噪。该联合建模提升了在稀疏条件下的鲁棒性，为统一生成式框架下的视频与几何感知提供了新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 相机参数恢复与新视角渲染被分开处理，在图像稀疏或位姿模糊时容易失败。
method: 提出Rays as Pixels视频扩散模型，用密集光线像素表示相机，并通过解耦自交叉注意力与视频帧联合去噪。
result: 联合分布建模在稀疏图像覆盖与模糊相机位姿下表现更稳健。
conclusion: 该框架统一了视频生成与相机几何感知。
---

## Abstract
Can we bridge the gap between perceiving camera trajectories and rendering novel views within a single generative framework? Recovering camera parameters from images and rendering scenes from novel viewpoints are considered the forward and inverse problems in the field of computer vision and graphics. Previous approaches treat these problems in isolation, often failing when image coverage is sparse or camera poses are ambiguous. In this work, we propose Rays as Pixels, a specialized Video Diffusion Model (VDM) that learns a joint distribution of videos and camera trajectories. We represent cameras as dense ray pixels (raxels) and simultaneously denoise them alongside video frames using a novel Decoupled Self-Cross Attention. This joint formulation enables us to: i) generate a video from multiple input images following a defined camera trajectory, ii) perform novel view synthesis from sparse views (without necessarily requiring camera poses), and iii) predict the camera trajectory from a raw video. We evaluate our model on pose estimation, camera-controlled video generation and validate its self-consistency. Please reference supplementary material for more qualitative results.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取失败，现有材料仅包含标题、作者、元数据与摘要。因此以下总结主要依据摘要，涉及数据集、算力、实验组数、具体指标等内容无法从现有材料确认，我会明确标注而不做臆测。

## 1. 核心问题与整体含义

- **研究动机**：相机参数恢复与新视角渲染长期被当作两个独立问题处理，前者是从图像推断相机位姿的逆问题，后者是从新视角渲染图像的前向问题。
- **背景痛点**：这种分离式处理在图像覆盖稀疏、相机位姿模糊或不完整时容易失败，且两个阶段之间缺乏一致性约束，误差会传播。
- **整体含义**：论文试图在一个统一的生成式框架中桥接“感知相机轨迹”和“渲染新视角”，通过学习视频与相机轨迹的联合分布，使视频生成与相机几何感知相互促进。

## 2. 方法论

- **核心思想**：提出 **Rays as Pixels**，一种专用视频扩散模型（Video Diffusion Model, VDM），联合建模视频帧与相机轨迹的分布。
- **相机表示**：将相机表示为 **密集光线像素（raxels）**，即每个像素对应一条光线，使相机轨迹能以类似图像像素的密集形式参与扩散建模，而不是仅用低维内外参向量表示。
- **联合去噪**：模型同时去噪视频帧和 raxels，通过一种新的 **Decoupled Self-Cross Attention** 机制进行交互。该机制解耦自注意力与交叉注意力，用于处理视频帧内部、光线像素内部以及视频与相机轨迹之间的跨模态关系。
- **算法流程（文字描述）**：输入带噪的视频帧表示与带噪的 raxels 表示；在扩散去噪的每一步中，通过解耦的自注意力和交叉注意力让视频模态与相机模态同步更新；最终得到相互一致的视频与相机轨迹。论文摘要未给出显式公式或损失函数。
- **支持任务**：
  - 从多张输入图像出发，按照指定相机轨迹生成视频；
  - 从稀疏视图进行新视角合成，且不一定需要预先提供相机位姿；
  - 从原始视频预测相机轨迹。

## 3. 实验设计

- **评估任务**：摘要明确提到在 **位姿估计（pose estimation）**、**相机控制视频生成（camera-controlled video generation）** 上评估，并验证模型的 **自一致性（self-consistency）**。
- **场景**：包括稀疏视图新视角合成、多图像按轨迹生成视频、从原始视频预测相机轨迹。
- **数据集 / Benchmark**：现有材料未给出具体数据集名称、benchmark 或评测协议。
- **对比方法**：现有材料未列出基线方法或对比对象。
- **评价指标**：摘要未说明使用了哪些定量指标，例如 PSNR、SSIM、LPIPS、旋转/平移误差等均无法确认。

## 4. 资源与算力

- 提供的文本中 **没有提及 GPU 型号、数量、训练时长、参数量或训练成本**。
- 因此无法总结算力资源。若需评估可复现性与计算开销，需要查阅论文正文或补充材料。

## 5. 实验数量与充分性

- 从摘要可确认至少覆盖三类评估：位姿估计、相机控制视频生成、自一致性验证；此外还涉及稀疏视图新视角合成和从视频预测轨迹等能力。
- 但现有材料 **没有给出具体实验组数、数据集数量、消融实验、基线数量或统计显著性分析**。
- 因此无法判断实验是否充分、客观、公平。仅就摘要而言，任务覆盖较广，但缺乏细节支撑，需正文确认。

## 6. 主要结论与发现

- 视频与相机轨迹的 **联合分布建模** 能提升在稀疏图像覆盖和模糊相机位姿条件下的鲁棒性。
- 该框架可以在统一生成式模型中同时支持视频生成、新视角合成和相机轨迹预测。
- 摘要认为该工作为统一视频生成与相机几何感知提供了新思路，并验证了模型的自一致性。

## 7. 优点

- **统一框架**：将相机参数恢复与视频/新视角生成放入同一扩散模型，减少两阶段方法的误差传播。
- **表示新颖**：用密集光线像素 raxels 表示相机，使相机轨迹与视频帧在表示层面更对齐，便于扩散模型处理。
- **注意力设计**：Decoupled Self-Cross Attention 有望缓解双模态联合去噪时的干扰问题。
- **稀疏视图友好**：支持在不一定提供相机位姿的情况下进行稀疏视图新视角合成，降低对位姿标注的依赖。
- **多任务能力**：同一模型覆盖视频生成、新视角合成和位姿估计，具备较强通用性。

## 8. 不足与局限

- **材料限制**：由于 PDF 正文未成功提取，无法核实方法细节、公式、实验设置和结果，当前总结只能基于摘要。
- **计算开销风险**：视频扩散模型叠加密集光线像素表示，可能带来较高的显存和计算成本，但文中未说明。
- **几何精度与生成质量平衡**：扩散生成具有随机性，如何保证生成视频与相机轨迹的几何一致性仍需正文验证。
- **泛化与场景限制**：对动态场景、大视角变化、复杂光照材质、非针孔相机或畸变相机的适用性未在现有材料中说明。
- **评估公平性未知**：缺少数据集、基线、指标和消融细节，无法判断实验是否充分、公平。
- **应用限制**：若模型规模大、推理慢，可能限制实时或移动端部署；对训练数据分布的依赖也可能带来偏差风险。

（完）
