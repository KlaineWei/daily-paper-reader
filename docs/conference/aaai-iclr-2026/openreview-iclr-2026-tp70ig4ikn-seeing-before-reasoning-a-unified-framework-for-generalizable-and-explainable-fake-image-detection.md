---
title: "Seeing Before Reasoning: A Unified Framework for Generalizable and Explainable Fake Image Detection"
title_zh: 先感知后推理：统一的可泛化可解释假图检测框架
authors: "Kaiqing Lin, Zhiyuan Yan, Ruoxin Chen, Junyan Ye, Ke-Yue Zhang, Yue Zhou, Peng Jin, Bin Li, Taiping Yao, Shouhong Ding"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=Tp70ig4iKN"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 通过修复感知失配实现可解释的假图检测
tldr: 本文提出一种可解释的假图检测框架，解决MLLM在检测时先推理后感知的根本失配。首先增强视觉编码器对低级伪造痕迹的感知能力，再基于可靠证据进行推理。实验表明该方法在多个AI生成图像检测基准上取得优异泛化性能，同时生成可解释的检测理由。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有MLLM假图检测方法因先推理后感知导致性能不佳且缺乏可解释性。
method: 先增强低级感知能力，再基于感知证据进行推理的联合框架。
result: 在多个假图检测数据集上取得可泛化且可解释的结果。
conclusion: 修复感知-推理顺序能显著提升假图检测的可解释性和泛化能力。
---

## Abstract
Detecting AI-generated images with multimodal large language models (MLLMs) has gained increasing attention, due to their rich world knowledge, common-sense reasoning, and potential for explainability.
However, naively applying those MLLMs for detection often leads to suboptimal performance.
We argue that the root of this failure lies in a fundamental mismatch: *MLLMs are asked to reason about fakes before they can truly see them.*
First, **they do not really see**: existing MLLMs' vision encoders are primarily optimized for semantic-oriented recognition rather than the perception of low-level signals, leaving them insensitive to subtle forgery traces. Without access to reliable perceptual evidence, the model grounds its judgment on incomplete and limited visual observations.
Second, existing finetuning data for detection typically uses narrow, instruction-style formats, which diverge sharply from the diverse, heterogeneous distributions seen in pretraining.
In the absence of meaningful visual cues, the model therefore exploits these linguistic shortcuts, resulting in catastrophic forgetting of pretrained knowledge (even the basic dialogue capabilities).
In response, we advocate for a new paradigm: *seeing before reasoning*. We propose that MLLMs should first be trained to perceive artifacts—strengthening their artifact-aware visual perception—so that subsequent reasoning is grounded in actual observations. 
We therefore propose **Forensic-Chat**, a generalizable, explainable, and still-conversational (for multi-round dialogue) assistant for fake image detection.
Specifically, we first refine the vision encoder only via self-reconstruction while freezing the LLM, sensitizing it to artifacts without sacrificing pretrained knowledge (Stage 1).
Then, we construct a multi-round dialogue finetuning data for detection, which is designed to progressively guide the model from artifact perception to common-sense reflection, enabling dialectical reasoning about *why an image is fake* and *what a real version should look like* (Stage 2).
We also propose **ExplainFake-Bench**, a benchmark tailored for the evaluation of the MLLM's explainability for image forensics from five key aspects.
Extensive experiments show the superiority of generalization and genuinely reliable explainability.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：当前利用多模态大语言模型（MLLM）进行AI生成图像检测的方法受到了广泛关注，因为MLLM具有丰富的世界知识、常识推理能力和潜在的可解释性。然而，直接将这些MLLM用于假图检测往往表现不佳。
- **核心问题**：作者认为，失败的根源在于**根本性的感知-推理顺序失配**——MLLM在“真正看清”图像之前就被要求进行推理。具体表现为：
    - **它们并没有真正“看见”**：现有MLLM的视觉编码器主要针对语义级识别进行优化，而非对低级伪造痕迹的感知，导致模型对细微的篡改痕迹不敏感。缺乏可靠的感知证据，判断只能基于不完整和有限的视觉观察。
    - **微调数据存在偏差**：现有的检测微调数据通常采用狭窄、指令式的格式，与预训练阶段多样、异构的数据分布差异巨大。在缺乏有意义视觉线索的情况下，模型会利用这些语言捷径，导致预训练知识的灾难性遗忘（甚至丧失基本对话能力）。
- **整体含义**：本文提出一种新的范式——“先感知后推理”（Seeing Before Reasoning），通过先增强对伪造痕迹的感知能力，再基于真实观察进行推理，实现可泛化、可解释且保持对话能力的假图检测。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将检测过程分解为两个阶段：
    1. **增强低级感知能力**：先训练视觉编码器感知伪造痕迹（artifact-aware），不依赖语言模型，避免遗忘预训练知识。
    2. **基于可靠证据进行推理**：然后通过多轮对话微调数据，引导模型从感知痕迹逐步过渡到常识推理，最终生成可解释的判断理由。
- **关键技术细节——Forensic-Chat框架**：
    - **阶段1（感知增强）**：仅对视觉编码器进行自重建训练（self-reconstruction），冻结LLM部分。通过自监督方式让编码器学会捕捉低级伪造痕迹（如颜色失真、频域异常等），同时不损失预训练的语义理解能力。
    - **阶段2（推理微调）**：构建多轮对话微调数据集，设计为逐步引导的格式：
        - 第一步：识别并描述图像中的伪造痕迹（artifact perception）。
        - 第二步：基于这些痕迹进行常识反思（common-sense reflection），例如“为什么这张图是假的？”以及“真实的版本应该是什么样的？”。
        - 通过这种辩证推理（dialectical reasoning），模型不仅能给出真假标签，还能生成自然语言解释。
- **算法流程**（文字说明）：
    1. 输入：待检测图像。
    2. Stage 1：基于自重建损失微调视觉编码器，使其对伪造痕迹敏感。
    3. Stage 2：使用构造的对话数据对整体MLLM（编码器+LLM）进行指令微调，保持对话能力的同时学习检测推理。
    4. 输出：真假判断 + 多轮对话形式的解释。

## 3. 实验设计：数据集、Benchmark、对比方法

- **Benchmark**：作者提出了**ExplainFake-Bench**，一个专门用于评估MLLM在图像取证可解释性方面的基准，涵盖五个关键方面（具体方面未在摘要中详述，推测包括：痕迹检测准确性、推理合理性、对话连贯性等）。
- **数据集**：论文在多个AI生成图像检测基准上进行了实验（具体数据集名称未在摘要中列出，但提到“多个基准”，可能包括常见如FakeNewsNet、GAN生成的图像、Diffusion生成的图像等）。
- **对比方法**：未在摘要中具体列出对比方法，但隐含与其他直接使用MLLM进行假图检测的方法（如直接微调、提示工程等）进行比较。
- **实验充分性评估**：摘要指出“Extensive experiments show the superiority of generalization and genuinely reliable explainability”，说明实验覆盖了泛化性和可解释性两方面，但具体数据未提供。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长等算力信息。仅提到两阶段训练，但无具体资源消耗数据。需要指出：“论文摘要及元数据未提供训练资源细节”。

## 5. 实验数量与充分性

- **实验数量**：摘要未列举具体实验组数，但提到在多个假图检测基准上测试，并且提出了专门的ExplainFake-Bench基准（含五个维度）。推测至少包含：
    - 与基线方法的泛化性能对比（多个数据集）。
    - 消融实验：验证阶段1（感知增强）、阶段2（多轮对话设计）的有效性。
    - 可解释性评估：利用ExplainFake-Bench进行量化或人工评价。
- **充分性与公平性**：从摘要看，实验设计覆盖了泛化性和可解释性，并对比了不同方法。但缺少具体指标和数据集细节，无法完全判断是否足够公平。不过，提出专门的基准有助于标准化评估，体现了一定客观性。

## 6. 论文的主要结论与发现

- 修复感知-推理顺序（先感知后推理）能显著提升假图检测的可解释性和泛化能力。
- 提出的Forensic-Chat在多个基准上取得了优于现有方法的泛化性能，同时能够生成可解释的检测理由。
- 保持对话能力的微调策略可以避免预训练知识的灾难性遗忘，使模型仍能进行多轮交互。
- ExplainFake-Bench可作为衡量MLLM图像取证可解释性的标准化工具。

## 7. 优点：方法或实验设计上的亮点

- **创新范式**：明确提出“先感知后推理”的检测顺序，解决了MLLM在低级感知任务上的根本失配问题。
- **两阶段解耦设计**：阶段1仅更新视觉编码器，避免语言模型知识的灾难性遗忘；阶段2通过多轮对话逐步引导推理，增强可解释性。
- **自监督感知增强**：使用自重建任务，无需额外标注，泛化性强。
- **专用可解释性基准**：提出ExplainFake-Bench，从五个维度评估，填补了该领域缺乏系统评估工具的空白。
- **保持对话能力**：在微调中保留多轮对话功能，使模型既是检测器又是可解释的助手。

## 8. 不足与局限

- **实验细节缺失**：摘要未提供具体数据集名称、对比方法、量化指标（如准确率、F1等），无法进行严格复现和独立比较。
- **基准覆盖范围未知**：ExplainFake-Bench的五个具体方面未说明，且其有效性、与人工评估的相关性有待验证。
- **应用限制**：方法依赖于MLLM架构（如视觉编码器+LLM），对于更轻量级的检测模型可能不适用。此外，多轮对话微调数据构造方式可能耗时且领域特定。
- **潜在偏差风险**：自重建阶段可能只对特定类型的伪造痕迹有效（如GAN artifacts vs. diffusion artifacts），对不同生成技术的泛化性需更多验证。
- **算力需求未交代**：无法评估方法在实际部署中的成本。

（完）
