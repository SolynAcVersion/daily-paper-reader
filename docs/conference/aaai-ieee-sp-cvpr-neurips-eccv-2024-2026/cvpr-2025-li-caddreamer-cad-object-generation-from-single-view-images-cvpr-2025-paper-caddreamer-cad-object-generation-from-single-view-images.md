---
title: "CADDreamer: CAD Object Generation from Single-view Images"
title_zh: CADDreamer：从单视图图像生成CAD物体
authors: "Li, Yuan, Lin, Cheng, Liu, Yuan, Long, Xiaoxiao, Zhang, Chenxu, Wang, Ningna, Li, Xin, Wang, Wenping, Guo, Xiaohu"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Li_CADDreamer_CAD_Object_Generation_from_Single-view_Images_CVPR_2025_paper.pdf"
tags: ["query:cad-spatial"]
score: 7.0
evidence: 从单张图像生成结构化CAD模型
tldr: 针对现有三维生成模型只能产生稠密且无结构网格、难以得到紧凑清晰边界的CAD模型这一问题，本文提出CADDreamer，从单张图像生成CAD物体。方法将基元语义编码进颜色域，并用基元感知的多视角扩散模型对齐预训练扩散先验，从而推断多视角法向与语义图。实验表明该方法能生成结构规整的CAD形体，为图像到CAD逆向建模提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1803, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1609, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 782, \"height\": 284, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 850, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1802, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1810, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 866, \"height\": 318, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 898, \"height\": 708, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 859, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-caddreamer-cad-object-generation-from-single-view-images-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 605, \"height\": 293, \"label\": \"Table\"}]"
motivation: 现有三维生成模型输出过于稠密、缺乏结构，与人工构建的紧凑清晰CAD模型差距很大。
method: 提出基元感知的多视角扩散模型，将基元语义编码进颜色域并约束扩散先验，推断多视角法向图。
result: 实验显示该方法可从单张图像生成结构规整、边界清晰的CAD形体。
conclusion: 为单图像到结构化CAD模型的生成提供了可行方案。
---

## Abstract
The field of diffusion-based 3D generation has experienced tremendous progress in recent times. However, existing 3D generative models often produce overly dense and unstructured meshes, which are in stark contrast to the compact, structured and clear-edged CAD models created by human modelers. We introduce CADDreamer, a novel method for generating CAD objects from a single image. This method proposes a primitive-aware multi-view diffusion model, which perceives both local geometry and high-level structural semantics during the generation process. We encode primitive semantics into the color domain, and enforce the strong priors in pre-trained diffusion models to align with the well-defined primitives. As a result, we can infer multi-view normal maps and semantic maps from a single image, thereby reconstructing a mesh with primitive labels. Correspondingly, we propose a set of fitting and optimization methods to deal with the inevitable noise and distortion in generated primitives, ultimately producing a complete and seamless Boundary Representation (B-rep) of a Computer-Aided Design (CAD) model. Experimental results demonstrate that our method can effectively recover high-quality CAD objects from single-view images. Compared to existing 3D generation methods, the models produced by CADDreamer are compact in representation, clear in structure, sharp in boundaries, and watertight in topology.

---

## 论文详细总结（自动生成）

# CADDreamer 论文中文总结

## 1. 核心问题与整体含义
- **研究动机**：现有基于扩散模型的单视图 3D 生成方法虽然进展显著，但通常输出过于稠密、无结构、缺乏语义的网格，与人类设计师创建的紧凑、结构化、边缘锐利的 CAD 模型差距很大。
- **核心问题**：如何从单张 RGB 图像直接生成高质量 CAD 物体的边界表示（B-rep），使其具备紧凑表示、清晰结构、锐利边缘和封闭拓扑。
- **整体含义**：论文提出 CADDreamer，将单视图 3D 生成从“低层网格重建”推进到“高层结构化 CAD 重建”，为图像到 CAD 的逆向建模提供新思路，可服务于游戏、制造、产品设计等需要结构化 3D 模型的场景。

## 2. 方法论
- **核心思想**：采用两模块框架：先进行基元感知的多视角生成，获得带基元标签的 3D 网格；再进行几何与拓扑提取，优化基元参数并构造水密 B-rep。
- **模块一：多视角生成**
  - 输入单视图 RGB，先用现成法向预测器生成法向图，以降低纹理和光照干扰。
  - 微调跨域多视角扩散模型 Wonder3D，同时生成 \(m=6\) 个视角的法向图和语义基元图。
  - 将基元语义编码到颜色域，使预训练扩散先验与明确定义的基元对齐；基元包括平面、圆柱、圆锥、球、圆环及边界特征线。
  - 多视角法向图输入 NeuS 重建完整 3D 网格，并去除颜色与纹理重建损失。
  - 语义基元图反投影到网格，利用特征线划分 2D patch，再通过 Graph Cut 合并为 3D 基元 patch。Graph Cut 中，反投影 patch 为节点，相邻/重叠 patch 连边，边权为 RANSAC 基元参数的余弦相似度，并通过阈值选择最优分割。
- **模块二：几何与拓扑提取**
  - 对每个 mesh patch 使用 RANSAC 提取基元参数，如平面法向与位置、圆柱轴与半径、圆锥半角与高度、圆环主/次半径、球心与半径等。
  - **几何优化**：从相邻 patch 推断相交关系，采样边界顶点作为 stitching vertices，最小化其在两个基元表面投影点之间的距离：
    \[
    f_{stch}(v_i)=\|\pi(v_i,P_A)-\pi(v_i,P_B)\|
    \]
    并最小化所有 stitching vertices 的总和。
  - 同时恢复平行、共线、垂直等几何关系：平行共享轴方向；共线用 \(p_A=p_B+\vec{x}_B t\) 优化 \(t\)；垂直在目标函数中加入 \(\vec{x}_C\cdot\vec{x}_D\) 项。使用 L-BFGS 优化，关系检测容差为 0.05。
  - **拓扑表示提取**：每个 3D patch 对应一个拓扑面，相邻两 patch 的边曲线对应拓扑边，连接超过两个 patch 的 mesh 顶点对应拓扑顶点，并继承半边缘方向。
  - **拓扑保持 CAD 重建**：对每条拓扑边，求相邻两基元交线，选投影距离最近者作为 CAD 曲线；对每个拓扑顶点，求两条 CAD 曲线交点，选最近者作为 CAD 顶点；用顶点裁剪曲线得到 CAD 边，用边裁剪基元得到 CAD 面，最终合并为水密 B-rep。

## 3. 实验设计
- **数据集/场景**
  - 合成数据集：从 ABC 和 DeepCAD 中整理 30,000 个无缝 CAD 模型，添加纹理和背景并渲染多视角图像，得到 29,000 训练样本和 1,000 测试样本。
  - 真实图像：使用 Canon EOS R5 相机和 Canon EF 70 镜头拍摄真实 CAD 物体，使用 Era3D 去背景并生成法向图。
- **Benchmark 与对比方法**
  - 对比方法包括：SyncDreamer、LRM、CRM、InstantMesh 等单视图重建方法，并统一接 Point2CAD 进行基元分割、参数估计和 B-rep 转换。
  - 传统 sketch-extrude 方法因无法处理球、圆环、圆锥等基元，仅在补充材料中比较。
- **评价指标**
  - 网格与基元：Chamfer Distance、Normal Consistency、基于顶点的分割准确率 SEG(V)、基于基元数量的分割准确率 SEG(P)。
  - B-rep：悬挂面比例 HF、B-rep 与真值之间的 Chamfer Distance。
- **主要结果**
  - CADDreamer 在表 2 中取得 CD 1.27、NC 92.6、SEG(V) 95.7、SEG(P) 97.9，显著优于 CRM、LRM、InstantMesh、SyncDreamer。
  - 表 3 中 CADDreamer 的 HF 仅 2.4%，B-rep CD 为 1.36，远低于对比方法。
  - 真实图像实验展示出较好的泛化能力，能重建较高质量 CAD 模型。

## 4. 资源与算力
- 论文明确说明实验在单台机器上进行，配备 **8 块 NVIDIA A100 GPU（每块 80GB）** 和 **AMD EPYC 7313 CPU**。
- 使用 Wonder3D 作为预训练模型以加速和稳定收敛。
- **未明确说明训练时长、总 GPU 小时数或具体训练轮数**。

## 5. 实验数量与充分性
- 合成实验规模较大：30,000 个 CAD 模型，其中 29,000 训练、1,000 测试。
- 进行了与 4 个主流单视图重建方法的定量和定性对比，覆盖网格、基元分割和 B-rep 质量三类指标。
- 包含真实图像定性实验，验证泛化能力。
- 论文提到消融实验和局限性分析在补充材料中，但正文未给出消融组数、具体设置和结果。
- **充分性评价**：合成定量对比较充分，指标较全面，对比 pipeline 较统一；但真实图像缺少定量评价，消融实验未在正文展开，因此整体充分性中等偏上，仍有一定提升空间。

## 6. 主要结论与发现
- CADDreamer 能从单张图像生成紧凑、结构清晰、边缘锐利、拓扑水密的 CAD B-rep 模型。
- 同时捕捉低层几何特征（法向图）和高层语义结构（基元图），可显著减少重建噪声和失真。
- 几何优化能恢复基元之间的相交、平行、垂直、共线关系，避免错误交线、悬挂面和非封闭 B-rep。
- 拓扑保持的 B-rep 构建策略有效提升 CAD 顶点、边、面的准确性和水密性。
- 相比现有 3D 生成方法，CADDreamer 在 Chamfer Distance、法向一致性、分割准确率和悬挂面比例上均明显更优。

## 7. 优点
- **语义增强的多视角扩散**：将基元语义编码到颜色域，利用预训练扩散先验理解 CAD 高层结构。
- **基元感知与 Graph Cut 分割**：不依赖传统网格/点云分割，能更精确地提取基元 patch。
- **几何优化算法**：显式恢复平行、垂直、共线和相交关系，提升 B-rep 拓扑正确性。
- **拓扑保持重建**：从分割网格提取拓扑表示，引导 CAD 曲线、顶点和面的生成，保证水密性。
- **实验设计较全面**：合成数据定量 + 真实图像定性，多基线、多指标，结果优势明显。
- **实际应用潜力**：输出为紧凑结构化 CAD 模型，比稠密网格更适合制造和产品设计。

## 8. 不足与局限
- **图像数量与分辨率限制**：方法性能受输入图像质量和数量约束，难以检测极细几何特征，可能导致拟合不准或重建不完整。
- **视角与遮挡问题**：与现有单视图重建方法类似，挑战性视角和复杂遮挡下表现受限，尤其当单张图未展示所有基元时。
- **基元类型有限**：主要覆盖平面、圆柱、圆锥、球、圆环等规则基元，未涉及自由曲面或更复杂 CAD 结构。
- **真实图像缺少定量评价**：真实场景仅展示定性结果，未给出大规模真实数据上的定量指标。
- **消融实验在补充材料**：正文未详细展示消融组数、设置和结果，难以

难以判断各模块贡献，也无法验证关键设计的必要性。除上述局限外，还有以下问题值得注意：

- **对上游法向预测的依赖较强**：法向预测器的误差会沿多视角生成、NeuS 重建、RANSAC 拟合和 B-rep 构造逐级传播，可能造成基元参数偏移或拓扑错误。
- **训练分布与真实场景存在差距**：训练数据主要来自 ABC、DeepCAD 等合成 CAD 模型，虽然加入纹理和背景增强，但与真实工业零件、扫描数据、复杂光照之间仍有域差异。
- **输出更接近静态 B-rep，而非可编辑参数化历史**：方法可生成 CAD 风格边界表示，但通常不恢复草图、拉伸、旋转、布尔运算等构造序列，因此在下游参数化编辑和设计重用方面仍有局限。
- **计算与推理成本披露不足**：正文未给出推理时间、显存占用、多视角扩散与 NeuS 优化耗时等效率指标，难以判断其在实际交互式建模中的可用性。
- **细节与复杂结构处理有限**：对薄壁、小孔、倒角、圆角、自由曲面、复杂相交和退化拓扑等情况，方法可能丢失细节或产生不稳定拟合。
- **评测指标仍偏几何与分割层面**：CD、NC、SEG、HF 和 B-rep CD 能反映重建质量，但对 CAD 拓扑等价性、参数精度、边/面匹配率、欧拉特征、可制造性等缺少更严格的评价。
- **真实图像评测缺少定量基准**：真实拍摄实验主要展示定性效果，样本规模、失败率和误差分布不明确，泛化能力仍需更大规模真实数据验证。
- **与基线对比存在 pipeline 影响**：将其他单视图重建方法统一接 Point2CAD 有助于公平比较，但最终结果也会受 Point2CAD 分割和 B-rep 转换能力限制，不能完全等同于各方法原生 CAD 生成能力。

## 9. 总体评价

总体而言，CADDreamer 的核心价值在于将单视图 3D 生成从“稠密、无结构网格”推进到“紧凑、结构化、水密 B-rep”，其“基元语义引导多视角扩散 + 几何关系优化 + 拓扑保持 CAD 重建”的路线具有较强启发性。它更适合规则机械零件类 CAD 物体，对自由曲面、复杂装配和工业级可编辑参数化建模仍有距离。

未来可改进方向包括：扩展基元库或引入自由曲面表示；联合优化多视角生成与基元参数；引入真实工业数据集和更严格的 CAD 拓扑/参数指标；报告效率与失败案例；进一步探索从 B-rep 恢复到参数化构造历史，从而提升实际设计场景中的可编辑性和可用性。

（完）
