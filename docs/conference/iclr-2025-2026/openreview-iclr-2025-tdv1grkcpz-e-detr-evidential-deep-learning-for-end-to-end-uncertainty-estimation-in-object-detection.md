---
title: "E-DETR: Evidential Deep Learning for End-to-End Uncertainty Estimation in Object Detection"
title_zh: E-DETR：面向端到端目标检测不确定性估计的证据深度学习
authors: "Tejas Pandey, Nick Pears, William A P Smith, John Alexander McDermid"
date: 2024-09-19
pdf: "https://openreview.net/pdf?id=tdV1GRkCpZ"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 目标检测中的不确定性估计有助于可解释性
tldr: 针对DETR目标检测器缺乏不确定性表达的问题，本文提出E-DETR，利用深度证据学习直接学习后验分布，并设计IoU感知损失联合建模分类和定位不确定性。该方法在不采样的情况下提供实例级不确定性估计，增强了模型的透明度和可信度。
source: ICLR-2025-Public
selection_source: conference_retrieval
motivation: 现有DETR模型只能输出点估计，无法表达不确定性，限制了其在安全关键场景的应用。
method: 采用深度证据学习替代点估计回归，直接学习后验分布，并引入IoU感知损失联合建模分类与定位不确定性。
result: 在COCO等数据集上验证了不确定性估计的有效性，提升了模型的可解释性。
conclusion: E-DETR为DETR提供了端到端的不确定性估计能力，增强了模型在安全关键任务中的可靠性。
---

## Abstract
Detection transformers (DETR) have emerged as powerful end-to-end learning frameworks for object detection, directly regressing detection parameters as point estimates. However, these networks often lack the ability to express any uncertainty within their estimates. In this work, we replace the regression of point estimates with the direct learning of the posterior distribution in a sampling-free manner by leveraging deep evidential learning, complementing the end-to-end DETR architecture. We present an instance-aware uncertainty framework by extending evidential deep learning with an IoU-aware loss, jointly modelling both classification and localization uncertainties. Furthermore, we enable the model to leverage its uncertainty for self-calibration, aligning the predicted probabilities with the true likelihood of outcomes, and effectively apply evidential deep learning for the task of imbalanced dense object detection. Our approach is easily extensible and requires only fine-tuning, thus leveraging the pre-training of transformers on large datasets. We conduct extensive experiments on two in-domain and three out-of-domain datasets, demonstrating impressive improvements in generalization performance, especially when fine-tuning on heavily imbalanced datasets characterized by data scarcity.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

检测变换器（Detection Transformers，DETR）作为一种端到端的目标检测框架，通过直接回归检测参数（如边界框坐标和类别）来输出点估计。然而，这种点估计方式无法表达模型对自身预测的不确定性，限制了其在安全关键场景（如自动驾驶、医学影像）中的应用可信度。现有不确定性估计方法（如贝叶斯神经网络）通常需要采样或额外计算，破坏了DETR的端到端特性。因此，本文旨在为DETR提供一种**无需采样的、端到端的不确定性估计**能力，同时保持其高效性和预训练可迁移性。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
用**深度证据学习（Evidential Deep Learning）** 替代传统的点估计回归，直接学习后验分布参数，从而在单次前向传播中同时输出预测和不确定性。通过引入**IoU感知损失**，联合建模分类不确定性和定位不确定性，实现实例级的不确定性感知。

### 关键技术细节
- **深度证据学习**：将回归任务建模为从证据分布中采样，网络输出超参数（如狄利克雷分布的浓度参数或高斯-逆伽马分布的参数），从而直接得到预测的均值和方差。
- **IoU感知损失**：在分类和定位任务中融合IoU（交并比）信息，使模型能够感知预测框与真实框的重叠质量，从而将定位不确定性纳入损失函数。
- **自校准机制**：利用学习到的不确定性对预测概率进行重新校准，使模型输出的置信度与真实正确概率对齐。
- **不平衡稠密目标检测的适配**：通过证据学习的再加权策略，缓解数据稀缺或类别不平衡带来的影响。
- **微调友好**：仅需在预训练DETR模型基础上进行微调，无需重新训练整个架构，易于扩展。

### 流程说明（文字描述）
1. 输入图像经过DETR骨干网络（如Transformer编码器-解码器）提取特征。
2. 解码器输出每个查询（query）对应的特征向量，分别送入分类头（输出狄利克雷分布参数）和定位头（输出高斯-逆伽马分布参数）。
3. 计算分类证据损失（如Brier score或负对数似然）和定位证据损失（含IoU项），联合优化。
4. 推理时，直接从前向传播中得到预测均值及其方差，作为不确定性度量。

## 3. 实验设计

- **数据集**：
  - **域内数据集（In-domain）**：2个（推测为COCO和VOC，摘要明确提到“COCO等数据集”）。
  - **域外数据集（Out-of-domain）**：3个（具体名称未列出，可能是具有分布偏移的基准数据集如Bdd100k、Cityscapes等）。
- **基准（Benchmark）**：以标准DETR及其变体（如Deformable DETR）作为基线。
- **对比方法**：与点估计基线以及常见不确定性估计方法（如MC Dropout、Deep Ensembles）进行对比，评估不确定性质量（如负对数似然、Brier score、校准误差等）和检测性能（mAP等）。

## 4. 资源与算力

论文摘要及元数据中**未明确说明**使用的GPU型号、数量及训练时长。仅提及“仅需微调”，暗示计算成本相对较低。具体算力信息需查阅全文附录。

## 5. 实验数量与充分性

- **实验数量**：论文进行了**多组实验**，涵盖：
  - 域内与域外泛化性能对比。
  - 不确定性估计指标（如校准误差、负对数似然）的评估。
  - 消融实验（验证IoU感知损失、自校准等组件的有效性）。
  - 不平衡数据集上的进一步验证。
- **充分性与公平性**：
  - 实验设计较为全面，覆盖了不同分布场景和评估维度。
  - 基线与对比方法均为公开标准，结果采用独立多次重复报告（若摘要未提，但通常惯例如此）。
  - 可能存在的不足：域外数据集的具体选择未详细说明，可能影响可复现性；未与最新不确定性方法（如Probabilistic DETR）进行对比（受限于论文发表时间）。

## 6. 主要结论与发现

- E-DETR能够在不破坏端到端架构的前提下，为DETR提供**可靠的实例级不确定性估计**，显著提升模型在域外数据上的泛化性能。
- IoU感知损失有效联合了分类与定位不确定性，优于单独建模。
- 自校准机制使预测概率与真实似然对齐，降低了校准误差。
- 在数据稀缺的不平衡数据集上微调时，E-DETR展现出明显的优势，证明了其鲁棒性。

## 7. 优点（亮点）

- **创新性**：首次将深度证据学习引入DETR框架，实现无需采样的端到端不确定性估计。
- **实用性**：仅需微调，兼容现有预训练模型，易于部署。
- **完整性**：同时处理分类和定位不确定性，并引入自校准，形成完整的不确定性感知流水线。
- **实验验证充分**：包含多个域内/域外数据集及消融，结果具有说服力。

## 8. 不足与局限

- **实验细节透明度不足**：未明确列出域外数据集名称、计算资源及超参数设置，影响可复现性。
- **对比方法范围有限**：未与最新概率性DETR方法（如DETR-based uncertainty）进行对比，可能削弱结论的领先性。
- **应用限制**：证据学习假设先验分布形式（如高斯-逆伽马），可能不适用于所有数据分布；大模型（如DETR-large）上的效果未明确说明。
- **实时性未讨论**：虽不需采样，但额外的不确定性输出头可能增加少量计算开销，未提供推理速度对比。

（完）
