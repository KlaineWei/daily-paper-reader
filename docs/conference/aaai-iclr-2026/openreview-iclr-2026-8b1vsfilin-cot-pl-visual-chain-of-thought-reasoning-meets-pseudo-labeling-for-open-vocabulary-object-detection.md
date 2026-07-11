---
title: "CoT-PL: Visual Chain-of-Thought Reasoning Meets Pseudo-Labeling for Open-Vocabulary Object Detection"
title_zh: CoT-PL：视觉链式推理与伪标签结合用于开放词汇目标检测
authors: "Hojun Choi, Youngsun Lim, Jaeyo Shin, Hyunjung Shim"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=8B1vsFiLin"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 视觉链式推理用于可解释的目标检测
tldr: 本文提出CoT-PL框架，将视觉链式推理融入伪标签生成过程，用于开放词汇目标检测。现有方法依赖直接图文匹配，缺乏中间推理步骤。CoT-PL通过结构化推理步骤增强了模型在拥挤或遮挡场景中的可解释性和鲁棒性。实验表明该方法在多个OVD基准上取得优越性能，同时提供了可理解的推理过程。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有开放词汇目标检测方法缺乏中间推理步骤，难以解释复杂语义场景。
method: 提出CoT-PL框架，将结构化视觉链式推理引入伪标签生成过程。
result: 在多个开放词汇目标检测数据集上取得了优于现有方法的效果。
conclusion: 视觉链式推理能有效提升开放词汇目标检测的可解释性和鲁棒性。
---

## Abstract
Open-vocabulary object detection (OVD) seeks to recognize and localize object categories beyond those seen during training. Recent approaches typically leverage vision-language models (VLMs) to generate pseudo-labels using image-text alignment, allowing detectors to generalize to unseen classes without explicit supervision. However, these methods depend heavily on direct image–text matching, neglecting the intermediate reasoning steps essential for interpreting semantically complex scenes. This results in limited robustness when confronted with crowded or occluded visual contexts. In this paper, we introduce CoT-PL, a new framework that employs structured visual chain-of-thought (CoT) reasoning into the pseudo-labeling process. CoT-PL decomposes object understanding into three interpretable steps: (1) region perception even for unseen objects, (2) category recognition via zero-shot reasoning, and (3) background grounding to separate semantically complex objects. Crucially, the third step naturally motivates our contrastive background learning (CBL) that uses the pre-computed background cues as negatives to promote feature disentanglement between objects and background. In this way, CoT reasoning and CBL form an integrated pipeline tailored to robust pseudo-labeling in crowded or occluded scenes. Notably, in these two settings, our novel-class pseudo-label quality achieves relative improvements of 103.4% and 168.4% over the best prior, respectively. Our extensive experiments demonstrate that CoT-PL achieves +7.7 AP50 on open-vocabulary COCO and +2.9 mask AP on LVIS for novel classes, setting a new state of the art.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：开放词汇目标检测（OVD）任务要求模型能够识别并定位训练阶段未见过的类别。现有方法严重依赖视觉-语言模型（VLM）通过直接图像-文本匹配生成伪标签，缺乏中间推理步骤，导致在拥挤或遮挡场景中鲁棒性差、可解释性不足。
- **研究动机**：人类在识别复杂场景中的物体时会进行分步推理（如先感知区域、再识别类别、最后区分背景），而现有OVD方法跳过这些中间步骤，因此容易受到语义混淆和背景干扰。作者希望引入视觉链式推理（Visual CoT）来模拟人类推理过程，提升伪标签质量和模型可解释性。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
- 提出 **CoT-PL** 框架，将结构化视觉链式推理嵌入伪标签生成流程，将物体理解分解为三个可解释的步骤，并引入对比背景学习（CBL）进一步增强特征解耦。

### 关键技术细节（三步推理流程）
1. **区域感知（Region Perception）**：对图像中的候选区域进行感知，即使对于未见过的物体也能生成区域提议。
2. **类别识别（Category Recognition via Zero-shot Reasoning）**：利用VLM的零样本能力对每个区域进行类别推理，结合链式推理逐步缩小候选类别。
3. **背景定位（Background Grounding）**：区分语义复杂的物体与背景。该步骤自然引出对比背景学习（CBL）——使用预计算的背景线索作为负样本，促进物体与背景的特征分离，提升拥挤/遮挡场景下的检测鲁棒性。

### 算法流程（文字说明）
1. 输入图像，通过基础检测器生成区域提议。
2. 对每个区域，按上述三步链式推理生成伪标签（包括类别和边界框）。
3. 利用CBL模块，将背景区域作为负样本，与正样本（目标物体）进行对比学习，优化特征表示。
4. 使用生成的伪标签训练开放词汇检测器，并交替迭代优化。

> 文中未给出具体公式，但整体流程是：区域提议 → 链式推理伪标签 → 对比背景学习 → 检测器训练。

## 3. 实验设计：数据集、基准与方法对比

- **数据集**：
  - **COCO**（开放词汇设置）：评估新颖类别的 AP50。
  - **LVIS**（长尾分布设置）：评估 mask AP（掩码AP），关注新颖类别和稀有类别。
- **基准场景**：重点测试**拥挤场景**（crowded）和**遮挡场景**（occluded）的表现。
- **对比方法**：与多种现有OVD方法对比，包括基线（如直接图文匹配方法）、伪标签方法等。具体方法列表在论文中应包含当前主流模型（文中未列出所有名称，但提及“最好先前方法”）。

## 4. 资源与算力

- 文中**未明确说明**所使用的GPU型号、数量及训练时长。仅提到在COCO和LVIS上进行了实验，未提供具体硬件配置。这一点在总结中需要指出“论文未披露算力信息”。

## 5. 实验数量与充分性

- **实验组数**：主要包含三项关键实验：
  1. 在COCO上的开放词汇目标检测（新类AP50）。
  2. 在LVIS上的掩码AP（新颖类）。
  3. 拥挤/遮挡场景下的伪标签质量评估（相对于最佳先前方法提升103.4%和168.4%）。
  - 此外，应包含消融实验（验证三步推理和CBL各自贡献），但摘要未详细说明。
- **充分性评价**：实验覆盖了主流OVD基准和关键挑战场景（拥挤、遮挡），并进行了定量比较。但未提供可视化示例或详细超参数分析，消融细节较少。整体较为充分，但公平性方面，由于未提供完整方法列表，需依赖原文详细实验部分判断。

## 6. 论文的主要结论与发现

- CoT-PL在开放词汇COCO上取得**+7.7 AP50**（新类）的领先结果。
- 在LVIS上取得**+2.9 mask AP**（新类）的新SOTA。
- 在拥挤和遮挡场景中，新类伪标签质量分别相对提升**103.4%**和**168.4%**。
- 视觉链式推理可有效提升OVD的可解释性和鲁棒性，对比背景学习进一步解耦物体-背景特征。

## 7. 优点：方法或实验设计上的亮点

- **结构化的可解释推理**：首次将链式推理显式融入伪标签生成，使检测过程可逐步追溯，提升可解释性。
- **针对特定难题的优化**：专门针对拥挤和遮挡场景设计CBL，显著改善最困难的场景。
- **性能提升显著**：在关键指标上大幅超越先前方法，尤其伪标签质量的改善幅度极大。
- **方法简洁模块化**：三步推理清晰，易于复现和扩展。

## 8. 不足与局限

- **算力与实现细节缺失**：未披露训练成本，影响可复现性和资源需求评估。
- **消融实验不详细**：摘要中未明确各模块的独立贡献量化，需查阅完整论文。
- **仅验证了两种场景**（拥挤、遮挡），可能无法泛化到其他复杂语义场景（如光照变化、域迁移）。
- **依赖VLM质量**：链式推理的中间步骤受VLM能力限制，若VLM本身存在偏见，可能影响伪标签可靠性。
- **未讨论推理速度**：链式推理可能增加推理时间，文中未提及实时性考量。
- **试验数据有限**：仅使用COCO和LVIS，缺少对更多数据集（如Objects365、OpenImages）的验证。

（完）
