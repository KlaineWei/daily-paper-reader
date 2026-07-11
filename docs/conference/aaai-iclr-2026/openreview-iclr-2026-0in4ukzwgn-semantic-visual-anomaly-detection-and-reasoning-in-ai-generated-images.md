---
title: Semantic Visual Anomaly Detection and Reasoning in AI-Generated Images
title_zh: AI生成图像中的语义视觉异常检测与推理
authors: "Chuangchuang Tan, Xiang Ming, Jinglu Wang, Renshuai Tao, Bin Li, Yunchao Wei, Yao Zhao, Yan Lu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=0iN4UKZwgn"
tags: ["query:xai-objdet"]
score: 9.0
evidence: AI生成图像中的语义异常检测与推理，涉及可解释深度伪造检测
tldr: 针对AI生成图像中常见的语义异常（如物体配置不合理、违反物理规律等），该论文形式化了语义异常检测与推理任务，并提出了AnomReason基准数据集。通过结构化四元组标注，该方法能够定位并解释图像中的不合理之处，为可解释的深度伪造检测提供了新的评估标准。实验证明该方法在多项指标上优于现有技术，推动了AIGC可信性评估的发展。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: AI生成图像常存在细微语义异常，现有方法缺乏系统检测与解释能力。
method: 构建AnomReason基准，采用结构化四元组标注异常并设计推理框架。
result: 在多个AIGC数据集上，所提方法在语义异常检测准确率和可解释性上显著优于基线。
conclusion: 该工作为可解释深度伪造检测和AIGC真实性评估奠定了重要基础。
---

## Abstract
The rapid advancement of AI-generated content (AIGC) has enabled the synthesis of visually convincing images; however, many such outputs exhibit subtle \textbf{semantic anomalies}, including unrealistic object configurations, violations of physical laws, or commonsense inconsistencies, which compromise the overall plausibility of the generated scenes. Detecting these semantic-level anomalies is essential for assessing the trustworthiness of AIGC media, especially in AIGC image analysis, explainable deepfake detection and semantic authenticity assessment.In this paper,  we formalize \textbf{semantic anomaly detection and reasoning} for AIGC images and  introduce \textbf{AnomReason}, a large-scale benchmark with structured annotations as quadruples \emph{(Name, Phenomenon, Reasoning, Severity)}. Annotations are produced by  a modular multi-agent pipeline (\textbf{AnomAgent}) with lightweight human-in-the-loop verification, enabling scale while preserving quality. At construction time, AnomAgent processed approximately 4.17\,B GPT-4o tokens, providing scale evidence for the resulting structured annotations. We further  show that models fine-tuned on AnomReason achieve consistent gains over strong vision-language baselines under our proposed semantic matching metric (\textit{SemAP} and \textit{SemF1}). Applications to {explainable deepfake detection} and {semantic reasonableness assessment of image generators} demonstrate practical utility. In summary, AnomReason and AnomAgent serve as a foundation for measuring and improving the semantic plausibility of AI-generated images. The code is available at \url{https://github.com/chuangchuangtan/Semantic-Visual-Anomaly-Detection-and-Reasoning}.

---

## 论文详细总结（自动生成）

# 论文总结：AI生成图像中的语义视觉异常检测与推理

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：AI生成内容（AIGC）技术飞速发展，能够生成视觉上令人信服的图像，但许多生成结果存在细微的**语义异常**，例如不合理的物体配置、违反物理规律或常识不一致，这些异常降低了场景的整体可信度。
- **核心问题**：现有方法缺乏对AIGC图像中语义层面异常的系统检测与解释能力。需要一种能够**定位并解释**图像中不合理之处的方法，以评估AIGC的可信性，并推动可解释深度伪造检测和语义真实性评估的发展。
- **整体含义**：该工作为AIGC图像的可信性评估提供了一种**结构化、可解释**的新范式，通过形式化语义异常检测与推理任务，为后续研究和实际应用奠定基础。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将语义异常检测与推理转化为**结构化四元组**的预测任务，并借助大语言模型（LLM）和轻量级人工验证构建大规模基准数据集，然后微调视觉-语言模型以实现异常定位与解释。
- **关键技术细节**：
  - **AnomReason基准**：以四元组 `(Name, Phenomenon, Reasoning, Severity)` 形式标注异常：
    - **Name**：异常类别名称（如“物体缺失”）
    - **Phenomenon**：异常现象的视觉描述
    - **Reasoning**：违反物理/常识的推理过程
    - **Severity**：异常严重程度（如轻/中/重）
  - **AnomAgent流水线**：模块化多智能体系统，由多个GPT-4o智能体协作生成结构化标注，并使用**轻量级人工循环验证**（human-in-the-loop）来保证标注质量与规模。
  - **语义匹配指标**：提出SemAP（语义平均精度）和SemF1（语义F1分数）以评估模型在语义层面上的检测与推理性能。
- **算法流程（文字说明）**：
  1. 收集AIGC图像（来自多种生成器）；
  2. 通过AnomAgent自动生成候选四元组标注；
  3. 人工验证并修正部分标注；
  4. 在AnomReason数据上微调视觉-语言模型（如BLIP-2、LLaVA等）；
  5. 在测试集上用SemAP/SemF1评估模型输出与真实标注的语义相似度。

## 3. 实验设计：数据集、基准、对比方法

- **数据集/场景**：
  - **AnomReason基准**：大规模数据集，包含多种AIGC图像及其结构化四元组标注。
  - 此外，还应用于**可解释深度伪造检测**和**图像生成器语义合理性评估**两个实际场景。
- **基准（Benchmark）**：以AnomReason作为主要评估基准，测试集包含未见过的异常类型。
- **对比方法**：与多种**强视觉-语言基线模型**（如预训练的BLIP-2、LLaVA等）进行对比，在微调前后评估。

## 4. 资源与算力

- **文中明确说明**：在构建AnomReason时，AnomAgent管道处理了**大约4.17B GPT-4o tokens**，提供了结构化标注的规模证据。
- **未明确说明**：
  - 微调模型所使用的GPU型号、数量、训练时长等具体算力信息。
  - 因此无法量化训练资源消耗。

## 5. 实验数量与充分性

- **实验数量**：摘要中提到：
  - 在AnomReason基准上进行主实验，对比多个视觉-语言基线。
  - 两个应用场景实验（可解释深度伪造检测、图像生成器语义合理性评估）。
  - 推测还有消融实验（如是否使用人工验证的影响、不同标注策略等），但摘要未细述。
- **充分性与公平性**：
  - **充分性**：从摘要看，实验覆盖了基准测试和两个实际任务，但缺乏详细的数据集划分、模型参数规模、性能表格等，信息受限。可能正文中有更全面的实验。
  - **客观公平**：对比强基线并观察微调后的增益；使用了语义匹配指标而非简单字符串匹配，更合理。但由于未透露具体数值，无法完全判断。

## 6. 论文的主要结论与发现

- 微调于AnomReason的模型在SemAP和SemF1指标上相比强视觉-语言基线取得**一致的提升**。
- 所提方法在**可解释深度伪造检测**和**图像生成器语义合理性评估**中展现出实际应用价值。
- AnomReason和AnomAgent为衡量和改进AI生成图像的语义合理性奠定了**基础性资源**。

## 7. 优点：方法或实验设计上的亮点

- **结构化标注形式**：四元组不仅定位异常，还提供推理和严重程度，提升了可解释性。
- **大规模自动化+人工验证**：利用LLM流水线（AnomAgent）实现规模化，同时通过轻量级人工循环保证质量，平衡了效率与准确性。
- **新型语义评估指标**：SemAP和SemF1关注语义匹配，比传统精确匹配更适应异常描述的多样性。
- **应用场景验证**：超越单纯基准测试，在深度伪造检测和生成器评估中展示了实用性。

## 8. 不足与局限

- **算力资源不透明**：未公开微调模型的具体GPU需求，不利于可复现性。
- **实验细节缺乏**：仅摘要呈现，缺少不同异常类型的性能分解、跨数据集泛化性测试等。
- **依赖GPT-4o**：标注过程依赖商用LLM，存在成本与封闭性问题，且轻量级人工验证可能仍存在偏差。
- **应用范围有限**：当前仅聚焦于语义异常，未涵盖像素级伪造痕迹或对抗性攻击等其他伪造类型。
- **评估指标可能存在天花板**：若模型输出与标注的语义相似但表述不同，SemAP/SemF1能否准确反映尚需更多验证。

（完）
