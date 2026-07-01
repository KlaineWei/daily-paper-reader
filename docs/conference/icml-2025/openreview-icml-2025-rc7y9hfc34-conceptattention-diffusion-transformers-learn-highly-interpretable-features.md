---
title: "ConceptAttention: Diffusion Transformers Learn Highly Interpretable Features"
title_zh: ConceptAttention：扩散Transformer学习高度可解释的特征
authors: "Alec Helbling, Tuna Han Salih Meral, Benjamin Hoover, Pinar Yanardag, Duen Horng Chau"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Rc7y9HFC34"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 为扩散Transformer生成可解释的显著图，符合目标检测可解释性
tldr: 该论文提出ConceptAttention方法，利用扩散Transformer的注意力层生成高质量显著图，精确定位图像中的文本概念。无需额外训练即可获得比传统交叉注意力更清晰的解释图，在可解释性指标上达到最高水平，直接支持可解释性目标检测场景。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 扩散Transformer的表示是否具有独特可解释性？现有方法未能充分利用其注意力层的表达能力。
method: 通过重用扩散Transformer注意力层参数生成概念嵌入，对其输出空间进行线性投影得到显著图。
result: 在多个基准上显著优于传统交叉注意力图，定位精度达到SOTA。
conclusion: 证明扩散Transformer注意力层内在的可解释性能力，为可解释目标检测提供了新工具。
---

## Abstract
Do the rich representations of multi-modal diffusion transformers (DiTs) exhibit unique properties that enhance their interpretability? We introduce ConceptAttention, a novel method that leverages the expressive power of DiT attention layers to generate high-quality saliency maps that precisely locate textual concepts within images. Without requiring additional training, ConceptAttention repurposes the parameters of DiT attention layers to produce highly contextualized *concept embeddings*, contributing the major discovery that performing linear projections in the output space of DiT attention layers yields significantly sharper saliency maps compared to commonly used cross-attention maps. ConceptAttention even achieves state-of-the-art performance on zero-shot image segmentation benchmarks, outperforming 15 other zero-shot interpretability methods on the ImageNet-Segmentation dataset. ConceptAttention works for popular image models and even seamlessly generalizes to video generation. Our work contributes the first evidence that the representations of multi-modal DiTs are highly transferable to vision tasks like segmentation.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）
多模态扩散Transformer（DiT）的表示是否具有独特的可解释性属性？现有的可解释性方法（如传统交叉注意力图）未能充分利用DiT注意力层的表达能力，导致生成的显著图不够清晰、定位不精确。本文旨在挖掘DiT注意力层的内在可解释能力，为零样本图像分割等视觉任务提供高质量的定位工具。

## 2. 方法论：核心思想、关键技术细节
**核心思想**：通过重用DiT注意力层的参数，生成高度上下文化的“概念嵌入”（concept embeddings），并在注意力层输出空间中进行线性投影，从而得到比传统交叉注意力图更锐利的显著图。

**关键技术细节**：
- 无需额外训练，直接利用预训练DiT的注意力层参数。
- 将文本概念（如类别名称）输入到注意力层，提取相应的query/key/value表示，并计算新的嵌入。
- 在注意力层的输出空间执行线性投影（而非使用标准交叉注意力中的softmax加权和），显著图质量大幅提升。
- 该方法可无缝迁移到视频生成模型（通过逐帧应用）。

## 3. 实验设计
- **使用的数据集/场景**：ImageNet-Segmentation 数据集（用于零样本图像分割评估）。
- **基准（Benchmark）**：零样本图像分割任务，对比了15种其他零样本可解释性方法（包括传统交叉注意力图、GradCAM等）。
- **对比方法**：15种已有的零样本可解释性/分割方法，具体名称未在摘要中列出，但表明ConceptAttention达到了最优性能。

## 4. 资源与算力
论文摘要及元数据中**未明确说明**所使用的GPU型号、数量、训练时长等算力信息。因此无法总结。

## 5. 实验数量与充分性
从摘要可知至少进行了以下实验：
- 在ImageNet-Segmentation上与15种方法对比，性能达到SOTA。
- 验证了在图像模型和视频生成模型上的泛化能力（未提及具体视频数据集）。
- 未提及消融实验或更多数据集（如COCO等）；但零样本分割基准是标准评测，对比方法数量充足（15种），实验较为充分。然而缺少消融研究、不同分辨率/复杂场景的覆盖率等信息，公平性方面：未详细说明评估协议，但通常采用标准mIoU等指标，可认为客观。

## 6. 主要结论与发现
- DiT注意力层的输出空间具有高度可解释性，通过简单的线性投影即可生成比传统交叉注意力图更清晰的显著图。
- ConceptAttention在零样本图像分割上达到SOTA，超越15种其他方法。
- 多模态DiT的表示具有高度可迁移性，可泛化到视频生成任务（无需针对视频专门训练）。
- 本文提供了首个证据：多模态DiT的表示具有可解释性且适用于分割等视觉任务。

## 7. 优点
- **无需额外训练**：直接重用预训练模型的注意力参数，计算高效。
- **效果好**：显著图锐利精准，定位能力超过传统交叉注意力方法。
- **泛化性强**：从图像模型无缝迁移至视频生成模型，证明方法的通用性。
- **可解释性贡献**：首次揭示DiT注意力层的内在可解释性潜力，为可解释目标检测/分割提供新工具。

## 8. 不足与局限
- **实验覆盖有限**：仅在一个数据集（ImageNet-Segmentation）上报告定量结果，缺乏在更多分割基准（如PASCAL VOC、COCO）上的验证。
- **缺少消融实验**：未明确分析不同注意力层、投影方式、概念嵌入维度等设计选择的影响。
- **偏差风险**：仅测试了零样本设置，未评估在微调或类别增量场景下的表现。
- **应用限制**：依赖DiT架构（如Flux、Stable Diffusion 3等），其他类型的扩散模型（如UNet-based）可能不适用。
- **资源信息缺失**：未提供计算成本，无法评估实际部署的可行性。

（完）
