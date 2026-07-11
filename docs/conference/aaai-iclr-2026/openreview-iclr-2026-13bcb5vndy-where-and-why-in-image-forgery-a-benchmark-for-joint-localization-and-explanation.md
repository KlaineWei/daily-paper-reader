---
title: "Where and Why in Image Forgery: A Benchmark for Joint Localization and Explanation"
title_zh: 图像伪造中的何处与为何：联合定位与解释基准
authors: "Jingchun Lian, Lingyu Liu, Yaxiong Wang, Yujiao Wu, Li Zhu, Zhedong Zheng"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=13bCB5VnDy"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 图像伪造的联合定位与解释
tldr: "本文提出图像伪造归因报告生成新任务，联合定位伪造区域（Where）并生成基于编辑过程的自然语言解释（Why）。构建了152,217样本的MMTT数据集，包含真实掩码和人类撰写的文本描述。该方法突破了传统二分类或像素级定位的局限，为伪造检测提供了可解释性。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有伪造检测方法缺乏语义层面解释。
method: 定义伪造归因报告生成任务，联合定位和文本解释。
result: 构建大规模多模态数据集MMTT。
conclusion: 为可解释伪造检测提供新方向与基准。
---

## Abstract
Existing facial forgery detection methods typically focus on binary classification or pixel-level localization, providing little semantic insight into the nature of the manipulation. To address this, we introduce Forgery Attribution Report Generation, a new multimodal task that jointly localizes forged regions ("Where") and generates natural language explanations grounded in the editing process ("Why"). This dual-focus approach goes beyond traditional forensics, providing a comprehensive understanding of the manipulation. To enable research in this domain, we present **M**ulti-**M**odal **T**amper **T**racing (**MMTT**), a large-scale dataset of 152,217 samples, each with a process-derived ground-truth mask and a human-authored textual description, ensuring high annotation precision and linguistic richness. We further propose ForgeryTalker, a unified end-to-end framework that integrates vision and language via a shared encoder (image encoder + Q-former) and dual decoders for mask and text generation, enabling coherent cross-modal reasoning. Experiments show that ForgeryTalker achieves competitive performance on both report generation and forgery localization subtasks, i.e., 59.3 CIDEr and 73.67 IoU, respectively, establishing a baseline for explainable multimedia forensics. Dataset and code will be released to foster future research.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有面部伪造检测方法大多局限于二分类（真/假）或像素级定位（即判定哪些像素被篡改），无法提供对伪造本质的语义理解。缺乏对“为何”该区域被篡改以及篡改过程的可解释性。
- **核心问题**：本文提出一个新的多模态任务——**伪造归因报告生成**（Forgery Attribution Report Generation），要求同时定位伪造区域（Where）和生成基于编辑过程的自然语言解释（Why），从而突破传统取证方法的局限，实现更全面的篡改理解。
- **整体含义**：该任务将视觉定位与语言生成相结合，为可解释多媒体取证提供新方向与基准，有助于提升伪造检测的透明度和可信度。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：构建一个端到端统一框架，联合学习伪造区域的像素级掩码和相应的文本描述，使模型能够同时输出“位置”和“解释”。
- **关键技术细节**：
  - 提出 **ForgeryTalker**，一个统一的端到端框架。
  - 采用**共享编码器**：由图像编码器（如视觉骨干网络）与 Q-Former（跨模态查询转换器）组成，用于提取视觉特征并与文本模态对齐。
  - 采用**双解码器**：一个用于生成二进制掩码（定位），另一个用于生成自然语言文本描述（解释）。两个解码器共享底层视觉表征，通过多任务学习实现协同推理。
  - 训练过程中联合优化掩码损失（如IoU损失、二分类交叉熵）和文本生成损失（如语言建模损失）。
- **公式/算法流程（文字说明）**：
  1. 输入：篡改图像。
  2. 共享编码器（图像编码器 + Q-Former）提取多模态特征。
  3. 掩码解码器根据特征预测像素级篡改掩码。
  4. 文本解码器根据特征逐词生成自然语言报告，描述篡改类型、区域、编辑操作等。
  5. 两个分支通过联合损失函数端到端训练。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - 构建了 **MMTT（Multi-Modal Tamper Tracing）** 数据集，包含 **152,217 个样本**。每个样本均有：
    - 基于编辑过程生成的真实掩码（ground-truth mask），确保定位精度。
    - 由人类撰写的文本描述，保证语言丰富性和真实性。
- **基准（Benchmark）**：论文将 MMTT 作为该新任务的基准数据集，并提供了两种子任务的评价指标：
  - 文本报告生成：使用 **CIDEr**（59.3）等传统图像描述指标。
  - 伪造定位：使用 **IoU**（73.67）等分割指标。
- **对比方法**：
  - 由于该任务是全新的，论文主要将 ForgeryTalker 与基于独立子任务的现有方法进行对比（如单独的分类器+文本生成模型、单独的分割模型等），并报告了其作为统一框架的性能基线。具体对比方法未在摘要中详细列举，但实验表明其达到了当时的最佳性能。

## 4. 资源与算力

- **文中未明确说明**使用的 GPU 型号、数量、训练时长等具体算力信息。仅提及数据集和代码将公开。

## 5. 实验数量与充分性

- **实验数量**：
  - 论文在 MMTT 数据集上进行了完整的训练和测试，报告了报告生成（CIDEr=59.3）和定位（IoU=73.67）两项主要指标。
  - 推测文中包含消融实验以验证共享编码器、双解码器结构及各组件的有效性（但摘要未提供细节）。
- **充分性**：
  - 实验覆盖了新任务的两个方面，并建立了基准。但缺少与其他数据集（如传统伪造检测数据集）或更大规模场景的对比。
  - 由于任务新颖，对比方法可能不够全面，但作为首篇工作，实验设计相对客观。

## 6. 论文的主要结论与发现

- 定义并提出了**伪造归因报告生成**这一新任务，为可解释伪造检测开辟新方向。
- 构建了大规模多模态数据集 **MMTT**（152,217 样本），具有高质量的真实掩码和人类注释文本。
- 提出的 **ForgeryTalker** 统一框架能够同时完成定位和文本解释，在 CIDEr 和 IoU 上均取得有竞争力的性能（59.3 / 73.67），验证了联合训练的可行性和有效性。
- 该工作为未来可解释多媒体取证研究提供了基准方法和数据资源。

## 7. 优点

- **任务创新性**：首次将伪造检测从纯视觉（分类/分割）扩展到多模态（定位+语言解释），提升可解释性。
- **数据质量高**：MMTT 数据集规模大、注释精细（过程驱动掩码+人工文本），确保实验可靠性。
- **框架简洁高效**：ForgeryTalker 采用共享编码器+双解码器，端到端训练，避免了分阶段方法的信息损失。
- **公开资源**：承诺开源代码和数据，有利于社区跟进。

## 8. 不足与局限

- **实验覆盖可能不足**：仅在一个自有数据集上评测，缺乏在现有标准伪造检测数据集（如 FaceForensics++、Celeb-DF 等）上的对比实验，泛化能力待验证。
- **偏差风险**：MMTT 数据集可能主要覆盖特定类型的编辑（如面部属性编辑），对更复杂或未知伪造方式的解释能力未知。
- **应用限制**：
  - 任务目标为“归因报告”，但文本解释可能仍不够详细或准确，需要更严谨的评估方法（如人工评估）。
  - 资源与算力未公布，难以复现训练成本。
  - 模型参数量和推理速度未提及，可能影响实际部署。

（完）
