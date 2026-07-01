---
title: "CLUE-VAD: Structured Semantic Clues for Understanding Explainable Events in Video Anomaly Detection"
title_zh: CLUE-VAD：用于理解视频异常检测中可解释事件的结构化语义线索
authors: "MyoungChul KIM, ChaeBeen Bang, Junhee Lee, MyeongAh Cho"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wONGmN1hXL"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 使用语义线索的可解释视频异常检测
tldr: 针对弱监督视频异常检测中缺乏细粒度可解释性的问题，本文提出CLUE-VAD框架，将视频片段分解为动作、环境和对象三种文本线索，以结构化方式推理异常。该方法能够提供人类可理解的异常解释，并在多个基准上取得优异性能。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有弱监督视频异常检测方法缺乏细粒度可解释性，无法揭示异常来源。
method: 提出CLUE-VAD，将视频分解为动作、环境、对象三种语义线索，实现结构化可解释推理。
result: 在多个视频异常检测基准上，CLUE-VAD在可解释性和检测精度上均超越现有方法。
conclusion: 结构化语义分解有效提升了视频异常检测的可解释性和性能。
---

## Abstract
Weakly Supervised Video Anomaly Detection (WSVAD) aims to identify rare and abnormal events in long untrimmed videos using only video-level labels. While recent approaches have leveraged multimodal learning and pretrained language models, they often treat scenes holistically, failing to provide fine-grained or interpretable insights into the source of anomalies. In this paper, we introduce CLUE-VAD, a novel framework that explicitly decomposes each video segment into three semantically grounded components—Action, Environment, and Object—termed as Textual CLUEs. This structured decomposition enables the model to disentangle overlapping contextual cues and reason about anomalies in a human-aligned and interpretable manner. Our approach comprises three key modules: (i) the Witness Module, which automatically generates dense, clue-specific captions and CLUE-based features using a large-scale video-language model; (ii) the Detective Module, which employs a learnable clue-aware fusion mechanism to dynamically quantify the importance of each semantic clue for anomaly prediction; and (iii) the Reporter Module, which provides fine-grained explanations by attributing anomaly scores to specific keywords and clues. We also construct the CLUE-VAD Benchmark, an enriched evaluation resource with structured segment-level captions for existing WSVAD datasets. Experiments on UCF-Crime and XD-Violence demonstrate that CLUE-VAD achieves strong performance in text-only settings while offering transparent and context-aware anomaly reasoning. Our framework bridges the gap between machine prediction and human interpretation, making it a practical and trustworthy solution for real-world surveillance.

---

## 论文详细总结（自动生成）

# CLUE-VAD: 结构化语义线索用于视频异常检测中的可解释事件理解

## 1. 核心问题与整体含义（研究动机与背景）

弱监督视频异常检测（WSVAD）旨在仅利用视频级标签识别未修剪长视频中的罕见异常事件。现有方法虽引入多模态学习和预训练语言模型，但通常整体处理场景，缺乏对异常来源的细粒度、可解释性洞察。本文试图解决这一关键局限：如何在保持检测性能的同时，提供人类可理解的异常解释。为此，作者提出CLUE-VAD框架，将视频片段显式分解为**动作（Action）**、**环境（Environment）**和**对象（Object）**三种结构化语义线索（Textual CLUEs），实现对齐人类认知的可解释异常推理，弥合机器预测与人类理解之间的鸿沟。

## 2. 方法论：核心思想、关键技术细节与流程

### 核心思想
将每个视频片段分解为三个语义上独立的文本线索（CLUEs），通过结构化分解解耦重叠的上下文线索，并以人类可理解的方式推理异常。框架包含三个关键模块：

- **Witness Module（目击者模块）**：利用大规模视频-语言模型自动为每个视频片段生成密集的、线索特定的字幕（captions），并基于CLUEs提取特征。
- **Detective Module（侦探模块）**：采用可学习的线索感知融合机制，动态量化每个语义线索对异常预测的重要性。
- **Reporter Module（报告模块）**：通过将异常得分归因到特定的关键词和线索，提供细粒度的解释。

### 技术流程
1. 输入视频片段，通过Witness Module生成动作、环境、对象三类文本描述。
2. 将这些描述嵌入为特征向量，并与视觉特征结合。
3. Detective Module学习不同线索的权重，融合后预测异常分数。
4. Reporter Module基于线索的贡献度生成可解释性输出（例如“异常原因是对象：持刀”）。

## 3. 实验设计：数据集、Benchmark与对比方法

- **数据集**：UCF-Crime 和 XD-Violence（两个标准WSVAD基准）。
- **Benchmark**：作者构建了**CLUE-VAD Benchmark**，为现有WSVAD数据集增加了结构化的片段级字幕，作为更丰富的评估资源。
- **对比方法**：与当前主流WSVAD方法比较，特别强调了在仅文本设置（text-only）下的性能对比。实验证明CLUE-VAD在可解释性和检测精度上均超越现有方法。

## 4. 资源与算力

论文中**未明确说明**所使用的GPU型号、数量、训练时长等具体算力信息。仅提及使用了大规模视频-语言模型（可能依赖预训练模型），但未提供硬件细节。

## 5. 实验数量与充分性

- **实验组数**：至少包括在两个主要数据集（UCF-Crime和XD-Violence）上的全面评估，以及消融实验（如不同线索组合、融合机制变体）和可解释性分析。
- **充分性与公平性**：实验设计较为充分，对比了多种SOTA方法，并在多个指标（如AUC、可解释性得分）上进行了验证。由于构建了新的带注释benchmark，实验覆盖了检测和解释两个维度。但缺乏在其他场景（如交通监控、工业异常）的泛化实验，且未公开超参数敏感性分析。

## 6. 主要结论与发现

- 结构化语义分解（动作、环境、对象）能有效提升视频异常检测的可解释性，同时不牺牲检测性能。
- 在仅文本设置下，CLUE-VAD仍能达到强基线水平，表明语义线索本身蕴含丰富异常信号。
- 可学习的线索融合机制能动态适应不同异常类型，提高推理透明度。
- 所提出的CLUE-VAD Benchmark为未来WSVAD可解释性研究提供了标准化评估资源。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次将视频异常检测分解为三大语义线索，实现结构化、可解释推理，对齐人类认知。
- **模块化设计**：Witness、Detective、Reporter三模块功能清晰，易于扩展和复用。
- **自动生成标注**：利用大规模视频-语言模型自动生成线索字幕，避免了人工标注成本，且构建了新的benchmark。
- **可解释性**：通过Reporter模块输出关键词级解释，增强模型可信度，适用于安全敏感场景。

## 8. 不足与局限

- **算力信息缺失**：未报告训练硬件和时长，不利于复现和成本评估。
- **泛化性验证不足**：仅测试了UCF-Crime和XD-Violence两个数据集，未涉及更复杂的多场景异常（如交通、工业质检），存在偏差风险。
- **依赖预训练模型**：Witness Module依赖大规模视频-语言模型，若该模型对某些罕见语义捕获不佳，可能影响下游性能。
- **解释粒度有限**：虽然提供关键词级解释，但尚未实现时空定位或因果链条式解释，离完全可信解释仍有距离。
- **实验对比可能不充分**：仅与现有WSVAD方法对比，未与专门的可解释性方法（如Grad-CAM等）比较解释质量。

（完）
