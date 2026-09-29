---
title: "PyTorchGeoNodes: Enabling Differentiable Shape Programs for 3D Shape Reconstruction"
title_zh: PyTorchGeoNodes：面向三维形状重建的可微形状程序
authors: "Stekovic, Sinisa, Artykov, Arslan, Ainetter, Stefan, D'Urso, Mattia, Fraundorfer, Friedrich"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Stekovic_PyTorchGeoNodes_Enabling_Differentiable_Shape_Programs_for_3D_Shape_Reconstruction_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 6.0
evidence: 通过可解释形状程序从图像重建三维物体及其参数
tldr: 论文针对形状程序在三维场景理解中长期被忽视的问题，指出其相比传统CAD模型检索可推理语义参数、支持编辑且内存占用低。为此提出PyTorchGeoNodes，将Blender设计的程序化模型解析为高效PyTorch代码以实现可微优化。结合遗传算法可同时优化离散与连续参数，从图像重建三维物体及其可解释参数。该工作为参数化、可解释的CAD式三维重建提供了可微工具。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1460, \"height\": 652, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1384, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1627, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 823, \"height\": 300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 670, \"height\": 302, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 837, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 696, \"height\": 553, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-stekovic-pytorchgeonodes-enabling-differentiable-shape-programs-for-3d-shape-reconstruction-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1670, \"height\": 1043, \"label\": \"Table\"}]"
motivation: 形状程序可推理语义参数并支持编辑，但在三维场景理解中尚未被充分利用。
method: 将Blender程序化模型解析为PyTorch可微代码，结合遗传算法优化离散与连续参数。
result: 可从图像重建三维物体及其可解释参数，兼具低内存与可编辑优势。
conclusion: 为可解释、参数化的CAD式三维重建提供了可微优化框架。
---

## Abstract
We propose PyTorchGeoNodes, a differentiable module for reconstructing 3D objects and their parameters from images using interpretable shape programs. Unlike traditional CAD model retrieval, shape programs allow reasoning about semantic parameters, editing, and a low memory footprint. Despite their potential, shape programs for 3D scene understanding have been largely overlooked. Our key contribution is enabling gradient-based optimization by parsing shape programs, or more precisely procedural models designed in Blender, into efficient PyTorch code. While there are many possible applications of our PyTochGeoNodes, we show that a combination of PyTorchGeoNodes with genetic algorithm is a method of choice to optimize both discrete and continuous shape program parameters for 3D reconstruction and understanding of 3D object parameters. Our modular framework can be further integrated with other reconstruction algorithms, and we demonstrate one such integration to enable procedural Gaussian splatting. Our experiments on the ScanNet dataset show that our method achieves accurate reconstructions while enabling, until now, unseen level of 3D scene understanding.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义
- **研究动机**：传统三维物体表示（体素、网格、SDF、NeRF、Gaussian Splatting、CAD 模型检索）各有局限：神经表示易产生伪影且内存大，CAD 检索受数据库覆盖限制，难以处理被遮挡、变形或语义参数不同的物体。
- **核心问题**：形状程序（shape programs）可生成可解释、可编辑、低内存占用的三维形状，但其参数从图像/RGB-D 扫描中估计很困难，尤其是离散参数（如书架层数、椅子腿数）与连续参数（如尺寸）混合时无法直接用梯度下降优化。
- **整体含义**：论文提出 **PyTorchGeoNodes**，把 Blender 中设计的程序化模型解析为可微 PyTorch 代码，使形状程序可用于三维重建与场景理解，并实现参数级、语义级的物体重建。

## 2. 方法论
### 2.1 核心思想
- 将 Blender Geometry Nodes 定义的形状程序视为计算图，解析/编译为 PyTorch 或 PyTorch3D 实现。
- 对连续参数支持梯度反传；对离散/布尔参数，结合遗传算法进行搜索，并在选择阶段用梯度下降细化连续参数。
- 进一步把 Gaussian Splatting 集成进形状程序，使程序化模型既能表达语义结构，又能捕捉细节和外观。

### 2.2 关键技术细节
- **节点类型**：Input、Math、Switch、Combine、Primitive、Transform、Mesh Line、Points on instances、Join geometry、Output geometry。
- **可微性**：Transform 等连续节点可微；Points on instances 依赖整数，Switch 依赖布尔值，因此不能单纯梯度优化。
- **优化目标**：
  - \(L(P)=\lambda_{CD}L_{CD}(P_C,S_h(P))+\lambda_G L_G(G,S_h(P))+\lambda_{Fl}L_{Fl}(P_C,S_h(P))\)。
  - \(L_{CD}\)：目标点云与生成形状的单向 Chamfer 距离。
  - \(L_G\)：遮挡网格惩罚，避免生成形状占据场景中被遮挡区域。
  - \(L_{Fl}\)：地面约束，使物体最低点贴近地板。
  - 权重：\(\lambda_{CD}=1,\lambda_G=0.5,\lambda_{Fl}=0.01\)。
- **参数搜索**：
  - 遗传算法流程：初始化种群、交叉、变异、选择。
  - 离散参数变异：以概率 \(P_m\) 从有效值集合中随机替换。
  - 连续参数变异：以概率加入高斯噪声或离散化候选值加噪声。
  - 选择阶段使用 PyTorchGeoNodes 对连续参数做梯度细化，再形成下一代种群。
- **Gaussian 集成**：
  - 扩展 Primitive 节点，使其同时创建可训练 Gaussian 参数。
  - 将网格子采样为三角形并初始化 Gaussian 的均值、尺度、旋转、颜色和透明度。
  - 先估计形状参数，再优化 Gaussian，损失包括颜色、深度、形状-Gaussian 一致性、正则项和背景一致性。
  - 由于重复部件在程序图中被克隆，Gaussian 参数可共享，从而利用对称性恢复被遮挡部分。

## 3. 实验设计
- **数据集/场景**：
  - 主要实验：ScanNet 验证场景中的 RGB-D 室内扫描。
  - 手动标注 176 个物体：57 个沙发、52 把椅子、67 张桌子。
  - 补充材料：自动生成合成场景，并包含额外物体类别。
- **Benchmark/指标**：
  - 重建质量：Chamfer 距离、绝对旋转误差。
  - 形状参数理解：连续参数平均绝对差、离散参数分类准确率。
  - 参数级评估是本文强调的重点，因为现有数据集通常不标注这些形状程序参数。
- **对比方法**：
  - GeoCode [27]：监督学习方法，使用 DGCNN 编码器和多参数解码器，在 10000 个合成实例上训练，再用 PyTorchGeoNodes 梯度细化。
  - 坐标下降（Coordinate Descent, CD）：逐参数替换搜索，再梯度细化。
  - 本文遗传算法：有/无梯度细化版本。
- **定性结果**：
  - 展示椅子、桌子、沙发的参数恢复与投影对齐。
  - 展示 Gaussian 集成后的程序化编辑，例如改变沙发宽度、移除靠背/扶手等。

## 4. 资源与算力
- 论文正文**未明确说明**使用的 GPU 型号、数量、训练时长或总计算量。
- 仅在致谢中提到使用了 GENCI-IDRIS 的 HPC 资源，Grant 2024-AD010615585。
- GeoCode 基线提到使用 10000 个随机生成的合成形状程序参数实例训练，但未给出硬件和训练时间细节。
- 因此，从给定文本无法评估其算力开销和复现所需资源。

## 5. 实验数量与充分性
- 主要真实数据实验集中在 ScanNet 的 3 个家具类别：沙发、椅子、桌子，共 176 个手动标注物体。
- 表 1 报告了 Table 类别的连续参数误差、离散参数分类准确率，以及所有类别的 Chamfer 距离和旋转误差。
- 消融/对比覆盖：
  - GeoCode 监督学习 vs 坐标下降 vs 遗传算法。
  - 有/无梯度细化。
  - 连续参数与离散参数分别评估。
- 补充材料包含合成场景、额外类别和下游点云分割应用。
- **充分性评价**：
  - 对该任务而言，实验覆盖了关键优化策略和真实数据，参数级评估较有针对性。
  - 但类别较少，仅限室内家具；未在多个真实数据集上验证。
  - 未报告多次运行的方差、显著性检验或完整运行时间。
  - 高斯集成部分主要是定性和编辑演示，缺少系统量化评估。
  - 对比方法数量有限，未与更多 CAD 检索、神经重建或 Gaussian 重建方法做大规模量化比较。

## 6. 主要结论与发现
- PyTorchGeoNodes 能有效把 Blender 形状程序转成可微 PyTorch 代码，使形状程序可用于三维重建优化。
- 遗传算法结合梯度细化，能同时优化离散和连续形状参数，在 ScanNet 上优于 GeoCode 监督学习和坐标下降基线。
- 梯度细化对连续参数精度有明显帮助。
- 方法能恢复语义参数，如桌面形状、腿类型、是否存在柜体/中板、沙发扶手/靠背等。
- 集成 Gaussian Splatting 后，可实现程序化 Gaussian 重建与编辑，并利用克隆部件恢复遮挡区域。
- 整体上，论文展示了可解释、参数化、可编辑的三维场景理解新路径。

## 7.

## 7. 局限性与未来工作

- **对程序库与先验结构的依赖较强**：方法假定目标物体可由预先定义的 Blender Geometry Nodes 形状程序表示。若真实物体的拓扑、部件组合或语义结构超出程序库覆盖范围，优化只能在已有程序空间内寻找近似解，可能无法恢复正确结构。
- **离散参数搜索的计算代价可能较高**：遗传算法需要维护种群并反复调用可微前向/反向过程，结合梯度细化后，单物体重建可能涉及大量迭代。论文未报告运行时间、收敛曲线或不同种群规模下的效率，因此实际可扩展性仍不明确。
- **目标函数与权重较手工化**：Chamfer、遮挡惩罚和地面约束的权重固定为 \(1,0.5,0.01\)，这些超参数可能对场景尺度、噪声水平和物体类别敏感。单向 Chamfer 距离也未必能充分约束所有几何细节。
- **真实实验覆盖有限**：ScanNet 上仅评估沙发、椅子、桌子三类家具，共 176 个手动标注物体，且参数级真值依赖人工标注。缺少跨数据集、跨场景类型、跨传感器噪声的系统验证，也未报告多次运行的方差或显著性检验。
- **Gaussian 集成部分量化不足**：将 Gaussian Splatting 嵌入形状程序是亮点，但相关实验主要是定性展示和编辑演示，缺少与纯 Gaussian 重建、NeRF 或网格重建方法在渲染质量、几何精度、编辑一致性上的系统量化比较。
- **遮挡与多物体场景仍具挑战**：虽然克隆部件和 Gaussian 共享可利用对称性恢复被遮挡区域，但方法仍主要针对单个物体或已分割物体。若分割错误、物体间严重遮挡或存在复杂接触关系，优化可能失败。
- **可复现性与资源报告不足**：正文未说明 GPU 型号、数量、训练/优化时长和总计算量，仅致谢 HPC 资源。这对复现和评估实际部署成本造成障碍。

未来可能的方向包括：
- 扩展或自动学习形状程序库，例如结合程序归纳、大语言模型生成候选程序或从 CAD 数据中挖掘可复用节点图。
- 用 Gumbel-Softmax、REINFORCE、MCMC 或可微离散松弛替代/补充遗传算法，以降低混合离散-连续优化成本。
- 将单物体参数重建扩展到多物体联合场景理解，联合推理物体位姿、部件关系与场景图。
- 建立带形状程序参数标注的标准化 benchmark，支持更公平的参数级评估。
- 进一步研究可编辑 Gaussian 表示，使程序参数、几何结构与外观属性能够联合优化并保持实时渲染能力。

## 8. 总体评价与启示

- **主要贡献**：论文把 Blender Geometry Nodes 这类程序化建模工具转化为可微 PyTorch 计算图，为“形状程序”与“基于图像/点云的可微重建”之间建立了桥梁。其价值不仅在于某个具体重建结果，而在于提供了一种可解释、可编辑、低内存的参数化三维表示优化框架。
- **方法亮点**：混合离散-连续优化策略较有针对性；用遗传算法处理离散结构、用梯度下降细化连续尺寸，符合形状程序参数的实际性质。将 Gaussian Splatting 嵌入程序节点，则尝试同时保留语义结构和外观细节，是较有前景的组合。
- **实验说服力**：在 ScanNet 家具类别上，参数级评估和与 GeoCode、坐标下降的对比显示该方法在离散参数恢复和连续参数细化方面有优势。但类别少、数据规模有限、缺少运行时间与方差报告，使其泛化性和效率仍待进一步证明。
- **对领域的启示**：该工作提示，三维重建不一定只能在体素、网格、SDF、NeRF 或 Gaussian 之间选择；程序化表示可作为中间层，把语义、结构和可编辑性引入优化过程。若能与自动程序生成、开放词汇分割和可微渲染更紧密结合，可能推动机器人、AR/VR、室内场景编辑和仿真数据生成等应用。
- **一句话总结**：PyTorchGeoNodes 是一次有意义的探索，证明了可微形状程序可用于参数级三维重建，但当前仍受程序库覆盖、优化效率和实验规模限制，距离开放世界通用场景理解还有明显距离。

（完）
