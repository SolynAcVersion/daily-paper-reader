---
title: "Think Before You Diffuse: Infusing Physical Rules into Video Diffusion"
title_zh: 扩散之前先思考：将物理规则注入视频扩散
authors: "Ke Zhang, Cihan Xiao, Jiacong Xu, Yiqun Mei, Vishal M. Patel"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=lPKsPBstHg"
tags: ["query:phys-video"]
score: 9.0
evidence: 将物理规则注入视频扩散以生成物理正确的视频
tldr: 论文指出视频扩散模型难以生成正确的物理效果，DiffPhy提出通用框架：先用大语言模型从文本提示中推断丰富的物理上下文，再用多模态大语言模型对生成过程的中间潜变量进行物理验证，并通过微调预训练视频扩散模型将其融入生成。实验表明该方法能生成物理正确且照片级逼真的视频，为物理感知视频生成提供了有效范式。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 视频扩散模型生成结果视觉效果好但物理效果正确性不足，难以处理复杂运动和交互。
method: 提出DiffPhy框架，用LLM从文本提示推断物理上下文，并用多模态LLM验证中间潜变量是否符合物理规则，再加微调注入。
result: 在多种物理效果的视频生成上实现了物理正确且照片级逼真的结果。
conclusion: 为视频扩散模型提供了一种通用、可微调的物理规则注入方式。
---

## Abstract
Recent video diffusion models have demonstrated their great capability in generating visually-pleasing results, while synthesizing the correct physical effects in generated videos remains challenging. The complexity of real-world motions, interactions, and dynamics introduce great difficulties when learning physics from data. In this work, we propose DiffPhy, a generic framework that enables physically-correct and photo-realistic video generation by fine-tuning a pre-trained video diffusion model. Our method leverages large language models (LLMs) to infer rich physical context from the text prompt. To incorporate this context into the video diffusion model, we use a multimodal large language model (MLLM) to verify intermediate latent variables against the inferred physical rules, guiding the model’s gradient updates accordingly. MLLM’s textual output is transformed into continuous signals. We then formulate a set of training objectives that jointly ensure physical accuracy and semantic alignment with the input text.  Additionally, failure facts of physical phenomena are corrected via attention injection. We also establish a high-quality physical video dataset containing diverse phyiscal actions and events to facilitate effective finetuning. Extensive experiments on public benchmarks demonstrate that DiffPhy is able to produce state-of-the-art results across diverse physics-related scenarios. Code and data will be made available post-review.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：现有视频扩散模型已经能生成视觉上非常逼真的视频，但生成视频中的**物理效果往往不正确**。真实世界中的运动、物体间交互、动力学过程非常复杂，模型仅从数据中学习这些规律非常困难。
- **核心问题**：如何让视频扩散模型在生成时不仅仅“看起来真实”，还能**符合物理规律**，例如物体碰撞、重力、形变、运动轨迹等。
- **整体含义**：该论文提出了一个通用框架 **DiffPhy**，通过将外部物理知识以可训练的方式注入预训练视频扩散模型，从而在不牺牲画面质量的前提下提升物理正确性。

## 2. 提出的方法论

- **核心思想**：采用“先思考再扩散”的思路，即在扩散生成过程中引入物理知识验证与修正，而不是仅依赖数据驱动。
- **关键技术细节**：
  - 使用**大语言模型（LLM）** 从文本提示（text prompt）中推断出丰富的物理上下文（如物体属性、运动类型、受力情况等）。
  - 使用**多模态大语言模型（MLLM）** 对扩散过程中的**中间潜变量（intermediate latent variables）** 进行物理验证，判断其是否符合已推断出的物理规则。
  - 将 MLLM 输出的文本判断结果转化为**连续信号**，用于指导模型的梯度更新。
  - 设计了一组**训练目标**，联合保证物理准确性与文本语义一致性。
  - 对物理现象中的“失败事实”（failure facts）采用**注意力注入（attention injection）** 的方式进行修正。
  - 构建了一个包含多种物理动作与事件的高质量物理视频数据集，用于微调预训练模型。
- **算法流程（文字说明）**：
  1. 输入文本提示；
  2. LLM 提取物理上下文；
  3. 视频扩散模型生成中间潜变量；
  4. MLLM 对潜变量进行物理规则验证；
  5. 将验证结果转化为连续损失信号；
  6. 结合物理验证损失与语义对齐损失，对扩散模型进行微调；
  7. 对失败物理事实使用注意力注入修正；
  8. 输出物理正确且照片级逼真的视频。

## 3. 实验设计

- **数据集**：论文在**公开基准（public benchmarks）** 上进行了实验，同时提出了一个自建的物理视频数据集用于微调。
- **场景覆盖**：涉及多种物理相关场景，包括但不限于复杂运动、交互和动态过程。
- **对比方法**：与现有视频扩散方法进行对比，论文声称在多种物理相关场景下取得了**最先进（state-of-the-art）结果**。
- **注意**：由于提供的论文内容仅为摘要和元数据，**具体使用的公开数据集名称、场景列表、对比方法列表均未在给定文本中明确列出**。

## 4. 资源与算力

- **未在提供内容中说明**：文中没有给出 GPU 型号、数量、训练时长、显存占用等具体算力信息。需要阅读全文才能获知。

## 5. 实验数量与充分性

- **实验数量的判断受限**：从摘要只能看出“大量实验”（extensive experiments）这一描述，但**无法得知具体实验组数**。
- **是否充分**：从声称来看，实验覆盖了多种物理场景并在公开基准上验证了方法，具有一定的广泛性；但缺少消融实验细节、定量指标对比表格等具体信息，难以全面评估其充分性。
- **是否客观、公平**：目前仅凭摘要无法判断对比设置是否公平、是否控制了变量。需要查看完整论文中的实验设置。

## 6. 主要结论与发现

- DiffPhy 能够生成**物理正确且照片级逼真**的视频；
- 它提供了一种**通用、可微调**的物理规则注入方式，可以适配预训练视频扩散模型；
- 相比现有方法，DiffPhy 在多种物理相关场景下表现更好；
- 验证了“LLM+ MLLM 引导扩散模型”这一范式的有效性。

## 7. 优点

- **通用性好**：不针对特定物理场景，而是构建一个通用框架；
- **结合大模型知识**：利用 LLM/MLLM 的语言理解和视觉理解能力，比纯数据驱动更可控；
- **可微调集成**：通过在预训练扩散模型上微调，不需要从零训练，效率更高；
- **物理验证机制**：引入中间潜变量级别的验证，能更早发现和修正物理错误；
- **注意力注入修正失败事实**：针对具体物理错误进行定向修正，思路新颖；
- **自建高质量物理视频数据集**：有利于后续微调和基准测试。

## 8. 不足与局限

- **信息不完整**：当前仅能基于摘要和元数据进行分析，无法确认实验细节、对比方法、具体指标等；
- **依赖大模型能力**：LLM/MLLM 的物理知识可能存在幻觉或错误，导致验证信号不准确；
- **验证成本较高**：在扩散过程中调用 MLLM 进行潜变量验证，可能带来额外的计算开销；
- **物理规则覆盖面有限**：物理现象极其多样，当前方法能处理的物理规则范围仍可能局限于训练数据和语言模型已知的常识；
- **数据集尚未公开**：论文提到代码和数据将在评审后发布，目前无法复现验证；
- **来源标注为被拒公开版本**：根据元数据，该论文为 ICLR-2026 被拒公开版本，说明其方法或实验可能仍存在审稿人认为的不足。

（完）
