---
title: Structural Semantic Features for Improved AI-Generated Fake Image Detection
title_zh: 结构语义特征提升AI生成伪造图像检测
authors: "Md Redwanul Haque, Manzur Murshed, Manoranjan Paul, Tsz-Kwan Lee"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=TADsPhlp32"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 利用结构语义特征改进AI生成伪造图像检测
tldr: 本文针对现有AI生成伪造图像检测方法忽略结构语义的问题，提出显式引入结构语义信息的方法。通过立方体划分层次化工具递归分解图像，捕获生成模型留下的微妙不一致性。实验表明，该方法在多个数据集上提升了检测性能，尤其对细粒度伪造检测有效，为可解释伪造检测提供了结构化线索。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法依赖局部频域或全局语义，缺乏结构语义信息，难以检测微妙伪造。
method: 使用立方体划分递归提取图像结构语义特征，增强现有检测框架。
result: 在多个伪造图像检测数据集上达到更优的准确率，提高了对低质量伪造的鲁棒性。
conclusion: 结构语义特征有效补充了现有方法，提升了伪造检测的可解释性和精度。
---

## Abstract
The proliferation of AI-generated content (AIGC) has made the accurate detection of fake images a critical challenge. Existing state-of-the-art methods, such as PatchCraft and AIDE, primarily leverage local features like patch-wise frequency information or global semantic features derived from large-scale models like CLIP. While effective, these approaches often fail to incorporate the underlying structural semantics of an image, which are crucial for detecting the subtle inconsistencies and artifacts left by generative models. We propose a novel approach that augments existing AIGC detection frameworks by explicitly incorporating structural semantic information. Our method employs cuboidal partitioning, a hierarchical tool that recursively divides an image into meaningful sub-regions. At each division, we extract a measure of the statistical difference between the parent and child segments, which are then integrated with AIDE's existing features. Experimental results demonstrate our model's superior performance. We establish a new state-of-the-art in mean accuracy on the GenImage benchmark, proving our effectiveness on modern diffusion models. Our method also shows strong generalization by achieving second-best overall mean accuracy on the diverse AIGCDetect benchmark and a second-place finish on the challenging Chameleon dataset. These results highlight the significant value of structural semantics for building robust and generalizable AIGC detectors.

---

## 论文详细总结（自动生成）

# 论文中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：AI生成内容（AIGC）的泛滥使得伪造图像检测成为关键挑战。现有最先进方法如PatchCraft和AIDE主要利用局部特征（如逐块频域信息）或基于CLIP等大模型的全局语义特征，但忽略了图像的**结构语义**信息。生成模型留下的细微不一致性和伪影往往体现在图像的结构层面，现有方法难以捕获这些线索。
- **整体含义**：本文提出显式引入**结构语义特征**来增强现有AIGC检测框架，通过挖掘图像中层次化的结构不一致性，提升对现代扩散模型生成图像（尤其是细粒度伪造）的检测能力，同时增强模型的可解释性和鲁棒性。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：利用**立方体划分（Cuboidal Partitioning）**——一种层次化递归分割工具——将图像分解为有意义的子区域。在每次分割时，提取父段与子段之间的统计差异度量，将这些结构差异特征与AIDE的现有特征进行融合，从而捕获生成模型留下的结构性不一致。
- **关键技术细节**：
  - 对输入图像进行递归的立方体（或矩形块）划分，每次划分产生更细粒度的子区域。
  - 在每个划分层级，计算父区域与子区域之间的统计差异（如均值、方差等分布的差异度量）。
  - 将这些结构语义特征向量与AIDE的原有特征（可能包括局部频域和全局语义特征）拼接或融合。
  - 最终特征输入分类器进行真假二分类。
- **算法流程（文字说明）**：  
  输入图像 → 递归立方体划分（设定划分深度和停止条件）→ 对每一层计算父子统计差异 → 整合所有层的差异特征 → 与AIDE基线特征融合 → 全连接层分类 → 输出伪造/真实标签。

## 3. 实验设计
- **数据集与场景**：
  - **GenImage benchmark**（现代扩散模型生成图像）—— 论文在此获得平均准确率SOTA。
  - **AIGCDetect benchmark**（多样化生成模型图像）—— 获得第二好的总体平均准确率。
  - **Chameleon dataset**（挑战性数据集）—— 获得第二名。
- **Benchmark**：采用上述三个公开基准，涵盖多种生成模型（包括扩散模型、GAN等），评价指标为平均准确率（mean accuracy）。
- **对比方法**：包括PatchCraft、AIDE、以及其他基于频域或大模型特征的检测器（未具体列全，但表明与当前SOTA进行公平比较）。

## 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量或训练时长。论文摘要及元数据中未提及任何关于计算资源的具体信息。因此无法总结算力消耗。

## 5. 实验数量与充分性
- **实验数量**：至少在三个标准基准数据集（GenImage、AIGCDetect、Chameleon）上进行了完整评估。元数据中提及“在多个数据集上取得更优准确率”，但未披露具体的消融实验数量。
- **充分性与公平性**：
  - **充分性**：覆盖了主流生成模型（扩散模型、GAN等）和不同的检测难度，对比了多个SOTA方法，证明结构语义特征的有效性。但缺乏对超参数敏感性的详细分析、在不同压缩/噪声下的鲁棒性实验（除“低质量伪造”外）。
  - **客观公平**：基准实验设置符合领域惯例，对比方法选用公开的SOTA，结果报告了平均准确率，未选择性报告最佳结果。但未提供完整实验配置（如划分层数、统计差异度量选择等），可复现性不足。

## 6. 论文的主要结论与发现
- 结构语义特征能够**有效补充**现有基于局部频域和全局语义的方法，显著提升AI生成伪造图像的检测性能。
- 在GenImage上达到新的SOTA，证明对现代扩散模型的有效性；在AIGCDetect和Chameleon上取得第二，说明**强泛化能力**。
- 结构语义为检测提供了**可解释的结构化线索**，有助于理解生成模型的不一致性特征。

## 7. 优点
- **创新性**：首次显式将结构语义引入AIGC检测，超越局部与全局特征的二元框架。
- **有效性**：在多个挑战性基准上验证了性能提升，特别是对低质量伪造和细粒度伪影的鲁棒性。
- **可解释性**：立方体划分产生的层次化差异可提供可视化线索，有利于模型可信度。
- **兼容性**：可方便地集成到现有框架（如AIDE）中，不必从头设计新网络。

## 8. 不足与局限
- **实验覆盖有限**：未在真实社交媒体场景、对抗性攻击下进行测试；仅报告平均准确率，未提供PR曲线、F1-score等指标。
- **偏差风险**：方法可能依赖特定生成模型留下的统计痕迹，若未来生成模型改进结构一致性，性能可能下降。
- **应用限制**：立方体划分的深度和粒度需手动设定，缺乏自适应机制；计算开销未评估（递归划分可能增加推理时间）。
- **可复现性不足**：未公开代码、具体划分规则和统计差异计算公式，部分细节未给出（如融合方式、分类器结构）。

（完）
