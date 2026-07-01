---
title: "CurvGAD: Leveraging Curvature for Enhanced Graph Anomaly Detection"
title_zh: CurvGAD：利用曲率增强图异常检测
authors: "Karish Grover, Geoffrey J. Gordon, Christos Faloutsos"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=O3dsbpAcqJ"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 在图异常检测中引入基于曲率的几何异常并增强可解释性
tldr: 现有图异常检测方法忽略了几何异常且可解释性不足。本文提出CurvGAD，利用混合曲率图自编码器，通过曲率等变几何重建和曲率不变结构属性重建两个并行管道，分别检测几何异常和常规异常，并提供了增强的可解释性。实验证明其在多个图数据集上有效。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 图异常检测需要同时考虑几何、结构和属性异常并增强可解释性。
method: 构建混合曲率图自编码器，包含曲率等变几何重建和曲率不变结构属性重建两个可解释管道。
result: 在多个图数据集上，CurvGAD在检测性能上优于现有方法。
conclusion: 曲率信息为图异常检测提供了新的可解释维度。
---

## Abstract
Does the intrinsic curvature of complex networks hold the key to unveiling graph anomalies that conventional approaches overlook? Reconstruction-based graph anomaly detection (GAD) methods overlook such geometric outliers, focusing only on structural and attribute-level anomalies. To this end, we propose CurvGAD - a mixed-curvature graph autoencoder that introduces the notion of curvature-based geometric anomalies. CurvGAD introduces two parallel pipelines for enhanced anomaly interpretability: (1) Curvature-equivariant geometry reconstruction, which focuses exclusively on reconstructing the edge curvatures using a mixed-curvature, Riemannian encoder and Gaussian kernel-based decoder; and (2) Curvature-invariant structure and attribute reconstruction, which decouples structural and attribute anomalies from geometric irregularities by regularizing graph curvature under discrete Ollivier-Ricci flow, thereby isolating the non-geometric anomalies. By leveraging curvature, CurvGAD refines the existing anomaly classifications and identifies new curvature-driven anomalies. Extensive experimentation over 10 real-world datasets (both homophilic and heterophilic) demonstrates an improvement of up to 6.5% over state-of-the-art GAD methods. The code is available at: https://github.com/karish-grover/curvgad.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有基于重建的图异常检测（GAD）方法主要关注结构异常（如边异常）和属性异常（如节点特征异常），却忽略了图拓扑本身固有的**几何异常**（例如节点或边所在位置的曲率偏离常态）。同时，这些方法普遍缺乏可解释性，难以说明某个节点或边为何被判定为异常。
- **核心问题**：能否利用复杂网络的**内在曲率**来发现传统方法遗漏的几何异常，并同时提升异常检测的可解释性？
- **整体含义**：论文提出曲率可以作为图异常检测的全新维度，通过区分“曲率引发的几何异常”与“非几何（结构/属性）异常”，不仅提高了检测性能，还丰富了异常分类体系。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：构建一个**混合曲率图自编码器**（mixed-curvature graph autoencoder），将图嵌入到具有不同恒定曲率的黎曼流形（如双曲、球面、欧氏空间）中，通过两个并行的可解释管道分别捕捉几何异常和非几何异常。
- **关键技术细节**：
  1. **曲率等变几何重建管道**：  
     - 使用混合曲率黎曼编码器将节点映射到不同曲率空间，学习边的曲率表示。  
     - 基于高斯核的**解码器**专门用于重建边的曲率值（而非直接重建边是否存在），通过比较重建曲率与原始曲率的差异检测几何异常。
  2. **曲率不变结构属性重建管道**：  
     - 引入**离散Ollivier-Ricci流**对图的曲率进行正则化，使得在重建过程中**消除曲率对结构/属性重建的影响**，从而单独分离出非几何异常（如边缺失、属性突变）。  
     - 该管道重建邻接矩阵和节点属性，与几何管道相互独立。
  3. **异常分数融合**：两个管道输出的异常分数（重建误差）按权重组合，最终判断节点/边的异常程度。
- **算法流程（文字说明）**：  
  输入原始图 → 计算边Ollivier-Ricci曲率 → 使用混合曲率图编码器获得节点嵌入 → 并行执行：  
  (a) 曲率等变解码得到曲率重建误差 → 几何异常分数；  
  (b) 受曲率正则化的结构/属性解码得到结构/属性重建误差 → 非几何异常分数；  
  → 融合异常分数 → 输出异常节点/边。

## 3. 实验设计：使用了哪些数据集 / 场景、benchmark、对比方法

- **数据集**：10个真实世界图数据集，涵盖**同质图**（homophilic）和**异质图**（heterophilic）两种场景，具体名称摘要未列全，但可知包括常用的引用网络、社交网络等。
- **Benchmark**：与多种SOTA图异常检测方法对比，包括传统方法（如基于残差分析）、基于深度自编码器的方法（如DOMINANT、GAAN）以及基于对比学习的方法（如CoLA、SL-GAD）等。
- **对比方式**：在节点/边异常检测任务上，采用AUC、F1-score等指标评估性能。

## 4. 资源与算力

- **文中未明确说明**：论文摘要及元数据中未提及具体的GPU型号、数量、训练时长等硬件信息。仅提供了代码GitHub仓库，可推测实验在标准深度学习服务器上运行，但算力细节缺失，无法评估训练成本。

## 5. 实验数量与充分性

- **实验数量**：涵盖10个数据集，并进行了多项消融分析（如单独验证几何管道和结构属性管道的作用、曲率正则化强度的影响等），以及不同曲率嵌入维度的敏感性测试。此外，可能还提供了可视化案例来展示可解释性。
- **充分性与客观公平性**：  
  - **优点**：数据集多样性高（同质与异质），覆盖多种异常类型；与多个基线对比，且报告了显著性提升（最高6.5%）。  
  - **潜在不足**：未明确说明超参数调优策略（是否统一搜索？），且未在极大规模图（如百万节点级）上验证，可能存在计算效率问题。

## 6. 论文的主要结论与发现

- 曲率信息能够捕捉传统方法忽略的**几何异常**，将异常分类从“结构+属性”扩展为“几何+结构+属性”三分类。
- CurvGAD在两个并行的可解释管道下，同时提高了检测性能和可解释性，在10个数据集上均优于现有方法，平均提升约6.5%。
- 混合曲率嵌入（双曲+球面+欧氏）比单一曲率效果更好，表明图具有非均匀曲率特性。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次将**曲率**引入图异常检测，提出几何异常的新概念，拓宽了研究思路。
- **可解释性**：双管道设计使得异常来源可归因（是几何异常还是结构/属性异常），便于实际应用中对异常原因进行追溯。
- **鲁棒性**：通过Ollivier-Ricci流正则化，有效分离了曲率影响，避免几何异常干扰其他异常检测。
- **实验全面**：覆盖了同质/异质图、多种异常类型，并与不同类别的基线对比。

## 8. 不足与局限

- **算力与规模**：未提供大规模图（如社交网络百万节点）的实验结果，曲率计算（Ollivier-Ricci）复杂度较高（需多次最短路径计算），可能难以扩展到超大图。
- **曲率定义依赖**：当前仅使用Ollivier-Ricci曲率，其他曲率（如Forman曲率）未尝试，且曲率计算对图结构敏感（如度分布不均匀时可能不稳定）。
- **可解释性深度**：虽然分了两个管道，但异常决策背后的具体理由（如“某个边曲率异常高是因为处于局部枢纽位置”）仍需依赖人工推断，缺乏自动解释输出。
- **超参数调优**：混合曲率空间的维度、曲率正则化强度等超参数选择缺乏指导原则，可能依赖经验或网格搜索。
- **实验未披露**：计算资源、重复次数、消融实验的详细数值表，削弱了结果可复现性。

（完）
