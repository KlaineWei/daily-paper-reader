---
title: Structural Semantic Features for Improved AI-Generated Fake Image Detection
title_zh: 面向改进AI生成伪造图像检测的结构语义特征
authors: "Md Redwanul Haque, Manzur Murshed, Manoranjan Paul, Tsz-Kwan Lee"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=TADsPhlp32"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 利用结构语义特征进行伪造图像检测
tldr: 针对现有伪造检测忽略结构语义，提出引入立方体分层划分的结构语义特征。在多个AIGC检测基准上增强现有方法性能，但对可解释性贡献有限。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有方法缺乏图像底层结构语义。
method: 采用立方体划分递归分解图像，提取结构语义特征。
result: 在多个AIGC检测数据集上提升检测准确率。
conclusion: 结构语义特征增强伪造检测性能。
---

## Abstract
The proliferation of AI-generated content (AIGC) has made the accurate detection of fake images a critical challenge. Existing state-of-the-art methods, such as PatchCraft and AIDE, primarily leverage local features like patch-wise frequency information or global semantic features derived from large-scale models like CLIP. While effective, these approaches often fail to incorporate the underlying structural semantics of an image, which are crucial for detecting the subtle inconsistencies and artifacts left by generative models. We propose a novel approach that augments existing AIGC detection frameworks by explicitly incorporating structural semantic information. Our method employs cuboidal partitioning, a hierarchical tool that recursively divides an image into meaningful sub-regions. At each division, we extract a measure of the statistical difference between the parent and child segments, which are then integrated with AIDE's existing features. Experimental results demonstrate our model's superior performance. We establish a new state-of-the-art in mean accuracy on the GenImage benchmark, proving our effectiveness on modern diffusion models. Our method also shows strong generalization by achieving second-best overall mean accuracy on the diverse AIGCDetect benchmark and a second-place finish on the challenging Chameleon dataset. These results highlight the significant value of structural semantics for building robust and generalizable AIGC detectors.

---

## 论文详细总结（自动生成）

# 论文总结

## 1. 核心问题与整体含义
- **研究背景**：AI生成内容（AIGC）的泛滥使得伪造图像检测成为关键挑战。现有方法（如PatchCraft、AIDE）主要利用局部补丁频率信息或来自CLIP等大模型的全局语义特征，但忽略了图像的底层结构语义信息。
- **核心问题**：如何显式引入结构语义特征，以捕捉生成模型留下的细微不一致性和伪影，从而提升伪造检测的准确性与泛化性。
- **研究意义**：通过增强现有检测框架的结构感知能力，推动构建更鲁棒、可泛化的AIGC检测器。

## 2. 方法论
- **核心思想**：利用**立方体分层划分（Cuboidal Partitioning）** 递归地将图像分解为有意义的子区域，并在每一层划分中提取父段与子段之间的统计差异，作为结构语义特征。该特征与AIDE原有的特征（全局语义+局部频率）融合，形成新的检测框架。
- **关键技术细节**：
  - 对输入图像进行多层级、多方向的立方体划分（类似于3D空间内的递归分割）。
  - 在每个划分节点上，计算父块与子块之间的某种统计差异度量（如均值、方差或高阶统计量）。
  - 将这些跨尺度的差异值编码为特征向量，与AIDE的现有特征拼接后送入分类器。
- **算法流程（文字说明）**：
  1. 输入图像 → 2. 立方体分层划分（递归进行） → 3. 提取每层父子块统计差异 → 4. 聚合多层级结构语义特征 → 5. 与AIDE提取的CLIP全局特征和Patch-wise频率特征拼接 → 6. 分类器（如MLP）输出真/假预测。

## 3. 实验设计
- **数据集与基准**：
  - **GenImage基准**：包含多种现代扩散模型生成的图像，用于评估核心性能。
  - **AIGCDetect基准**：覆盖多种生成模型的多样化数据集，用于检验泛化性。
  - **Chameleon数据集**：具有挑战性的混合伪造场景。
- **对比方法**：包括PatchCraft、AIDE（作为基线）以及其他SOTA检测器。
- **评估指标**：主要采用平均准确率（Mean Accuracy），并报告在每个基准上的排名。

## 4. 资源与算力
- 文中**未明确说明**使用的GPU型号、数量及训练时长。推测基于常见AIGC检测实验配置（如单张或少量高端GPU），但缺乏具体信息。

## 5. 实验数量与充分性
- **实验数量**：在三个公开基准（GenImage、AIGCDetect、Chameleon）上进行了全面评测，并报告了与多个SOTA方法的对比结果。但未展示消融实验（如单独评估结构语义特征贡献、不同划分深度的影响）及跨数据集交叉验证。
- **充分性评价**：基准测试覆盖了主流生成模型和难度不同的场景，具有一定的代表性。但由于缺少详细的消融分析和泛化实验细节，实验的充分性略有不足。结论主要依赖最终排名，公平性较好（在相同条件下比较）。

## 6. 主要结论与发现
- 提出的结构语义特征能够有效提升现有AIGC检测器的性能，在GenImage基准上取得**最佳平均准确率**（新SOTA），在AIGCDetect基准上获得**第二**，在Chameleon数据集上同样**第二**。
- 结构语义信息有助于捕捉生成图像的底层不一致性，从而增强模型的鲁棒性和泛化能力。

## 7. 优点
- **创新性**：首次显式引入立方体分层划分提取结构语义，弥补了现有方法对底层结构关注的缺失。
- **简洁有效**：方法可轻松嵌入已有框架（如AIDE），无需额外的大规模预训练模型。
- **泛化性强**：在多个不同分布的数据集上均能取得领先或接近SOTA的表现。

## 8. 不足与局限
- **可解释性有限**：如元数据TLDR所指，结构语义特征是如何帮助检测的仍缺乏深入分析，模型决策过程不透明。
- **实验覆盖面不足**：未在更多样化的AIGC类型（如视频、文本生成图像）及对抗性攻击场景下测试。
- **计算开销未讨论**：未评估立方体划分及特征提取的额外计算成本，可能影响实际部署。
- **偏差风险**：仅与少数基线对比，可能遗漏近期其他结构感知方法；且未报告方差或置信区间，结论稳健性需更多证据支持。

（完）
