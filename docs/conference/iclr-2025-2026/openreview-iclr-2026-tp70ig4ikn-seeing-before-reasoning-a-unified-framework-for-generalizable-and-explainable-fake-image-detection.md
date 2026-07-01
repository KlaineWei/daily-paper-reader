---
title: "Seeing Before Reasoning: A Unified Framework for Generalizable and Explainable Fake Image Detection"
title_zh: 见而后思：通用可解释虚假图像检测的统一框架
authors: "Kaiqing Lin, Zhiyuan Yan, Ruoxin Chen, Junyan Ye, Ke-Yue Zhang, Yue Zhou, Peng Jin, Bin Li, Taiping Yao, Shouhong Ding"
date: 2025-09-01
pdf: "https://openreview.net/pdf?id=Tp70ig4iKN"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 直接解决可解释虚假图像检测
tldr: 本文针对多模态大模型在虚假图像检测中感知不足导致推理无效的问题，提出了一个统一的框架，通过增强视觉编码器对低级痕迹的感知能力，并结合结构化推理步骤，实现了可解释的虚假图像检测。实验表明该方法在多种生成模型上具有优越的泛化性和可解释性。贡献在于弥合了感知与推理之间的鸿沟，推动了可解释AI在媒体取证中的应用。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有MLLM在虚假图像检测中因视觉编码器对低级痕迹不敏感而表现不佳，且缺乏可解释性。
method: 提出一个统一框架，先增强视觉感知能力，然后基于推理步骤生成解释，实现可泛化且可解释的虚假图像检测。
result: 在多个基准数据集上超越现有方法，同时提供清晰的检测解释。
conclusion: 该方法有效结合感知与推理，为可解释虚假检测提供了新范式。
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

# 论文总结：《Seeing Before Reasoning: A Unified Framework for Generalizable and Explainable Fake Image Detection》

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：多模态大语言模型（MLLMs）因其丰富的世界知识、常识推理能力和可解释性潜力，被越来越多地用于检测AI生成的虚假图像。
- **核心问题**：现有MLLMs在虚假图像检测中表现不佳，根源在于**视觉感知与推理之间的错配**：
  - 视觉编码器主要针对语义级识别（如物体分类）优化，对低频、细微的伪造痕迹（如噪声、边界不连续）不敏感，导致模型“看不见”真正证据。
  - 现有的微调数据多采用狭窄的指令格式，与预训练阶段多样的数据分布差异大，模型易学得语言捷径，导致灾难性遗忘（甚至丢失基本对话能力）。
- **整体含义**：作者主张应先增强模型的低级痕迹感知能力，再进行结构化推理，提出“先见后思”（Seeing Before Reasoning）的新范式，从而构建通用、可解释且保持对话能力的虚假图像检测助手。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将虚假图像检测分解为两个阶段：
  - **阶段1：增强视觉感知**——仅对视觉编码器进行自重建训练，冻结LLM部分，使其对伪造痕迹敏感，同时不遗忘预训练知识。
  - **阶段2：结构化推理**——构建多轮对话微调数据，引导模型从痕迹感知逐步过渡到常识反思，输出关于“为什么假”和“真实版本应如何”的辩证推理。
- **关键技术细节**：
  - 视觉编码器微调采用**自重建损失**（self-reconstruction），迫使编码器捕捉像素级差异，从而强化对低层痕迹的敏感性。
  - 构造的对话数据包含三个阶段：感知层（识别具体伪造区域） → 分析层（解释伪造原因） → 反思层（推测真实内容），形成渐进式推理链。
  - 整体框架命名为 **Forensic-Chat**，支持多轮交互，保持对话能力。
- **公式与算法流程**（文字说明）：
  - 输入图像 → 阶段1：冻结LLM，仅更新视觉编码器权重，最小化重建误差（如MSE损失）。
  - 阶段2：使用构建的多轮对话数据，全模型微调（或部分微调），训练模型按顺序回答：① 观察到哪些伪造痕迹；② 根据痕迹判断真伪；③ 结合常识解释并描述可能真实版本。

## 3. 实验设计

- **数据集/场景**：
  - 使用了多个基准数据集，涵盖不同生成模型（如GAN、扩散模型、Deepfake等）生成的图像。
  - 提出了新的**可解释性基准 ExplainFake-Bench**，从5个关键维度（真实感、一致性、细节、合理性、可信度）评估MLLM的可解释性。
- **对比方法**：与多种基线方法（包括直接使用MLLM、传统检测器、其他微调MLLM方法）进行对比。
- **具体实验**：
  - 在多个标准检测数据集上对比泛化性能（跨生成模型迁移）。
  - 在ExplainFake-Bench上对比可解释性评分。
  - 消融实验：① 有无阶段1感知增强；② 不同推理数据构造方式；③ 冻结/微调不同模块。

## 4. 资源与算力

- **论文未明确说明使用的GPU型号、数量或训练时长**。仅提及方法在标准计算资源下可复现，但未提供具体算力细节。需要自行根据实验规模估算（例如8×A100 或 V100，但无官方数据）。

## 5. 实验数量与充分性

- **实验数量**：至少包含：
  - 主检测实验：在多个数据集上（如≥4个）对比泛化准确率和F1。
  - 可解释性评测：在ExplainFake-Bench的5个维度上对比评分。
  - 消融实验：约3-4组（如有无阶段1、不同数据构造策略）。
  - 对话能力保留测试：验证多轮对话质量未被破坏。
- **充分性评估**：实验设计较为全面，覆盖了泛化性、可解释性和对话保持三大目标。但缺少对极端场景（如罕见生成模型、强对抗攻击）的测试，且可解释性评估指标可能依赖人工标注，存在主观性。

## 6. 主要结论与发现

- 所提方法在多个虚假图像检测基准上**显著超越现有MLLM基线**，尤其在跨生成模型泛化上表现突出。
- 提供的可解释性输出（结构化推理链）比直接输出判断更清晰、更可信，且被ExplainFake-Bench验证具有较高真实感和一致性。
- 第一阶段感知增强是模型能力提升的关键，缺失该阶段会导致推理空洞和语言捷径。
- 该方法成功保留了模型的对话能力，未发生灾难性遗忘。

## 7. 优点

- **方法创新**：首次系统性地将“感知增强”和“结构化推理”分离，解决MLLM在细粒度视觉任务中的核心瓶颈。
- **设计与实践亮点**：
  - 自重建损失仅微调视觉编码器，避免LLM遗忘，技术简洁高效。
  - 多轮对话推理数据设计巧妙，可逐步引导模型进行辩证思考，增强可解释性的同时保持交互性。
  - 提出了专门针对可解释性评估的benchmark（5个维度），填补了领域空白。
- **实验验证**：在泛化性、可解释性、对话保持三个维度均进行严谨对比，消融实验充分。

## 8. 不足与局限

- **实验覆盖**：测试数据集虽然多样，但可能未覆盖最新生成模型（如Sora视频帧或4K高保真图像），泛化性上限未知。
- **偏差风险**：可解释性评估依赖人工标注或自动度量（如ExplainFake-Bench），可能存在主观偏差；且检测基准数据可能包含特定伪造模式，模型容易过拟合。
- **应用限制**：
  - 需要两阶段训练，整体流程较复杂。
  - 虽然保持对话能力，但多轮推理可能引入冗余或幻觉，在实时检测场景中效率不足。
  - 论文未讨论模型对对抗攻击（如精心设计的对抗扰动）的鲁棒性。
- **算力信息缺失**：未提供训练耗费的具体资源，难以评估复现成本。

（完）
