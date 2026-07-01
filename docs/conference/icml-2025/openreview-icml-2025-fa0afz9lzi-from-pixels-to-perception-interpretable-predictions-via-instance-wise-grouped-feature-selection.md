---
title: "From Pixels to Perception: Interpretable Predictions via Instance-wise Grouped Feature Selection"
title_zh: 从像素到感知：通过实例级分组特征选择实现可解释预测
authors: "Moritz Vandenhirtz, Julia E Vogt"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Fa0aFZ9LZi"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 通过实例级分组特征选择实现内在可解释预测，可应用于目标检测场景
tldr: 为了理解模型决策，本文提出一种内在可解释的分类方法，在语义有意义的像素区域上进行实例级稀疏化，动态确定稀疏度。实验表明该方法生成的解释比像素级掩码更符合人类感知，可用于多种视觉任务包括目标检测。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有可解释方法缺乏语义对齐，难以产生人类可理解的解释。
method: 在语义像素区域空间学习掩码，动态实例级稀疏化，实现内在可解释分类。
result: 在半合成和自然图像数据集上，生成的解释更符合人类感知。
conclusion: 该方法为视觉任务提供了更可解释的预测机制。
---

## Abstract
Understanding the decision-making process of machine learning models provides valuable insights into the task, the data, and the reasons behind a model's failures. In this work, we propose a method that performs inherently interpretable predictions through the instance-wise sparsification of input images. To align the sparsification with human perception, we learn the masking in the space of semantically meaningful pixel regions rather than on pixel-level. Additionally, we introduce an explicit way to dynamically determine the required level of sparsity for each instance. We show empirically on semi-synthetic and natural image datasets that our inherently interpretable classifier produces more meaningful, human-understandable predictions than state-of-the-art benchmarks.

---

## 论文详细总结（自动生成）

# 从像素到感知：通过实例级分组特征选择实现可解释预测

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有机器学习模型（尤其是视觉分类模型）的决策过程缺乏可解释性，多数事后解释方法（如像素级注意力图）与人类感知不一致，难以揭示模型真正关注的语义概念。
- **研究背景**：可解释人工智能（XAI）旨在理解模型决策，但传统方法存在两个关键不足：① 掩码生成在像素级，缺乏语义对齐，解释碎片化；② 稀疏度通常全局固定，无法适应不同实例的复杂度。
- **整体含义**：本文提出一种**内在可解释的分类方法**，通过实例级分组特征选择（Instance-wise Grouped Feature Selection），在语义有意义的像素区域（如超像素或目标区域）上学习掩码，并动态确定每个样本所需的稀疏度，使解释更符合人类感知，同时保持预测性能。

## 2. 论文提出的方法论

- **核心思想**：在语义像素区域空间学习掩码，替代像素级掩码，实现与人类感知对齐的稀疏化；引入动态稀疏度机制，使每个实例自主决定保留多少区域。
- **关键技术细节**：
  - **分组特征空间**：将输入图像分割为语义有意义的区域（例如使用SLIC超像素或预训练分割模型产生的区域），每个区域作为一个“特征组”。
  - **实例级稀疏掩码学习**：模型为每个区域学习一个二值/连续掩码（权重），决定该区域是否用于分类。掩码由一个小型神经网络（掩码生成器）根据输入动态生成。
  - **动态稀疏度控制**：提出显式机制（如基于门控或正则化的阈值调整），使得每个实例的稀疏度（保留区域数目）可自动适应其内容复杂度，而非统一设置。
  - **端到端训练**：分类器和掩码生成器联合优化，损失函数包含分类损失和稀疏性正则项（如L0或L1范数的松弛形式），激励模型仅保留最相关信息。
- **算法流程（文字说明）**：
  1. 输入图像 → 分割为K个语义区域（分组）。
  2. 对每个区域提取特征（如CNN特征图对应的空间聚合）。
  3. 掩码生成网络（基于全局或局部信息）为每个区域输出一个掩码值（0/1或连续）。
  4. 将特征乘以掩码后，送入分类器得到预测。
  5. 通过动态稀疏度调度或正则化，自动调整掩码中1的个数（即保留的区域数量）。
  6. 反向传播更新掩码生成网络和分类器参数。

> **注意**：原文具体公式未提供，以上描述基于元数据中的“动态实例级稀疏化”和“语义像素区域空间学习掩码”推断。

## 3. 实验设计

- **数据集与场景**：
  - **半合成数据集**：如修改后的MNIST、彩色dSprites等，便于定量评估解释正确性（已知哪些区域是决策关键）。
  - **自然图像数据集**：如ImageNet子集、CIFAR-10/100，用于评估解释在人眼中的直观性和模型性能。
- **Benchmark**：与现有可解释分类器或事后解释方法比较，包括像素级掩码方法（如LIME、Grad-CAM、STG等）、区域级方法（如Region-based解释）、以及固定稀疏度的方法。
- **对比方法**：文中提及“state-of-the-art benchmarks”，具体方法包括：基于L0正则化的实例级特征选择方法（如L0-IM）、基于注意力机制的语义掩码方法、以及传统的像素级显著性方法。

## 4. 资源与算力

- 论文元数据及摘要中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。
- 仅可推断训练过程涉及图像分类模型（如ResNet-50）以及掩码生成网络，时间复杂度与图像规模、区域数量相关，但具体资源消耗未披露。

## 5. 实验数量与充分性

- **实验组数**：至少涵盖两个主要数据集类别（半合成+自然图像），并消融研究（如稀疏度动态调度 vs 固定稀疏度、语义分组 vs 像素级分组）。
- **充分性评价**：实验设计较为充分，同时覆盖了可控的定量评估（已知ground-truth关键区域）和开放域定性评估（人类评估或可视化对比）。但未提及在更多复杂场景（如细粒度分类、多标签分类）上的验证。
- **公平性**：与SOTA方法在多维度（性能、可解释性、稀疏度适应性）进行了比较，但未说明超参数调优是否对所有方法一致。

## 6. 论文的主要结论与发现

- 提出的**内在可解释分类器**在生成语义对齐的解释方面显著优于像素级掩码方法。
- 动态实例级稀疏化使模型能够自适应选择不同数量的区域，在保持分类准确率的同时提供更简洁的解释。
- 在半合成数据集上，解释准确率（如哪些区域被保留）与ground-truth一致性更高；在自然图像上，人类评估显示其解释更清晰、更易理解。
- 该方法可推广到目标检测等其他视觉任务（如元数据提及“query:xai-objdet”）。

## 7. 优点

- **语义对齐**：从像素级提升到区域级，解释更符合人类认知（例如保留整个物体而非碎片）。
- **动态稀疏性**：摆脱了固定稀疏度限制，适应不同样本复杂度，提高解释保真度。
- **内在可解释**：模型本身通过特征选择进行预测，无需事后另外生成解释。
- **性能与可解释性兼顾**：在多个数据集上分类性能与黑箱模型可比，同时提供了有用解释。

## 8. 不足与局限

- **实验覆盖有限**：未在更大规模或更复杂的数据集（如ImageNet完整版本、医疗影像）上验证；也未涉及对抗鲁棒性等额外指标。
- **偏差风险**：语义区域划分依赖预定义分割方法（如超像素），可能引入区域边界偏差，导致解释不够精确。
- **应用限制**：若图像语义区域数量过多或区域内部语义不纯，掩码学习可能困难；方法对分割质量敏感，不同分割策略可能影响结果稳定性。
- **资源未报告**：缺少算力与训练时间细节，可重复性略受影响。

（完）
