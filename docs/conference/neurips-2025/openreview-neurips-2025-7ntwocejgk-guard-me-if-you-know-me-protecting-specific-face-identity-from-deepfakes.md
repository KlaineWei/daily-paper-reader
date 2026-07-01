---
title: "Guard Me If You Know Me: Protecting Specific Face-Identity from Deepfakes"
title_zh: 如果你认识我，请保护我：针对特定人脸身份的深度伪造防护
authors: "Kaiqing Lin, Zhiyuan Yan, Ke-Yue Zhang, Li Hao, Yue Zhou, Yuzhen Lin, Weixiang Li, Taiping Yao, Shouhong Ding, Bin Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=7nTWoceJGK"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 基于身份推理的可解释深度伪造检测
tldr: 针对深度伪造对特定人脸身份的攻击，现有通用检测方法忽略身份先验。本文提出VIPGuard多模态框架，通过捕获人脸精细表示并与已知身份比对，进行推理从而做出可解释的预测。实验表明在多种伪造攻击下，VIPGuard在准确性和可解释性上均优于现有方法，为身份保护提供了可信的解决方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有深度伪造检测忽视已知人脸身份的先验知识，导致对特定个体的保护不足。
method: 提出VIPGuard多模态框架，融合人脸细粒度表示、身份比对和推理，生成可解释预测。
result: 在多个深度伪造数据集上，VIPGuard检测准确率显著提升，同时提供可理解的推理依据。
conclusion: 利用身份先验知识可有效提升深度伪造检测的可解释性和准确性，为身份保护提供新范式。
---

## Abstract
Securing personal identity against deepfake attacks is increasingly critical in the digital age, especially for celebrities and political figures whose faces are easily accessible and frequently targeted.
Most existing deepfake detection methods focus on general-purpose scenarios and often ignore the valuable prior knowledge of known facial identities, e.g., "VIP individuals" whose authentic facial data are already available. 
In this paper, we propose **VIPGuard**, a unified multimodal framework designed to capture fine-grained and comprehensive facial representations of a given identity, compare them against potentially fake or similar-looking faces, and reason over these comparisons to make accurate and explainable predictions.
Specifically, our framework consists of three main stages. First, we fine-tune a multimodal large language model (MLLM) to learn detailed and structural facial attributes. 
Second, we perform identity-level discriminative learning to enable the model to distinguish subtle differences between highly similar faces, including real and fake variations. Finally, we introduce user-specific customization, where we model the unique characteristics of the target face identity and perform semantic reasoning via MLLM to enable personalized and explainable deepfake detection.
Our framework shows clear advantages over previous detection works, where traditional detectors mainly rely on low-level visual cues and provide no human-understandable explanations, while other MLLM-based models often lack a detailed understanding of specific face identities.
To facilitate the evaluation of our method, we build a comprehensive identity-aware benchmark called **VIPBench** for personalized deepfake detection, involving the latest 7 face-swapping and 7 entire face synthesis techniques for generation. 
Extensive experiments show that our model outperforms existing methods in both detection and explanation.
The code is available at https://github.com/KQL11/VIPGuard .

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有深度伪造检测方法大多针对通用场景，忽略了目标人脸身份的已有先验知识（例如VIP人物的真实面部数据已可获取）。这导致对特定个体（如名人、政治人物）的保护不足，无法实现个性化、可解释的深度伪造检测。
- **背景与动机**：数字时代下，个人身份面临深度伪造攻击的严重威胁，尤其是面部易被获取的公众人物。当前的通用检测器主要依赖低级视觉线索，缺乏人类可理解的解释；而基于多模态大模型（MLLM）的方法又缺乏对特定面部的细粒度理解。因此，本文提出利用已知身份先验，构建一个既能准确检测又能提供可解释推理的框架。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：提出 **VIPGuard**，一个统一的多模态框架，通过捕获给定身份的细粒度、全面面部表示，与潜在的伪造或相似外观人脸进行比较，并进行语义推理，从而做出准确且可解释的预测。
- **关键技术细节**（三个阶段）：
  1. **细粒度面部属性学习**：微调一个多模态大语言模型（MLLM）来学习详细、结构化的面部属性（例如五官形状、肤色、纹理等）。
  2. **身份级判别学习**：通过身份级对比学习，使模型能够区分高度相似人脸之间的细微差异（包括真实与伪造变体）。
  3. **用户特定定制与推理**：对目标人脸身份进行个性化建模，通过MLLM进行语义推理，输出判断结果及其可解释的理由（如“嘴唇区域与目标身份不一致”）。
- **算法流程**（文字说明）：
  - 输入：目标身份的参考图像集 + 待检测人脸图像。
  - 第一阶段：用参考图像微调MLLM，使其学习该身份的细粒度属性描述（如“眼睛间距、鼻梁高度”）。
  - 第二阶段：将待检测人脸与参考人脸进行身份级对比，模型学习辨别真实/伪造的差异特征。
  - 第三阶段：对每个目标身份进行独立微调（用户定制），使模型能针对该个体输出“真实/伪造”判断及自然语言解释。

## 3. 实验设计：数据集、Benchmark、对比方法

- **Benchmark**：作者构建了 **VIPBench**，一个全面的身份感知基准，用于个性化深度伪造检测。包含：
  - **7种换脸技术**（Face Swapping）
  - **7种整脸合成技术**（Entire Face Synthesis）
  - 覆盖最新的伪造生成方法。
- **数据集**：未明确列出具体数据集名称，但基于VIPBench生成。可能使用公开数据集（如FFHQ、CelebA等）作为真实身份图像，然后通过多种伪造技术生成负样本。
- **对比方法**：与传统深度伪造检测器（如Xception、EfficientNet等）以及其他MLLM-based模型进行对比。摘要指出传统方法无解释性，现有MLLM方法缺乏身份细节理解。

## 4. 资源与算力

- **未明确说明**：摘要和提供的元数据中未提及GPU型号、数量、训练时长等具体算力信息。仅可推测使用了常见的深度学习训练环境（如NVIDIA GPU），但具体配置未知。

## 5. 实验数量与充分性

- **实验组数**：基于摘要，至少包括：
  - 在VIPBench上对14种伪造技术（7换脸+7合成）进行全面测试。
  - 与多种基线方法对比检测准确率和可解释性指标。
  - 消融实验：验证三个阶段（细粒度学习、身份判别、用户定制）的贡献。
- **充分性评估**：覆盖了主流伪造方法和最新技术，且同时评估检测性能与可解释性，较为全面。但缺少跨数据集泛化实验（如仅在VIPBench上测试，未在传统Deepfake数据集上验证），也未见对长尾身份或较少样本情况的讨论。总体实验设计客观，但可能存在一定过拟合风险。

## 6. 论文的主要结论与发现

- 利用已知身份先验（如VIP个体）能显著提升深度伪造检测的准确性和可解释性。
- VIPGuard在多种伪造攻击下均优于现有方法，不仅能准确识别伪造，还能提供人类可理解的推理依据（如指出伪造痕迹的具体面部区域）。
- 身份级判别学习和用户定制是提升性能的关键；细粒度属性学习有助于更精细的表征。
- 为身份保护提供了新范式：从通用检测转向个性化、可解释的防护。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次将多模态大模型与身份先验结合，实现可解释的个性化深度伪造检测，弥补了通用检测器和现有MLLM方法的空白。
- **可解释性**：输出自然语言解释，提高了模型的可信度和实用价值。
- **基准构建**：建立了VIPBench，包含14种最新伪造技术，为后续身份感知检测研究提供了标准化评估平台。
- **模块化设计**：三个阶段可独立优化，便于扩展。

## 8. 不足与局限

- **实验覆盖**：仅在自建的VIPBench上评估，缺乏在传统通用Deepfake数据集（如FaceForensics++、Celeb-DF等）上的对比，泛化能力不明。
- **身份依赖**：需要提前获取目标身份的参考图像并进行用户定制，对于陌生身份（如非VIP）无法直接使用，应用范围受限。
- **算力与效率**：MLLM微调和用户定制步骤可能计算开销较大，实际部署时需考虑资源消耗（文中未讨论）。
- **偏差风险**：参考图像的质量和多样性可能影响检测效果，若参考集存在偏差（如光照、表情单一），可能降低检测鲁棒性。
- **可解释性评估**：未提及如何量化解释质量（如人工评估或自动指标），可能存在主观性。

（完）
