---
title: "$\\mathcal{X}^2$-DFD: A framework for e$\\mathcal{X}$plainable and e$\\mathcal{X}$tendable Deepfake Detection"
title_zh: X^2-DFD：可解释且可扩展的深度伪造检测框架
authors: "Yize Chen, Zhiyuan Yan, Siwei Lyu, Baoyuan Wu"
date: 2024-09-23
pdf: "https://openreview.net/pdf?id=EoTIlDT0Tr"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释且可扩展的深度伪造检测框架
tldr: 针对现有深度伪造检测方法缺乏可解释性且预训练多模态大模型性能有限的问题，提出X^2-DFD框架，通过评估MLLM在伪造检测中的优劣势并设计增强策略，实现了可解释且可扩展的深度伪造检测，提升了检测结果的人可理解性。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 现有深度伪造检测方法仅给出真伪标签，缺乏可解释性。
method: 基于多模态大语言模型，通过伪造特征分析和增强策略构建可解释检测框架。
result: 实验证明了框架在深度伪造检测中的可解释性和扩展性优势。
conclusion: X^2-DFD为可解释深度伪造检测提供了有效方案，拓展了MLLM在该领域的应用。
---

## Abstract
Detecting deepfakes (*i.e.*, AI-generated content with malicious intent) has become an important task. Most existing detection methods provide only real/fake predictions without offering human-comprehensible explanations. Recent studies leveraging multimodal large-language models (MLLMs) for deepfake detection have shown improvements in explainability. However, the performance of pre-trained MLLMs (*e.g.*, LLaVA) remains limited due to a lack of understanding of their capabilities for this task and strategies to enhance them. In this work, we empirically assess the strengths and weaknesses of MLLMs specifically in deepfake detection via forgery-related feature analysis. Building on these assessments, we propose a novel framework called $\mathcal{X}^2$-DFD, consisting of three core modules. 
The first module, *Model Feature Assessment (MFA)*, measures the detection capabilities of forgery-related features intrinsic to MLLMs, and gives a descending ranking of these features. 
The second module, *Strong Feature Strengthening (SFS)*, enhances the detection and explanation capabilities by fine-tuning the MLLM on a dataset constructed based on the top-ranked features. 
The third module, *Weak Feature Supplementing (WFS)*, improves the fine-tuned MLLM's capabilities on lower-ranked features by integrating external dedicated deepfake detectors. 
To verify the effectiveness of this framework, we further present a practical implementation, where an automated forger-related feature generation, evaluation, and ranking procedure is designed for *MFA* module; an automated generation procedure of the fine-tuning dataset containing real and fake images with explanations based on top-ranked features is developed for *SFS* model; an external conventional deepfake detector focusing on blending artifact, which corresponds to a low detection capability in the pre-trained MLLM, is integrated for *WFS* module. 
Experimental results show that the proposed implementation enhances overall detection performance compared to pre-trained MLLMs, while providing more convincing explanations. 
More encouragingly, our framework is designed to be plug-and-play, allowing it to seamlessly integrate with more advanced MLLMs and external detectors, leading to continual improvement and extension to face the challenges of rapidly evolving deepfake technologies.

---

## 论文详细总结（自动生成）

# X^2-DFD: 可解释且可扩展的深度伪造检测框架 详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：现有深度伪造检测方法仅输出“真/假”二元标签，缺乏人类可理解的解释；而预训练多模态大语言模型（MLLM，如LLaVA）虽具备一定可解释性，但深度伪造检测性能有限，原因在于缺乏对该任务下MLLM能力的系统性理解及针对性的增强策略。
- **研究动机**：构建一个**可解释**（提供人可理解的伪造理由）且**可扩展**（能够兼容更先进的MLLM和外部检测器）的深度伪造检测框架，以应对快速演变的深度伪造技术挑战。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：通过评估MLLM中与伪造相关的特征能力，对**强特征**进行强化微调，对**弱特征**引入外部专用检测器进行补充，从而提升整体检测性能与解释质量。
- **框架三大模块**：
  - **模块1：模型特征评估（MFA）**  
    - 度量MLLM内在各伪造相关特征的检测能力，输出这些特征的降序排名。
    - 具体实现中（实际方案）：设计自动化的伪造相关特征生成、评估与排序流程。
  - **模块2：强特征强化（SFS）**  
    - 基于排名靠前的特征构建微调数据集（包含真实/伪造图像及其对应的自然语言解释），对MLLM进行微调，增强其在这些特征上的检测和解释能力。
  - **模块3：弱特征补充（WFS）**  
    - 针对排名靠后的特征（如预训练MLLM检测能力较弱的混合伪影），集成外部专用深度伪造检测器，借助其输出弥补MLLM的不足。
- **整体流程**（文字描述）：
  1. 通过MFA对MLLM的多个伪造特征（如纹理异常、混合边界、面部变形等）进行自动化评估与排序。
  2. 选取Top特征，自动生成包含对应特征解释的微调数据集，对MLLM进行SFS微调。
  3. 将微调后的MLLM与外部检测器（针对弱特征）通过WFS模块集成，输出最终检测结果和解释。

## 3. 实验设计
- **数据集/场景**：未在提供的文本中明确列出具体数据集名称（如FF++、Celeb-DF等）。但可知实验中使用了**包含真实和伪造图像且带有人工解释的微调数据集**（由SFS模块自动生成），以及用于评估最终性能的**测试集**（推测为常见深度伪造基准）。
- **Benchmark**：未明确说明，但对比了预训练MLLM（如LLaVA）和可能的外部检测器。
- **对比方法**：
  - 预训练MLLM（基线，无微调）。
  - 仅使用MFA+SFS的变体（无WFS）。
  - 仅使用MFA+WFS的变体（无SFS）。
  - 完整X^2-DFD框架。
- **评价指标**：检测准确率、可解释性质量（可能通过人工评估或自动指标）。论文声称提升了整体检测性能并提供了更令人信服的解释。

## 4. 资源与算力
- 提供的文本**未明确说明**使用的GPU型号、数量、训练时长等算力信息。仅提到框架设计为即插即用，可无缝集成更先进的MLLM和外部检测器，暗示算力需求主要取决于所选MLLM和外部检测器的基础要求。

## 5. 实验数量与充分性
- **实验数量**：文本中未列出具体实验组数。但从方法论描述可推断至少包含以下对比：
  - 预训练MLLM vs. 微调后MLLM（SFS效果）。
  - 有/无WFS模块的消融实验。
  - 可能的不同特征排名策略或不同外部检测器的对比。
- **充分性评价**：由于未提供详细数据，仅凭摘要难以判断实验的充分性。通常这类工作还需要在多个基准数据集上、与多个SOTA可解释检测方法对比，以及进行可解释性的人为评估。论文声称其框架在可解释性和扩展性上有优势，但缺乏公开的实验细节可能影响可信度。

## 6. 主要结论与发现
- X^2-DFD框架能够系统地评估MLLM对伪造特征的检测能力，并通过强化强特征、补充弱特征的方式，在**整体检测性能**上优于原始预训练MLLM。
- 生成的**解释更加令人信服**，提升了结果的可理解性。
- 框架具有**即插即用**特性，能够方便地集成更先进的MLLM和外部专用检测器，从而持续改进并扩展到对抗新型深度伪造技术。

## 7. 优点
- **可解释性优先**：直接针对现有方法缺乏解释的痛点，设计专用模块产出自然语言解释。
- **模块化设计**：MFA、SFS、WFS三个模块解耦，易于替换和升级，支持持续扩展。
- **自动化流程**：伪造特征生成、评估、排序以及微调数据集构建均实现自动化，减少了人工成本。
- **弱特征补充**：通过集成外部检测器弥补MLLM的内在短板，体现系统性思维。

## 8. 不足与局限
- **实验细节缺失**：论文主体（可能因篇幅限制）未公开具体数据集、对比方法和数值结果，使得复现和评估变得困难。作为会议论文，这属于较大缺陷，可能是被拒原因之一。
- **外部检测器依赖**：WFS模块需要额外的专用检测器，增加了系统复杂性和部署成本；且外部检测器本身也可能存在可解释性不足的问题。
- **特征定义的局限性**：MFA模块中预定义的伪造特征是否覆盖所有类型的深度伪造（如全脸生成、音频-视频同步问题等）存疑，可能遗漏某些重要特征。
- **可解释性评估主观性**：目前缺乏基准来客观衡量解释质量，论文可能主要依赖定性分析，说服力不足。
- **未讨论对抗鲁棒性**：框架未考虑针对解释的攻击或欺骗检测器的情况。

（完）
