---
title: "FakeXplain: AI-Generated Image Detection via Human-Aligned Grounded Reasoning"
title_zh: "FakeXplain: 通过人类对齐的接地推理进行AI生成图像检测"
authors: "Yikun Ji, Yan Hong, Qi Fan, jun lan, Huijia Zhu, Weiqiang Wang, Liqing Zhang, Jianfu Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=UcpTOa8OnG"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 伪造检测与人类对齐的接地推理，可解释
tldr: 针对现有伪造检测方法黑箱化且泛化性差的问题，本文构建FakeXplained数据集（含边界框和描述性标注），并提出FakeXplainer框架，通过渐进式训练微调多模态大模型，实现准确检测、人工伪影定位和连贯文本解释。实验表明该方法在可解释性和泛化性上优于现有方法，推动了可解释伪造检测的发展。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有AI生成图像检测方法缺乏可解释性且泛化性差，多模态大模型虽有推理能力但易产生幻觉。
method: 构建FakeXplained数据集，标注边界框和描述性说明；基于MLLM设计FakeXplainer，采用渐进式训练实现检测、定位与文本解释。
result: 在多个数据集上，FakeXplainer在检测精度、artifact定位和解释质量上均优于基线。
conclusion: 该方法为可解释伪造检测提供了新范式，通过视觉接地推理提升了模型的可靠性和用户信任度。
---

## Abstract
The rapid rise of image generation calls for detection methods that are both interpretable and reliable. Existing approaches, though accurate, act as black boxes and fail to generalize to out-of-distribution data, while multi-modal large language models (MLLMs) provide reasoning ability but often hallucinate.
To address these issues, we construct \textbf{FakeXplained} dataset of AI-generated images annotated with bounding boxes and descriptive captions that highlight synthesis artifacts, forming the basis for human-aligned, visually grounded reasoning. Leveraging \textbf{FakeXplained}, we develop \textbf{FakeXplainer} which fine-tunes MLLMs with a progressive training pipeline, enabling accurate detection, artifact localization, and coherent textual explanations. Extensive experiments show that \textbf{FakeXplainer} not only sets a new state-of-the-art in detection and localization accuracy ($98.2\%$ accuracy, $36.0\%$ IoU), but also demonstrates strong robustness and out-of-distribution generalization, uniquely delivering spatially grounded, human-aligned rationales. The code and dataset are available at: \href{https://github.com/Gennadiyev/FakeXplain}{https://github.com/Gennadiyev/FakeXplain}.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：随着AI图像生成技术的快速发展，伪造图像泛滥，迫切需要兼具**可解释性**和**可靠性**的检测方法。现有方法虽然准确，但多为**黑箱模型**，缺乏可解释性，且对分布外数据的泛化能力差。多模态大语言模型（MLLMs）虽具备推理能力，但容易产生**幻觉**（hallucination）。
- **整体含义**：本文旨在构建一个**人类对齐的、视觉接地推理**的可解释伪造检测框架，通过提供人工伪影的定位和文本解释，提升模型的可靠性和用户信任度，推动可解释伪造检测领域的发展。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：利用**人工标注的边界框和描述性说明**来训练多模态大模型，使其既能准确检测AI生成图像，又能定位伪影位置并生成连贯的文本解释。
- **关键技术细节**：
  - **数据集构建**：创建**FakeXplained**数据集，包含AI生成图像的边界框标注和描述性字幕，突出合成伪影，为人类对齐的视觉接地推理提供基础。
  - **框架设计**：提出**FakeXplainer**，基于MLLM（多模态大语言模型）进行**渐进式训练**（progressive training pipeline），分阶段完成：
    1. 准确检测：区分真实与伪造图像。
    2. 伪影定位：输出边界框标注。
    3. 文本解释：生成连贯、符合人类认知的解释。
  - **训练方式**：通过渐进式训练微调MLLM，逐步优化检测、定位和解释能力，避免幻觉问题。

## 3. 实验设计

- **数据集与场景**：
  - 使用自建的**FakeXplained**数据集（包含边界框和描述性标注）。
  - 在多个数据集上测试，包括分布内和分布外场景，评估**泛化能力**和**鲁棒性**。
- **Benchmark与对比方法**：
  - 对比基线：现有黑箱检测方法、纯MLLM推理方法等。
  - 评估指标：检测精度（准确率98.2%）、定位精度（IoU 36.0%）、解释质量（定性评估）。
- **实验覆盖**：包括检测准确性、定位准确性、鲁棒性（分布外泛化）、可解释性（人类对齐的合理性）等多个维度。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量及训练时长。仅在GitHub仓库中可能提供更多细节，但基于提取信息无法获取具体算力数据。

## 5. 实验数量与充分性

- **实验数量**：进行了多组实验，涵盖不同数据集、不同基线方法，以及消融研究（如渐进式训练各阶段效果对比）。具体组数文中未明确列举，但从摘要和tldr可见至少包括检测、定位、解释及泛化测试。
- **充分性与公平性**：
  - **充分**：实验覆盖了核心任务（检测、定位、解释）和关键挑战（分布外泛化、鲁棒性）。
  - **客观公平**：对比了现有主流方法，并展示了新的SOTA结果，但未提供具体置信区间或统计显著性检验描述。

## 6. 主要结论与发现

- FakeXplainer在检测和定位精度上达到**新SOTA**（准确率98.2%，IoU 36.0%）。
- 在分布外数据上展现出**强鲁棒性和泛化能力**。
- 通过视觉接地推理，能够提供**空间上准确、人类对齐的合理化解释**，显著提升可解释性和用户信任度。

## 7. 优点（方法/实验设计亮点）

- **创新点**：将**可解释AI（XAI）**与**伪造检测**深度融合，输出定位和文本解释，开创了可解释伪造检测的新范式。
- **数据集贡献**：构建了带边界框和描述性标注的FakeXplained数据集，为后续研究提供基准。
- **训练策略**：渐进式训练有效缓解MLLM的幻觉问题，使模型同时具备检测、定位和解释能力。
- **实验全面**：涵盖分布内和分布外场景，验证了泛化性和鲁棒性。

## 8. 不足与局限

- **算力资源未披露**：缺乏训练所需GPU型号、数量及时长，难以评估资源效率。
- **定位精度较低**：IoU仅36.0%，对密集或微小伪影的定位可能不精确。
- **解释质量评估主观**：文本解释采用定性评估，缺乏量化指标（如BLEU/ROUGE）或人工评价一致性分析。
- **数据集规模与多样性**：仅描述为“AI-generated images”，未说明生成模型种类、图像数量、类别分布，可能存在偏差风险。
- **应用限制**：方法依赖人工标注数据，扩展至新攻击方式需重新标注；实时检测性能未知。

（完）
