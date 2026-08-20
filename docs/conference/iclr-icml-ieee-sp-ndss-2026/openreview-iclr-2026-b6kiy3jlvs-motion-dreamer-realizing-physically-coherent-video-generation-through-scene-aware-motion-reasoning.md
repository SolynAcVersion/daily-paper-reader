---
title: "Motion Dreamer: Realizing Physically Coherent Video Generation through Scene-Aware Motion Reasoning"
title_zh: 运动梦想家：通过场景感知运动推理实现物理连贯的视频生成
authors: "Tianshuo Xu, ZhiFei Chen, Leyi Wu, Hao LU, Yuying Chen, Bingbing Liu, Ying-Cong Chen"
date: 2025-09-08
pdf: "https://openreview.net/pdf?id=b6KiY3jlvS"
tags: ["query:phys-video"]
score: 9.0
evidence: 直接针对生成符合物理规律的物理连贯视频
tldr: 现有视频生成模型在生成逻辑与物理上连贯的未来场景上常失败，原因是端到端训练中感知保真度与长时程结构能力相互冲突。为此提出 Motion Dreamer，将运动推理与视觉合成显式解耦，并设计实例流表示。在自动驾驶与机器人场景上，该方法能基于首帧与稀疏运动线索生成复杂场景，显著改善物理连贯性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频生成模型常因追求感知保真度而忽略长时程物理结构，难以生成符合物理规律和逻辑的未来场景。
method: 提出两阶段框架 Motion Dreamer，将运动推理与视觉合成显式解耦，引入实例流作为稀疏到稠密的运动表示。
result: 实验表明该方法能基于初始帧和稀疏运动线索生成复杂场景，并显著提升物理连贯性。
conclusion: 证明显式分离运动推理与视觉合成是获得物理合理视频生成的有效路径，对自动驾驶和机器人应用尤为重要。
---

## Abstract
Current video generation models often fail to produce logically and physically coherent future scenarios, a critical weakness for applications in autonomous driving and robotics. This stems from a fundamental conflict in end-to-end training: the pursuit of perceptual fidelity diverts capacity from modeling long-range temporal structure, while architectural priors fail to enforce physical laws. We introduce Motion Dreamer, a two-stage framework that resolves this conflict by explicitly decoupling motion reasoning from visual synthesis. Our approach is designed to generate complex scenes from an initial frame and sparse motion cues. To achieve this, we introduce instance flow, a novel sparse-to-dense motion representation, and a motion inpainting training strategy. Together, these techniques allow the model to robustly infer a complete, coherent motion field from partial inputs. This motion-aware representation then guides a synthesis model to generate high-fidelity video grounded in plausible dynamics. Across extensive experiments on robotics, physics, and a large-scale driving dataset, Motion Dreamer significantly outperforms leading methods in both motion coherence and visual realism.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 当前视频生成模型在生成**逻辑与物理上连贯的未来场景**方面存在明显不足，尤其在自动驾驶和机器人等对物理规律敏感的应用领域。
- 根本原因在于**端到端训练中存在内在冲突**：
  - 追求感知保真度（视觉逼真）会分散模型对**长时程时间结构**建模的能力；
  - 现有架构先验不足以强制模型遵守物理定律。
- 因此，本文试图解决“如何生成物理连贯、视觉逼真的未来视频”这一核心问题，强调运动推理与视觉合成需要分离而非混合端到端训练。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：显式解耦**运动推理**（motion reasoning）与**视觉合成**（visual synthesis），形成两阶段框架。
- **整体框架名称**：Motion Dreamer
- **输入条件**：初始帧（first frame）+ 稀疏运动线索（sparse motion cues）
- **关键技术**：
  1. **实例流（instance flow）**：一种新颖的**稀疏到稠密**（sparse-to-dense）运动表示，用于表征复杂场景中各个实例的运动场。
  2. **运动修复训练策略（motion inpainting training strategy）**：训练模型从部分/稀疏输入中鲁棒地推断出完整、连贯的运动场。
- **算法流程（文字描述）**：
  - 第一阶段：利用初始帧和稀疏运动线索，通过运动推理模型（基于实例流和运动修复策略）生成稠密且连贯的完整运动场；
  - 第二阶段：将运动场作为条件/引导，输入视觉合成模型，生成与运动场一致的高保真视频帧序列。
- 该流程保证视频生成“物理上可信”（grounded in plausible dynamics），而不单纯依赖像素层面的端到端拟合。

## 3. 实验设计：数据集、基准与对比方法

- **数据集/场景**：
  - 机器人场景（robotics）
  - 物理模拟场景（physics）
  - 大规模自动驾驶数据集（large-scale driving dataset）
- **Benchmark**：未在摘要中明确说明具体基准名称（如特定排行榜），但实验中使用了上述三类典型场景作为评测基准。
- **对比方法**：与“leading methods”（领先方法）进行比较，虽未列出具体方法名称，但指出在运动连贯性和视觉真实感两方面均显著优于这些方法。

## 4. 资源与算力

- 论文提供的文本中**未明确提及**使用的GPU型号、数量、训练时长、计算资源规模等具体信息。
- 因此无法从现有内容中总结算力配置，需查阅论文全文实验设置部分才能获知。

## 5. 实验数量与充分性

- 从摘要来看，实验涵盖**三大类场景**（机器人、物理、自动驾驶），属于多场景泛化验证。
- 可能还包括消融实验（如对实例流表示和运动修复策略的效果分析），但摘要中未明确列出具体消融数量。
- **充分性评估**：
  - 客观上覆盖了论文声称的应用领域（自动驾驶、机器人），场景较广；
  - 但缺乏细节，无法判断是否进行了大规模系统性消融、不同运动类型/复杂度的细分测试等；
  - 对比方法未列出具体名称，公平性难以从摘要直接验证。

## 6. 论文的主要结论与发现

- Motion Dreamer 能够基于**初始帧和稀疏运动线索**生成复杂场景，并显著提升视频的**物理连贯性**和**视觉真实感**。
- 在运动连贯性和视觉真实感两个关键指标上，Motion Dreamer 均优于现有领先方法。
- 证明了**显式分离运动推理与视觉合成**是获得物理合理视频生成的有效路径，对自动驾驶和机器人应用尤为重要。

## 7. 优点：方法或实验设计上的亮点

- **两阶段解耦设计**：将难解的长时程物理结构问题从视觉渲染中剥离，针对性解决端到端训练的冲突。
- **实例流表示**：引入了稀疏到稠密的运动表示，能够有效描述复杂场景中多个实例的运动，具有较好的表达能力和可解释性。
- **运动修复策略**：提高了模型在部分/稀疏输入下的鲁棒性，贴近真实应用（如仅有稀疏传感器线索）场景。
- **应用导向明确**：针对自动驾驶和机器人等对物理一致性要求高的领域设计，实验也覆盖了这些领域，实用价值突出。

## 8. 不足与局限

- **实验细节不透明**：摘要中未提供对比方法名称、具体指标数值、数据集规模、训练设置等，无法充分判断公平性与普适性。
- **算力资源未披露**：文中未报告GPU/TPU、训练时长等，影响可复现性评估。
- **可能存在的偏差风险**：物理和机器人场景多为模拟环境，真实世界复杂动态（如非刚体形变、遮挡、多物体交互）是否完全覆盖不得而知；部署到真实系统时可能面临领域差距。
- **应用限制**：输入依赖初始帧和稀疏运动线索，对于需要纯文本或无条件生成的场景不直接适用；实例流表示对物体分割/实例标注可能有一定要求，限制了无监督或弱监督场景的适用性。

（完）
