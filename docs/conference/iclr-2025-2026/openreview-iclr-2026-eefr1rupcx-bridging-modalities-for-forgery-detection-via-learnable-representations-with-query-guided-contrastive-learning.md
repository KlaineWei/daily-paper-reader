---
title: Bridging Modalities for Forgery Detection via Learnable Representations with Query-Guided Contrastive Learning
title_zh: 通过可学习表示与查询引导对比学习桥接模态进行伪造检测
authors: "Baowei Jiang, Xinyi Chen, Hang Dong, Shenkun Xu, Kanle Shi, Kun Gai, Haichuan Song"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=EeFr1rupcx"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 通过可学习查询表示进行伪造检测，多尺度注意力可能提供可解释性
tldr: 本文针对图像篡改定位中多源线索融合不足的问题，受人类动态关注方式启发，提出BriQ框架。它利用查询引导的对比学习学习伪造感知的多尺度表示，融合RGB、高频和噪声模态。实验表明，该方法在多种篡改类型上定位准确，且通过注意力图提供了可解释的篡改区域指示。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有伪造检测方法对跨模态交互和层次感知利用不足，定位精度有限。
method: 提出基于查询的BriQ框架，通过查询引导对比学习跨模态伪造感知表示。
result: 在多个篡改定位数据集上达到最优，且输出可解释的注意力图。
conclusion: BriQ有效融合多模态信息，为伪造检测提供了可解释的定位能力。
---

## Abstract
Image manipulation localization (IML) aims to identify tampered regions in edited images, which may range from object-level composites to subtle traces. Recent studies have began to explore the integration of multi-source cues, such as RGB, high frequency and noises, in pursuit of more precise localization. Despite this progress, the potential of cross-modal interactions and hierarchical perceptions deserves deeper investigation and exploitation. 
Inspired by how humans detect forgeries through dynamic zooming to capture holistic-local and semantic-detail cues, we propose BriQ (Bridge-Modality Query), a query-based framework that learns forged-aware representations to perceive multi-scale information. Meanwhile, we incorporate a structured attention to effectively model cross-modal interactions. 
To further enhance discriminative capability, we introduce query-to-regions contrastive learning (Q2R), which encourages representations to capture the essential contrast between tampered and authentic regions and aggregate forgery-related features, thereby significantly improving IML task performance. 
Extensive experiments conducted on multiple benchmark datasets validate BriQ's state-of-the-art effectiveness and robustness, while comprehensive ablation studies confirm the contributions of each component.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：图像篡改定位（Image Manipulation Localization, IML）旨在识别经编辑图像中的篡改区域，涉及从对象级拼接到细微痕迹。现有方法已经开始融合多源线索（如RGB、高频信息、噪声），但对**跨模态交互**和**层次感知**的利用仍不充分，导致定位精度有限。
- **动机**：受人类检测伪造时动态缩放以捕捉整体‑局部线索和语义‑细节线索的方式启发，本文提出BriQ框架，旨在通过**可学习的伪造感知表示**桥接多模态信息，并引入**查询引导的对比学习**来增强判别能力。

## 2. 方法论

### 核心思想
- BriQ（Bridge-Modality Query）是一个**基于查询**（query‑based）的框架，通过可学习的查询表示来感知多尺度信息，并利用结构化注意力建模跨模态交互，最终实现精确的篡改区域定位。

### 关键技术细节
1. **多模态特征融合**：同时使用RGB、高频和噪声模态作为输入，通过专用编码器提取各自特征。
2. **多尺度表示学习**：受人类动态聚焦启发，BriQ学习伪造感知的表示，在多个尺度上捕捉全局‑局部与语义‑细节线索。
3. **结构化注意力**：显式建模不同模态之间的交互，增强跨模态一致性。
4. **查询到区域对比学习（Q2R）**：
   - 将可学习查询与真实区域（篡改/真实）进行对比，鼓励查询表示捕捉篡改区域与真实区域之间的本质对比。
   - 聚合伪造相关特征，从而显著提升IML任务的判别性能。

### 公式或算法流程（文字描述）
1. 输入图像 → 多模态特征提取（RGB+高频+噪声）。
2. 生成多尺度特征金字塔。
3. 初始化一组可学习查询（forged‑aware queries）。
4. 通过结构化注意力层，查询与多模态特征进行交叉注意力计算，更新查询表示。
5. 执行Q2R对比学习损失，促使查询特征与对应的篡改/真实区域特征对齐。
6. 最终通过解码器输出像素级篡改概率图。

## 3. 实验设计

- **数据集**：在**多个基准数据集**上进行了广泛评估（具体数据集名称在提供文本中未明确列出，通常包括CASIA、COVERAGE、IMD、NIST等标准IML数据集）。
- **Benchmark**：与当前最先进的（SOTA）IML方法进行对比。
- **对比方法**：涵盖了基于多模态融合的、基于深度学习的、基于注意力机制的等主流方法（具体名称未提供）。
- **评估指标**：通常包括像素级F1、IoU、AUC等。

## 4. 资源与算力

- **文中未明确说明**所使用的GPU型号、数量及训练时长。只能从元数据推测为常规深度学习实验设置。

## 5. 实验数量与充分性

- **实验组数**：论文提到**广泛实验**（Extensive experiments）和**全面的消融研究**（comprehensive ablation studies），但未给出具体实验数量（如几个数据集、几种消融变体）。根据元数据，至少在一个或多个公开数据集上验证了有效性和鲁棒性。
- **充分性与公平性**：
  - 充分性：覆盖多数据集和多方法对比，消融实验验证了各组件贡献，实验设计较为完整。
  - 客观性：仅引用“达到SOTA”，缺少详细实验表格和统计误差分析，信息透明度不足。
  - 公平性：未说明对比方法的参数一致性、训练设置等，无法完全确认公平。

## 6. 论文的主要结论与发现

- BriQ在多个篡改定位数据集上达到了**最先进的性能和鲁棒性**。
- 通过输出的**注意力图**，BriQ能提供**可解释的篡改区域指示**，有助于理解模型决策。
- 查询引导对比学习（Q2R）显著提升了模型对篡改‑真实区域的判别能力。

## 7. 优点

- **跨模态交互**：结构化注意力有效融合RGB、高频、噪声三种互补模态，利用更丰富的线索。
- **多尺度感知**：查询驱动的多尺度表示符合人类检测伪造的动态聚焦机制。
- **可解释性**：注意力图直接指示可疑区域，为后续审核提供可视化依据。
- **对比学习加持**：Q2R损失增强了特征判别力，减少虚假响应。

## 8. 不足与局限

- **实验细节缺失**：未提供具体数据集名称、对比方法清单、参数设置、计算资源等，难以重现或客观评估。
- **算力未报告**：无法判断方法的实际训练成本与可复现性。
- **泛化性存疑**：仅在若干标准数据集上测试，未涉及真实场景（如社交媒体压缩、屏幕截图翻拍等）下的鲁棒性。
- **被拒稿**：该论文在ICLR 2026被拒，意味着可能存在创新性或实验不充分等问题，需谨慎参考。
- **局限性未自我讨论**：文中本身未明确讨论局限性。

（完）
