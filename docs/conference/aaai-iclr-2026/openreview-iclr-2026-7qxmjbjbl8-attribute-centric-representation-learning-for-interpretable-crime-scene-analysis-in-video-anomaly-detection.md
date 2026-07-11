---
title: Attribute-Centric Representation Learning for Interpretable Crime Scene Analysis in Video Anomaly Detection
title_zh: 面向可解释犯罪场景分析的属性中心表示学习在视频异常检测中的应用
authors: "Akshat Rampuria, Kushagra Khare, Kamalakar Vijay Thakare, Debi Dogra, Heeseung Choi, Hyungjoo Jung, Ig-Jae Kim"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=7qXmJbjbl8"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 通过属性中心表示实现可解释的视频异常检测
tldr: 针对视频异常检测的可解释性需求，提出属性中心的表示学习框架，通过显式建模犯罪相关属性，模型可以学习到细粒度、解耦的表征，从而对异常事件提供可解释的分析。此外，扩展了UCA数据集，添加了超过150万条属性级标注，为可解释视频异常检测提供了基准。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视频异常检测需要可解释性，但现有数据集缺乏属性级标注，模型难以学习细粒度表示。
method: 提出属性中心学习框架，显式条件视频表示于犯罪相关属性，并扩展数据集添加大量属性标注。
result: 模型在视频异常检测任务上实现了可解释的异常分析，属性级标注显著提升了细粒度表示学习。
conclusion: 为视频异常检测提供了一种可解释性强的属性中心方法，并建立了大规模属性级标注数据集。
---

## Abstract
Automatic crime scene analysis is an important application area for representation learning in Video Anomaly Detection (VAD). Effective interpretation of anomalous events requires models to learn rich, disentangled representations that capture fine-grained, crime-relevant attributes. However, widely used VAD datasets (e.g., UCA, CUVA) primarily offer coarse event-level labels and they lack attribute-level supervision often needed for modeling crime-specific behaviors. To bridge this gap, we propose an attribute-centric learning framework that explicitly conditions video representations on crime-causing attributes. We extend the UCA dataset with over 1.5M new attribute-centric annotations generated using carefully designed prompts and LLMs. These annotations enable supervised fine-tuning of a curated CLIP-based model, leading to more discriminative, attribute-aware video representations, and precise event captions. An LLM-based summarizer then distills these captions into context-rich explanations, facilitating interpretable scene understanding. Our approach answers three core questions in crime scene analysis: \textbf{What? When? How?} Extensive experiments show that the proposed representation learning framework yields significant improvements ($\approx 20\%\uparrow$) in attribute-centric crime classification accuracy and ($\approx 6.4\%\uparrow$) according to MMEval scores over the baselines. We further analyze and mitigate biases in MMEval to ensure robustness and fair evaluation. These results highlight the importance of attribute-conditioned representation learning for interpretable and reliable VAD.

---

## 论文详细总结（自动生成）

# 论文总结：面向可解释犯罪场景分析的属性中心表示学习在视频异常检测中的应用

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：视频异常检测（VAD）在犯罪场景分析中需要可解释性，但现有方法仅学习粗粒度表示，难以提供细粒度的犯罪相关属性分析。广泛使用的数据集（如UCA、CUVA）只提供事件级标签，缺乏属性级监督。
- **背景**：传统VAD方法无法回答“发生了什么、何时发生、如何发生”这三个核心问题。可解释性是关键需求，但缺少属性级标注和相应学习框架。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：提出属性中心学习框架，显式地将视频表示条件化（condition）于犯罪诱因属性（crime-causing attributes），从而学习丰富、解耦的细粒度表示。
- **关键技术细节**：
  - 扩展UCA数据集，使用精心设计的提示和LLM生成超过150万个新的属性中心标注。
  - 基于这些标注，对精选的CLIP模型进行监督微调，以获得更具判别性、属性感知的视频表示，并生成精确的事件描述（event captions）。
  - 利用基于LLM的总结器（summarizer）将这些描述蒸馏为上下文丰富的解释，实现可解释的场景理解。
  - 框架能回答三个核心问题：**What? When? How?**（发生了什么？何时？如何？）

## 3. 实验设计
- **数据集**：主要使用UCA数据集，并对其进行扩展（新增150万+属性级标注）。可能还涉及CUVA数据集（但摘要未明确说明作为基准）。
- **基准（Benchmark）**：自身扩展后的UCA数据集，文中未提及现有其他公开benchmark。
- **对比方法**：与基线方法（baselines）比较，具体基线名称未在摘要中列出。

## 4. 资源与算力
- **文中说明**：摘要未提及使用的GPU型号、数量、训练时长等具体算力信息。因此无法总结。

## 5. 实验数量与充分性
- **实验数量**：从摘要看，主要进行了两类实验：属性中心犯罪分类准确率（attribute-centric crime classification accuracy）和MMEval评分。
- **充分性**：摘要仅报告了两项主要指标提升（≈20%↑分类准确率，≈6.4%↑MMEval）。未提及消融实验、不同数据集对比、超参数敏感性等，实验设置不够详实。可能论文正文有更多实验，但摘要中信息不足。整体需参考全文判断公平性和客观性。

## 6. 主要结论与发现
- 属性中心表示学习框架在属性级别犯罪分类准确率上提升约20%，在MMEval得分上提升约6.4%。
- 分析并缓解了MMEval评估中的偏差，确保评估鲁棒性。
- 证明了属性条件表示对于可解释、可靠的VAD至关重要。

## 7. 优点
- **创新性**：首次将属性中心表示学习引入VAD可解释性，并大幅扩展了属性级标注数据集。
- **可解释性**：通过回答What/When/How三个核心问题，提供多维度解释。
- **效果显著**：在两个指标上均有较大提升（尤其是分类准确率+20%）。

## 8. 不足与局限
- **实验覆盖**：摘要中仅提及UCA扩展数据集和baseline对比，未涉及多个数据集、多种异常类型、实时性等评估。泛化性有待验证。
- **偏差风险**：虽然分析了MMEval偏差，但LLM生成的属性标注可能引入语言模型偏见，真实场景标签噪声未讨论。
- **应用限制**：依赖大量属性标注的生成（LLM+手工提示），成本较高；框架复杂度高，可能难以部署在实时监控中。
- **算力信息缺失**：无法评估训练成本和可复现性。

（完）
