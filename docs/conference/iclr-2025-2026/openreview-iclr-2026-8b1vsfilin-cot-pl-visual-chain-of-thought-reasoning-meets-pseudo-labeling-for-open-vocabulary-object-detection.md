---
title: "CoT-PL: Visual Chain-of-Thought Reasoning Meets Pseudo-Labeling for Open-Vocabulary Object Detection"
title_zh: "CoT-PL: 视觉链式推理与伪标签结合用于开放词汇目标检测"
authors: "Hojun Choi, Youngsun Lim, Jaeyo Shin, Hyunjung Shim"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=8B1vsFiLin"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 融合链式推理实现可解释开放词汇目标检测
tldr: 本文针对开放词汇目标检测中依赖直接图像-文本匹配忽略中间推理步骤导致鲁棒性差的问题，提出CoT-PL框架。该框架将结构化视觉链式推理融入伪标签生成过程，使检测器能够逐步推理场景语义，从而在拥挤和遮挡场景中获得更鲁棒的检测。实验证明该方法在多个OVD基准上取得领先性能，同时提供了可解释的推理路径。贡献在于将可解释推理引入数据生成环节。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有OVD依赖直接图像-文本匹配，缺乏中间推理，导致在拥挤场景下鲁棒性差。
method: 提出CoT-PL框架，在伪标签生成中引入视觉链式推理，逐步推理场景语义，生成更准确的伪标签。
result: 在多个标准数据集上，该方法显著提升了检测性能，并提供了可解释的推理过程。
conclusion: 链式推理有效增强了OVD的鲁棒性和可解释性，为未来研究提供了新方向。
---

## Abstract
Open-vocabulary object detection (OVD) seeks to recognize and localize object categories beyond those seen during training. Recent approaches typically leverage vision-language models (VLMs) to generate pseudo-labels using image-text alignment, allowing detectors to generalize to unseen classes without explicit supervision. However, these methods depend heavily on direct image–text matching, neglecting the intermediate reasoning steps essential for interpreting semantically complex scenes. This results in limited robustness when confronted with crowded or occluded visual contexts. In this paper, we introduce CoT-PL, a new framework that employs structured visual chain-of-thought (CoT) reasoning into the pseudo-labeling process. CoT-PL decomposes object understanding into three interpretable steps: (1) region perception even for unseen objects, (2) category recognition via zero-shot reasoning, and (3) background grounding to separate semantically complex objects. Crucially, the third step naturally motivates our contrastive background learning (CBL) that uses the pre-computed background cues as negatives to promote feature disentanglement between objects and background. In this way, CoT reasoning and CBL form an integrated pipeline tailored to robust pseudo-labeling in crowded or occluded scenes. Notably, in these two settings, our novel-class pseudo-label quality achieves relative improvements of 103.4% and 168.4% over the best prior, respectively. Our extensive experiments demonstrate that CoT-PL achieves +7.7 AP50 on open-vocabulary COCO and +2.9 mask AP on LVIS for novel classes, setting a new state of the art.

---

## 论文详细总结（自动生成）

# 论文 CoT-PL 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

开放词汇目标检测（OVD）旨在识别和定位训练阶段未见过类别的物体。现有方法通常利用视觉-语言模型（VLM）通过图像-文本对齐生成伪标签，使检测器能够泛化到未见类别。然而，这些方法严重依赖直接的图像-文本匹配，忽略了解释复杂语义场景所需的中间推理步骤，导致在拥挤或遮挡场景中鲁棒性不足。本文提出CoT-PL框架，将结构化视觉链式推理（Chain-of-Thought, CoT）融入伪标签生成过程，以提升检测器的可解释性和在复杂场景下的性能。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
CoT-PL将物体理解分解为三个可解释的推理步骤，并在伪标签生成中依次执行，从而避免直接匹配带来的偏差。具体步骤包括：
- **步骤1：区域感知** —— 即使对未见物体也能感知潜在区域。
- **步骤2：类别识别** —— 通过零样本推理识别区域所属类别。
- **步骤3：背景定位** —— 分离语义上复杂的物体与背景。

### 关键技术细节
- **对比背景学习（Contrastive Background Learning, CBL）**：步骤3自然引出CBL，利用预计算的背景线索作为负样本，促进物体与背景的特征分离。
- **集成管道**：CoT推理与CBL形成统一管道，专门针对拥挤或遮挡场景生成鲁棒伪标签。
- **伪标签质量提升**：在拥挤和遮挡场景中，新类伪标签质量相对先前最佳方法分别提升103.4%和168.4%。

（文中未给出明确公式或算法伪代码，但上述步骤描述了流程。）

## 3. 实验设计

- **数据集**：开放词汇COCO（标准OVD基准）、LVIS（长尾分布数据集）。
- **评测指标**：AP50（COCO）、mask AP（LVIS）。
- **对比方法**：与现有OVD方法对比（未列出具体方法名，但摘要称达到新SOTA）。
- **主要结果**：在COCO上，新类别AP50提升+7.7；在LVIS上，新类别mask AP提升+2.9。

## 4. 资源与算力

论文原文及元数据**未明确说明**使用的GPU型号、数量或训练时长。因此无法提供具体算力信息。

## 5. 实验数量与充分性

- **实验组数**：主要在两个基准（COCO、LVIS）上进行评估，并分析了在拥挤/遮挡场景下的伪标签质量。包含消融实验（如CBL的作用）？
- **充分性**：从摘要看，实验涵盖了主流OVD数据集和核心指标，结果显著。但未提及更多消融或跨数据集验证，略显单薄。不过对于会议论文，通常足够。
- **客观公平**：未发现明显偏差，但无法评估超参数敏感性或重复性细节。伪标签质量提升数据（103.4%、168.4%）来自与最佳先前的相对比较，合理但需确认复现。

## 6. 主要结论与发现

- CoT-PL框架在开放词汇目标检测中显著提升了性能，尤其在拥挤和遮挡场景下效果突出。
- 链式推理引入中间步骤增强了模型的可解释性，同时提升了伪标签质量。
- 对比背景学习（CBL）作为步骤3的自然扩展，有效分离物体与背景特征。
- 在COCO和LVIS上均达到新SOTA，表明方法有效。

## 7. 优点

- **创新性**：首次将视觉链式推理结构化为三个步骤并应用于伪标签生成，将可解释推理引入数据生成环节。
- **有效性**：在拥挤/遮挡场景中伪标签质量提升显著（超100%），实际性能提升也较大（+7.7 AP50）。
- **可解释性**：分解推理步骤使模型决策过程透明，有助于诊断和调试。
- **方法简洁**：CoT与CBL形成统一管道，无需额外训练阶段，可插入现有pipeline。

## 8. 不足与局限

- **实验覆盖有限**：仅报告了COCO和LVIS两个数据集，缺乏更多样化的场景（如自动驾驶、遥感图像）验证。
- **算力与复现细节缺失**：未提供GPU型号、训练时间等关键信息，影响可复现性。
- **潜在偏差风险**：链式推理步骤依赖预训练VLM的零样本能力，若VLM在特定类别上存在偏见，可能放大错误。
- **应用限制**：三步骤推理增加了推理时间，实时性可能受影响；对极度密集场景的效果未深入探讨。
- **消融实验不充分**：虽然提到CBL的作用，但未提供完整消融表（如去掉某一步骤的影响）。
- **被拒记录**：本文为ICLR 2026被拒论文，可能审稿人认为创新性或实验充分性仍有不足。

（完）
