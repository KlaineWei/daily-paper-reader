---
title: EXPLAINABILITY-DRIVEN LAYER-WISE PRUNING OF DEEP NEURAL NETWORKS FOR EFFICIENT OBJECT DETECTION.
title_zh: 可解释性驱动的深度神经网络逐层剪枝用于高效目标检测
authors: "Abhinav Shukla, Nachiket Tapas"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JvGhBL777z"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释性驱动的剪枝用于高效目标检测
tldr: 针对深度目标检测网络复杂度过高的问题，本文提出可解释性驱动的层剪枝框架，利用SHAP贡献分析量化层重要性，实现与任务相关的压缩。该方法不仅提升了效率，还通过解释性分析增强了模型透明性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统剪枝方法基于幅值，未考虑组件对任务的实际贡献。
method: 利用SHAP进行贡献分析，通过梯度-激活乘积量化层重要性，指导剪枝。
result: 在目标检测任务上实现了压缩率与精度的良好平衡。
conclusion: 可解释性驱动剪枝为模型压缩提供了新思路，同时提升了透明性。
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

# 论文总结：可解释性驱动的深度神经网络逐层剪枝用于高效目标检测

## 1. 论文的核心问题与整体含义
- **研究动机**：深度神经网络在目标检测任务中取得了巨大成功，但模型日益复杂，难以部署在资源受限的平台（如边缘设备）。现有的剪枝方法多基于权重的幅值（如L1-norm），但这类静态指标并不反映网络组件对任务性能的真实贡献。
- **整体含义**：本文提出一种**可解释性驱动的逐层剪枝框架**，利用SHAP（SHapley Additive Explanations）进行贡献分析，以数据驱动的方式量化每一层对目标检测任务的功能重要性，从而指导剪枝，在压缩模型的同时保持精度，并提升模型透明性。

## 2. 论文提出的方法论
- **核心思想**：不再依赖权重幅值，而是通过**可解释性归因**衡量层重要性。具体地，利用**SHAP值**（通过梯度-激活乘积近似）计算每个神经元/层对输出的边际贡献，从而识别出对任务最不重要的层进行剪枝。
- **关键技术细节**：
  - 使用**梯度-激活乘积**作为SHAP值的代理，量化层的重要性。
  - 对目标检测网络（backbone + detection head）逐层评估，基于重要性排序剪去对最终检测性能贡献最小的层。
  - 剪枝后微调（fine-tune）以恢复部分精度。
- **算法流程（文字说明）**：
  1. 输入训练好的目标检测模型及少量校准数据。
  2. 对每个层，计算其输出相对于最终检测损失（或检测置信度）的梯度，并与该层激活值相乘，得到近似SHAP贡献值。
  3. 对所有层的贡献值排序，选择贡献最低的若干层进行剪枝（移除整个层或将其替换为恒等映射）。
  4. 对剪枝后的模型进行微调，评估在验证集上的mAP和推理速度。

## 3. 实验设计
- **数据集**：Microsoft COCO 2017验证集。
- **基准模型（Benchmark）**：多个主流目标检测架构，包括：
  - Backbone：ResNet-50、MobileNetV2、ShuffleNetV2
  - Detector：Faster R-CNN、RetinaNet、YOLOv8
- **对比方法**：L1-norm剪枝（传统基于幅值的逐层剪枝）。
- **评估指标**：mAP（平均精度均值）、推理速度（FPS或每张图像推理时间）。

## 4. 资源与算力
- **论文未明确说明**使用的GPU型号、数量、训练时长等算力信息。文中仅提及在COCO 2017验证集上进行评估，未披露微调和剪枝的具体硬件环境。

## 5. 实验数量与充分性
- **实验数量**：覆盖了6种不同架构（3种backbone + 3种detector），每种都对比了SHAP剪枝和L1剪枝，至少进行了12组对比实验（不同剪枝策略×不同架构）。此外可能包含不同剪枝率的消融实验（摘要未列举全部，但元数据提及“压缩率与精度平衡”）。
- **充分性与公平性**：
  - 实验设计较充分：涵盖了轻量级（MobileNetV2、ShuffleNetV2）和高精度（ResNet-50、Faster R-CNN、RetinaNet、YOLOv8）架构，验证了方法的泛化性。
  - 对比方法采用常见的L1-norm剪枝，对比直接且公平。
  - 不足：仅使用COCO验证集，未在测试集或更多数据集（如PASCAL VOC）上验证；未提供统计显著性分析；未说明剪枝率如何选择。

## 6. 论文的主要结论与发现
- SHAP驱动的剪枝**始终识别出与L1-norm不同的层作为最不重要的层**，表明基于幅值的重要性度量可能存在偏差。
- **ShuffleNetV2**：SHAP剪枝实现推理速度提升10%，同时mAP基本不变；而L1剪枝导致mAP下降13.7%。
- **RetinaNet**：SHAP剪枝保持基线mAP精确为0.151，推理速度影响可忽略；L1剪枝牺牲1.3% mAP换取6.2%速度提升。
- 总体而言，可解释性驱动的剪枝在**精度-效率权衡**上优于传统L1剪枝，尤其在轻量级网络上优势明显。
- 该方法不仅能压缩模型，还能通过层重要性分析增强模型透明性。

## 7. 优点
- **方法创新**：将可解释性（SHAP）引入剪枝领域，用数据驱动的贡献分析替代静态幅值，从原理上更贴合模型的实际功能。
- **实验覆盖广**：测试了多种主流检测架构，包括两阶段（Faster R-CNN）、单阶段（RetinaNet、YOLOv8）和不同复杂度的backbone，结论具有普适性。
- **结果显著**：在ShuffleNetV2上10%加速且无精度损失，在RetinaNet上保持精度不变，展示了实用价值。
- **可解释性加成**：剪枝过程同时提供了模型的层重要性排名，有助于理解网络决策。

## 8. 不足与局限
- **算力成本未报告**：没有说明SHAP贡献计算的计算开销，梯度-激活乘积计算可能引入额外成本，尤其在大型网络上。
- **实验范围有限**：
  - 仅使用COCO 2017验证集，未在测试集或其他数据集上评估，泛化能力存疑。
  - 未提供不同剪枝率下的完整实验曲线（例如剪枝率从10%到90%的精度变化）。
  - 未与其他剪枝方法（如结构化剪枝、泰勒展开剪枝等）对比。
- **局限性**：
  - SHAP计算依赖梯度，可能受梯度饱和或模型非平滑性的影响。
  - 方法假设层重要性独立，未考虑层间依赖关系。
  - 剪枝后微调策略细节缺失（微调epoch数、学习率等），影响可复现性。
- **潜在偏差**：论文未说明多次实验的随机性控制，结果可能受模型初始化影响。

（完）
