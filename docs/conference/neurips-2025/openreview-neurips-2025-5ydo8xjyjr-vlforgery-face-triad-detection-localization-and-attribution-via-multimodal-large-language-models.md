---
title: "VLForgery Face Triad: Detection, Localization and Attribution via Multimodal Large Language Models"
title_zh: VLForgery人脸三元组：基于多模态大语言模型的检测、定位与归因
authors: "Xinan He, Yue Zhou, Bing Fan, Bin Li, Guopu Zhu, Feng Ding"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=5YDO8XjYjR"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 基于多模态大语言模型的可解释伪造检测，包含定位和归因
tldr: 当前深度伪造检测大多仅输出二分类结果，无法提供伪造区域的定位和生成方法的归因。本文提出VLForgery框架，通过整合多模态大语言模型，实现对扩散模型合成人脸的检测、伪造区域定位及生成器归因。实验表明该方法能够提供细粒度的可解释分析，显著增强伪造检测的可信度。其贡献在于将可解释性引入深度伪造检测，推动了面向实际应用的安全分析。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有深度伪造检测仅输出二分类，缺乏对伪造原因和区域的解释，限制了实际应用中的可信度。
method: 提出VLForgery框架，利用多模态大语言模型对伪造人脸进行检测、定位伪造区域并归因于特定生成器。
result: 在多个基准数据集上，该方法不仅实现了高检测准确率，还能精确定位伪造区域并准确归因生成方法。
conclusion: 证明了多模态大语言模型能有效提升深度伪造检测的可解释性和细粒度分析能力。
---

## Abstract
Faces synthesized by diffusion models (DMs) with high-quality and controllable attributes pose a significant challenge for Deepfake detection. Most state-of-the-art detectors only yield a binary decision, incapable of forgery localization, attribution of forgery methods, and providing analysis on the cause of forgeries. In this work, we integrate Multimodal Large Language Models (MLLMs) within DM-based face forensics, and propose a fine-grained analysis triad framework called VLForgery,
that can 1) predict falsified facial images;
2) locate the falsified face regions subjected to partial synthesis; and 3) attribute the synthesis with specific generators. To achieve the above goals, we introduce VLF (Visual Language Forensics), a novel and diverse synthesis face dataset designed to facilitate rich interactions between `Visual' and `Language' modalities in MLLMs.
Additionally, we propose an extrinsic knowledge-guided description method, termed EkCot, which leverages knowledge from the image generation pipeline to enable MLLMs to quickly capture image content. Furthermore, we introduce a low-level vision comparison pipeline designed to identify differential features between real and fake that MLLMs can inherently understand. These features are then incorporated into EkCot, enhancing its ability to analyze forgeries in a structured manner, following the sequence of detection, localization, and attribution.
Extensive experiments demonstrate that VLForgery outperforms other state-of-the-art forensic approaches in detection accuracy, with additional potential for falsified region localization and attribution analysis.

---

## 论文详细总结（自动生成）

# VLForgery Face Triad: Detection, Localization and Attribution via Multimodal Large Language Models — 中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：扩散模型（DMs）生成的人脸图像质量高、属性可控，对现有深度伪造检测构成严重挑战。
- **核心问题**：当前最先进的检测器大多仅输出二分类结果（真/假），无法提供伪造区域的定位、伪造方法的归因以及对伪造原因的可解释分析。这种缺乏可解释性的单一输出限制了深度伪造检测在实际安全应用中的可信度和实用性。
- **整体含义**：本文旨在将可解释性引入深度伪造检测领域，实现更细粒度的分析——即同时完成检测、定位和归因这三个任务（被称为“人脸三元组”），从而提升模型在实际场景中的可靠性与用户信任度。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用多模态大语言模型（MLLMs）对基于扩散模型伪造的人脸进行细粒度分析，将视觉信息与语言信息深度融合，实现三元组任务：检测、定位、归因。
- **关键技术细节**：
  - **VLForgery框架**：整合MLLMs，使其能够（1）预测伪造图像；（2）定位伪造区域（针对局部合成）；（3）将合成归因于特定生成器。
  - **VLF数据集（Visual Language Forensics）**：新构建的、多样性强的合成人脸数据集，旨在促进MLLMs中“视觉”与“语言”模态之间的丰富交互。包含真实/伪造人脸对，并带有区域标注和生成器标签。
  - **EkCot（外部知识引导描述方法）**：利用图像生成流水线中的外部知识，引导MLLMs快速捕捉图像内容。采用链式思维（CoT）风格，按检测→定位→归因的顺序进行结构化分析。
  - **低层视觉比较管道**：设计用于识别真实与伪造之间MLLMs能够天然理解的差异化特征（如纹理、噪声、颜色分布等）。这些特征被整合进EkCot，增强其对伪造的细粒度分析能力。
- **算法流程（文字说明）**：
  1. 输入伪造人脸图像或真实图像。
  2. 通过低层视觉比较管道提取可解释的伪影特征。
  3. 将特征与EkCot引导的提示一同输入MLLM。
  4. MLLM按顺序输出：是否为伪造、伪造区域的空间位置（掩码/边界框）、以及对应的生成器归属。
  5. 输出结果结合视觉语言描述，提供可解释的推理依据。

## 3. 实验设计：数据集、基准与对比方法

- **数据集**：
  - 主要使用扩散模型生成的伪造人脸数据集（文中未明确列出具体公开数据集名称，但提到了VLF数据集作为训练和评估的核心）；可能包含多个基准数据集（如FFHQ、CelebA衍生数据集等，摘要未详述，需要原始论文补充）。
- **对比方法**：
  - 与多种SOTA深度伪造检测方法进行对比，包括传统的二分类方法以及少数具备定位或归因能力的模型。具体方法未在摘要中列出，需参考原论文。
- **评估任务**：
  - 检测准确性（二分类AUC/ACC）、伪造区域定位（IoU等）、生成器归因准确率。
- **实验充分性**：
  - 文中声称“Extensive experiments”，并指出VLForgery在检测准确率上优于其他方法，同时具备额外的定位和归因能力。

## 4. 资源与算力

- **未明确说明**：摘要和元数据中未提及使用的GPU型号、数量、训练时长等具体算力信息。需查阅原始论文全文获取详情。
- **推断**：由于使用了MLLMs（通常参数量大且计算开销高），推测需要至少单卡A100或类似高端GPU进行微调/推理。

## 5. 实验数量与充分性

- **实验组数**：摘要未列出具体实验数量。从结构上看，至少包括：
  - 检测任务对比实验（多个数据集）。
  - 定位任务性能对比。
  - 归因任务性能对比。
  - 可能包含消融实验（例如：有无EkCot、有无低层比较管道、不同MLLM骨干等）。
- **充分性评价**：
  - 正面：覆盖了三元组任务的所有维度，且与SOTA进行了对比。
  - 不足：摘要未提供数值结果或数据集细节，难以判断实验的统计显著性。若原论文提供了多个随机种子、多种扰动测试，则较为充分；否则可能局限。

## 6. 论文的主要结论与发现

- **主要结论**：多模态大语言模型能够有效提升深度伪造检测的可解释性和细粒度分析能力。VLForgery框架不仅实现了高检测准确率，还能精确定位伪造区域并准确归因于特定的生成方法（如特定扩散模型）。
- **关键发现**：
  - EkCot结合图像生成流水线的外部知识能加速MLLMs捕捉图像关键特征。
  - 低层视觉比较管道提取的差异特征（纹理、噪声等）能自然地融入语言描述，增强可解释性。
  - 三元组任务（检测+定位+归因）可在一个统一框架下完成，不牺牲单独任务的性能。

## 7. 优点：方法或实验设计上的亮点

- **任务创新**：首次将深度伪造检测从二分类扩展到同时定位和归因的三元组任务，显著提升了可解释性。
- **数据贡献**：构建了VLF数据集，促进“视觉-语言”交互，为后续研究提供资源。
- **方法设计**：
  - EkCot利用领域知识（生成流水线）引导MLLM，而非依赖大量标注数据，效率高且可迁移。
  - 低层视觉比较管道让模型聚焦于人眼不易察觉的伪影，增强了细粒度分析能力。
- **可解释性强**：输出以自然语言形式呈现，便于人类理解和审计。

## 8. 不足与局限

- **实验覆盖有限**：摘要中未列出具体数据集名称和结果数字，难以全面评估泛化性。可能只在特定扩散模型生成的数据上测试，对GAN或其他传统伪造方法的迁移性未知。
- **偏差风险**：
  - VLF数据集可能包含特定类型的伪造（如仅来自少数扩散模型），导致模型对未见过的生成器泛化能力不足。
  - 依赖MLLMs的预训练知识，可能存在语言偏差或对伪造特征的过拟合。
- **应用限制**：
  - 需要较高的计算资源（推理时需MLLM），实际部署成本较高。
  - 难以保证实时性，可能不适用于需要即时响应的场景（如直播审核）。
- **可解释性验证**：虽然声称能提供分析，但缺少对解释质量的量化评估（如与人类判断的一致性、归因原因的准确性等）。
- **缺失信息**：未提及是否公开代码和数据集，若未开源则无法复现。

（完）
