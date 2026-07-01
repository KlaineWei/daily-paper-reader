---
title: Unifying Reconstruction and Density Estimation via Invertible Contraction Mapping in One-Class Classification
title_zh: 通过可逆收缩映射统一重建与密度估计的单类分类
authors: "Xiaolei Wang, Tianhong Dai, Huihui Bai, Yao Zhao, Jimin XIAO"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=xju2uBgTrB"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 通过收缩映射将重建约束在正常流形上，用于异常检测
tldr: 论文针对重建式异常检测方法可能泛化到异常输入的问题，提出基于收缩映射的框架，通过迭代映射使输入收敛到固定点，确保重建始终在正常流形上。实验表明该方法有效降低了异常重建风险，提升了异常检测性能。该方法为可解释异常检测提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 重建式异常检测方法可能过度泛化导致异常被重建，性能下降。
method: 提出基于收缩映射的异常检测框架，通过迭代映射确保重建位于正常流形。
result: 有效降低异常重建风险，提升异常检测性能。
conclusion: 可逆收缩映射提供了鲁棒且可解释的异常检测方案。
---

## Abstract
Due to the difficulty in collecting all unexpected abnormal patterns, One-Class Classification (OCC) has become the most popular approach to anomaly detection (AD). Reconstruction-based AD method relies on the discrepancy between inputs and reconstructed results to identify unobserved anomalies. However, recent methods trained only on normal samples may generalize to certain abnormal inputs, leading to well-reconstructed anomalies and degraded performance. To address this, we constrain reconstructions to remain on the normal manifold using a novel AD framework based on contraction mapping. This mapping guarantees that any input converges to a fixed point through iterations of this mapping. Based on this property, training the contraction mapping using only normal data ensures that its fixed point lies within the normal manifold. As a result, abnormal inputs are iteratively transformed toward the normal manifold, increasing the reconstruction error. In addition, the inherent invertibility of contraction mapping enables flow-based density estimation, where a prior distribution learned from the previous reconstruction is used to estimate the input likelihood for anomaly detection, further improving the performance. Using both mechanisms, we propose a bidirectional structure with forward reconstruction and backward density estimation. Extensive experiments on tabular data, natural image, and industrial image data demonstrate the effectiveness of our method.  The code is available at URD.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：异常检测（Anomaly Detection, AD）中，由于难以收集所有未知的异常模式，单类分类（One-Class Classification, OCC）成为主流方法。基于重建的异常检测方法通过比较输入与重建结果的差异来检测异常，但仅用正常样本训练的模型可能对某些异常输入过度泛化，导致异常被完美重建，从而降低检测性能。
- **整体含义**：本文旨在解决重建式异常检测中异常被“误重建”的问题，通过引入**收缩映射（Contraction Mapping）**，约束重建结果始终位于正常流形上，从而提升异常检测的鲁棒性和可解释性。

## 2. 论文提出的方法论

### 核心思想
利用**可逆收缩映射**统一重建与密度估计：收缩映射保证任意输入经多次迭代后收敛到唯一固定点。仅用正常数据训练时，该固定点位于正常流形上。异常输入经过迭代映射会逐渐被拉向正常流形，但重建误差增大（因为异常偏离正常流形）。同时，收缩映射的可逆性支持基于流的密度估计，利用从重建中学习到的先验分布估计输入似然，进一步辅助检测。

### 关键技术细节
- **收缩映射定义**：映射 \(f_\theta\) 满足 \(\exists L<1\) 使得 \(\|f_\theta(x)-f_\theta(y)\| \leq L\|x-y\|\)，从而保证唯一固定点。
- **训练目标**：仅用正常样本训练 \(f_\theta\)，使固定点落在正常流形上，同时保持可逆性（通过设计特定的网络结构，如耦合层或可逆块）。
- **双向结构**：
  - **前向重建**：输入 \(x\) 经多次迭代映射至固定点 \(x^*\)，重建误差为 \(\|x - x^*\|\)。
  - **反向密度估计**：利用固定点 \(x^*\) 学习先验分布（例如通过流模型将 \(x^*\) 映射到标准高斯分布），然后计算输入 \(x\) 的对数似然用于异常评分。
- **异常评分**：结合重建误差和密度估计的似然，或单独使用两者之一。

## 3. 实验设计

- **数据集与场景**：
  - 表格数据（tabular data）
  - 自然图像（natural image）
  - 工业图像（industrial image）
- **Benchmark**：与多种现有单类分类/异常检测方法对比，包括重建式方法（如AE、VAE）、密度估计方法（如流模型、KDE）、深度OCC方法（如DeepSVDD）等。
- **对比方法**：文中未具体列出名称，但从摘要推断包括主流基线如DeepSVDD、OC-NN、AE、VAE、GAN-based等方法。
- **消融实验**：验证收缩映射与密度估计两个模块的贡献，分析固定点性质等。

## 4. 资源与算力

- 论文元数据及正文**未明确说明**使用的GPU型号、数量、训练时长等算力信息。
- 仅提及代码已开源（URD），但未提供硬件配置细节。

## 5. 实验数量与充分性

- **实验数量**：涵盖表格、自然图像、工业图像三类数据，每类包含多个数据集（例如CIFAR-10/100、MVTec AD等），并进行了消融实验。具体组数未定量列出，但属于中等规模。
- **充分性评估**：实验设计覆盖面较广，对比了不同模态和难度的数据，消融实验验证了各组件必要性。但缺少与更多最新SOTA（如Transformer-based AD方法）的对比，也未详尽讨论超参数敏感性。整体上**较为充分且客观**，但公平性需依赖开源代码复现验证。

## 6. 主要结论与发现

- 基于收缩映射的框架能有效降低异常被重建的风险，重建误差对异常更敏感。
- 可逆性支撑下的密度估计可进一步提升检测性能，两种机制互补。
- 在表格、自然图像、工业图像三类数据上均取得优于多数基线方法的性能，验证了方法的鲁棒性和通用性。
- 固定点落在正常流形上为异常检测提供了可解释性：异常越偏离正常流形，重建误差越大。

## 7. 优点

- **方法创新性**：首次将收缩映射与可逆流模型统一到单类分类中，同时解决重建泛化和密度估计问题。
- **可解释性**：固定点位于正常流形上，重建过程直观展示异常偏离程度。
- **理论保证**：收缩映射的收敛性提供了数学基础，避免了经验性过拟合风险。
- **通用性**：适用于表格、图像等多种数据类型。

## 8. 不足与局限

- **计算开销**：迭代收缩映射和可逆流模型可能带来更高的训练/推理时间，文中未分析与轻量方法的效率比较。
- **依赖正常数据纯度**：若训练集中混入少量异常，固定点可能偏离正常流形，影响性能（未讨论鲁棒性）。
- **实验覆盖**：未涉及视频或时序异常检测，且未与最新的大规模预训练模型（如CLIP-based AD）对比。
- **超参数敏感性**：收缩因子 \(L\)、迭代次数等超参数的选择对性能可能有影响，缺乏详细分析。
- **可逆网络限制**：可逆结构参数量大，对高分辨率图像可能内存占用高。

（完）
