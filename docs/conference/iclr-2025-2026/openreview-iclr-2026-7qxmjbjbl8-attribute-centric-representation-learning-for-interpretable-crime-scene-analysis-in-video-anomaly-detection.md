---
title: Attribute-Centric Representation Learning for Interpretable Crime Scene Analysis in Video Anomaly Detection
title_zh: 面向属性中心表示学习的可解释视频异常检测犯罪现场分析
authors: "Akshat Rampuria, Kushagra Khare, Kamalakar Vijay Thakare, Debi Dogra, Heeseung Choi, Hyungjoo Jung, Ig-Jae Kim"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=7qXmJbjbl8"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 通过属性中心学习实现可解释视频异常检测
tldr: 针对视频异常检测中缺乏属性级标注导致可解释性不足的问题，本文提出属性中心学习框架，显式建模犯罪相关属性。通过扩展UCA数据集添加150万属性标注，该方法在可解释异常检测任务上取得显著提升。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有视频异常检测数据集缺乏属性级标注，限制了对异常事件的可解释分析。
method: 提出属性中心学习框架，利用扩展的细粒度属性标注来条件化视频表示。
result: 在扩展数据集上，该方法在可解释性和检测性能上均达到领先水平。
conclusion: 属性级别的监督能有效提升视频异常检测的可解释性和准确性。
---

## Abstract
Automatic crime scene analysis is an important application area for representation learning in Video Anomaly Detection (VAD). Effective interpretation of anomalous events requires models to learn rich, disentangled representations that capture fine-grained, crime-relevant attributes. However, widely used VAD datasets (e.g., UCA, CUVA) primarily offer coarse event-level labels and they lack attribute-level supervision often needed for modeling crime-specific behaviors. To bridge this gap, we propose an attribute-centric learning framework that explicitly conditions video representations on crime-causing attributes. We extend the UCA dataset with over 1.5M new attribute-centric annotations generated using carefully designed prompts and LLMs. These annotations enable supervised fine-tuning of a curated CLIP-based model, leading to more discriminative, attribute-aware video representations, and precise event captions. An LLM-based summarizer then distills these captions into context-rich explanations, facilitating interpretable scene understanding. Our approach answers three core questions in crime scene analysis: \textbf{What? When? How?} Extensive experiments show that the proposed representation learning framework yields significant improvements ($\approx 20\%\uparrow$) in attribute-centric crime classification accuracy and ($\approx 6.4\%\uparrow$) according to MMEval scores over the baselines. We further analyze and mitigate biases in MMEval to ensure robustness and fair evaluation. These results highlight the importance of attribute-conditioned representation learning for interpretable and reliable VAD.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：视频异常检测（VAD）在自动犯罪现场分析中具有重要应用，但现有主流数据集（如UCA、CUVA）仅提供粗粒度的**事件级标签**，缺乏**属性级监督**，导致模型无法学习细粒度、犯罪相关的属性（如“持刀”、“奔跑”等），从而难以实现可解释的异常事件分析。
- **整体意义**：本文旨在通过**属性中心表示学习**，显式地以犯罪相关属性为条件来建模视频表征，从而回答犯罪现场分析的三个核心问题：**发生什么（What）？何时发生（When）？如何发生（How）？**，提升VAD的可解释性和准确性。

## 2. 论文提出的方法论

### 核心思想
- 提出**属性中心学习框架**，将视频表示显式地**条件化**于犯罪相关属性（如物体、动作、环境等），通过属性级监督学习更**区分性、属性感知**的视频特征。
- 利用大语言模型（LLM）和精心设计的提示生成大量属性级标注，扩展数据集，并基于CLIP模型进行微调，最终用LLM摘要器生成上下文丰富的解释。

### 关键技术细节
1. **数据集扩展**：在UCA数据集基础上，使用设计好的提示和LLM（如GPT）生成超过**150万**条新的属性中心标注，覆盖犯罪相关属性。
2. **模型微调**：基于**CLIP**模型，利用扩展的属性标注进行**监督微调**，使模型学习属性感知的视频表示。
3. **事件描述生成**：微调后的模型输出更精确的事件描述（captions）。
4. **LLM摘要器**：将事件描述蒸馏为上下文丰富的解释，实现可理解的场景分析。

### 公式/算法流程（文字说明）
- 输入视频片段 → 通过CLIP编码得到初始特征 → 结合属性条件（属性嵌入）进行条件化表示学习 → 输出属性感知特征 → 用于分类/描述 → LLM生成最终解释。

## 3. 实验设计

- **数据集**：主要使用**UCA**（UCF Crime Analysis）数据集，并进行了**属性级扩展**。
- **Benchmark**：在扩展后的UCA数据集上进行评估，对比基线方法。
- **对比方法**：未明确列出具体基线名称，但提到与现有VAD方法（可能包括原始UCA方法、仅事件级监督的方法等）对比。
- **任务**：属性中心犯罪分类准确率、事件描述质量（MMEval分数）。

## 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。
- 仅提到基于CLIP模型进行微调，通常需要单卡或多卡GPU（如V100/A100），但文中无具体披露。

## 5. 实验数量与充分性

- **实验组数**：至少包括：
  - 属性中心犯罪分类准确率对比（约20%提升）。
  - 事件描述质量MMEval分数对比（约6.4%提升）。
  - 对MMEval中的偏差进行了分析和缓解（消融或分析实验）。
- **充分性评估**：
  - **较充分**：在主要指标上进行了量化对比，且额外分析了偏差问题。
  - **不足**：未在多个数据集（如CUVA）上进行验证，仅局限在UCA扩展版本；未提供消融实验细节（如去掉属性条件、不同生成策略等）。

## 6. 主要结论与发现

- **属性级监督**能显著提升视频异常检测的可解释性和准确性。
- 属性中心学习框架在**属性分类准确率**上提升约20%，在**MMEval分数**上提升约6.4%。
- 通过分析并缓解MMEval中的偏差，确保了评估的鲁棒性和公平性。
- 证明了属性条件化表示学习对于可解释、可靠VAD的重要性。

## 7. 优点

- **创新性**：首次将属性级标注引入VAD，解决可解释性瓶颈。
- **数据扩展**：利用LLM高效生成150万属性标注，成本可控。
- **可解释性**：通过“What/When/How”框架直观展示异常事件解释。
- **效果显著**：在核心指标上获得大幅提升。

## 8. 不足与局限

- **数据集单一**：仅基于UCA扩展，未在CUVA等其他数据集验证，泛化性存疑。
- **算力披露缺失**：无法评估方法复现难度和资源需求。
- **偏差分析有限**：虽然分析了MMEval偏差，但未说明是否在其他评估指标存在类似问题。
- **依赖LLM**：使用LLM生成标注和摘要，可能引入噪声或偏见，且推理开销较高。
- **实验完整性**：缺少详细的消融实验（如不同属性粒度、不同LLM影响等），对比方法不够具体。

（完）
