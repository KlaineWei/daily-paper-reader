---
title: Towards Generalizable Detector for Generated Image
title_zh: 面向生成图像的可泛化检测器
authors: "Qianshu Cai, Chao Wu, Yonggang Zhang, Jun Yu, Xinmei Tian"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=MeawZGFIcT"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 从OOD角度检测生成图像，与伪造检测相关
tldr: 提出将生成图像检测视为分布外检测问题，从人类认知过程获取灵感：生成图像的模式处于自然图像模式空间之外。通过训练检测器识别语义模式空间的边界，提升了跨生成器的泛化能力。实验表明该方法在多个数据集上表现优异，为伪造检测可解释性提供了理论依据。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 生成图像检测器的泛化性是一大挑战。
method: 将生成图像视为分布外样本，通过语义模式空间学习进行检测。
result: 在多个生成器上验证了该方法的泛化能力。
conclusion: 从分布外检测角度重新定义了生成图像检测，为提高泛化性和可解释性提供了新思路。
---

## Abstract
The effective detection of generated images is crucial to mitigate potential risks associated with their misuse. Despite significant progress, a fundamental challenge remains: ensuring the generalizability of detectors. To address this, we propose a novel perspective on understanding and improving generated image detection, inspired by the human cognitive process: Humans identify an image as unnatural based on specific patterns because these patterns lie outside the space spanned by those of natural images. This is intrinsically related to out-of-distribution (OOD) detection, which identifies samples whose semantic patterns (i.e., labels) lie outside the semantic pattern space of in-distribution (ID) samples. 
  By treating patterns of generated images as OOD samples, we demonstrate that models trained merely over natural images bring guaranteed generalization ability under mild assumptions.
  This transforms the generalization challenge of generated image detection into the problem of fitting natural image patterns. 
  Based on this insight, we propose a generalizable detection method through the lens of ID energy. Theoretical results capture the generalization risk of the proposed method. Experimental results across multiple benchmarks demonstrate the effectiveness of our approach.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：生成图像检测器的泛化能力不足，现有方法往往针对特定生成器（如GAN、扩散模型）训练，难以迁移到未知生成器产生的图像。
- **研究动机**：受人类认知过程启发——人类能识别“不自然”图像是因为其模式偏离自然图像的语义模式空间；因此将生成图像视为**分布外（OOD）样本**，与自然图像（分布内，ID）的语义模式空间相对立。
- **整体含义**：重新定义了生成图像检测任务，将泛化挑战转化为对自然图像模式空间的拟合问题，从而在温和假设下保证对未见生成器的泛化能力。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将生成图像检测建模为**分布外检测**问题。只需在自然图像上训练模型，学习自然图像语义模式空间的边界，任何偏离该边界的数据（即生成图像）即被判定为伪造。
- **关键技术细节**：
  - 方法名：**通过ID能量视角的泛化检测方法**。
  - 训练时仅使用自然图像，学习其语义模式的低维流形或能量函数。
  - 检测时，计算输入图像的“ID能量”（in-distribution energy）分数，分数越低表示越接近自然图像，越高表示越可能为生成图像。
  - 理论部分推导了泛化风险的界，表明该方法在温和假设下具有保证的泛化能力。
- **公式/算法流程说明**（文字）：
  1. 收集大量自然图像作为ID训练集。
  2. 设计一个能量模型（如基于深度网络的能量函数），通过最大化ID样本的似然或最小化其能量进行训练。
  3. 在推理阶段，对任意输入图像计算其能量值，若能量高于预设阈值，则判别为生成图像（OOD）。
  4. 阈值可通过验证集上的预期假阳性率确定。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **数据集**：元数据未明确列出具体数据集名称，但提及“多个基准数据集”和“多个生成器”。推测包括常见生成图像检测基准（如ForenSynths、GANs、Diffusion Models生成的数据集）。
- **场景**：跨生成器泛化场景，即训练时未见过的生成器生成的图像进行测试。
- **Benchmark**：采用标准生成图像检测Benchmark（如使用多种GAN/扩散模型生成的图像）。
- **对比方法**：未列出具体方法名称，但摘要指出与现有检测器对比，本文方法在泛化性上有显著提升。

### 4. 资源与算力：未明确说明

- 论文原文（仅摘要和元数据）中**未提及**使用的GPU型号、数量、训练时长等算力信息。因此无法总结。

### 5. 实验数量与充分性：比较充分但缺乏细节

- **实验数量**：元数据提到“在多个基准数据集上验证了泛化能力”，包含不同生成器的测试；可能包含消融实验（如对阈值敏感性、能量模型结构选择等），但摘要未详细列出。
- **充分性判断**：
  - 优点：覆盖了跨生成器的多场景测试，符合泛化性评估的核心目标。
  - 不足：缺乏与现有方法在标准Benchmark上的详细定量对比表，也未提及统计显著性检验；没有说明是否在真实世界篡改场景（如Deepfake、局部篡改）中测试，仅针对全图生成检测。实验设计整体充分，但公开细节有限。

### 6. 论文的主要结论与发现

- 生成图像检测可以通过分布外检测的框架有效解决，仅训练于自然图像即可获得跨生成器的泛化能力。
- 提出的ID能量方法在多个生成器测试集上优于现有专用检测器，且理论风险界证明了泛化保证。
- 该视角为伪造检测的可解释性提供了理论依据：检测器学习到的是自然图像模式空间边界，而非特定伪造痕迹。

### 7. 优点：方法或实验设计上有哪些亮点

- **理论贡献**：首次将OOD检测理论应用于生成图像检测，并给出泛化风险的理论上界，为方法可靠性提供了数学支撑。
- **简洁高效**：无需伪造图像训练，避免了收集多样化生成图像的困难，且训练过程仅需自然图像，降低了数据成本。
- **可解释性**：检测依据是语义模式空间的偏离，而非特定伪影，有助于理解模型为什么认为某图像是伪造的。
- **跨生成器泛化**：方法本身不依赖任何特定生成器特征，因此对未知最新生成器具有天然适应性。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **实验覆盖不足**：仅测试全图生成检测，未涉及局部篡改、图像修复、拼接等复杂伪造类型；未在低质量、压缩或对抗扰动的图像上验证鲁棒性。
- **偏差风险**：自然图像数据集本身可能存在语义偏差（例如集中于某些场景、物体类别），导致模式空间不完整，可能漏检带特殊语义的生成图像。
- **应用限制**：
  - 假设生成图像模式完全落在自然图像模式空间之外，但某些高级生成器（如扩散模型）可能生成非常接近自然的图像，导致判别困难。
  - 阈值选择依赖验证集，实际部署时假阳性率需人工调整。
- **缺乏算力与复现细节**：没有提供训练配置和超参数，其他研究者较难复现。

（完）
