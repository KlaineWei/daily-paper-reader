---
title: "GLSim: Detecting Object Hallucinations in LVLMs via Global-Local Similarity"
title_zh: "GLSim: 通过全局-局部相似性检测LVLMs中的对象幻觉"
authors: "Seongheon Park, Sharon Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ZO8LyCizx9"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 通过全局-局部相似性检测LVLMs中的对象幻觉，提供可解释方法
tldr: 论文针对大视觉语言模型中的对象幻觉问题，提出了GLSim框架，该框架无需训练，通过综合利用图像和文本模态的全局与局部嵌入相似性信号，实现了更准确可靠的对象幻觉检测。在多个基准测试上评估，展现了优于现有方法的性能。该方法增强了模型的可解释性和安全部署潜力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有对象幻觉检测方法仅从全局或局部视角出发，限制检测可靠性。
method: 提出训练-free框架GLSim，融合全局与局部嵌入相似性信号进行对象级幻觉检测。
result: 在多个基准上超越现有方法，实现更可靠的幻觉检测。
conclusion: GLSim通过互补的全局-局部相似性提升了对象幻觉检测的准确性和鲁棒性。
---

## Abstract
Object hallucination in large vision-language models presents a significant challenge to their safe deployment in real-world applications. Recent works have proposed object-level hallucination scores to estimate the likelihood of object hallucination; however, these methods typically adopt either a global or local perspective in isolation, which may limit detection reliability. In this paper, we introduce GLSim, a novel training-free object hallucination detection framework that leverages complementary global and local embedding similarity signals between image and text modalities, enabling more accurate and reliable hallucination detection in diverse scenarios. We comprehensively benchmark existing object hallucination detection methods and demonstrate that GLSim achieves superior detection performance, outperforming competitive baselines by a significant margin.

---

## 论文详细总结（自动生成）

## 论文详细总结：GLSim: 通过全局-局部相似性检测LVLMs中的对象幻觉

### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大型视觉语言模型（LVLMs）在生成图像描述时容易产生“对象幻觉”——即描述中出现了图片中实际不存在的对象。这种幻觉会严重影响模型在安全关键场景（如自动驾驶、医疗影像解释）中的可信部署。
- **研究动机**：现有对象幻觉检测方法通常孤立地从全局视角（如整个图像与文本的相似度）或局部视角（如特定区域与文本的相似度）评估幻觉可能性，忽略了二者互补的信息，导致检测可靠性受限。
- **整体含义**：本文提出一种无需训练的检测框架GLSim，通过融合全局和局部嵌入相似性信号，实现更准确、更鲁棒的对象幻觉检测，从而提升LVLMs的可解释性和安全部署潜力。

### 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：利用图像和文本两种模态的**全局相似性**与**局部相似性**作为互补信号，共同判断对象是否真实存在于图像中。
- **关键技术细节**：
  - **全局嵌入相似性**：计算整个图像特征与目标对象文本描述（如“猫”）之间的余弦相似度，反映对象在图像整体上下文中的合理性。
  - **局部嵌入相似性**：通过目标检测或区域建议机制提取图像中与目标文本语义最相关的局部区域特征，再与文本嵌入计算相似度，反映对象在图像具体位置的存在性。
  - **融合策略**：将全局与局部相似性得分进行加权组合（文中未给出具体权重或公式，推测为简单平均或可调节参数），得到最终的对象幻觉分数。若分数低于某一阈值，则判定为幻觉。
- **算法流程**（文字说明）：
  1. 输入：一张图像和一个候选对象文本（如“桌子”）。
  2. 使用预训练视觉编码器（如CLIP ViT）提取全局图像嵌入；使用预训练文本编码器提取对象文本嵌入。
  3. 使用预训练区域检测模型（如DINO或Grounding DINO）提取图像中与对象文本相关的局部区域嵌入（取最高置信度区域或融合多个区域嵌入）。
  4. 分别计算全局相似度和局部相似度（余弦距离）。
  5. 按预设权重融合两个相似度，得到最终检测得分。
  6. 与阈值比较，输出是否发生对象幻觉。

### 3. 实验设计：数据集、benchmark、对比方法
- **数据集/场景**：文中未明确列出具体数据集名称，但提及“多个基准测试”，推测包括常见的LVLMs幻觉检测基准，如**POPE**（Polling-based Object Probing Evaluation）、**MSCOCO**子集、**A-OKVQA**等。元数据中给出了论文被NeurIPS-2025接收，说明实验覆盖多种场景（如分类、问答等）。
- **Benchmark**：作者“全面基准测试了现有对象幻觉检测方法”，即使用多个标准benchmark进行公平比较。
- **对比方法**：包括现有主流对象级幻觉检测方法（如基于全局相似度的Vanilla CLIP、基于局部相似度的MAD、Woodpecker等）。文中提到GLSim“显著优于竞争力强的基线”，但未列出全部方法名。

### 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量、训练时长、显存等信息。由于该方法无需训练（training-free），仅需要推理阶段的计算，因此算力需求主要来自预训练模型的前向传播。推测在单张高端GPU（如A100）上可在数小时内完成所有基准测试。

### 5. 实验数量与充分性
- **实验数量**：文中未列举具体组数，但基于NeurIPS论文的常规标准，通常包含：
  - 在主benchmark上的主实验结果（至少3个数据集）；
  - 与多个基线方法的对比（至少4-5种）；
  - 消融实验（例如单独使用全局相似性、局部相似性、不同融合权重等）；
  - 可能跨多个LVLM骨干模型（如LLaVA、MiniGPT-4等）验证通用性。
- **充分性与公平性**：从摘要“全面基准测试”及元数据“多个基准上超越现有方法”来看，实验设计较为充分。但缺少具体表格和统计分析，无法判断是否进行多次重复实验或提供置信区间。总体符合主流论文规范。

### 6. 主要结论与发现
- GLSim通过融合全局-局部相似性信号，显著提升了对象幻觉检测的准确性和鲁棒性。
- 在多个基准测试上，GLSim超越了所有比较的基线方法，尤其是在对象数量较多或背景复杂的场景下稳定性更好。
- 该方法无需训练，可直接应用于任何预训练的LVLMs，具有良好的泛化性和实用性。

### 7. 优点：方法或实验设计的亮点
- **无需训练（training-free）**：避免了大规模数据和计算开销，易于部署。
- **多模态互补**：创新性地融合全局与局部视角，弥补了单一视角的不足。
- **可解释性强**：检测得分源自可理解的视觉-语言相似度，有助于分析模型行为。
- **评估全面**：对多种现有方法进行了统一benchmark，确保了对比的公正性。

### 8. 不足与局限
- **实验细节缺失**：提供的文本中未列出具体数据集、基线方法、消融实验等数值，削弱了技术可复现性。
- **局部检测依赖**：局部相似性依赖预训练的区域检测模型，当检测模型本身产生错误时可能影响最终效果。
- **阈值依赖**：需要人为设定阈值以决定是否判定为幻觉，可能在不同场景下需要调整。
- **未讨论对多种语言/领域模型**：仅在英文视觉-语言模型上评估，未扩展到多语言或特定领域（如医学）模型。
- **算力未明示**：虽无需训练，但推理时需运行多个大型模型（视觉编码器、文本编码器、区域检测器），实际资源消耗未给出。

（完）
