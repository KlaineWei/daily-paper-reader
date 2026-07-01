---
title: "FakeShield: Explainable Image Forgery Detection and Localization via Multi-modal Large Language Models"
title_zh: "FakeShield: 基于多模态大语言模型的可解释图像伪造检测与定位"
authors: "Zhipei Xu, Xuanyu Zhang, Runyi Li, Zecheng Tang, Qing Huang, Jian Zhang"
date: 2025-01-22
pdf: "https://openreview.net/pdf?id=pAQzEY7M03"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释伪造检测与定位
tldr: 针对现有图像伪造检测方法黑盒特性及泛化能力有限的问题，提出FakeShield框架，利用多模态大语言模型实现可解释的图像伪造检测与定位，不仅评估图像真实性并生成篡改区域掩码，还提供基于像素级与图像级依据的判断理由，提升了可解释性和跨篡改方法的泛化能力。
source: ICLR-2025-Accepted
selection_source: conference_retrieval
motivation: 现有伪造检测方法存在黑盒特性且泛化能力有限，亟需可解释的检测方案。
method: 提出FakeShield框架，基于多模态大语言模型，联合评估图像真实性、生成篡改区域掩码并给出判断依据。
result: 实验表明该方法在多种篡改方式下具有良好检测性能和可解释性。
conclusion: FakeShield有效实现了可解释的图像伪造检测与定位，推动了可解释AI在伪造检测领域的应用。
---

## Abstract
The rapid development of generative AI is a double-edged sword, which not only facilitates content creation but also makes image manipulation easier and more difficult to detect. Although current image forgery detection and localization (IFDL) methods are generally effective, they tend to face two challenges: \textbf{1)} black-box nature with unknown detection principle, \textbf{2)} limited generalization across diverse tampering methods (e.g., Photoshop, DeepFake, AIGC-Editing). To address these issues, we propose the explainable IFDL task and design FakeShield, a multi-modal framework capable of evaluating image authenticity, generating tampered region masks, and providing a judgment basis based on pixel-level and image-level tampering clues. Additionally, we leverage GPT-4o to enhance existing IFDL datasets, creating the Multi-Modal Tamper Description dataSet (MMTD-Set) for training FakeShield's tampering analysis capabilities. Meanwhile, we incorporate a Domain Tag-guided Explainable Forgery Detection Module (DTE-FDM) and a Multi-modal Forgery Localization Module (MFLM) to address various types of tamper detection interpretation and achieve forgery localization guided by detailed textual descriptions. Extensive experiments demonstrate that FakeShield effectively detects and localizes various tampering techniques, offering an explainable and superior solution compared to previous IFDL methods. The code is available at https://github.com/zhipeixu/FakeShield.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有图像伪造检测与定位（IFDL）方法存在两个主要挑战：一是黑盒特性，检测原理不透明，缺乏可解释性；二是对不同篡改方式（如Photoshop、DeepFake、AIGC编辑）的泛化能力有限。
- **研究动机**：生成式AI的快速发展使得图像篡改变得更加容易且难以检测，急需一种既能准确检测和定位篡改区域，又能提供可解释判断依据的方法。
- **整体含义**：FakeShield旨在解决上述问题，推动可解释AI在伪造检测领域的应用，提升检测结果的可信度和跨场景泛化能力。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程（文字说明）
- **核心思想**：基于多模态大语言模型（MLLM），同时完成图像真实性评估、篡改区域掩码生成以及基于像素级和图像级线索的判断理由输出。
- **关键技术细节**：
  - **MMTD-Set**：利用GPT-4o增强现有IFDL数据集，构建多模态篡改描述数据集，用于训练FakeShield的篡改分析能力。
  - **DET-FDM（Domain Tag-guided Explainable Forgery Detection Module）**：域标签引导的可解释伪造检测模块，处理多种类型的篡改检测解释。
  - **MFLM（Multi-modal Forgery Localization Module）**：多模态伪造定位模块，在详细文本描述引导下实现精准的伪造定位。
- **算法流程（文字描述）**：
  1. 输入图像经过多模态编码器提取特征。
  2. 域标签引导的可解释检测模块根据图像内容判断是否被篡改，并生成像素级和图像级的篡改线索文字。
  3. 多模态伪造定位模块结合文字描述和图像特征，输出篡改区域掩码。
  4. 最终输出包括：真实性判断（真/假）、定位掩码、以及解释性文字（如篡改类型、边界特征等）。

### 3. 实验设计：数据集、基准、对比方法
- **数据集**：主要使用增强后的MMTD-Set（由GPT-4o注入篡改描述），可能包含传统篡改（Photoshop）、DeepFake、AIGC编辑等类型。
- **基准**：与现有IFDL方法进行对比，但未明确列出具体基准名称（如ManiDet、CAT-Net等），仅称“previous IFDL methods”。
- **对比方法**：未详细列举，但声称在多种篡改方式下有效，并优于前人方法。

### 4. 资源与算力
- 文中未明确说明使用的GPU型号、数量及训练时长，也未提及具体算力消耗信息。因此无法总结具体资源。

### 5. 实验数量与充分性
- **实验数量**：仅从摘要可知进行了“大量实验”（extensive experiments），包括不同篡改技术的检测与定位效果评估，未提及具体实验组数或消融实验设置。
- **充分性与公平性**：缺少具体数据、消融研究、可视化结果等细节，难以全面判断实验的充分性和客观性。但使用了GPT-4o增强数据集并设计了领域专用模块，可能在一定程度上保证了实验的针对性。由于未公开完整实验细节，公平性无法确认。

### 6. 论文的主要结论与发现
- FakeShield能够有效检测和定位多种篡改技术，相比先前IFDL方法提供了可解释性更强的解决方案。
- 多模态大语言模型结合域标签引导和细粒度定位模块，在提升泛化能力的同时保留了可解释性。
- 利用GPT-4o构建的MMTD-Set对训练篡改分析能力有积极作用。

### 7. 优点：方法或实验设计上的亮点
- **可解释性创新**：首次将多模态大语言模型用于IFDL，输出自然语言解释，打破了黑盒局限。
- **数据增强策略**：利用GPT-4o自动生成篡改描述，构建高质量多模态训练数据，降低人工标注成本。
- **模块化设计**：DET-FDM和MFLM分工明确，兼顾全局解释与细粒度定位，结构清晰。
- **泛化能力**：覆盖多种篡改类型（传统、深度伪造、AIGC编辑），比以往方法更全面。

### 8. 不足与局限
- **实验细节缺失**：未提供定量结果（如准确率、IOU等指标）、消融实验、对比方法的性能数据，无法充分评估方法的实际提升幅度。
- **算力与效率未说明**：多模态大模型通常计算成本高，但文中未讨论推理速度或资源消耗，可能限制实际部署。
- **数据偏置风险**：MMTD-Set基于GPT-4o生成，可能引入模型自身的偏见或错误，且未验证其与真实篡改场景的一致性。
- **应用限制**：仅针对图像伪造，未涉及视频、音频等其他模态；可解释性输出的可靠性和准确度尚需人工评估。

（完）
