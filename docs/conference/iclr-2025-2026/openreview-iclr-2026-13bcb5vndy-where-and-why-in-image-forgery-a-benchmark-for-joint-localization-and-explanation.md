---
title: "Where and Why in Image Forgery: A Benchmark for Joint Localization and Explanation"
title_zh: 图像伪造的Where和Why：联合定位与解释的基准
authors: "Jingchun Lian, Lingyu Liu, Yaxiong Wang, Yujiao Wu, Li Zhu, Zhedong Zheng"
date: 2025-09-04
pdf: "https://openreview.net/pdf?id=13bCB5VnDy"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 联合定位和自然语言解释的图像伪造检测
tldr: "现有伪造检测仅分类或像素级定位，缺乏语义解释。本文提出伪造归因报告生成任务，联合定位伪造区域（Where）并生成基于编辑过程的自然语言解释（Why）。构建了包含152,217个样本的大规模数据集MMTT，每个样本有真实掩码和人工标注文本描述。该工作为图像伪造检测提供了全面的可解释性分析。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有伪造检测缺乏对篡改操作的语义解释。
method: 提出伪造归因报告生成任务，利用MMTT数据集联合训练定位和文本生成。
result: 构建了大规模多模态数据集，实验证明了联合定位和解释的有效性。
conclusion: 该方法超越了传统取证，提供了对伪造的全面理解。
---

## Abstract
Existing facial forgery detection methods typically focus on binary classification or pixel-level localization, providing little semantic insight into the nature of the manipulation. To address this, we introduce Forgery Attribution Report Generation, a new multimodal task that jointly localizes forged regions ("Where") and generates natural language explanations grounded in the editing process ("Why"). This dual-focus approach goes beyond traditional forensics, providing a comprehensive understanding of the manipulation. To enable research in this domain, we present **M**ulti-**M**odal **T**amper **T**racing (**MMTT**), a large-scale dataset of 152,217 samples, each with a process-derived ground-truth mask and a human-authored textual description, ensuring high annotation precision and linguistic richness. We further propose ForgeryTalker, a unified end-to-end framework that integrates vision and language via a shared encoder (image encoder + Q-former) and dual decoders for mask and text generation, enabling coherent cross-modal reasoning. Experiments show that ForgeryTalker achieves competitive performance on both report generation and forgery localization subtasks, i.e., 59.3 CIDEr and 73.67 IoU, respectively, establishing a baseline for explainable multimedia forensics. Dataset and code will be released to foster future research.

---

## 论文详细总结（自动生成）

# 中文总结：图像伪造的Where和Why：联合定位与解释的基准

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有面部伪造检测方法通常仅关注二分类（真/假）或像素级定位，缺乏对篡改操作背后语义本质的深入解释。仅知道“哪里被篡改”不足以理解“为什么被篡改”以及“如何被篡改”。
- **研究动机**：推动多媒体取证从“二元判断”向“可解释性分析”演进，使伪造检测结果不仅可信，还具备可理解性。
- **整体含义**：本文首次提出“伪造归因报告生成”（Forgery Attribution Report Generation）这一多模态任务，联合实现伪造区域定位（Where）和基于编辑过程的自然语言解释（Why），为图像伪造检测提供了全新的综合性基准。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：构建统一框架，同时生成篡改区域的语义掩码和描述编辑过程的文本报告，实现视觉与语言的多模态协同推理。
- **关键技术细节**：
  - **数据集 MMTT**：大规模多模态篡改追踪数据集，包含152,217个样本，每个样本配有由编辑过程导出的真实掩码和人工编写的文本描述，保证注释精确性和语言多样性。
  - **模型 ForgeryTalker**：
    - 共享编码器：采用图像编码器 + Q-Former（Querying Transformer）结构，融合视觉与文本特征。
    - 双解码器：一个用于生成像素级篡改掩码（Where），另一个用于生成自然语言报告（Why）。
    - 端到端联合训练，使得两个任务相互促进，实现连贯的跨模态推理。
- **算法流程（文字说明）**：输入待检测图像 → 图像编码器提取特征 → Q-Former对齐视觉与语言表征 → 经共享编码后的特征分别送入掩码解码器和文本解码器 → 掩码解码器输出二值篡改区域；文本解码器输出描述篡改操作原因和过程的句子。

## 3. 实验设计
- **使用的数据集**：主要基于本文构建的 **MMTT** 数据集（152,217个样本）。文中未提及在其他公开数据集上的评估，可能因为该任务是新提出的。
- **Benchmark**：本文自身成为联合定位与解释任务的基准（baseline）。对比方法方面：由于任务是新增的，没有直接可比的其他方法。作者将ForgeryTalker自身的两个子任务结果作为基线：
  - 报告生成子任务：CIDEr分数为59.3。
  - 伪造定位子任务：IoU为73.67。
- **对比方法**：未明确列出具体对比方法，仅设定本框架作为baseline。

## 4. 资源与算力
- 论文中**未明确说明**使用的GPU型号、数量、训练时长等具体算力资源。仅提到数据集和代码将公开，但未披露训练成本。因此无法评估算力消耗情况。

## 5. 实验数量与充分性
- **实验数量**：仅展示了两个核心指标（CIDEr和IoU）的单一结果，未报告消融实验、不同组件的影响或在不同难度子集上的测试。整体实验数量较少。
- **充分性与公平性**：由于任务为新提出，缺乏其他方法作为对比基准，因此无法判断模型是否优于其他替代方案。实验设计仅演示了框架可行性，但未深入验证其鲁棒性、泛化性或与现有方法的公平比较。数据集内部可能存在的偏差（如伪造类型分布、语言风格差异）也未经细致分析。

## 6. 论文的主要结论与发现
- ForgeryTalker在伪造定位（73.67 IoU）和报告生成（59.3 CIDEr）两项子任务上取得了有竞争力的性能，验证了联合训练的有效性。
- 本文所构建的MMTT数据集（152,217样本）为可解释多媒体取证提供了大规模高质量资源。
- 该工作超越了传统仅分类或定位的伪造检测，提供对篡改的全面理解（既知道在哪里，也知道为什么）。

## 7. 优点
- **任务创新**：首次提出“伪造归因报告生成”任务，将检测从二元分类+像素定位提升到语义解释层面，极具前瞻性。
- **数据构建**：MMTT数据集人工编写文本描述，结合过程推导掩码，保证了标注精度和语言丰富度，是该领域的重要贡献。
- **模型设计**：端到端联合框架（共享编码+双解码）简洁优雅，有效利用跨模态信息。
- **开放资源**：承诺公开数据和代码，有利于后续研究复现和拓展。

## 8. 不足与局限
- **实验覆盖面窄**：仅在一个自制数据集上报告结果，缺少在多样化的公开伪造数据集（如FaceForensics++、DFDC等）上的测试，泛化能力未知。
- **缺乏消融分析**：未验证Q-Former、双解码器联合训练等组件各自的贡献，未分析掩码预测对文本生成的影响。
- **对比不足**：没有与其他方法（如单独的定位模型+单独的文本生成模型）比较，难以说明联合框架的优越性。
- **文本生成质量评估局限**：CIDEr指标虽通用，但未必能完全反映伪造解释的准确性和语义合理性，缺乏人工评估。
- **偏差风险**：MMTT数据集可能偏向特定伪造类型或语言风格，导致模型在真实场景下的适用性受限。
- **未报告计算开销**：没有提供训练时间、显存消耗等资源信息，不利于实际部署评估。

（完）
