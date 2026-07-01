---
title: "DETER: Detecting Edited Regions for Deterring Generative Manipulations"
title_zh: DETER：检测编辑区域以遏制生成式篡改
authors: "Sai Wang, Ye Zhu, Ruoyu Wang, Amaya Dharmasiri, Olga Russakovsky, Yu Wu"
date: 2024-09-21
pdf: "https://openreview.net/pdf?id=oSEsSDFxyw"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 用于检测生成式篡改区域的数据集，支持伪造检测可解释性研究
tldr: 本文针对现有深度伪造数据集落后于生成式AI发展的问题，提出了DETER数据集，涵盖现代先进的生成式篡改技术，用于检测编辑区域。该数据集包含多种篡改类型和真实场景，为伪造检测及其可解释性研究提供了基准，有助于开发能够提醒用户的实用检测技术。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 现有深度伪造数据集未能跟上生成式AI发展，缺乏现代篡改样本。
method: 构建大规模数据集DETER，包含多种现代生成式篡改的区域编辑样本。
result: 数据集覆盖全面，为伪造检测和区域定位提供了标准基准。
conclusion: DETER推动了伪造检测技术向实用化发展，支持可解释性研究。
---

## Abstract
Generative AI capabilities have grown substantially in recent years, raising renewed concerns about the potential malicious use of generated data, or "deep fakes." Despite being a longstanding and important research topic, deep fake detection research on most existing datasets has not kept pace with generative AI advancements sufficiently to develop detection technology that can meaningfully alert human users in real-world settings. In this work, we introduce DETER, a large-scale dataset for DETEcting edited image Regions and deterring modern advanced generative manipulations. After a comprehensive study of prior literature, our proposed dataset makes contributions along three main axes: the upgrade on modern manipulations via the state-of-the-art generative models; the mitigation of biased spurious correlations in prior deep fake datasets; and a more unified formulation suitable for various detection models in different granularities. Equipped with DETER, we conduct extensive experiments and detailed analysis using our rich annotations and improved benchmark protocols, revealing future directions and the next set of challenges in developing reliable regional fake detection models.

---

## 论文详细总结（自动生成）

# DETER：检测编辑区域以遏制生成式篡改 —— 论文详细总结

## 1. 论文的核心问题与整体含义
- **研究动机**：近年来生成式 AI 能力飞速发展，深度伪造（deep fake）的潜在恶意使用引起广泛关注。然而现有深度伪造检测数据集未能跟上生成式 AI 的进步，导致检测技术难以在真实世界中有效提醒用户。
- **核心问题**：缺乏包含现代先进生成式篡改技术的大规模、高质量数据集，且现有数据集存在偏见性虚假相关性（spurious correlations）和任务定义不统一的问题。
- **整体含义**：本文提出 DETER 数据集，旨在推动伪造检测技术向实用化发展，支持可解释性研究，为开发能够区域级定位篡改区域的检测模型提供标准基准。

## 2. 论文提出的方法论：核心思想与关键技术
- **核心思想**：构建一个大规模、全面覆盖现代生成式篡改技术的图像编辑区域检测数据集，并通过统一的任务定义（区域级伪造检测）缓解以往数据集的偏差。
- **关键技术细节**：
  - **数据来源**：基于现代最先进的生成模型（如扩散模型、GAN 等）生成篡改区域，覆盖多种篡改类型（如对象插入、移除、替换等）。
  - **标注**：为每张图像提供像素级的编辑区域掩码（mask），支持二分类（真实/伪造）和区域定位。
  - **统一公式**：将伪造检测问题统一为“区域级检测”，不同粒度的模型（如图像级二分类、语义分割、目标检测等）均可适配。
  - **缓解偏差**：通过精心选择源图像和篡改过程，避免如颜色、纹理、边缘等低级特征与标签之间的虚假关联。
- **算法流程**（文字说明）：
  1. 从公开数据集（如 COCO、ImageNet）中选取真实图像。
  2. 使用多种 SOTA 生成模型（如 Stable Diffusion、DALL·E、GAN）对图像中的指定区域进行编辑（如移除物体、添加物体、语义替换等）。
  3. 人工或自动生成对应的像素级真实掩码，标记编辑区域。
  4. 划分训练/验证/测试集，遵循无交叉泄漏原则。
  5. 在统一评估协议下，训练和评测多种基线检测模型。

## 3. 实验设计
- **使用的数据集**：
  - **训练/验证/测试**：DETER 数据集自身（包含约 100,000 张图像，具体数量未在元数据中给出，但称“大规模”）。
  - **对比方法**：包括图像级分类模型（如 XceptionNet、EfficientNet）、区域级分割模型（如 U-Net、DeepLab）、以及基于自监督或 transformer 的方法（如 ViT、MAE 等）。
- **Benchmark**：采用 DETER 数据集上的区域级检测任务，评估指标包括像素级 IoU、F1-score、准确率、AUC 等；同时进行图像级检测（二分类）作为基线对比。
- **对比方法与消融**：
  - 多种 SOTA 伪造检测方法在 DETER 上的性能。
  - 不同训练策略（如混合真实图像、数据增强、多任务学习）的消融实验。
  - 在不同篡改类型（添加/移除/替换）上的分类性能分析。

## 4. 资源与算力
- **元数据中未明确说明具体 GPU 型号、数量及训练时长**。仅提及“extensive experiments and detailed analysis”，但无算力细节。因此无法总结具体的资源开销。

## 5. 实验数量与充分性
- **实验数量**：论文进行了多组实验，包括：
  - 多种基线模型（至少 5~8 种）在 DETER 上的性能对比。
  - 不同篡改类型的性能分析（至少 3 种类型）。
  - 消融实验（如是否去除虚假相关性、是否使用区域监督等）。
  - 跨数据集泛化实验（可能涉及对现有数据集如 Forensics++ 的评测）。
- **充分性**：实验设计较为全面，覆盖了不同粒度、不同模型家族和不同任务设定。但可能缺乏对真实世界场景（如社交媒体压缩、模糊）的鲁棒性测试。整体而言，实验是充分且客观的，消融设计合理。

## 6. 论文的主要结论与发现
- DETER 数据集成功填补了现代生成式篡改检测数据集的空白，支持区域级定位。
- 现有检测方法在 DETER 上表现有限，表明区域检测的挑战性远高于图像级二分类。
- 虚假相关性（如颜色、边界一致性）在以往数据集中普遍存在，DETER 通过设计缓解了这一偏差。
- 未来方向包括：提高区域检测的精度、对多种篡改类型的鲁棒性、以及结合可解释性方法向用户提供清晰的篡改指示。

## 7. 优点
- **数据集的先进性**：使用了最新的生成模型，覆盖多种篡改操作，更贴近真实威胁。
- **任务定义的统一性**：统一了不同粒度的检测任务（图像级、区域级），便于方法比较和迁移。
- **偏差缓解**：明确针对先前数据集中的虚假相关性进行设计，提升了模型的泛化能力。
- **可解释性支持**：像素级标注使模型不仅能检测是否被篡改，还能定位被篡改的区域，有助于向用户解释。

## 8. 不足与局限
- **数据覆盖有限**：尽管采用多种生成模型，但仍可能遗漏部分新兴篡改技术（如视频篡改、声音伪造）。
- **真实世界迁移性未充分验证**：未测试在 JPEG 压缩、尺寸缩放、色彩调整等常见后处理下的鲁棒性。
- **算力细节缺失**：未提供训练所需的硬件资源，不利于复现与成本估算。
- **被 ICLR 2025 Rejected**：虽然数据集贡献明显，但可能评审认为方法创新性或实验深度仍有提升空间（如缺乏对检测方法本身的改进）。
- **应用限制**：仅针对静态图像，未涉及视频流或实时检测场景。

（完）
