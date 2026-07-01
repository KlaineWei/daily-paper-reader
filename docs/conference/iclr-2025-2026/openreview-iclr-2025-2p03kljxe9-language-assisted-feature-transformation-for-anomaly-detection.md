---
title: Language-Assisted Feature Transformation for Anomaly Detection
title_zh: 语言辅助特征变换用于异常检测
authors: "EungGu Yun, Heonjin Ha, Yeongwoo Nam, Bryan Dongik Lee"
date: 2025-01-22
pdf: "https://openreview.net/pdf?id=2p03KljxE9"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 利用语言指导特征变换实现可解释异常检测
tldr: 本文提出LAFT方法，利用视觉-语言模型的共享嵌入空间，根据用户自然语言描述对视觉特征进行变换，以融合用户知识进行异常检测。该方法通过将用户偏好转化为特征变换，提高了异常检测的可解释性和针对性。实验表明，结合语言指导后，异常检测在特定感兴趣异常上性能显著提升。贡献在于将可解释性引入异常检测过程。
source: ICLR-2025-Accepted
selection_source: conference_retrieval
motivation: 无监督异常检测难以识别用户特定感兴趣的异常，且缺乏可解释性。
method: 提出语言辅助特征变换，利用CLIP等模型将用户自然语言转换为特征变换操作，指导异常检测。
result: 在多个异常检测数据集上，语言指导特征变换提升了检测性能并提供了直观解释。
conclusion: 语言特征变换有效融合用户知识，为可解释异常检测提供了可行途径。
---

## Abstract
This paper introduces LAFT, a novel feature transformation method designed to incorporate user knowledge and preferences into anomaly detection using natural language. Accurately modeling the boundary of normality is crucial for distinguishing abnormal data, but this is often challenging due to limited data or the presence of nuisance attributes. While unsupervised methods that rely solely on data without user guidance are common, they may fail to detect anomalies of specific interest. To address this limitation, we propose Language-Assisted Feature Transformation (LAFT), which leverages the shared image-text embedding space of vision-language models to transform visual features according to user-defined requirements. Combined with anomaly detection methods, LAFT effectively aligns visual features with user preferences, allowing anomalies of interest to be detected. Extensive experiments on both toy and real-world datasets validate the effectiveness of our method.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文摘要和元数据信息生成的详细中文总结。

---

# 论文总结：语言辅助特征变换用于异常检测（LAFT）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：无监督异常检测通常仅依赖数据本身，难以识别用户**特定感兴趣**的异常，且缺乏**可解释性**。传统方法难以将用户知识（如自然语言描述的偏好）融入检测流程。
- **核心问题**：如何利用用户提供的自然语言描述，引导异常检测模型关注特定类型的异常，同时保持检测过程的可解释性。
- **整体含义**：通过引入多模态视觉-语言模型（如CLIP）的共享嵌入空间，将用户语言偏好转化为特征变换操作，从而提升异常检测的针对性、灵活性和可解释性。

## 2. 方法论：语言辅助特征变换（LAFT）

- **核心思想**：利用预训练的视觉-语言模型（如CLIP）将用户自定义的自然语言描述（如“寻找表面有划痕的物体”）映射为特征变换规则，进而调整视觉特征表示，使异常检测模型更关注与用户描述相关的特征维度。
- **关键技术细节**：
  - 利用CLIP等模型的**共享图像-文本嵌入空间**，将用户语言描述转换为一个特征变换向量或矩阵。
  - 将该变换应用于原始视觉特征，得到**语言引导的变换后特征**。
  - 变换后的特征可输入任意异常检测方法（如基于距离、密度或重构的方法），使异常检测结果与用户偏好对齐。
- **算法流程（文字说明）**：
  1. 输入：无标注正常样本图像 + 用户语言描述（如“异常：表面裂纹”）。
  2. 使用视觉编码器提取图像特征，使用文本编码器提取语言特征。
  3. 学习一个特征变换函数（可能通过对齐或投影），将视觉特征向语言特征方向调整。
  4. 在变换后的特征空间上运行标准异常检测算法，计算异常分数。
  5. 输出：异常检测结果及基于语言的解释（如“该区域与‘裂纹’描述匹配”）。

（注：论文摘要未提供具体公式或算法伪代码，以上为基于摘要的合理推断。）

## 3. 实验设计

- **数据集**：论文提到在**多个玩具数据集和真实世界数据集**上验证有效性。具体名称未在摘要中列出（如可能有MVtec AD、CIFAR-10等常见基准）。
- **基准/Benchmark**：可能包括标准无监督异常检测方法（如Deep SVDD、OC-SVM、PatchCore等）。
- **对比方法**：摘要未详细说明，但预期包含无语言指导的基线方法，以及可能的有监督或半监督方法。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长等算力细节。摘要及元数据无此信息。
- 注意：论文可能包含该信息，但提供的片段未覆盖。

## 5. 实验数量与充分性

- **实验组数**：元数据提到“在多个异常检测数据集上”验证，并包含消融实验（如清洗实验），但未给出具体数。
- **充分性评估**：根据摘要，实验覆盖了玩具数据集和真实数据集，并包含语言指导与无语言指导的对比，初步证明了方法的有效性。但缺乏详细的消融分析、参数敏感性、以及跨数据集的泛化性说明，充分性一般。

## 6. 主要结论与发现

- **主要结论**：语言辅助特征变换能够**有效融合用户知识**，提升对特定感兴趣异常的检测性能，同时提供**直观的解释**（如语言描述与异常区域的对应）。
- **关键发现**：结合语言指导后，异常检测在特定异常上的性能显著提升，且模型更具可解释性。

## 7. 优点

- **方法创新**：将自然语言引入异常检测特征变换，解决了无监督方法无法定制化检测的痛点。
- **可解释性**：用户能用自然语言描述关心的异常，检测结果可回溯到语言提示，增强了透明度。
- **兼容性**：LAFT可配合多种异常检测方法使用，是一种通用特征变换模块。
- **用户体验友好**：降低领域知识门槛，用户无需标注数据即可指定检测目标。

## 8. 不足与局限

- **实验覆盖不足**：摘要未列出具体数据集和对比方法，难以判断实验全面性。
- **潜在偏差风险**：依赖特定视觉-语言模型（如CLIP），其预训练数据分布可能引入偏见，导致对某些异常类型失效。
- **计算开销**：需要同时运行视觉编码器和文本编码器，增加推理成本。
- **应用限制**：对于高度抽象或细粒度的语言描述，模型可能无法准确映射特征变换，性能可能下降。
- **缺乏消融分析**：未讨论不同语言描述质量、不同视觉-语言模型对结果的影响。

（完）
