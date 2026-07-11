---
title: "So-Fake: Benchmarking Social Media Image Forgery Detection"
title_zh: So-Fake：社交媒体图像伪造检测基准
authors: "Zhenglin Huang, Tianxiao Li, Xiangtai Li, Haiquan Wen, Yiwei He, Jiangning Zhang, Hao Fei, Xi Yang, Baoyuan Wu, Xiaowei Huang, Bei Peng, Guangliang Cheng"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=frqg27qMkd"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 包含可解释性评估的伪造检测基准
tldr: 本文介绍So-Fake，一个面向社交媒体的图像伪造检测基准。包含大规模数据集So-Fake-Set和评估协议，首次在基准中纳入可解释性和域外泛化评估。旨在推动可解释伪造检测的发展。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有伪造检测数据集缺乏多样性和可解释性评估。
method: 构建大规模社交媒体伪造检测数据集并设计包含解释评估的协议。
result: 该基准为可解释伪造检测提供了标准化评估平台。
conclusion: So-Fake推动了对伪造检测可解释性的研究。
---

## Abstract
Recent advances in AI-powered generative models have enabled the creation of increasingly realistic synthetic images, posing significant risks to information integrity and public trust on social media platforms. While robust detection frameworks and diverse, large-scale datasets are essential to mitigate these risks, existing academic efforts remain limited in scope: current datasets lack the diversity, scale, and realism required for social media contexts, and evaluation protocols rarely account for explanation or out-of-domain generalization.
To bridge this gap, we introduce \textbf{So-Fake}, a comprehensive social media-oriented dataset for forgery detection consisting of two key components. First, we present \textbf{So-Fake-Set}, a large-scale dataset with over \textbf{2 million} photorealistic images from diverse generative sources, synthesized using a wide range of generative models. Second, to rigorously evaluate cross-domain robustness, we establish \textbf{So-Fake-OOD}, a novel and large-scale (\textbf{100K}) out-of-domain benchmark sourced from real social media platforms and featuring synthetic imagery from commercial models explicitly excluded from the training distribution, creating a realistic testbed that mirrors actual deployment scenarios. Leveraging these complementary datasets, we present \textbf{So-Fake-R1}, a baseline framework that applies reinforcement learning to encourage interpretable visual rationales. Experiments show that So-Fake surfaces substantial challenges for existing methods. By integrating a large-scale dataset, a realistic out-of-domain benchmark, and a multi-dimensional evaluation protocol, So-Fake establishes a new foundation for social media forgery detection research.

---

## 论文详细总结（自动生成）

# So-Fake：社交媒体图像伪造检测基准

## 1. 核心问题与整体含义（研究动机与背景）

- **问题**：AI生成模型（如扩散模型、GAN等）使得合成图像越来越逼真，对社交媒体平台的信息真实性和公众信任构成严重威胁。现有伪造检测研究存在两大局限：一是数据集缺乏多样性、规模和现实性，无法反映社交媒体真实场景；二是评估协议很少考虑可解释性（explanation）或域外泛化（out-of-domain generalization），导致检测方法的鲁棒性和实用性不足。
- **整体含义**：本文旨在填补社交媒体图像伪造检测领域的基准空白，通过构建大规模、多样化、包含可解释性评估的基准，推动该领域向更实用、更可靠的方向发展。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：构建一个面向社交媒体的综合伪造检测基准，包含三个关键组件：
  1. **So-Fake-Set**：大规模数据集，包含超过200万张来自多种生成模型的逼真图像，覆盖广泛的生成源。
  2. **So-Fake-OOD**：新颖的大规模域外（OOD）基准，包含10万张图像，来源于真实社交媒体平台，并采用从训练分布中明确排除的商业模型生成的合成图像，模拟实际部署场景。
  3. **So-Fake-R1**：一个基线框架，应用强化学习（Reinforcement Learning）来鼓励生成可解释的视觉理由（interpretable visual rationales），从而提升检测的可解释性。
- **关键技术细节**：
  - 数据集构建：收集来自不同生成模型（如扩散模型、GAN等）的合成图像，并确保真实图像的来源多样性；OOD基准特别选用商业模型（如Midjourney、DALL·E等）生成的图像，以测试跨域泛化能力。
  - 评估协议：除了传统的二分类检测准确率等指标，还引入可解释性评估和域外泛化评估，形成多维度评估体系。
  - So-Fake-R1：将强化学习应用于伪造检测任务，通过奖励机制引导模型在给出检测结果的同时，给出可解释的区域或特征，增强模型的可信度。

## 3. 实验设计：数据集、基准与方法对比

- **数据集与场景**：
  - 训练集：So-Fake-Set（200万+图像），内包含多种生成源（扩散、GAN等）的合成图像与真实图像。
  - 域外测试集：So-Fake-OOD（10万图像），来源于真实社交媒体平台，且生成模型为训练中未见过的商业模型。
  - 评估场景：包括域内测试（在So-Fake-Set划分的测试集上）和域外泛化测试（在So-Fake-OOD上），以及可解释性评估（需要额外标注或人工评价）。
- **基准方法**：文中提到“existing methods”，但未具体列出对比方法名称。根据摘要，实验表明现有方法在So-Fake上遇到显著挑战，暗示可能对比了多种传统检测方法和最新深度伪造检测方法。
- **实验设计**：采用多维度评估协议，但未提供具体指标细节（如AUC、准确率、F1、解释性指标等）。推测实验包括：分类准确率、OOD泛化性能、可解释性质量（如注意力图与真实伪造区域的一致性）。

## 4. 资源与算力

- **文中未明确说明使用的GPU型号、数量、训练时长等算力信息**。仅提到构建了包含200万+图像的数据集和基线框架So-Fake-R1，但未披露训练该基线所需的计算资源。若进行基准测试，推测需要大规模GPU集群，但论文在此部分未做说明。

## 5. 实验数量与充分性

- **实验数量**：由于仅提供摘要，无法得知具体实验组数。但根据描述，至少包含以下实验：
  - 在So-Fake-Set上的域内检测性能评估。
  - 在So-Fake-OOD上的域外泛化评估。
  - 可解释性评估（可能包括对比有无RL解释的变体）。
  - 可能还包含消融实验（如不同生成源的影响、不同backbone的影响等）。
- **充分性与公平性**：从基准构建角度看，So-Fake-Set和So-Fake-OOD的规模与多样性优于现有数据集，为公平比较提供了基础。但未提供具体对比方法的来源和实现细节，难以判断对比是否公平（如是否采用了统一训练流程、超参数等）。此外，缺少对基线So-Fake-R1与现有解释方法的对比细节，实验完整性有待原文补充。

## 6. 主要结论与发现

- **主要结论**：
  - So-Fake基准为现有伪造检测方法带来了显著挑战，表明现有方法在多源、社交媒体真实场景和域外泛化方面表现不佳。
  - 通过集成大规模数据集、真实域外基准和多维度评估协议，So-Fake为社交媒体伪造检测研究建立了新基础。
  - So-Fake-R1基线表明，利用强化学习可以鼓励模型生成可解释的视觉理由，但该基线本身仍有很多改进空间（暗示当前方法在So-Fake上准确率等指标并不高）。

## 7. 优点（方法与实验设计亮点）

1. **数据集规模与多样性**：So-Fake-Set达200万+图像，来自多种生成模型，覆盖广泛，显著超过现有伪造检测数据集（如FaceForensics++、DFDC等通常仅几十万张或更少，且来源单一）。
2. **域外泛化评估**：专门构建So-Fake-OOD基准（10万张），使用训练中未见过的商业模型图像，模拟真实部署场景，弥补了现有基准缺乏OOD评估的不足。
3. **可解释性纳入评估**：首次在伪造检测基准中引入可解释性要求，推动研究从“黑箱检测”向“可解释检测”发展，提升实际可信度。
4. **基线框架创新**：应用强化学习生成视觉理由，为可解释伪造检测提供了一种新思路，且与基准配套发布，方便后续研究对比。
5. **面向社交媒体**：数据来源和场景设计贴近社交媒体真实环境（如低质量、压缩、多平台），实用性强。

## 8. 不足与局限

1. **实验细节缺失**：当前仅提供摘要，缺乏完整的实验设置、对比方法、指标定义、显著性分析等，无法全面评估方法的性能与复现性。
2. **可解释性评估标准不明确**：如何量化“视觉理由”的质量未说明，可能依赖人类标注或特定指标（如IoU、可解释性分数），但未在摘要中提及，存在评估偏差风险。
3. **基线So-Fake-R1性能未知**：未给出具体检测准确率或OOD结果，难以判断该基线是否具有竞争力。若效果不佳，可能削弱基准的参考价值。
4. **数据集偏差**：尽管来源多样，但合成图像和真实图像的分布仍可能与现实社交媒体数据存在差异（如用户上传场景、分辨率、后期处理等），OOD基准仅针对生成模型，未覆盖其他域外因素（如不同平台、不同内容类型）。
5. **计算资源未披露**：大规模数据集和强化学习训练需要大量GPU，未公开算力不利于其他研究者复现和评估成本。
6. **缺乏与最新方法的全面对比**：未列出对比的具体方法和结果，无法判断So-Fake相比现有基准的挑战程度是否客观。

（完）
