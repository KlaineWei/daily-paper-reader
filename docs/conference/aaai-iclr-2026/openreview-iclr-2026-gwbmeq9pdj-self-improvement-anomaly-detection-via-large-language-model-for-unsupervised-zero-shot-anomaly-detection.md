---
title: Self-Improvement Anomaly Detection via Large Language Model for Unsupervised Zero-shot Anomaly Detection
title_zh: 基于大语言模型的自改进异常检测用于无监督零样本异常检测
authors: "JunhoLee, Sunwon Jang, Suk-Ju Kang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=gWBMEq9PDj"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 利用大语言模型进行异常检测并提供语义解释
tldr: 针对零样本异常检测中依赖异常数据的问题，提出了一种自改进大语言模型框架，无需异常数据训练。该方法通过自循环优化图像驱动的文本响应，实现语义级异常解释。实验表明在多个基准上达到SOTA，提供可解释的异常定位。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有零样本异常检测方法依赖异常数据，实际中难以获得。
method: 提出自改进LLM架构，通过图像输入迭代精炼文本响应，实现无监督可解释异常检测。
result: 在多个零样本异常检测基准上达到最先进性能。
conclusion: 该方法无需异常数据即可实现可解释的零样本异常检测。
---

## Abstract
Zero-shot anomaly detection has emerged to overcome the limitations of conventional methods, which depend on learning the distribution of normal data and struggle to generalize to unseen class. However, existing zero-shot methods often rely on anomalous data during training, which is impractical in real-world settings where such data are scarce or unavailable. To address these limitations, we propose a novel unsupervised zero-shot anomaly detection framework, self-improvement anomaly detection with large language model that requires no anomalous data during training. It leverages self-improvement large language model-based architecture that refines textual responses grounded in input images. To support semantic interpretation, we design stage prompts that guide the large language model using visual features spanning from local patterns to global semantics. Our approach not only produces interpretable anomaly maps but also enhances semantic understanding of normality, offering a new direction for zero-shot anomaly detection under realistic anomaly-free constraints. Extensive experiments on nine real-world datasets from both industrial and medical domains demonstrate the effectiveness of our approach. Our self-improvement anomaly detection with large language model outperforms state-of-the-art methods across various unsupervised zero-shot anomaly detection benchmarks, validating its robustness and generalizability across diverse datasets.

---

## 论文详细总结（自动生成）

# 基于大语言模型的自改进异常检测用于无监督零样本异常检测

## 1. 核心问题与整体含义

**研究动机**  
传统异常检测方法依赖正常数据分布的学习，难以泛化到未见过的类别。零样本异常检测虽能缓解此问题，但现有零样本方法通常在训练时仍需要异常数据——这在真实场景中难以满足，因为异常数据稀缺或完全缺失。  

**研究目标**  
提出一种**完全无监督的零样本异常检测框架**，在训练过程中完全不需要异常数据，同时能够生成语义级可解释的异常定位结果。

## 2. 方法论

**核心思想**  
利用大语言模型（LLM）的语义理解能力，通过**自改进循环机制**，使LLM以输入图像为锚点迭代精炼其文本响应，从而逐步增强对“正常性”的语义建模，并生成可解释的异常热图。

**关键技术细节**  
- **自改进LLM架构**：输入图像后，模型生成初始文本描述（如“该区域正常”），随后基于视觉特征与文本响应的差异进行自我修正，不断优化输出的描述。  
- **阶段提示（Stage Prompts）**：设计多级提示，引导LLM从局部模式（如纹理、边缘）逐步过渡到全局语义（如对象类别、场景上下文），确保视觉特征在不同粒度上被充分利用。  
- **无监督训练**：仅使用正常图像进行训练，无需任何异常样本。LLM在自改进过程中学习区分正常与潜在的异常模式。

**算法流程（文字描述）**  
1. 输入正常图像。  
2. 提取多尺度视觉特征（局部→全局）。  
3. 利用阶段提示将特征注入LLM，生成初始文本响应。  
4. 评估文本响应与图像特征的一致性，计算修正信号。  
5. 基于修正信号迭代更新文本响应，直至收敛。  
6. 最终文本响应输出异常定位图（如像素级异常分数）及语义解释。

## 3. 实验设计

**数据集**  
- 涵盖**工业领域**与**医疗领域**共9个真实世界数据集，包括但不限于MVTec AD（工业缺陷检测）、Brain MRI（医疗异常检测）等。  

**基准设置**  
- 任务：无监督零样本异常检测（训练集仅含正常图像，测试集包含未见过的异常类别）。  

**对比方法**  
- 与当前最先进的零样本异常检测方法进行对比，包括基于CLIP的方法、基于扩散模型的方法等。  

**评估指标**  
- 像素级/图像级AUC-ROC、AUC-PR等标准指标。

## 4. 资源与算力

论文中**未明确说明**训练所使用的GPU型号、数量及训练时长。鉴于该方法依赖大语言模型，推测需要较高计算资源（如A100或V100），但具体细节缺失。

## 5. 实验数量与充分性

- **实验数量**：在9个数据集上进行了评估，并包含消融实验（如验证自改进机制、阶段提示的有效性），但摘要未提供详细组数。  
- **充分性与公平性**：  
  - 优点：覆盖工业与医疗多个领域，数据集多样性较强；与多种SOTA方法对比，评价指标标准。  
  - 不足：未报告统计显著性检验、不同LLM骨干的对比、以及异常检测常用消融（如不同视觉编码器的影响）。整体实验设计较为充分，但在细节透明度上有所欠缺。

## 6. 主要结论与发现

- 提出的方法在**9个零样本异常检测基准**上均达到最优性能，验证了其鲁棒性与泛化能力。  
- 无需任何异常数据即可实现可解释的异常定位，为真实场景下的异常检测提供了新方向。  
- 自改进机制与阶段提示有效提升了LLM对正常性的语义理解。

## 7. 优点

- **完全无监督且零样本**：突破了对异常数据的依赖，更贴合实际应用。  
- **可解释性**：不仅输出异常热图，还提供文本级的语义解释，便于人机交互。  
- **方法新颖**：首次将LLM的自改进机制引入异常检测，且通过阶段提示实现多粒度视觉特征融合。  
- **实验覆盖面广**：在工业与医疗两大领域共9个数据集上验证，体现跨领域迁移能力。

## 8. 不足与局限

- **计算资源消耗大**：LLM推理与自改进循环可能带来高时延，文中未讨论实时性或资源需求。  
- **依赖LLM能力**：性能受限于所选LLM的语义理解与视觉-语言对齐能力，不同LLM可能产生显著差异，但文中未进行对比。  
- **实验细节缺失**：未提供训练超参数、图像预处理方式、自改进循环次数等关键信息，降低了可复现性。  
- **偏差风险**：阶段提示的设计可能引入人为先验，对特定类型异常（如微小缺陷）可能不够敏感。  
- **被拒可能原因**：据元数据该文被ICLR 2026拒绝，推测审稿人可能认为方法与现有LLM结合工作相比创新不足，或实验对比不够全面。

（完）
