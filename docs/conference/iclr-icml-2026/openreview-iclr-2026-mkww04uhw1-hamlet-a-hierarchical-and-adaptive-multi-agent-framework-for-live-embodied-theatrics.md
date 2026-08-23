---
title: "HAMLET: A Hierarchical and Adaptive Multi-Agent Framework for Live Embodied Theatrics"
title_zh: HAMLET：面向现场具身戏剧的层次化自适应多智能体框架
authors: "Shufan Jiang, Sizhou Chen, Chi Zhang, Xiao-Lei Zhang, Xuelong Li"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=MKwW04UHW1"
tags: ["query:manga-drama"]
score: 7.0
evidence: 基于LLM的戏剧创作与实时表演框架，适用于戏剧内容生成。
tldr: 该文提出HAMLET，一个面向戏剧创作与实时线上表演的层次化自适应多智能体框架。给定简单主题，框架先生成叙事蓝图，再在在线表演阶段依此进行即兴演绎，让模型具备主动性与场景交互能力。相比需要详细用户输入的现有方法，该框架降低了使用门槛并提升临场沉浸感，对戏剧与短剧内容的自动化创排具有借鉴意义。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LLM戏剧生成缺乏主动性和物理场景交互，且需要详细用户输入。
method: 层次化自适应多智能体框架先规划叙事蓝图，再引导现场即兴表演。
result: 能根据简单主题实时生成具身戏剧表演，提升参与感和沉浸感。
conclusion: 为短剧的自动化编排与交互式内容生成提供了新思路。
---

## Abstract
Creating an immersive and interactive theatrical experience is a long-term goal in the field of interactive narrative. The emergence of large language models (LLMs) provides a new path to achieve this goal. However, existing LLM-based drama generation methods often produce models that lack initiative and cannot interact with the physical scene, while typically requiring detailed user input that diminishes the immersion of live performance. To address these challenges, we propose HAMLET, a hierarchical adaptive multi-agent framework focused on drama creation and real-time online performance. Given a simple topic, the framework first generates a narrative blueprint to guide the subsequent improvisational performance. In the online performance phase, each actor is equipped with an adaptive reasoning module that enables decision-making based on their personas, memories, goals, and emotional states during complex group chat scenarios. Beyond dialogue, actor agents engage in embodied interactions by changing the state of scene props through actions such as opening a letter or picking up a weapon, which are broadcast to update the global environmental context. To objectively assess the quality of live embodied theatrics, we establish a comprehensive evaluation method and introduce HAMLETJudge, a specialized critic model for automated evaluation. Experimental results demonstrate that HAMLET excels in creating expressive, coherent, and physically interactive theatrical experiences in an autonomous manner.

---

## 论文详细总结（自动生成）

# HAMLET：面向现场具身戏剧的层次化自适应多智能体框架 —— 论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **长期目标**：创造沉浸式、交互式的戏剧体验是交互叙事领域的长期追求目标。
- **LLM 带来的新机遇**：大语言模型（LLM）的兴起为这一目标提供了新的技术路径。
- **现有方法的不足**：
  - 基于LLM的戏剧生成方法往往产生缺乏主动性的模型，无法主动推进剧情；
  - 无法与物理场景进行交互，缺少"具身性"；
  - 通常需要用户提供详细输入，这削弱了现场表演的沉浸感。
- **HAMLET 的定位**：给定一个简单主题（simple topic），框架即可自动生成叙事蓝图并引导实时的即兴表演，强调自主性、场景交互与沉浸感。

## 2. 方法论：核心思想与技术细节

- **核心思想**：采用"先规划，后即兴"的层次化架构，将戏剧创作划分为离线规划与在线表演两个阶段。
- **阶段一：叙事蓝图生成**
  - 输入极简主题，框架自动生成叙事蓝图（narrative blueprint），作为后续表演的宏观指导。
- **阶段二：在线即兴表演**
  - 每个演员Agent配备**自适应推理模块（adaptive reasoning module）**，能够在复杂的群聊式场景中基于以下维度进行决策：
    - 人格（personas）
    - 记忆（memories）
    - 目标（goals）
    - 情绪状态（emotional states）
- **具身交互机制**：
  - 演员不仅进行对话，还能通过具体动作改变场景道具的状态（例如打开信件、拾起武器）；
  - 这些动作会被广播，以更新全局环境上下文（global environmental context）。
- **评估机制**：
  - 建立了一套综合评估方法；
  - 提出 **HAMLETJudge**——一个专门的批判性评论模型（critic model），用于自动化评估实时具身戏剧的质量。
- **无公式说明**：文中以文字性框架描述为主，未涉及具体数学公式或算法伪代码。

## 3. 实验设计

- **数据集/场景**：所提供的材料中**未明确说明**使用了哪些数据集或具体戏剧场景。
- **Benchmark**：材料仅提及"建立了一套综合评估方法"，但未说明是否有既有基准（benchmark）作为对比参照。
- **对比方法**：材料中**未列出**与哪些已有方法进行了定量或定性对比。摘要仅声称"实验结果证明HAMLET擅长……"，未给出对比基线细节。

## 4. 资源与算力

- 所提供的论文提取文本中**未提及任何算力信息**，包括：
  - GPU 型号与数量；
  - 训练时长；
  - 参数量级或推理开销。
- 因此，从现有材料无法评估该方法的计算资源需求与工程实现成本。

## 5. 实验数量与充分性

- **实验数量**：从摘要和元数据中无法获知具体开展了多少组实验（如不同数据集上的测试、消融实验等）。
- **充分性判断**：
  - 论文声称"实验结果表明"其方法优于现有方案，但缺乏实验细节支撑；
  - 由于未披露评估数据集、对比方法与消融设置，**无法客观判断实验的充分性、公平性与可复现性**；
  - 该论文为 ICLR-2026 接收论文，得分 7.0，表明评审对其创新性有一定认可，但实验透明度仍需以完整论文为准。

## 6. 主要结论与发现

- HAMLET 能够以**自主方式**创建富有表现力（expressive）、连贯（coherent）且具有物理交互性（physically interactive）的戏剧体验。
- 该方法有效降低了用户的使用门槛（仅需简单主题），同时提升了现场表演的参与感与沉浸感。
- 为短剧/戏剧的自动化编排与交互式内容生成提供了新的技术思路。

## 7. 优点

- **架构创新**："层次化蓝图 + 在线即兴"的设计兼顾了宏观叙事可控性与微观表演灵活性；
- **具身交互**：通过改变道具状态实现Agent与物理场景的互动，较之纯对话式戏剧生成有明显突破；
- **自适应决策**：综合人格、记忆、目标、情绪等多维度信息进行推理，使表演更自然、更个性化；
- **低门槛输入**：仅需简单主题即可驱动完整表演，优于依赖详细用户输入的既有方法；
- **自动化评估**：提出专门的HAMLETJudge批判模型，为客观量化戏剧质量提供了一种新工具。

## 8. 不足与局限

- **实验细节缺失**：提供的材料中未披露数据集、评估场景、对比基线与消融实验，无法验证方法的普适性和优越性；
- **算力成本未知**：未报告GPU、训练时间等资源消耗，难以评估其实用性和可扩展性；
- **评估主观性风险**：依赖LLM作为评判器（HAMLETJudge）虽能自动化评估，但"表现力""连贯性"等指标本身具有主观性，其评估标准需进一步验证；
- **应用边界**：当前框架是否适用于真实物理舞台、长时程表演、多人实时协同等场景尚不明确；
- **依赖LLM能力**：表演质量和主动性高度受底层LLM能力的制约，在复杂情节下可能出现幻觉或逻辑断裂。

（完）
