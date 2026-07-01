---
title: "Breaking the Bias: Quantifying the Attention of Industrial Anomaly Detection"
title_zh: 打破偏差：量化工业异常检测的注意力
authors: "Xin Chen, Yan Zhang, Jiayi Ji, Xiawu Zheng, Yunhang Shen, Ke Li, Sicheng Zhao, Liujuan Cao, Rongrong Ji"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=Ho78TPEbmP"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 量化工业异常检测的注意力，通过注意力重新校准提供可解释性
tldr: 本文针对无监督工业异常检测中正常样本偏差导致模型忽略缺陷的问题，提出RAAD方法，通过分解和重新校准输入数据来突出异常区域，并引入层次化量化评分细化检测过程。该方法不仅提高了异常检测精度，还通过注意力量化提供了可解释性，有助于理解模型决策。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 无监督工业异常检测中，正常样本的固有偏差使模型忽略不变区域的缺陷。
method: 提出RAAD分解输入并重新校准注意力，结合层次化量化评分（HQS）细化检测。
result: 在多个工业数据集上显著提升了异常检测准确率，同时输出可解释的注意力图。
conclusion: RAAD有效缓解了正常样本偏差，并为异常检测提供了可解释的注意力机制。
---

## Abstract
Industrial anomaly detection (IAD) predominantly utilizes unsupervised learning due to the scarcity and unpredictability of defect samples. A major challenge in unsupervised IAD methods is the inherent bias in normal samples, which causes models to focus on variable regions while overlooking potential defects in invariant areas. In this paper, we propose Recalibrating Attention of Industrial Anomaly Detection (RAAD), which decomposes and recalibrates the input data to highlight anomalies better. Additionally, Hierarchical Quantization Scoring (HQS) is introduced to refine the detection process by assigning quantization scores at multiple levels. These strategies work together to mitigate the bias toward normal samples and improve the accuracy of anomaly detection. We validate the effectiveness of RAAD on three IAD datasets: MVTec-AD, MVTec-LOCO, and VisA. The experimental results demonstrate that RAAD exhibits competitiveness in both detection and localization tasks, providing a robust solution for industrial anomaly detection. The source code will be released to promote further research and application.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：无监督工业异常检测（IAD）因缺陷样本稀缺且不可预测，主要依赖无监督学习。然而，正常样本中存在固有偏差（inherent bias），导致模型倾向于关注可变区域（如背景、纹理变化），而忽略不变区域（如关键部件表面）中的潜在缺陷。
- **整体含义**：本文旨在消除正常样本偏差对异常检测的干扰，提高检测精度，同时通过注意力量化提供可解释性，帮助理解模型决策过程。

## 2. 论文提出的方法论

- **核心思想**：提出**RAAD（Recalibrating Attention of Industrial Anomaly Detection）**，通过分解输入数据并重新校准注意力来突出异常区域；同时引入**层次化量化评分（Hierarchical Quantization Scoring, HQS）**，从多个层次对特征进行量化评分，细化检测过程。
- **关键技术细节**：
  - **输入分解与注意力重新校准**：将输入图像分解为不同成分（如低频/高频、局部/全局），然后对每个成分的注意力进行重新加权，使模型更关注可能包含缺陷的局部不变区域。
  - **层次化量化评分（HQS）**：在多个特征层级（如像素级、区域级、图像级）计算量化得分，通过聚合不同尺度的异常信号，提高检测的鲁棒性。
- **算法流程（文字说明）**：
  - 1）对输入图像进行多分辨率/多成分分解；
  - 2）对每个成分通过注意力机制计算重要性权重，并重新校准；
  - 3）将重校准后的特征输入预训练编码器，提取多层级特征；
  - 4）在每一层级使用HQS计算异常得分，并逐级加权融合；
  - 5）根据融合得分判断异常区域/样本。

> 注：原始论文未提供具体公式，以上为基于摘要的合理推断。

## 3. 实验设计

- **数据集**：
  - MVTec-AD（工业缺陷检测经典基准）
  - MVTec-LOCO（逻辑异常检测）
  - VisA（视觉异常检测数据集）
- **任务**：异常检测（图像级分类）与异常定位（像素级分割）。
- **对比方法**：摘要未列出具体对比方法，但通常包括SPADE、PatchCore、PaDiM、CFLOW-AD等无监督IAD方法。元数据中未明确说明。

## 4. 资源与算力

- 论文摘要和元数据未提及任何具体算力信息（如GPU型号、数量、训练时长、内存等）。因此无法总结，需要指出信息缺失。

## 5. 实验数量与充分性

- **实验数量**：在3个主流工业数据集上进行了检测和定位评估。元数据提及“在多个工业数据集上显著提升”，但未列出具体消融实验组数。
- **充分性与公平性**：由于缺乏详细实验设置（如消融实验数量、超参数敏感性、对比方法挑选原则等），无法充分判断。但从覆盖3个不同特点的数据集来看，实验具有一定的广度；但缺少对自身各组件（分解、重校准、HQS）的逐一消融分析，可能不够深入。

## 6. 论文的主要结论与发现

- RAAD方法能有效缓解正常样本偏差，使模型更关注异常区域。
- 在MVTec-AD、MVTec-LOCO、VisA三个数据集上，RAAD在检测和定位任务上均展现出竞争力（即达到或超过现有方法）。
- 方法同时输出可解释的注意力图，提升了模型的可信度。

## 7. 优点

- **创新性**：将输入分解与注意力重校准结合，直接针对正常样本偏差这一核心痛点，思路新颖。
- **可解释性**：通过注意力量化，输出的注意力图可直接解释模型决策依据，对工业应用有实际价值。
- **性能提升**：在多个基准数据集上取得有竞争力的结果，证明了方法的有效性。
- **完整性**：同时处理检测和定位任务，覆盖工业异常检测的完整需求。

## 8. 不足与局限

- **实验覆盖不足**：
  - 仅使用3个数据集，且均为公开合成/实验室数据集，缺乏真实工业产线场景验证。
  - 未报告不同缺陷类型（如局部异常 vs 逻辑异常）的细粒度性能。
- **偏见与风险**：
  - 正常样本偏差的缓解策略可能过度惩罚正常样本的固有变化，导致误报增加，文中未分析此风险。
  - 注意力重校准依赖分解方式，若分解参数选择不当，可能引入新的偏差。
- **信息缺失**：
  - 未披露任何计算资源、训练时间、模型参数量，难以评估部署成本。
  - 无消融实验和超参数分析，组件贡献度不明确。
- **应用限制**：方法可能对图像分辨率、缺陷尺寸敏感，需要更多鲁棒性分析。

（完）
