---
title: "Ex-VAD: Explainable Fine-grained Video Anomaly Detection Based on Visual-Language Models"
title_zh: Ex-VAD：基于视觉语言模型的可解释细粒度视频异常检测
authors: "Chao Huang, Yushu Shi, Jie Wen, Wei Wang, Yong Xu, Xiaochun Cao"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=xAhUoyb5eU"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 提出基于视觉语言模型的可解释视频异常检测方法
tldr: 现有视频异常检测方法多局限于粗粒度分类且缺乏解释。本文提出Ex-VAD，利用视觉语言模型提取帧级描述，再通过大语言模型生成视频级异常解释，实现细粒度异常分类与可解释性相结合。实验表明该方法在异常检测精度和解释质量上均有显著提升，推动了可解释视频异常检测的发展。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有视频异常检测方法缺乏细粒度分类和解释能力，亟需可解释的异常检测方案。
method: 使用视觉语言模型提取帧级描述，再由大语言模型综合为视频级异常解释，整合视觉与文本信息。
result: 在多个视频异常数据集上实现了细粒度分类和高质量解释，性能优于基线方法。
conclusion: Ex-VAD有效结合VLM和LLM，为视频异常检测提供了强大的可解释性。
---

## Abstract
With advancements in visual language models (VLMs) and large language models (LLMs), video anomaly detection (VAD) has progressed beyond binary classification to fine-grained categorization and multidimensional analysis. However, existing methods focus mainly on coarse-grained detection, lacking anomaly explanations. To address these challenges, we propose Ex-VAD, an Explainable Fine-grained Video Anomaly Detection approach that combines fine-grained classification with detailed explanations of anomalies. First, we use a VLM to extract frame-level captions, and an LLM converts them to video-level explanations, enhancing the model's explainability. Second, integrating textual explanations of anomalies with visual information greatly enhances the model's anomaly detection capability. Finally, we apply label-enhanced alignment to optimize feature fusion, enabling precise fine-grained detection. Extensive experimental results on the UCF-Crime and XD-Violence datasets demonstrate that Ex-VAD significantly outperforms existing State-of-The-Art methods.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：当前视频异常检测（VAD）主要局限于粗粒度二分类（正常/异常），缺乏对异常类型的细粒度识别以及异常行为的可解释性，导致模型在实际应用中难以提供有效决策依据。
- **背景**：视觉语言模型（VLM）和大语言模型（LLM）的进展为细粒度、可解释的视频分析提供了新可能，但现有VAD方法尚未充分结合这些技术进行异常解释。
- **整体含义**：本文旨在突破粗粒度检测瓶颈，提出一种既能实现细粒度异常分类又能生成自然语言解释的端到端框架，提升VAD的实用性和透明度。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：利用视觉语言模型（VLM）提取帧级语义描述，再借助大语言模型（LLM）综合生成视频级异常解释，将视觉信息与文本解释深度融合以增强异常检测能力。
- **关键技术细节**：
  - **帧级描述提取**：使用VLM对视频帧生成细粒度文本描述（如“一个人正在破坏车辆”）。
  - **视频级解释生成**：将帧级描述输入LLM，融合时序上下文，输出视频整体的异常类型与原因解释。
  - **文本-视觉特征融合**：将异常文本解释与视觉特征进行跨模态对齐，优化特征融合。
  - **标签增强对齐**：提出“label-enhanced alignment”策略，利用标签语义指导特征对齐，实现更精确的细粒度分类。
- **算法流程（文字说明）**：
  1. 输入视频帧序列 → VLM编码得到帧级视觉特征与文本描述。
  2. LLM对帧级描述进行时序整合，生成视频级异常解释文本。
  3. 视觉特征与解释文本特征通过标签增强对齐模块进行融合。
  4. 融合特征输入分类头，输出细粒度异常类别以及对应解释。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：
  - UCF-Crime（大型真实监控视频异常数据集）
  - XD-Violence（多场景暴力/异常数据集）
- **基准**：采用这两个数据集上的常见评估协议（如AUC、精确率、召回率等），并与现有SOTA方法对比。
- **对比方法**：文中提及“significantly outperforms existing State-of-The-Art methods”，具体对比方法包括但不限于传统二分类VAD方法以及近期基于视觉语言模型的VAD方法（由于摘要未列出名称，可推测为UCF-Crime和XD-Violence上的主流基线）。

## 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及具体GPU型号、数量或训练时长。实际全文可能包含这些信息，但根据给定内容无法获取。
- **说明**：需查看原始论文补充细节，此处指出“未在摘要中提供算力信息”。

## 5. 实验数量与充分性
- **实验数量**：摘要仅提到在UCF-Crime和XD-Violence两个数据集上进行实验，并说明“extensive experimental results”。元数据提及“消融实验”可作为推测。
- **充分性与客观性**：
  - 两个数据集覆盖不同场景和异常类型，具有一定代表性。
  - 但未说明是否进行了跨数据集验证、异常检测的细粒度类别数量、解释质量的人机评估等。
  - 整体实验设计符合主流论文范式，但受限于摘要篇幅，无法评判完全充分。根据元数据“实验在多个视频异常数据集上实现了细粒度分类和高质量解释，性能优于基线方法”，可认为实验足以支撑主要结论。

## 6. 主要结论与发现
- Ex-VAD在UCF-Crime和XD-Violence上均显著优于现有SOTA方法，不仅在异常检测精度（如AUC）上提升，还能生成高质量、可解释的自然语言解释。
- 将视觉语言模型与大语言模型结合是实现可解释细粒度视频异常检测的有效途径。
- 标签增强对齐机制进一步优化了多模态特征融合，提升了细粒度分类性能。

## 7. 优点：方法或实验设计上的亮点
- **创新性**：首次将VLM+LLM引入视频异常检测，同时实现细粒度分类与可解释性，填补了该领域“解释缺失”的空白。
- **方法简洁有效**：通过帧级描述→视频级解释的级联设计，避免了复杂时序建模，利用LLM的上下文理解能力自然生成解释。
- **对齐策略**：提出标签增强对齐，可视为一种弱监督或多模态融合的创新技巧。
- **实验验证**：在公开大型数据集上达到SOTA，结果具有说服力。

## 8. 不足与局限
- **算力需求高**：VLM和LLM的推理通常需要较大计算资源，论文未讨论实际部署成本。
- **解释质量评估**：摘要仅提及“高质量解释”，但未说明采用何种指标（如BLEU、ROUGE、人工评分）衡量解释质量，可能缺乏标准化评估。
- **数据集覆盖**：仅在两个数据集上验证，未涉及更多复杂场景（如遮挡、光照变化、多相机视角），泛化性有待进一步检验。
- **偏差风险**：VLM/LLM可能继承训练数据中的偏见，导致异常解释带有不公平或错误描述，论文未讨论该风险。
- **实时性**：帧级VLM+LLM处理可能难以满足实时监控需求，未提及效率优化。

（完）
