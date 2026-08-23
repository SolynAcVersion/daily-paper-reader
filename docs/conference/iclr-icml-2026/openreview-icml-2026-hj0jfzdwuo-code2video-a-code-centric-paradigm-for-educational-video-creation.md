---
title: "Code2Video: A Code-centric Paradigm for Educational Video Creation"
title_zh: Code2Video：以代码为中心的教育视频创作范式
authors: "Yanzhe Chen, Kevin Qinghong Lin, Mike Zheng Shou"
date: 2026-04-30
pdf: "https://openreview.net/pdf/3338bb228c33fb79f153d11dd93d5f35d9a792c3.pdf"
tags: ["query:manga-drama"]
score: 5.0
evidence: 以代码为中心的智能体框架用于生成结构化视频，可迁移到短剧等短剧集视频的自动创作。
tldr: 本文针对生成式模型难以生成结构精确、领域知识丰富的教育视频的问题，提出Code2Video，一种以代码为中心的智能体框架。它通过编写可执行的Python程序来生成视频，包含规划故事板、代码生成与自动修复、以及基于视觉锚定提示的布局优化三个模块。实验表明其生成的视频具有精确结构和连贯转场。该范式可推广到短剧等需要强结构控制的结构化视频自动创作。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 生成式模型难以生成具有精确结构、领域知识和连贯转场的教育视频。
method: 提出Code2Video，一个以代码为中心的智能体框架，通过编写可执行Python程序生成视频，包含Planner、Coder和Critic三个智能体，利用视觉锚定提示进行布局优化。
result: 实验证明Code2Video能生成结构精确、连贯的教育视频。
conclusion: 提供了一种利用显式代码控制视频生成的途径，虽面向教育，但方法可迁移到其他结构化视频内容生成。
---

## Abstract
While recent generative models can synthesize videos in pixel space, they often fail to produce educational videos with precise structures, domain knowledge, and coherent transitions. We argue that this setting is better served by operating in a renderable environment that is explicitly controlled by code. We propose **Code2Video**, a code-centric agent framework that generates educational videos by writing executable Python programs. Code2Video includes three agents: a *Planner* that converts lecture content into a temporal storyboard, a *Coder* that turns the storyboard into runnable code with scope-guided auto-fix, and a *Critic* that refines layout using a VLM guided by *visual anchor prompting*, *i.e.*, mappings from target visual outcomes to code edits. For evaluation, we build **MMMC**, a benchmark of professionally produced, discipline-specific educational videos. We assess Code2Video using aesthetic scores (VLM-as-a-Judge), code efficiency, and **TeachQuiz**, an end-to-end metric that measures how well an *unlearned* VLM can recover knowledge after watching generated videos. Code2Video improves performance by 40% over direct code generation and produces videos comparable to human-crafted tutorials. The code and datasets are available at [https://github.com/showlab/Code2Video](https://github.com/showlab/Code2Video).

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：尽管生成式模型在像素空间中已能合成高质量视频，但生成**结构精确、领域知识丰富、转场连贯**的教育视频仍然是一大挑战。教育视频要求严格的逻辑顺序、准确的术语表达和清晰的可视化呈现，而这正是像素级生成模型的短板。
- **核心问题**：如何从教学文本内容出发，高效、可控地生成具有专业结构和完整领域知识的教育视频。
- **整体含义**：论文提出一个关键观点——此类任务不应在像素空间中直接生成，而应在一个**可渲染的、由代码显式控制的执行环境**中完成。这为结构化视频生成开辟了一条以代码为中介的新范式，不仅适用于教育视频，也具备推广到短剧等结构化叙事视频自动创作的可能。

## 2. 论文提出的方法论

- **核心思想**：以代码为中心（Code-centric），将视频生成问题转化为代码编写问题——通过生成可执行的 Python 程序来控制渲染环境，从而精确生成视频。
- **框架总览**：提出 **Code2Video**，一个由三个智能体（Agent）组成的协作框架：
  1. **Planner（规划器）**：将讲座/教学内容转换为**时间线故事板（temporal storyboard）**，负责结构化组织和内容分段。
  2. **Coder（编码器）**：将故事板转换为**可运行的代码**，并具备 **scope-guided auto-fix**（范围引导的自动修复）能力——当代码执行出错或渲染效果不符时，自动定位问题范围并修复。
  3. **Critic（评审器）**：利用视觉语言模型（VLM）对布局进行优化，采用 **visual anchor prompting（视觉锚定提示）** 技术，即建立“目标视觉结果 → 代码修改方向”的映射，引导 VLM 给出针对性的代码编辑建议。
- **技术特点**：整个流程无需在像素空间做生成，所有视觉内容都由代码渲染得到，因此结构可控、转场自然、可完全复现。

## 3. 实验设计

- **新基准**：构建了 **MMMC**（Multi-disciplinary, Multi-modal, Multi-video Comparison）基准，包含**专业制作、分学科**的教育视频，用于评估模型生成效果。
- **评估指标**：
  - **美学评分**：以 VLM 作为评审（VLM-as-a-Judge）评估视频画面质量。
  - **代码效率**：衡量生成代码的执行效能。
  - **TeachQuiz（端到端指标）**：让一个**未学习过该知识**的 VLM 观看生成视频后回答问题，测量其**知识恢复程度**，以此反映视频的教学有效性。
- **对比方法**：主要对比**直接代码生成**（不加智能体协作/修复机制）和**人工制作的教学视频**。

## 4. 资源与算力

- **原文未明确说明**：论文摘要中未提供 GPU 型号、数量、训练或推理时长等信息。这是因为该框架的核心是基于预训练模型（大语言模型 + 视觉语言模型）的推理与代码渲染，而非重训练，因此论文对专用算力支出披露较少。

## 5. 实验数量与充分性

- **实验组数**：从摘要看，至少包含三方面评估：
  1. Code2Video vs. 直接代码生成的对比实验；
  2. Code2Video vs. 人工教程的对比实验；
  3. 基于 TeachQuiz 指标的端到端教学效果测试，以及美学、代码效率等多维度评测。
- **充分性评价**：评估维度较全面——既关注视频本身的视觉质量（美学评分），也关注代码层面的效率，还通过 TeachQuiz 从“教学效果”这一最终目标做闭环验证。但摘要信息有限，未披露具体视频数量、学科覆盖范围、消融实验细节（如去掉每个智能体的效果），因此关于各模块贡献的验证充分度尚不能完全确定。

## 6. 论文的主要结论与发现

- **效果显著**：Code2Video 相比直接代码生成方法，性能提升 **40%**（综合指标）。
- **可比人工**：生成视频的质量与人工制作的教学视频相当。
- **范式有效**：证明了“显式代码控制渲染”这一路径在结构化视频生成上具有明显优势，优于直接像素空间生成。
- **可迁移性**：虽然面向教育视频，但该方法可推广到短剧等需要强结构控制的视频内容自动创作。

## 7. 优点

- **范式创新**：跳出“生成式模型直接合成像素”的惯性思路，转向代码渲染，从根本上解决结构可控性问题，思路新颖且实用。
- **工程完整**：Planner → Coder → Critic 的三智能体协作链路闭环，每个环节都有明确职责，且 Critic 的视觉锚定提示将“看的见”的视觉问题与“可执行”的代码修改直接联动，提高了迭代修复效率。
- **评估体系独特**：TeachQuiz 指标从“教学效果”而非单纯画面质量来评价教育视频，贴近实际应用目标，是评价设计上的亮点。
- **对用户友好**：代码和数据开源，便于复现和后续研究。

## 8. 不足与局限

- **实验信息不完整**：摘要中未提供足够细节，如 MMMC 基准的视频数量、学科类型、难度分布，以及消融实验的完整设置，实验覆盖的透明度有待加强。
- **依赖 VLM 评估**：美学评分和 TeachQuiz 均依赖 VLM，存在一定的主观性和偏差风险，且 VLM 的知识恢复能力可能受预训练数据影响，不一定完全代表真实学习效果。
- **面向特定场景**：目前验证集中于教育视频品类，对短剧等其他结构化视频的迁移效果尚未给出直接实验证据。
- **算力成本未披露**：虽然无需大型训练，但多智能体多轮调用 LLM/VLM 的推理成本和代码渲染的计算开销未被讨论。
- **内容表达受限**：代码渲染虽保证结构精确，但在表现力上可能不如像素空间生成——例如复杂的实拍场景、精细纹理和情感表达，代码化生成的适用范围仍有边界。

（完）
