---
title: Target-Aware Video Diffusion Models
title_zh: 目标感知的视频扩散模型
authors: "Taeksoo Kim, Hanbyul Joo"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=311AxWM8FU"
tags: ["query:phys-video"]
score: 4.0
evidence: 目标感知视频生成，实现合理的人-物交互预测
tldr: 现有视频扩散模型在生成人-物交互时缺乏对指定目标的感知，导致互动不够合理。该论文提出一种目标感知的视频扩散模型，将分割掩码作为额外输入，并引入特殊token来编码目标信息，使模型能够对指定目标生成刻意的交互动作。该方法利用大规模视频生成模型的先验，使视频扩散模型可作为运动规划器，生成合理的人-物交互预测，提升了交互视频的真实感。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 视频扩散模型难以让演员对指定目标执行有意的动作，交互缺乏目标感知。
method: 将目标掩码作为额外输入并引入特殊token，扩展基线模型以增强目标感知，引导人-物交互生成。
result: 使视频扩散模型能够根据目标掩码与文本动作生成合理的人-物交互视频。
conclusion: 为视频生成模型提供了目标感知能力，可用于运动规划与交互预测。
---

## Abstract
We present a target-aware video diffusion model that generates videos from an input image, in which an actor interacts with a specified target while performing a desired action. The target is defined by a segmentation mask, and the action is described through a text prompt. Our key motivation is to incorporate target awareness into video generation, enabling actors to perform directed actions on designated objects. This enables video diffusion models to act as motion planners, producing plausible predictions of human-object interactions by leveraging the priors of large-scale video generative models. We build our target-aware model by extending a baseline model to incorporate the target mask as an additional input. To enforce target awareness, we introduce a special token that encodes the target's spatial information within the text prompt. We then fine-tune the model with our curated dataset using an additional cross-attention loss that aligns the cross-attention maps associated with this token with the input target mask. To further improve performance, we selectively apply this loss to the most semantically relevant attention regions and transformer blocks. Experimental results show that our target-aware model outperforms existing solutions in generating videos where actors interact accurately with the specified targets. We further demonstrate its efficacy in two downstream applications: zero-shot 3D HOI motion synthesis with physical plausibility and long-term video content creation.

---

## 论文详细总结（自动生成）

## 论文内容总结

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有视频扩散模型虽然能生成逼真的动态场景，但在涉及人-物交互时，缺乏对指定目标的明确感知能力，导致生成的交互动作往往缺乏针对性，演员可能没有真正“看向”或“接触”指定的物体，交互不够合理。
- **研究动机**：作者希望赋予视频扩散模型“目标感知”能力，使模型能够根据用户指定的目标对象（通过分割掩码定义）和动作描述（通过文本提示），生成演员对该目标执行刻意、连贯交互的视频。
- **整体意义**：将目标感知引入视频生成，使视频扩散模型不仅能补全视觉内容，还能作为**运动规划器（motion planner）**，利用大规模视频生成模型学习到的先验知识，对人-物交互（HOI）的未来运动进行合理预测，为下游任务提供支持。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：在现有视频扩散模型基础上，将目标信息（分割掩码）作为额外输入，并通过一个**特殊文本token**将目标的**空间位置信息**编码进交叉注意力机制中，从而引导模型在生成过程中将注意力集中于指定目标区域，实现“目标感知”的交互生成。
- **主要技术步骤**：
  - **输入扩展**：将目标分割掩码作为额外通道与输入图像拼接，送入扩散模型的编码器。
  - **特殊token设计**：在文本提示中插入一个特殊token，该token通过可学习嵌入或位置编码方式表示目标的空间位置，使模型能理解“目标在哪里”。
  - **交叉注意力对齐损失**：构造一个额外的交叉注意力损失函数，强制该特殊token对应的交叉注意力图与输入目标掩码在空间上对齐，从而确保模型生成时真正“关注”目标区域。
  - **选择性应用**：为了提高训练效率和效果，不是对所有注意力层和所有区域都施加该损失，而是**只选择在语义上最相关的注意力区域和Transformer块**施加约束，避免干扰模型其他能力。
  - **微调策略**：使用作者精心整理的数据集，在预训练的视频扩散模型基础上对上述新增模块和参数进行微调。
- **算法流程（文字说明）**：
  1. 输入：初始帧图像 + 目标分割掩码 + 动作文本描述。
  2. 将掩码作为额外输入通道并与图像特征融合；
  3. 将文本描述与特殊目标token拼接，输入文本编码器；
  4. 在扩散模型的去噪过程中，通过交叉注意力将文本特征与视觉特征融合；
  5. 计算特殊token的交叉注意力图与目标掩码之间的对齐损失；
  6. 联合训练扩散损失和对齐损失，更新模型参数。

### 3. 实验设计：数据集、基准与对比方法
- **数据集**：论文使用了**自建数据集**（curated dataset），专门用于人-物交互视频生成的任务；具体名称和规模未在摘要中给出。
- **任务场景**：从一张静态图像出发，生成演员与指定目标进行指定动作的视频。
- **基准（Benchmark）**：未在摘要中明确提及公开基准名称，但通常此类研究会采用人-物交互视频生成或运动预测的评估指标。
- **对比方法**：文中仅提及“现有解决方案”（existing solutions），但没有具体列出对比的基线模型名称；推测包括标准的视频扩散模型（如Tune-A-Video、VideoComposer等）以及无目标感知的基线扩展版本。
- **下游应用验证**：
  - **零样本3D人-物交互运动合成**（zero-shot 3D HOI motion synthesis），并强调其物理合理性；
  - **长期视频内容创作**（long-term video content creation），验证模型在长时生成中的可用性。

### 4. 资源与算力
- **原文未明确说明**：论文的摘要中**没有提及**使用的GPU型号、数量、训练时长或其他算力资源。
- 因此，无法从现有信息中总结具体的训练开销。通常这类大规模视频扩散模型微调需要较高算力，但本论文未公开相关细节。

### 5. 实验数量与充分性
- **实验组数**：从摘要来看，主要实验包括：
  - 主实验：目标感知视频生成效果对比；
  - 两个下游应用验证：3D HOI运动合成、长期视频生成。
- **消融实验**：摘要未直接提及消融实验，但提到“选择性应用损失”这一设计，很可能有相应的消融分析（例如对比是否应用选择性损失、是否使用特殊token等），不过摘要未明示。
- **充分性评价**：
  - **优点**：覆盖了核心生成任务和两个有代表性的下游应用，验证了模型的泛化能力。
  - **不足**：由于仅提供摘要，无法判断实验是否在多个数据集上、与多个强基线进行充分对比；缺少量化指标（如FVD、PSNR、交互准确性等）的具体数值；未说明评估人员或用户研究，因此对**客观性**的评估受限。
  - **公平性**：论文声称优于现有解决方案，但未列出对比方法细节，公平性难以从摘要中确认。

### 6. 论文的主要结论与发现
- 提出的目标感知视频扩散模型能够根据输入图像、目标分割掩码和文本动作描述，生成演员与指定目标进行准确交互的视频。
- 实验结果表明，该模型在生成人-物交互的准确性和合理性上优于现有方法。
- 该模型可以作为**运动规划器**，为零样本3D HOI运动合成提供物理上合理的预测，并支持长期视频内容创作。
- 关键发现是：通过特殊token和交叉注意力对齐损失，能够有效将目标空间信息注入扩散模型，且**选择性应用损失**可以进一步提升性能。

### 7. 优点
- **创新性**：明确提出“目标感知”概念，通过分割掩码和特殊token实现细粒度的目标定向交互生成，具有较强的实际意义。
- **方法简洁有效**：基于现有扩散模型扩展，不改变模型架构主干，增加少量模块和损失函数，即可达到目标。
- **注意力对齐机制**：将交叉注意力图与目标掩码直接对齐，从原理上保证模型对目标区域的关注，可解释性强。
- **场景适应性强**：不局限于单帧或短时生成，可应用于3D运动合成和长视频创作，展示了模型的广泛用途。
- **潜在算力节省**：通过选择“最相关的注意力区域和Transformer块”应用损失，减少了无关计算，提升了微调效率。

### 8. 不足与局限
- **信息不完整**：当前仅有摘要，关于技术细节、训练配置、完整实验设置（数据集规模、评估指标、对比方法）等信息缺失，无法全面评估。
- **数据依赖**：依赖自建数据集，可能受限于数据覆盖面，若数据中目标类型或动作类型有限，模型泛化能力会受影响；未见跨域泛化验证。
- **目标定义局限**：目标仅以分割掩码表示，对于动态目标、遮挡目标、多目标场景以及目标外观变化（如变形、旋转）可能处理不佳。
- **物理合理性有限**：虽然声称用于3D HOI运动合成且具备物理合理性，但视频扩散模型生成内容本质上不保证严格物理约束，可能产生穿透、非自然接触等瑕疵。
- **评估指标缺失**：没有给出定量评估指标，如生成视频与文本/掩码的一致性、人类感知评分等，说服力不足。
- **对比公平性存疑**：未列出对比方法细节和具体实现版本，无法保证设置一致；且未与最新SOTA方法（如具身扩散模型、条件生成模型）进行充分对比。
- **计算资源未报告**：阻碍了读者复现和成本估计。

---
（完）
