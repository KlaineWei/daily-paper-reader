---
title: "CAKE: Category Aware Knowledge Extraction for Open-Vocabulary Object Detection"
title_zh: CAKE：面向开放词汇目标检测的类别感知知识提取
authors: "Shiyuan Ma, Donglin Qian, Kai Ye, Shengchuan Zhang"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/32639/34794"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 目标检测方法，缺乏可解释性关注
tldr: 该论文针对开放词汇目标检测中未知类别被抑制的问题，提出CAKE方法，利用视觉语言模型进行类别感知知识提取，改善了未知类别的检测性能。但方法本身不提供可解释性，专注于知识蒸馏。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32639/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 832, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32639/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1830, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32639/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 875, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32639/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1824, \"height\": 547, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32639/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1452, \"height\": 824, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32639/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1686, \"height\": 493, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32639/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 867, \"height\": 454, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32639/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 885, \"height\": 355, \"label\": \"Table\"}]"
motivation: 现有知识蒸馏框架未能利用全局类别信息，导致模型过拟合基类并抑制新类别。
method: 通过类别感知的知识提取，从视觉语言模型中提取类别特定知识，并缓解新类别被抑制问题。
result: 在开放词汇目标检测基准上取得显著性能提升。
conclusion: 该方法有效增强了模型对未知类别的检测能力，但可解释性方面未探索。
---

## Abstract
Open vocabulary object detection (OVOD) task aims to detect objects of novel categories beyond the base categories in the training set. To this end, the detector needs to access image-text pairs containing rich semantic information or the visual language pre-trained model (VLM) learned on them. Recent OVOD methods rely on knowledge distillation from VLMs. However, there are two main problems in current methods: (1) Current knowledge distillation frameworks fail to take advantage of the global category information of VLMs and thus fail to learn category-specific knowledge. (2) Due to the overfitting phenomenon of base categories during training, current OVOD networks generally have the problem of suppressing novel categories as background. To address these two problems, we propose a Category Aware Knowledge Extraction framework (CAKE), which consists of a Category-Specific Knowledge Distillation branch (CSKD) and a Category Generalization Region Proposal Network (CG-RPN). CSKD can more fully extract category-strong related information through category-specific distillation, and it is also conducive to filtering the exclusion problem between individuals of the same category; in this process, the model constructs a category-specific feature set to maintain high-quality category features. CG-RPN leverages the guidance of feature set to adjust the confidence scores of region proposals, thereby mining proposals that potentially contain novel categories of objects.
Extensive experiments show that our method can plug and play well with many existing methods and significantly improve their detection performance. Moreover, our CAKE framework can reach the-state-of-the-art performance on OV-COCO and OV-LVIS datasets.

---

## 论文详细总结（自动生成）

# CAKE：面向开放词汇目标检测的类别感知知识提取 — 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：开放词汇目标检测（OVOD）旨在检测训练集中未出现的新类别（novel categories）目标。现有方法依赖从视觉语言模型（如CLIP）进行知识蒸馏，但存在两个关键问题：（1）蒸馏框架未能充分利用VLM的全局类别信息，无法学习类别特定的知识；（2）由于模型在基类（base categories）上过拟合，导致新类别容易被抑制为背景。
- **研究动机**：为了解决上述问题，作者提出CAKE框架，通过类别感知的知识提取（Category-Aware Knowledge Extraction）来增强新类别的检测能力，并缓解基类过拟合。

## 2. 方法论：核心思想、关键技术细节

### 整体框架
CAKE由两个核心模块组成：**类别特定知识蒸馏分支（CSKD）**和**类别泛化区域提议网络（CG-RPN）**。框架基于Faster R-CNN构建，利用CLIP作为教师模型。

### 关键模块

#### （1）类别特定知识蒸馏（CSKD）
- **目标**：提取与类别高度相关的特征，构建高质量的类别特定特征集。
- **组成**：
  - **对象级蒸馏（OD）**：对区域提议的特征进行蒸馏，包括特征嵌入对齐和关系矩阵对齐（相似度矩阵）。损失函数包含个体特征距离和关系矩阵差异。
  - **簇级蒸馏（CD）**：将同一类别的特征聚类，并对齐学生和教师的聚类中心；同时增强不同类别间的分离性。损失包含簇中心距离和跨簇距离。
- **特征集S**：使用CLIP嵌入构建高质量特征集，每个类别对应一个聚类簇，每个簇维护不超过l个特征。特征质量得分（QS）基于对象性和密度计算，并引入时间衰减因子。只有QS高于阈值的特征才能更新到S中。

#### （2）类别泛化区域提议网络（CG-RPN）
- **目标**：缓解RPN对基类的偏见，挖掘可能包含新类别的提议。
- **方法**：
  - 从特征集S中通过奇异值分解（SVD）得到特征子空间Ω。
  - 对每个提议的嵌入fp，计算其与Ω上投影的余弦相似度μ，作为相关性分数。
  - 调整最终的对象性分数：p = max(min(o + ρ(μ), 1), 0)，其中o是RPN原始分数，ρ为可学习的线性层。
  - 损失函数包括二元交叉熵损失和回归损失（仅对正样本）。

#### （3）整体训练目标
L = L_reg + L_cls + λ1 L_CG-RPN + λ2 L_CSKD，其中L_CSKD = L_OD + λ3 L_CD。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **OV-COCO**：从COCO中划分48个基类、17个新类别，15个未使用。评估指标为AP_novel_50、AP_base_50、AP_50。
  - **OV-LVIS**：从LVIS v1中划分337个罕见类别（新类别）和886个常见/频繁类别（基类）。评估指标为AP_r（罕见类）、AP_c、AP_f、AP。
- **基准设置**：遵循ViLD和OV-RCNN的划分方式，训练时移除新类别标注。采用Faster R-CNN（ResNet-50）为主干，基线方法为OC-OVD。
- **对比方法**：
  - OV-COCO：对比OADP、DK-DETR、BARON、LBP、OV-DETR、VL-PLM、RegionCLIP、CoDet、Detic、GOAT、OC-OVD等。
  - OV-LVIS：对比DetPro、OC-OVD、OADP、CORA、DK-DETR、BARON、CoDet、LBP等。
  - 插件评估：将CAKE集成到OC-OVD、OADP、BARON中，并与RALF对比。

## 4. 资源与算力

- 论文明确提及：使用Nvidia RTX 3090 GPU，batch size=8（每GPU 2张图像），梯度下降采用SGD（weight decay=1e-4，momentum=0.9）。学习率0.01，在8和11 epoch时降低10倍。训练1× schedule（90000次迭代）。未具体说明使用多少张GPU，推测为4张或8张。未明确训练总时长。

## 5. 实验数量与充分性

- **实验组数**：至少包括以下部分：
  - OV-COCO上4种基准设置（V-OVD, G-OVD, C-OVD, WS-OVD）的结果对比。
  - OV-LVIS上的检测与分割结果对比。
  - 插件测试：3个基线方法（OC-OVD, OADP, BARON）的增强效果。
  - 消融实验：CSKD和CG-RPN各组件的影响；超参数（λ1, λ2, λ3, l, τ, T_QS）分析（部分在补充材料）。
  - 可视化对比（6个场景）。
- **充分性评价**：实验覆盖了主流基准、多个对比方法、多种设置；消融实验验证了各组件的贡献，且插件测试证明了泛化性。但超参数敏感度分析仅在补充材料中，未在正文充分展开。整体实验设计客观公平，遵循了领域标准划分。

## 6. 主要结论与发现

- CAKE在OV-COCO的WS-OVD设置下达到AP_novel_50=41.8，AP_50=55.7，超越所有基于Faster R-CNN的方法，并接近甚至超过使用更强骨干（ViT、Swin）或Deformable DETR的方法。
- 在OV-LVIS上，AP_r达到25.0，比基线OC-OVD提升18.4%，且在所有类别上（AP=34.9）显著领先。
- 插件实验表明CAKE可有效提升OC-OVD、OADP、BARON的性能，优于同类插件方法RALF。
- 消融实验显示：对象级蒸馏贡献6.2 AP_novel_50，簇级蒸馏贡献2.1，CG-RPN进一步带来1.2提升。即便不引入新类别先验知识，CG-RPN也能显著提升。

## 7. 优点

- **方法创新性**：提出簇级蒸馏（CD）来学习类别强相关信息，同时利用特征集进行对象挖掘，有效解决了基类过拟合和新类别抑制问题。
- **插件即插即用**：CAKE可无缝集成到多种OVOD方法中，显著提升性能，表明其通用性。
- **实验全面**：覆盖多种基准设置、大规模数据集、多种对比方法和消融分析。
- **可视化直观**：展示的示例清晰表明CAKE能检测更多新类别对象且定位更准确。

## 8. 不足与局限

- **可解释性不足**：论文未探讨CAKE为何能提升新类别检测的机理，缺乏对特征集如何学习类别特定知识的理论分析。
- **超参数依赖**：多个超参数（λ1~λ3、l、τ、T_QS）需要通过随机搜索确定，未提供鲁棒性分析。
- **计算开销**：CG-RPN需要进行SVD分解并在每个批次更新特征集，可能增加训练时间，但论文未分析与基线相比的计算成本。
- **应用限制**：仅在Faster R-CNN架构上验证，未在Transformer类检测器（如DETR）上测试其通用性（虽然称“即插即用”，但实际仅验证了Faster R-CNN变体）。
- **数据集偏差**：OV-LVIS中罕见类别数量远大于常见类别，但模型在常见类别上的性能提升有限（AP_f仅提高约5.9个点 vs 新类别18.4个点），可能存在类别不平衡风险。
- **缺少消融实验细节**：关键超参数和特征集大小l的影响仅放在补充材料，正文中未充分讨论。

（完）
