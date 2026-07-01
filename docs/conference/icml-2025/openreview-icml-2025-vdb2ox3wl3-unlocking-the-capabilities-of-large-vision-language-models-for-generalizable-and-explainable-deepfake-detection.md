---
title: Unlocking the Capabilities of Large Vision-Language Models for Generalizable and Explainable Deepfake Detection
title_zh: 解锁大视觉语言模型用于通用且可解释的深度伪造检测
authors: "Peipeng Yu, Jianwei Fei, Hui Gao, Xuan Feng, Zhihua Xia, Chip Hong Chang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=vDB2oX3Wl3"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 利用大视觉语言模型进行可解释深度伪造检测
tldr: 本文提出一种框架，利用大视觉语言模型（LVLM）实现可解释的深度伪造检测。通过知识引导的伪造检测器、伪提示学习器和语言模型，该框架不仅能够识别伪造区域，还能提供语言解释。实验表明，该方法在多个伪造检测基准上取得优异性能，同时具备强泛化性和可解释性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: LVLM在深度伪造检测中潜力未开发，且缺乏可解释性。
method: 设计知识引导的伪造检测器与伪提示学习器，结合LLM生成解释。
result: 在多个数据集上实现高精度和可解释的伪造检测。
conclusion: 该框架成功赋予LVLM可解释深度伪造检测能力。
---

## Abstract
Current Large Vision-Language Models (LVLMs) have demonstrated remarkable capabilities in understanding multimodal data, but their potential remains underexplored for deepfake detection due to the misalignment of their knowledge and forensics patterns. To this end, we present a novel framework that unlocks LVLMs' potential capabilities for deepfake detection. Our framework includes a Knowledge-guided Forgery Detector (KFD), a Forgery Prompt Learner (FPL), and a Large Language Model (LLM). The KFD is used to calculate correlations between image features and pristine/deepfake image description embeddings, enabling forgery classification and localization. The outputs of the KFD are subsequently processed by the Forgery Prompt Learner to construct fine-grained forgery prompt embeddings. These embeddings, along with visual and question prompt embeddings, are fed into the LLM to generate textual detection responses. Extensive experiments on multiple benchmarks, including FF++, CDF2, DFD, DFDCP, DFDC, and DF40, demonstrate that our scheme surpasses state-of-the-art methods in generalization performance, while also supporting multi-turn dialogue capabilities.

---

## 论文详细总结（自动生成）

好的，根据您提供的论文元数据和摘要信息，我将生成一份详细的中文总结。请注意，由于原始论文PDF内容未成功提取，以下所有信息严格基于您给出的元数据字段和摘要部分。若论文内有更详细的实验细节或资源说明，此处无法涵盖。

---

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：当前大型视觉语言模型（LVLM）在多模态理解任务中表现出色，但在深度伪造检测领域的潜力尚未被充分挖掘。
- **核心问题**：LVLM 的知识与深度伪造检测所需的取证模式之间存在不匹配（misalignment），导致 LVLM 无法直接有效地用于深度伪造检测。
- **研究动机**：本文旨在解锁 LVLM 在深度伪造检测中的潜力，同时弥补现有方法在**可解释性**上的不足——大多数深度伪造检测器只能输出真假标签，无法提供语言层面的解释。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：构建一个框架，利用 LVLM 进行通用且可解释的深度伪造检测，能够同时实现伪造分类、伪造区域定位，并通过自然语言给出检测理由。
- **关键技术细节**：
  - **知识引导的伪造检测器（KFD）**：计算图像特征与“原始/伪造图像描述嵌入”之间的相关性，从而完成伪造分类和定位。
  - **伪提示学习器（FPL）**：将 KFD 的输出进行处理，构建细粒度的伪造提示嵌入。
  - **大型语言模型（LLM）**：接收伪造提示嵌入、视觉嵌入以及问题提示嵌入，生成文本形式的检测响应（即解释）。
- **算法流程（文字描述）**：
  1. 输入图像经过图像编码器提取特征。
  2. KFD 模块利用预定义的“原始”和“伪造”描述嵌入，通过相关性计算判断图像属于真实还是伪造，并定位可疑区域。
  3. FPL 模块将 KFD 的定位与分类信息转化为可学习的细粒度提示。
  4. 上述提示与视觉特征、用户问题提示一同送入 LLM，LLM 输出自然语言解释（如“图像在眼睛区域存在仿造痕迹”）。
- **公式**：论文中未提供明确公式，但核心操作为特征相似度计算与提示学习。

## 3. 实验设计：数据集、Benchmark、对比方法

- **数据集**：FF++ (FaceForensics++)、CDF2 (Celeb-DF v2)、DFD (DeepFakeDetection)、DFDCP (DeepFakeDetection Challenge Preview)、DFDC (DeepFake Detection Challenge)、DF40 等多个主流深度伪造检测基准。
- **Benchmark**：上述六个数据集共同构成了评价泛化性和可解释性的基准。
- **对比方法**：文中提到“surpasses state-of-the-art methods”，但未在摘要中列举具体方法名称。推测对比了近年来基于 CNN、Transformer 及视觉语言模型的深度伪造检测算法。

## 4. 资源与算力

- **未明确说明**：论文元数据及摘要中未提及使用的 GPU 型号、数量、训练时长等算力信息。因此无法给出具体数据。
- **备注**：由于使用 LVLM (如 LLaVA 等) 和 LLM，推测需要较高显存的 GPU（如 A100）进行训练和推理，但具体细节需查阅全文。

## 5. 实验数量与充分性

- **实验数量**：在至少 6 个公开数据集上进行了评估（FF++, CDF2, DFD, DFDCP, DFDC, DF40），涵盖多种伪造方法和质量。
- **充分性评估**：
  - **正面**：数据集覆盖了主流测试集，包含跨数据集评估，有利于验证泛化性。
  - **不足**：摘要中未提及消融实验、参数量分析、推理速度等。由于缺乏全文，无法判断实验是否完全充分、客观、公平。但根据 ICML 2025 的接受标准，推测实验设计较为严谨。
- **注意**：可解释性实验（如人类评估、生成解释的质量指标）未在摘要中提及，可能存在于全文。

## 6. 论文的主要结论与发现

- **主要结论**：本文提出的框架成功解锁了 LVLM 在深度伪造检测中的能力，在多个基准上取得了**超越现有最优方法的泛化性能**，同时支持**多轮对话**和**可解释性**。
- **发现**：通过知识引导的伪造检测器与伪造提示学习器，可以有效对齐 LVLM 的知识与取证模式，从而生成准确且可读的检测解释。

## 7. 优点：方法或实验设计上的亮点

- **方法亮点**：
  - 首次将 LVLM 系统地引入深度伪造检测，并同时解决分类、定位和解释三个任务。
  - 设计了 KFD 和 FPL 模块，弥补了 LVLM 与深度伪造领域知识的差距。
  - 支持多轮对话，增强了人机交互体验。
- **实验设计亮点**：
  - 在多达 6 个公开数据集上进行测试，覆盖不同伪造技术和质量，泛化性验证充分。
  - 对比当前最优方法并取得领先，证明有效性。

## 8. 不足与局限

- **实验覆盖的局限**：
  - 仅使用了面部深度伪造数据集，未提及对非人脸伪造（如全身 DeepFake、GAN 生成图像）的检测能力。
  - 未详细说明可解释性的量化评估（如 BLEU、ROUGE 或人类判断一致性），仅说明能生成文本响应。
- **偏差风险**：
  - 训练数据可能存在域偏差（如主要基于公开数据集，对特定伪造模式过拟合）。
  - LLM 生成解释时可能存在幻觉或语义不准确。
- **应用限制**：
  - 模型依赖 LVLM 和 LLM，计算开销大，推理速度慢，不适合实时检测。
  - 依赖预设的“原始/伪造图像描述嵌入”，需预定义，可能限制对新类型伪造的泛化。
- **资源与算力未公开**：无法评估部署成本。

---

（完）
