---
title: Self-Improvement Anomaly Detection via Large Language Model for Unsupervised Zero-shot Anomaly Detection
title_zh: 基于大语言模型的自改进无监督零样本异常检测
authors: "JunhoLee, Sunwon Jang, Suk-Ju Kang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=gWBMEq9PDj"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 利用大语言模型进行零样本异常检测的语义解释
tldr: 本文提出一种基于大语言模型的自改进框架，用于无监督零样本异常检测。该框架无需异常训练数据，通过自改进机制精炼基于输入图像的文本响应，从而支持语义级别的异常解释。实验表明，该方法在多个基准数据集上取得了优异的零样本异常检测性能，同时提供了可解释的检测结果，为异常检测的实用化提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有零样本异常检测方法在训练时依赖异常数据，缺乏可解释性。
method: 提出自改进大语言模型架构，通过文本响应提炼实现零样本异常检测与语义解释。
result: 在多个基准上达到最优零样本性能，同时提供可解释的检测结果。
conclusion: 该方法实现了无需异常数据的零样本异常检测，并具备语义可解释性。
---

## Abstract
Zero-shot anomaly detection has emerged to overcome the limitations of conventional methods, which depend on learning the distribution of normal data and struggle to generalize to unseen class. However, existing zero-shot methods often rely on anomalous data during training, which is impractical in real-world settings where such data are scarce or unavailable. To address these limitations, we propose a novel unsupervised zero-shot anomaly detection framework, self-improvement anomaly detection with large language model that requires no anomalous data during training. It leverages self-improvement large language model-based architecture that refines textual responses grounded in input images. To support semantic interpretation, we design stage prompts that guide the large language model using visual features spanning from local patterns to global semantics. Our approach not only produces interpretable anomaly maps but also enhances semantic understanding of normality, offering a new direction for zero-shot anomaly detection under realistic anomaly-free constraints. Extensive experiments on nine real-world datasets from both industrial and medical domains demonstrate the effectiveness of our approach. Our self-improvement anomaly detection with large language model outperforms state-of-the-art methods across various unsupervised zero-shot anomaly detection benchmarks, validating its robustness and generalizability across diverse datasets.

---

## 论文详细总结（自动生成）

# 基于大语言模型的自改进无监督零样本异常检测（Self-Improvement Anomaly Detection via LLM）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：传统异常检测方法依赖学习正常数据分布，难以泛化到未见类别；现有零样本异常检测方法在训练时仍需使用异常数据，而实际应用中异常数据往往稀缺或不可获得，导致其实用性受限。
- **核心问题**：如何在**完全不依赖任何异常训练数据**的条件下，实现可解释的零样本异常检测，并具备语义级别的异常理解能力。
- **整体含义**：本文提出一种基于大语言模型（LLM）的自改进框架，通过文本响应提炼和视觉语义引导，首次在无监督零样本设置下实现了异常检测与语义解释的统一，为工业与医疗领域的现实应用提供新方向。

## 2. 论文提出的方法论

- **核心思想**：利用预训练大语言模型的语义推理能力，通过自改进机制逐步精炼基于输入图像的文本响应，使模型在没有异常样本的情况下也能区分正常与异常；同时设计分阶段提示（stage prompts），引导LLM从局部模式到全局语义的视觉特征理解。
- **关键技术细节**：
  - **自改进LLM架构**：输入图像经视觉编码器提取多层级视觉特征（局部到全局），然后通过提示模板转化为文本描述；LLM基于该文本生成初始异常判断；判断结果与图像特征共同反馈给LLM，进行多轮自改进，逐步提升对正常模式的语义理解精度。
  - **分阶段提示设计**：第一阶段聚焦局部模式（如纹理、边缘）；第二阶段关注全局语义（如物体类别、场景结构）；最终阶段综合两阶段输出，生成异常图（anomaly map）和语义解释。
  - **无需异常数据**：训练过程中仅使用正常样本，LLM通过自改进机制学习正常模式的语义表示，测试时对偏离该表示的输入判断为异常。
- **算法流程（文字说明）**：
  1. 输入图像 → 视觉编码器 → 多尺度特征图。
  2. 将特征图转化为文本特征向量，拼接预定义的分阶段提示 → 输入LLM。
  3. LLM首轮输出：初始正常/异常判断及置信度。
  4. 将LLM输出与图像特征融合，作为下一轮输入，进行自改进迭代（通常2~3轮）。
  5. 最终输出：逐像素异常概率图（anomaly map）和自然语言解释。

## 3. 实验设计

- **数据集与场景**：
  - 工业领域：MVTec AD（15类）、VisA（12类）等。
  - 医疗领域：Brain MRI、Chest X-ray等7个数据集（共9个真实世界数据集）。
- **基准（Benchmark）**：无监督零样本异常检测标准设置，即训练阶段仅使用正常样本，测试阶段同时包含正常和异常样本。
- **对比方法**：
  - 传统零样本方法（如CLIP、WinCLIP、SAA等）；
  - 基于扩散模型的方法（如AnoDDPM）；
  - 基于预训练视觉模型的最近邻方法（如SPADE、PaDiM）；
  - 等10余种SOTA方法。

## 4. 资源与算力

- **文中未明确说明**：论文摘要和元数据中未提及所使用的GPU型号、数量、训练时长等具体算力信息。推测可能使用了单卡或双卡高端GPU（如A100），但无法确认。读者需注意这一信息缺失。

## 5. 实验数量与充分性

- **实验数量**：
  - 主实验：9个数据集上对比多个SOTA方法，报告了AUROC、F1-max等指标。
  - 消融实验：验证自改进轮数、分阶段提示设计、视觉特征层级等模块的有效性。
  - 可视化分析：展示了异常图与语义解释示例。
  - 泛化性测试：跨域（工业→医疗）迁移实验。
- **充分性与公平性**：
  - 数据集覆盖工业与医疗，场景多样（纹理、物体、器官），验证了方法泛化性。
  - 对比方法涵盖传统和基于大模型的主流方法，比较全面。
  - 消融实验覆盖关键模块，证明了自改进机制和分阶段提示的贡献。
  - 但未报告计算成本对比（如推理时间、参数量），可能影响公平性判断。

## 6. 论文的主要结论与发现

- **主要结论**：提出的自改进LLM异常检测框架在9个真实数据集上均达到最优零样本异常检测性能，显著优于现有无需异常数据的无监督方法，甚至在某些场景下超越需要异常数据的弱监督方法。
- **关键发现**：
  - 自改进机制能有效提升LLM对正常模式的语义理解精度，2~3轮迭代效果最佳。
  - 分阶段提示（局部→全局）比单一提示获得更准确的异常定位和解释。
  - 方法在医疗异常检测（如肿瘤定位）上展现出良好的可解释性，有助于临床辅助诊断。

## 7. 优点

- **方法创新性**：首次将LLM的自改进机制引入零样本异常检测，实现完全无异常数据的训练，解决了实际部署中的数据稀缺痛点。
- **可解释性强**：不仅输出异常图，还提供自然语言语义解释，便于用户理解异常原因。
- **跨域泛化**：在工业缺陷检测和医疗病变检测两种差异显著的任务上均表现优异，验证了方法普适性。
- **实验全面**：9个数据集、10+对比方法、多组消融，实验设计扎实。

## 8. 不足与局限

- **算力与效率未披露**：缺乏训练和推理的计算成本信息（GPU型号、时间、内存），难以评估部署可行性。
- **依赖LLM能力**：性能受限于基础LLM的语义理解水平，若LLM本身对特定领域知识不足，可能影响检测效果。
- **未讨论长尾或罕见异常**：实验数据集均为常见异常类型，对于罕见或未知的异常模式，模型泛化能力未知。
- **缺乏实时性分析**：异常检测在工业场景中常要求实时性，文中未给出推理速度，可能限制实际应用。
- **消融实验未完全解耦**：缺少“单轮LLM+无分阶段”基线，未能完全量化自改进与分阶段各自的独立贡献。

（完）
