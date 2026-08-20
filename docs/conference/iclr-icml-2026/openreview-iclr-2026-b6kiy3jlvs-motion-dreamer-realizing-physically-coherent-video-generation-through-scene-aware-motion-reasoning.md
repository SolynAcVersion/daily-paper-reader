---
title: "Motion Dreamer: Realizing Physically Coherent Video Generation through Scene-Aware Motion Reasoning"
title_zh: 运动梦想家：通过场景感知运动推理实现物理一致的视频生成
authors: "Tianshuo Xu, ZhiFei Chen, Leyi Wu, Hao LU, Yuying Chen, Bingbing Liu, Ying-Cong Chen"
date: 2025-09-08
pdf: "https://openreview.net/pdf?id=b6KiY3jlvS"
tags: ["query:phys-video"]
score: 9.0
evidence: 显式针对物理一致的视频生成，将运动推理与视觉合成解耦
tldr: 针对视频生成模型难以生成物理一致未来场景的问题，提出Motion Dreamer两阶段框架。该框架显式解耦运动推理与视觉合成，引入实例流这一稀疏到密集的运动表示，从初始帧和稀疏运动线索生成复杂场景。实验表明该方法在物理一致性上明显优于端到端基线，为自动驾驶和机器人应用提供支持。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 当前视频生成模型常因感知保真度与长时结构建模冲突，难以生成逻辑与物理一致的未来场景。
method: 提出Motion Dreamer两阶段框架，显式解耦运动推理与视觉合成，并引入实例流这一稀疏到密集的运动表示。
result: 方法能够从初始帧和稀疏运动线索生成复杂场景，在物理一致性方面显著优于端到端基线。
conclusion: 将运动推理与视觉合成分离是提升视频生成物理一致性的有效途径。
---

## Abstract
Current video generation models often fail to produce logically and physically coherent future scenarios, a critical weakness for applications in autonomous driving and robotics. This stems from a fundamental conflict in end-to-end training: the pursuit of perceptual fidelity diverts capacity from modeling long-range temporal structure, while architectural priors fail to enforce physical laws. We introduce Motion Dreamer, a two-stage framework that resolves this conflict by explicitly decoupling motion reasoning from visual synthesis. Our approach is designed to generate complex scenes from an initial frame and sparse motion cues. To achieve this, we introduce instance flow, a novel sparse-to-dense motion representation, and a motion inpainting training strategy. Together, these techniques allow the model to robustly infer a complete, coherent motion field from partial inputs. This motion-aware representation then guides a synthesis model to generate high-fidelity video grounded in plausible dynamics. Across extensive experiments on robotics, physics, and a large-scale driving dataset, Motion Dreamer significantly outperforms leading methods in both motion coherence and visual realism.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前的视频生成模型在生成未来场景时，往往难以保证逻辑与物理上的一致性，即生成的视频内容可能违反物理规律（如物体运动轨迹不合理、遮挡关系错误等）。
- **问题根源**：端到端训练存在根本性矛盾——模型在训练中被分配大量能力用于追求单帧画面的感知保真度（perceptual fidelity），从而削弱了对长时时间结构建模的能力；与此同时，现有架构的先验知识也未能有效地将物理定律强制嵌入生成过程。
- **应用价值**：此问题对于自动驾驶和机器人等对时空一致性要求极高的领域的应用至关重要，因为这类系统依赖对未来视频帧物理合理的预测来做出决策。
- **整体含义**：论文主张将“运动推理”与“视觉合成”两个环节从耦合的端到端模型中解耦，避免感知保真度与运动结构建模之间的资源冲突，从而在根本上提升视频生成的物理一致性。

## 2. 论文提出的方法论

### 核心思想
- 提出 **Motion Dreamer**，一个明确的**两阶段框架**，将运动推理与视觉合成**显式解耦**。
- 核心逻辑：先用运动推理模型从初始帧和稀疏运动线索中预测出完整的、物理一致的运动场；再用合成模型基于该运动场生成高保真的视频内容。

### 关键技术细节
- **实例流（Instance Flow）**：一种新颖的**稀疏到密集运动表示**方法。它从稀疏的运动输入（如关键点轨迹、用户指定的稀疏运动矢量）出发，推断出覆盖全场景的密集运动场，使得每个像素/实例都有明确且连贯的运动描述。
- **运动修补训练策略（Motion Inpainting Training Strategy）**：训练模型在仅有部分运动信息可见的情况下，鲁棒地将缺失的运动信息补全为完整连贯的运动场，增强模型从部分线索恢复全局运动结构的能力。

### 算法流程（文字说明）
1. **输入**：初始视频帧 + 稀疏运动线索。
2. **阶段一（运动推理）**：利用实例流表示和运动修补训练策略，将稀疏输入转化为完整、稠密且物理自洽的运动场。
3. **阶段二（视觉合成）**：以运动场为条件（即运动感知表征），驱动一个合成模型生成与运动场时空对齐的高保真视频帧。
4. **输出**：物理连贯且视觉逼真的未来视频序列。

## 3. 实验设计

- **数据集/场景**：
  - 机器人（robotics）场景数据集
  - 物理模拟（physics）场景数据集
  - 大规模驾驶（large-scale driving）数据集
- **Benchmark**：研究在运动一致性（motion coherence）和视觉真实感（visual realism）两个维度上建立了评估基准（论文未给出具体数据集名称与评估指标细节）。
- **对比方法**：与“领先方法”（leading methods）及端到端基线进行了比较。论文明确指出 Motion Dreamer 在运动一致性和视觉真实感上均显著优于这些对比方法（具体对比方法名称未在摘要中列出）。

## 4. 资源与算力

- 论文提供的摘要与元数据中**未明确报告**具体的算力信息，包括 GPU 型号、GPU 数量、训练时长等。
- 无法从现有内容获知训练开销、推理速度或硬件配置等资源消耗细节。

## 5. 实验数量与充分性

- 实验覆盖了**三种不同领域**的场景数据集（机器人、物理模拟、自动驾驶），体现了跨领域的广泛验证。
- 论文提到进行了“广泛的实验”（extensive experiments），并报告了与领先方法的对比结果。
- **不足之处**：当前提供内容中**未展示具体实验数量细节**，例如消融实验、不同组件（如实例流的贡献、两阶段解耦的有效性）的分离分析、以及详细量化指标表格等。因此，无法从现有信息全面判断实验的统计完备性；但从跨域验证和显著性能提升来看，实验设计具有较好的客观性基础。

## 6. 论文的主要结论与发现

- 将运动推理与视觉合成进行**显式分离**是提升视频生成物理一致性的有效途径，化解了端到端训练中的资源冲突。
- 实例流这一稀疏到密集的运动表示，能有效支持从部分运动线索中预测完整连贯的运动场。
- Motion Dreamer 同时在**运动一致性**与**视觉真实感**上显著优于现有端到端方法，验证了两阶段范式在自动驾驶、机器人等物理敏感任务中的实用性。

## 7. 优点

- **方法创新性**：明确提出运动推理与视觉得解耦的两阶段思想，针对物理一致性问题的病因进行直接回应。
- **表示设计精妙**：实例流作为稀疏到密集的运动表示，兼顾了输入的可控性（稀疏线索易获取）与输出的完整性（稠密运动场可直接驱动合成）。
- **训练策略针对性强**：运动修补训练策略专门强化模型对不完整运动信息的鲁棒推断能力，贴近现实应用中的输入条件。
- **跨领域验证**：在机器人、物理、驾驶三大不同场景上进行验证，增强了结论的普适性和说服力。

## 8. 不足与局限

- **信息透明度不足**：摘要和元数据中没有提供具体数据集名称、评估指标、量化结果表格、消融实验等关键细节，限制了对方法有效性的精确评估。
- **算力信息缺失**：未报告训练资源、时间和成本，不利于其他研究者复现和比较效率。
- **未提及泛化边界**：没有明确讨论方法在处理极端物理场景（如非刚体形变、流体动力学、多物体复杂交互）时可能面临的失效模式。
- **应用限制**：论文定位在自动驾驶和机器人领域，但未讨论实时性、模型参数量、部署成本等工程层面的可行性问题，离实际产品落地仍有距离。
- **对比范围有限**：仅笼统提及“领先方法”，未声称与具体 SOTA 模型体系（如扩散式视频模型、世界模型类方法等）的详尽对比，公平性细节待进一步披露。

（完）
