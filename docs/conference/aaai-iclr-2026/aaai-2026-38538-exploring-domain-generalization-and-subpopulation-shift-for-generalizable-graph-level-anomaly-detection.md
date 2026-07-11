---
title: Exploring Domain Generalization and Subpopulation Shift for Generalizable Graph-Level Anomaly Detection
title_zh: 探索域泛化和子群偏移用于可泛化的图级异常检测
authors: "Xiaoxiang Li, Xihe Xie, Hai Wan, Xibin Zhao"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38538/42500"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 图级异常检测但未涉及可解释性
tldr: 本文研究图级异常检测中的域泛化和子群偏移问题，首次形式化GLAD的OOD泛化问题。提出一个框架应对两种分布偏移，但未涉及可解释性。该方法在多个图数据集上提升了泛化能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有图级异常检测方法缺乏对分布外场景的泛化能力。
method: 形式化GLAD的OOD泛化问题，提出处理域泛化和子群偏移的框架。
result: 在多个图数据集上展示了较好的泛化性能。
conclusion: 该工作强调了图级异常检测中泛化的重要性。
---

## Abstract
Graph-level anomaly detection (GLAD), which identifies rare or atypical graphs within a graph set, is crucial for applications such as image analysis, industrial defect inspection and fraud detection. However, existing GLAD approaches typically rely on the in-distribution hypothesis while lacking generalization capability for out-of-distribution (OOD) scenarios (e.g., different graph sizes), which largely limits the application in the real world. For the first time, we formulate the OOD generalization problem for GLAD, where testing graph data exhibit significant distributional shifts from training data.  To tackle two common types of distributional shifts, domain generalization and subpopulation shift, we propose the Fine-Grained Subpopulation Graph-Level Anomaly Detection (FGS-GLAD). First, we propose a Graph Information Bottleneck-based Anomaly Detection Module (GIB4AD) that implements graph reverse distillation and graph information bottleneck on the graph to enhance task-relevant feature extraction for domain generalization. Second, We propose a Fine-Grained Subpoulation Inference Module (FGSI) to predict fine-grained subpopulations and focus on critical inter-subpopulation features through a supervised contrastive mechanism. Experiments on seven benchmark datasets and ten baselines demonstrate our model's superiority in handling domain generalization and subpopulation shift.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：图级异常检测（GLAD）在工业缺陷检测、图像分析、欺诈检测等领域具有重要应用。然而，现有GLAD方法普遍假设训练和测试数据来自同一分布，这在实际场景中往往不成立——测试数据可能经历显著的**分布偏移**（out-of-distribution, OOD），例如新的化合物家族、新的图结构模式等。因此，提升GLAD在OOD场景下的泛化能力成为关键挑战。
- **整体含义**：本文首次形式化了图级异常检测中的OOD泛化问题，并聚焦于两类常见偏移——**域泛化**（测试集包含训练中未见过的全新域）和**子群偏移**（训练与测试共享部分域，但子群比例或分布不同）。作者提出FGS-GLAD框架，旨在同时解决这两种偏移，使GLAD模型在实际部署中具有更强的鲁棒性和可靠性。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
FGS-GLAD由两个主要模块组成：
- **GIB4AD**（基于图信息瓶颈的异常检测模块）：通过图反向蒸馏和图信息瓶颈理论，提取与任务相关的紧凑子图表示，增强域泛化能力。
- **FGSI**（细粒度子群推断模块）：无监督地发现数据中的细粒度子群，并通过监督对比学习机制使模型关注关键子群间特征，以缓解子群偏移。

### 关键技术细节
1. **图反向蒸馏（Graph Reverse Distillation）**：
   - 教师编码器（冻结）从输入图中提取多尺度层级特征。
   - 学生解码器尝试以相反顺序重建教师的层级特征，重建误差作为异常分数。
   - 这种设计迫使学生在受限表示中学习正常模式，从而使异常图在重建时产生更大偏差。

2. **图信息瓶颈（Graph Information Bottleneck, GIB）**：
   - 在教师和学生之间插入瓶颈层，通过随机注意力机制（可微分Gumbel-Softmax采样）为每一条边计算保留概率，得到任务相关的子图邻接矩阵 \( A_S = \alpha \odot A \)。
   - 该子图仅保留对异常检测最关键的边，过滤冗余信息，提升OOD泛化。

3. **细粒度子群推断模块**：
   - 子群分类器：基于瓶颈子图嵌入，通过GNN和softmax输出每个样本属于C个细粒度子群的概率。
   - 监督细粒度对比学习（SFCL）：
     - 正样本对包含同粗粒度类（正常或异常）中的所有样本，但为同一子群内的正样本赋予更大权重（超参数α>1）。
     - 损失函数 \( L_{SFCL} = \frac{1}{|B|}\sum_{i\in B} \log\frac{N_i}{D_i} \)，其中 \(N_i\) 区分不同子群和同一子群的贡献，\(D_i\) 归一化所有非自身样本。

4. **总体目标函数**：\( L = L_{recon} + \alpha L_{SFCL} + \beta L_{distill} \)，联合优化邻接矩阵重建、对比学习和蒸馏损失。

## 3. 实验设计

- **数据集**：使用7个基准数据集，涵盖两类分布偏移场景：
  - **GOOD基准**：Motif-Base、Motif-Size（合成图）、CMNIST-Color（图结构MNIST）、HIV-Scaffold、HIV-Size（分子图）。
  - **DrugOOD基准**：DrugOOD-IC50-Scaffold、DrugOOD-IC50-Size（生物活性分子图）。
- **基准方法对比**：分为两组：
  - **图OOD方法**：GSAT、CIGA、PGIB、IGM（共4种）。
  - **图级异常检测方法**：SIGNET、MUSE、iGAD（共3种）。
- **评价指标**：Recall、ROC-AUC、F1-Score。所有实验重复5个随机种子。

## 4. 资源与算力

论文在**实验实现细节**部分说明：所有实验使用**NVIDIA V100 GPU（16GB内存）** 进行。优化器为Adam（学习率0.001，权重衰减1e-5），训练200轮并基于验证损失早停。**未明确说明使用的GPU数量**，也未提及训练总时长。但基于单卡V100和200轮训练，推测算力需求处于中等水平。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验：在7个数据集上进行，每个数据集有2种偏移类型（Scaffold/Size、Base/Size、Color等），共计多组结果（表1和表2）。
  - 消融实验：在4个代表性数据集（CMNIST-Color、HIV-Scaffold、Motif-Base、DrugOOD-IC50-Scaffold）上对比了Baseline、Baseline-F（加FGSI）、Baseline-G（加GIB4AD）和完整模型（表3）。
  - 超参数敏感性：对α和β进行网格搜索，在3个数据集上展示热力图（图3）。
  - 计算复杂度对比：与PGIB和SIGNET在训练时间和内存消耗上对比（图4）。
- **充分性**：实验覆盖了合成图和真实分子图，偏移类型多样，消融设计合理，超参数分析全面。但未包含跨更大规模数据集（如百万级图）的评估，也未探讨不同GNN骨干的影响。

## 6. 主要结论与发现

- FGS-GLAD在所有7个数据集、多种偏移设置下**一致优于**所有基线方法，在ROC-AUC、Recall、F1上平均提升约4.5%-5.1%。
- **图OOD方法（GSAT等）** 在不同场景下表现不稳定，说明它们难以应对细粒度子群偏移。
- **传统GLAD方法（MUSE、SIGNET等）** 在OOD场景下性能大幅下降，证实它们缺乏分布偏移鲁棒性。
- 消融实验显示：GIB4AD和FGSI两个模块均显著提升性能，且完整模型效果最佳，验证了联合设计的必要性。
- 计算复杂度比最优方法（PGIB和SIGNET）更低（训练快26.7%-36.8%，内存少14.3%-28.6%）。

## 7. 优点

- **问题新颖性**：首次系统定义并解决GLAD中的OOD泛化问题，填补了领域空白。
- **方法融合巧妙**：将图反向蒸馏、信息瓶颈、细粒度对比学习有机结合，既增强域泛化又缓解子群偏移。
- **无监督子群发现**：无需细粒度标注，通过对比学习自动挖掘子群，实用性强。
- **实验充分且公平**：涵盖合成和真实分子数据集，与10种基线（含SOTA）比较，消融和超参数分析完整。
- **计算效率高**：设计轻量，训练速度和内存占用优于同类方法，具有可扩展性。

## 8. 不足与局限

- **未涉及可解释性**：虽然论文提及“可解释”相关标签，但方法本身未提供图级别的异常解释（如关键子图可视化），这与提示中提到的“xai-objdet”标签不完全匹配。
- **数据集规模有限**：GOOD和DrugOOD数据集的图规模相对较小（最多几万个图），未在超大规模图（如百万级）或更复杂场景（如动态图）中验证。
- **骨干网络单一**：仅采用一种GNN结构（未具体说明型号），未探索不同GNN骨干对泛化能力的影响。
- **假设条件**：假设异常仅通过图结构特征体现，可能遗漏节点属性异常等其他类型。
- **子群数量C需人工设定**：子群数量为超参数，未提供自适应选择策略，可能影响通用性。
- **对比方法不足**：未与最新图OOD方法（如2025年后方法）比较，部分基线（如MUSE、SIGNET）本身非设计用于OOD，对比可能不全面。

（完）
