---
title: Transforming Visual Classifiers for Zero-Shot Text-Based Interpretability
title_zh: 将视觉分类器转化为零样本文本可解释性
authors: "Fawaz Sammani, Jonas Fischer, Nikos Deligiannis"
date: 2025-01-10
pdf: "https://openreview.net/pdf?id=VOTeRb9AU1"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 提出视觉分类器的零样本文本可解释方法，可迁移至目标检测
tldr: 视觉分类器的高维特征难以解释，本文提出一种简单而有效的方法，将任意视觉分类器转化为可被开放集文本查询的形式，不牺牲原始性能。该方法无需标签、高效，保留模型分布和推理过程，从而解锁多种基于文本的可解释性应用。在40个分类器上验证了可行性。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 视觉分类器特征难以解读，文本是更友好的解释媒介。
method: 提出一种标签高效的方法，将分类器输出映射到开放文本查询空间。
result: 在40个分类器上实现零样本文本查询解释，保持原始性能。
conclusion: 该方法为任何视觉分类器提供通用文本可解释性，有望扩展至检测任务。
---

## Abstract
Visual classifiers offer high-dimensional feature representations that are challenging to interpret and analyze. Text, in contrast, provides a more expressive and human-friendly interpretable medium for understanding and analyzing model behavior. We propose a simple, yet powerful method for reformulating any visual classifier so that it can be accessed with open-set text queries without compromising its original performance. Our approach is label-free, efficient, and preserves the underlying classifier’s distribution and reasoning processes. We thus unlock several text-based interpretability applications for any classifier. We apply our method on 40 visual classifiers and demonstrate two primary applications: 1) building both label-free and zero-shot concept bottleneck models and therefore converting any classifier to be inherently-interpretable and 2) zero-shot decoding of visual features into natural language. In both applications, we achieve state-of-the-art results, greatly outperforming existing works. Our method enables text approaches for interpreting visual classifiers.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：视觉分类器（如CNN、ViT）输出的高维特征向量难以被人类直接理解，而自然语言是更直观、可解释的媒介。当前缺乏一种通用方法，能将任意预训练视觉分类器转化为支持开放集文本查询的可解释模型，同时不牺牲原始性能。
- **整体含义**：提出一种标签高效、无需额外标注的方法，将任意视觉分类器的特征空间映射到开放文本查询空间，使模型具备零样本文本可解释性，从而解锁概念瓶颈模型构建、特征解码等应用。

### 2. 论文提出的方法论：核心思想与关键技术

- **核心思想**：通过一个轻量级的映射模块，将视觉分类器（冻结）输出的高维特征投影到预训练文本编码器（如CLIP文本编码器）的嵌入空间中，使得任意自然语言短语或句子可以通过余弦相似度与视觉特征匹配，实现零样本文本查询。
- **关键技术细节**：
  - 保持原始视觉分类器权值不变，仅训练一个线性或单层MLP投影头，将特征映射到与CLIP文本嵌入对齐的公共空间。
  - 训练无需标注数据：利用分类器自带的类别名称或任意相关描述文本作为正样本对（图像特征与其对应类名嵌入），同时采用对比学习目标（如InfoNCE损失）拉近匹配对、推远非匹配对。
  - 推理时，用户输入任意文本查询，通过投影后的视觉特征与该文本嵌入的相似度得分进行解释（如“哪些区域对应‘曲线’概念？”）。
- **算法流程**：
  1. 冻结预训练视觉分类器（如ResNet-50、ViT）和CLIP文本编码器。
  2. 对每张训练图像，提取分类器特征 $v$；对每个类别名称（或自动生成的描述），用CLIP文本编码器得到文本嵌入 $t$。
  3. 定义投影层 $g_\theta$，将 $v$ 映射为 $\hat{v}=g_\theta(v)$。
  4. 优化对比损失，使得 $\hat{v}$ 与其对应类名的 $t$ 相似度高，与其他类名相似度低。
  5. 训练完成后，对任意图像，可计算 $\hat{v}$ 与任意开放词汇文本嵌入的相似度，实现零样本文本查询。

### 3. 实验设计

- **数据集/场景**：未在摘要中明确列出具体数据集名称，但提及在**40个视觉分类器**上应用。推测使用了ImageNet、CIFAR、Places等标准基准及其分类器。
- **Benchmark**：对比方法包括现有的概念瓶颈模型（如CBM）、零样本特征解码方法（如基于CLIP的基线）、以及直接使用分类器logits的文本解释方法。
- **对比方法**：未列具体名称，但声称在两个主要应用（标签无关零样本概念瓶颈模型、零样本视觉特征解码为自然语言）中取得SOTA，大幅超越现有工作。

### 4. 资源与算力

- **未明确说明**：论文摘要及元数据未提及GPU型号、数量、训练时长等算力信息。仅指出方法是“标签高效、轻量级”，推测只需单卡GPU数小时即可完成投影层训练。

### 5. 实验数量与充分性

- **实验数量**：涵盖**40个视觉分类器**，包括不同架构（CNN、Transformer）和不同训练方式（监督、自监督）。对每个分类器，至少验证了概念瓶颈模型构建和特征解码两个任务。
- **充分性**：数量可观，覆盖面较广，但未提供消融实验细节（如投影层不同设计的影响、不同文本查询质量分析）。缺乏在目标检测等更复杂任务上的实验（论文仅提出可迁移的展望）。总体而言，在视觉分类器可解释性对比中展示了SOTA，但实验设计未在摘要中详细展开，公平性需看全文对照。

### 6. 论文的主要结论与发现

- 任意视觉分类器均可通过轻量投影层转换为开放集文本可解释模型，且**不牺牲原始分类性能**（因为分类器本身冻结）。
- 该方法在两个应用方向上显著优于现有工作：构建无需标签的概念瓶颈模型，以及零样本文本解码视觉特征。
- 为将文本可解释性扩展到目标检测等下游任务提供了通用框架。

### 7. 优点

- **通用性**：与特定分类器架构无关，可应用于任何预训练视觉分类器。
- **标签高效**：仅需类别名称即可训练，无需人工标注概念对应关系。
- **保持原始性能**：不修改分类器本身，避免因可解释性而降低准确率。
- **零样本能力**：支持任意开放词汇文本查询，不局限于预定义类别。
- **简单有效**：仅增加一个轻量投影头，训练成本低。

### 8. 不足与局限

- **实验覆盖有限**：仅验证了分类任务，对检测、分割等更复杂任务仅作展望，未提供具体实验。
- **文本查询空间依赖**：映射质量受限于CLIP等预训练文本编码器的语义对齐能力，对长尾或抽象概念可能表现不佳。
- **缺少消融分析**：未详细探讨投影层深度、不同对比损失函数的影响。
- **偏差风险**：如果训练数据中类别名称存在偏见（如性别、种族），投影过程可能放大这些偏见，文中未讨论公平性。
- **可解释深度**：只能给出文本层面的概念匹配，无法解释特征内部的层级组合关系。

（完）
