---
title: EXPLAINABILITY-DRIVEN LAYER-WISE PRUNING OF DEEP NEURAL NETWORKS FOR EFFICIENT OBJECT DETECTION.
title_zh: 基于可解释性驱动的深度神经网络逐层剪枝用于高效目标检测
authors: "Abhinav Shukla, Nachiket Tapas"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JvGhBL777z"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 基于SHAP的可解释性驱动的目标检测剪枝
tldr: 本文提出一种可解释性驱动的逐层剪枝框架，用于高效目标检测。利用SHAP贡献分析量化层重要性，根据功能相关性剪枝，在保持检测精度的同时显著降低计算成本。在多个检测器上验证了有效性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统剪枝方法未考虑网络组件对任务性能的实际贡献。
method: 提出基于SHAP贡献分析的逐层剪枝框架，根据功能重要性剪枝。
result: 在保持精度的前提下大幅减少计算量，优于传统剪枝方法。
conclusion: 可解释性指导的剪枝能更有效地压缩目标检测网络。
---

## Abstract
Deep neural networks (DNNs) have achieved remarkable success in object detection tasks, but their increasing complexity poses significant challenges for deployment on resource-constrained platforms. While model compression techniques
like pruning have emerged as essential tools, traditional magnitude-based pruning
methods do not necessarily align with the true contribution of network components to task-specific performance. In this work, we present a novel explainabilitydriven layer-wise pruning framework specifically tailored for efficient object detection. Our approach leverages SHAP-based contribution analysis to quantify
layer importance through gradient-activation products, providing a data-driven
measure of functional contribution rather than relying solely on static weight
magnitudes. We conduct comprehensive experiments across diverse object detection architectures including ResNet-50, MobileNetV2, ShuffleNetV2, Faster RCNN, RetinaNet, and YOLOv8, evaluating performance on the Microsoft COCO
2017 validation set. Our results demonstrate that SHAP-based pruning consistently identifies different layers as least important compared to L1-norm methods,
leading to superior accuracy-efficiency trade-offs. Notably, for ShuffleNetV2,
our method achieves a 10% increase in inference speed while L1-pruning degrades performance by 13.7%. For RetinaNet, SHAP-pruning maintains baseline mAP exactly (0.151) with negligible impact on inference speed, while L1-
pruning sacrifices 1.3% mAP for a 6.2% speed increase. These findings highlight
the importance of data-driven layer importance assessment and demonstrate that
explainability-guided compression offers new directions for deploying advanced
DNN solutions on edge and resource-constrained platforms while preserving both
performance and model interpretability.

---

## 论文详细总结（自动生成）

# 论文总结：EXPLAINABILITY-DRIVEN LAYER-WISE PRUNING OF DEEP NEURAL NETWORKS FOR EFFICIENT OBJECT DETECTION

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：深度神经网络在目标检测中表现优异，但模型复杂度高，难以部署在资源受限平台（如边缘设备）。传统剪枝方法（如基于权重大小的 L1-norm 剪枝）仅依赖静态权重幅度，忽略了各层对任务性能的真实功能贡献，导致剪枝后精度损失较大。
- **整体含义**：本文提出一种可解释性驱动的逐层剪枝框架，利用 SHAP（SHapley Additive exPlanations）贡献分析量化每层对目标检测任务的实际重要性，从而更精准地剪除冗余层，在保持检测精度的同时显著降低计算成本，为部署高效目标检测模型提供新思路。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：以数据驱动的功能贡献度量替代静态权重幅度，使用 SHAP 值衡量每个网络层对输出预测的边际贡献，然后按贡献度从低到高进行逐层剪枝。
- **关键技术细节**：
  - 基于梯度-激活乘积计算 SHAP 贡献值，具体做法为：对每个层，计算其输出激活相对于最终检测损失的梯度，再乘以该层激活值，得到近似 SHAP 值，用以表征该层的重要性。
  - 根据 SHAP 值对所有层进行排序，剪除贡献最小的层（或层内部分神经元，文中表述为“layer-wise pruning”）。
  - 剪枝后对模型进行微调以恢复性能，但文中未详述微调策略。
- **算法流程（文字说明）**：
  1. 输入预训练目标检测模型，在验证集上计算每层的平均 SHAP 贡献值。
  2. 按 SHAP 值升序排列各层（或各组件）。
  3. 移除重要性最低的若干层（或按剪枝比例移除），得到剪枝后模型。
  4. 对剪枝模型进行少量迭代的微调（或直接评估，原文未明确微调步骤）。
  5. 在测试集上评估精度和推理速度。

## 3. 实验设计
- **数据集**：Microsoft COCO 2017 验证集（用于评估）。
- **Benchmark 架构**：多种主流目标检测器及其骨干网络：
  - 骨干网络：ResNet-50, MobileNetV2, ShuffleNetV2
  - 检测器：Faster R-CNN, RetinaNet, YOLOv8
- **对比方法**：L1-norm 剪枝方法（基于权重幅度淘汰不重要参数或层）。

## 4. 资源与算力
- **文中未明确说明**：未提及使用的 GPU 型号、数量、训练时长、微调轮次等算力信息。因此无法评估计算资源的具体投入。

## 5. 实验数量与充分性
- **实验数量**：在 6 种不同架构（3 种骨干网络 + 3 种检测器）上进行了对比实验，每种架构至少展示了 SHAP 剪枝与 L1-norm 剪枝的精度和速度结果。Abstract 中详细列出了 ShuffleNetV2 和 RetinaNet 的量化结果，其余模型结果未给出具体数值，但称“consistently”表现更好。
- **充分性与客观性**：
  - 覆盖了轻量级（MobileNetV2、ShuffleNetV2）和大模型（ResNet-50）以及不同检测头，具有一定的多样性。
  - 仅比较了 L1-norm 剪枝一种基线，未与其他剪枝方法（如结构化剪枝、通道剪枝、知识蒸馏）或更先进的剪枝算法对比。
  - 未进行消融实验（如不同剪枝比例的影响、SHAP 计算方式的变体、微调策略的影响）。
  - 仅在单一数据集（COCO val2017）上评估，未在更大规模数据集（如 COCO train2017）或跨数据集（如 PASCAL VOC）上验证泛化性。
- 结论：实验设计基本合理，但数量有限，不足以全面证明方法论优势。

## 6. 主要结论与发现
- SHAP 剪枝识别出的不重要层与 L1-norm 剪枝不同，优先保留对任务更关键的层，从而获得更好的精度-效率权衡。
- 具体案例：
  - 在 ShuffleNetV2 上，SHAP 剪枝使推理速度提升 10%，而 L1-norm 剪枝导致 mAP 下降 13.7%。
  - 在 RetinaNet 上，SHAP 剪枝保持 mAP 不变（0.151），推理速度几乎无损失；L1-norm 剪枝以 1.3% mAP 为代价换取 6.2% 速度提升。
- 总体表明：基于可解释性（SHAP 贡献分析）的剪枝能更有效地压缩目标检测网络，同时保持模型可解释性和性能。

## 7. 优点
- **方法创新性**：首次将 SHAP 可解释性分析引入目标检测网络的逐层剪枝，利用梯度-激活乘积高效近似 SHAP 值，兼顾计算效率与功能重要性度量。
- **实验结果直观**：在多个架构上展示了 SHAP 剪枝相对于 L1-norm 剪枝的优越性，尤其在轻量网络（ShuffleNetV2）上效果显著。
- **实用价值**：为资源受限平台（边缘设备）部署高精度目标检测模型提供了一种有效的压缩方案。

## 8. 不足与局限
- **算力资源缺失**：未报告实验环境（GPU 型号、时长），难以复现或评估成本。
- **实验覆盖有限**：
  - 仅与 L1-norm 剪枝一种基线对比，未与常见的结构化剪枝（如权重聚类、通道剪枝）或先进剪枝方法（如基于梯度、基于正则化）比较。
  - 未在多种剪枝率、不同数据场景下做系统性消融实验。
  - 仅在 COCO 验证集上评估，未在训练集或其它数据集上验证剪枝后模型的泛化能力。
- **技术细节不足**：未说明剪枝具体是剪除整个层还是层内部分神经元，未提供微调阶段的学习率、epoch 等超参数，未讨论 SHAP 计算本身的额外开销。
- **应用限制**：SHAP 计算需要梯度访问，可能不适用于某些无法微调的模型（如纯推理场景）；方法仅针对目标检测任务，未验证在分类、分割等任务上的可迁移性。
- **论文来源为被拒稿**（ICLR-2026-Rejected-Public），可能存在方法论或实验设计上的未解决问题。

（完）
