---
title: Anchor Frame Bridging for Coherent First-Last Frame Video Generation
title_zh: 锚帧桥接：面向连贯的首末帧视频生成
authors: "Xuehan Hou, Meng Fan, Pengchong Qiao, Zesen Cheng, Yian Zhao, Lei Zhu, Kaiwen Cheng, Chang Liu, Jie Chen"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=isNjWnVsUR"
tags: ["query:phys-video"]
score: 4.0
evidence: 增强帧间时间一致性，可为物理一致性目标提供支撑
tldr: 首末帧视频生成中，中间帧常出现语义退化、目标形变等破坏时间一致性的问题。锚帧桥接在语义间断最大的关键位置自适应插值锚帧，显式连接边界帧与中间帧的语义，无需训练即可缓解语义漂移，且具备即插即用与可泛化性，显著提升视频整体一致性。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 首末帧视频生成存在中间帧语义退化、场景失真和目标形变等问题，破坏时间一致性。
method: 提出锚帧桥接方法，在语义间断最大的位置自适应插值锚帧，显式桥接边界帧到中间帧的语义连续性。
result: 该方法即插即用，无需训练，能有效缓解中间帧语义漂移，提升时间一致性和泛化性。
conclusion: 锚帧桥接为视频生成的时间一致性增强提供了一种训练无关且可泛化的有效手段。
---

## Abstract
First-last frame video generation has recently gained significant attention. It enables coherent motion generation between specified first and last frames. However, this approach suffers from semantic degradation in intermediate frames, causing scene distortion and subject deformation that undermine temporal consistency.
 To address this issue, we introduce Anchor Frame Bridging (AFB), a novel plug-and-play method that explicitly bridges semantic continuity from boundary frames to intermediate frames, offering training-free adaptability and generalizability. By adaptively interpolating anchor frames at temporally critical locations exhibiting maximal semantic discontinuities, our approach effectively mitigates semantic drift in intermediate frames. Specifically, we propose an adaptive anchor frame selection module, which generates text-aligned candidate frames via frame order reversal and selects anchors based on semantic continuity. Subsequently, we develop anchor frame guided generation, which leverages the selected anchor frames to guide semantic propagation across intermediate frames, ensuring consistent boundary semantics and preserving temporal coherence throughout the video sequence. The final video is synthesized using the first frame, last frame, selected anchor frames, and the text prompt.
 The results demonstrate that our method significantly enhances the temporal consistency and overall quality of generated videos. Specifically, when applied to the Wan2.1-I2V model, it yields improvements of 16.58\% in FVD and 10.21\% in PSNR. The codes are provided in the supplementary material.

---

## 论文详细总结（自动生成）

## 论文总结：锚帧桥接（Anchor Frame Bridging）——面向连续首尾帧视频生成的时间一致性增强

> 说明：本总结基于论文标题、元数据及摘要内容撰写。由于仅有摘要文本可供分析，部分实验细节、数据集名称和算力信息无法从当前材料中确认，已在下文相应位置明确指出。

---

### 1. 核心问题与研究动机

- 研究对象为**首尾帧视频生成**（First-Last Frame Video Generation），即根据给定的第一帧、最后一帧（以及文本提示）生成中间帧，实现两帧之间的连贯运动生成。
- 现有方法面临的主要问题：**中间帧语义退化**（semantic degradation），表现为场景扭曲（scene distortion）、主体形变（subject deformation），这些问题严重破坏视频的**时间一致性**（temporal consistency）。
- 这种语义漂移（semantic drift）源于模型难以在边界帧之间维持稳定的语义传播，尤其是当首尾帧间运动幅度大、语义变换剧烈时，中间帧容易出现内容偏移或结构崩坏。
- 因此，论文的核心目标是在**不改变底层生成模型**的前提下，显式地增强中间帧与边界帧之间的语义连续性，从而提升整体的视频生成质量与一致性。

---

### 2. 方法论：Anchor Frame Bridging（AFB）

#### 2.1 核心思想
- 提出**锚帧桥接（AFB）**概念：在视频序列中语义间断最剧烈的位置，自适应地插值若干“锚帧”（anchor frames），以这些锚帧为“跳板”，将边界帧的语义逐步传播到所有中间帧。
- 该方法属于**即插即用（plug-and-play）**方案，**无需训练**（training-free），可直接应用于现有的首尾帧视频生成模型。

#### 2.2 技术组成（两个模块）

**模块一：自适应锚帧选择模块（Adaptive Anchor Frame Selection）**

- 通过**帧序反转**（frame order reversal）生成与文本对齐的候选帧：将首尾帧互换后再次生成，以暴露不同方向上的语义变迁路径。
- 基于**语义连续性**（semantic continuity）判定标准，从候选帧中筛选出那些对应时间点语义断裂最严重的位置作为锚帧插入点。
- 选择策略的核心依据是：在语义间断最大处插值锚帧，能最有效地弥补边界帧与中间帧之间的语义鸿沟。

**模块二：锚帧引导生成模块（Anchor Frame Guided Generation）**

- 利用已选定的锚帧，引导中间帧的生成过程，使语义信息从边界帧逐步、稳定地传播至全部中间帧。
- 锚帧在此过程中充当“中间锚点”，提供局部语义参照，确保生成过程保持边界语义一致，并由此保障整条视频序列的时间连贯性。
- 最终视频由**第一帧、最后一帧、选定的锚帧以及文本提示**共同合成。

#### 2.3 算法流程（文字描述）

1. 输入：给定的首帧图像、末帧图像及文本提示。
2. 首尾帧互换位置，执行反向生成以获取候选帧序列。
3. 计算各候选帧与相邻帧之间的语义连续程度，定位语义极大断裂位置。
4. 在这些位置插入锚帧，形成“边界帧 + 锚帧 + 边界帧”的参考序列。
5. 使用锚帧引导中间帧生成，迭代补充各段空缺帧，直至整段视频完整。
6. 输出最终合成视频。

> 摘要中未给出具体数学公式，因此此处以文字逻辑描述算法流程。

---

### 3. 实验设计

由于当前可得材料仅包含摘要，实验设计部分的信息较为有限，具体如下：

- **评估场景**：在 Wan2.1-I2V 模型上进行了应用测试（即使用该模型作为基础生成器，叠加 AFB 方法）。
- **评测指标**：
  - **FVD（Fréchet Video Distance）**：衡量生成视频整体分布与真实视频分布之间的距离，越低越好，报告结果为**改进 16.58%**（即 FVD 相对降低 16.58%）。
  - **PSNR（峰值信噪比）**：衡量视频帧重建质量，越高越好，报告结果为**提升 10.21%**。
- **Benchmark 与对比方法**：摘要中**未明确列出**评测所用数据集名称（如 UCF101、Something-Something、MSR-VTT 等），也**未列出所对比的具体基线方法**。目前仅能确认与未使用 AFB 的 Wan2.1-I2V 基线进行了对比（即消融式前后对比）。
- **源代码**：论文在补充材料中提供了代码。

---

### 4. 资源与算力（无明确信息）

- 当前摘要和元数据中**未提及任何算力信息**，包括：
  - GPU 型号与数量（如 A100、V100、H800 等）；
  - 训练或推理时长；
  - 显存占用等资源指标。
- 由于该方法宣称“无需训练”，可以推测算力消耗主要体现在推理阶段的多次采样与锚帧选择过程上，但没有具体数据可供佐证。

---

### 5. 实验数量与充分性评估

- **从摘要中仅能看到一组应用实验**：即 AFB + Wan2.1-I2V 的实验结果。
- **已在摘要中提到的指标**：FVD（相对改进 16.58%）与 PSNR（相对提升 10.21%）。
- **未在摘要中出现但对充分性评估至关重要的内容**：
  - 缺乏多数据集验证；
  - 缺乏与多种现有方法（如同类 video diffusion 模型、其他 plug-and-play 时间一致性增强方法）的横向对比；
  - 缺乏对“锚帧数量”这一超参数的敏感性分析；
  - 缺乏消融实验的说明（例如，移除自适应选择模块、固定间隔插帧替代自适应插帧等变体）；
  - 缺乏对泛化性的系统验证（如迁移到其他 I2V / 视频生成模型的表现）。
- **评估结论**：从摘要信息来看，实验报告尚不充分，覆盖面有限；其公平性和客观性有待于完整论文中补充的详细实验来支撑。不过，考虑到代码已公开，可复现性是一个加分项。

---

### 6. 主要结论与发现

- AFB 方法能**显著增强生成视频的时间一致性**，有效缓解中间帧的语义漂移问题。
- 在 Wan2.1-I2V 模型上，FVD 相对改进 16.58%，PSNR 提升 10.21%，表明该方法在感知质量与保真度两个维度上均有明显增益。
- 该方法具有**无需训练**、**即插即用**和**可泛化**的优势，能够在不修改底层模型的情况下直接提升视频生成的连贯性，具备较高的实用价值。

---

### 7. 方法亮点与优势

- **训练无关性**：无需针对特定模型重新训练或微调，部署成本低、通用性强。
- **即插即用**：可直接挂载到现有首尾帧视频生成模型之上，作为后处理/引导模块使用，适配性强。
- **自适应锚帧选择**：而非固定间隔插帧，能根据语义连续性动态确定最需要锚定的时间位置，针对语义断裂最严重处进行干预，定位精准高效。
- **显式语义桥接机制**：通过锚帧显式连接边界帧与中间帧，从根源上抑制语义漂移的累积，设计逻辑清晰、与问题对应性强。
- **代码开源**：提供源码，有利于后续研究者复现与扩展。

---

### 8. 不足与局限

- **实验证据不足**：摘要仅报告了在一个基础模型（Wan2.1-I2V）上的指标，缺乏多模型、多数据集的系统验证，难以充分证明其普适性。
- **缺少消融与敏感性分析**：未展示“锚帧数量”、“语义连续性的度量方式”、“候选帧生成策略”等关键设计选择对结果的影响。
- **缺少对比实验细节**：未说明与哪些现有方法对标、基线设置是否统一公平。
- **计算开销未知**：帧序反转生成候选帧 + 语义连续性评估可能在推理阶段引入额外的多次采样成本，但论文未披露效率指标。
- **指标覆盖面有限**：FVD 和 PSNR 是常用的视频质量指标，但缺少人类感知评价（如 MOS）以及字幕-视频对齐（text-video alignment）等指标，对时间一致性这一核心维度的刻画略显单薄。
- **潜在风险**：锚帧插入位置与数量选取可能对输入视频的长度、运动模式敏感，是否在所有场景下均能维持性能提升，仍需更多实验支撑。

---

（完）
