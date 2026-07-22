---
title: Interpretable Peripheral Blood Cell Classification via Vision-Language Concept Bottleneck and Soft Decision Tree
title_zh: 基于视觉-语言概念瓶颈和软决策树的可解释外周血细胞分类
authors: "Chen, K., Hu, T."
date: 2026-07-20
pdf: "https://www.biorxiv.org/content/10.64898/2026.07.14.738462v1.full.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 通过视觉-语言概念瓶颈和软决策树实现可解释分类
tldr: "现有深度学习外周血细胞分类系统无法用临床形态标准解释决策，妨碍审计验证。本文提出两阶段可解释流水线：先用ConceptCLIP将细胞图像零样本映射到70个形态概念得分，再用软决策树基于这些得分分类。在BloodMNIST上达到94.86%准确率，决策路径完全可追溯，并自动分离出未标注的粒细胞亚型，验证了概念瓶颈与决策树结合的可解释价值。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1763, \"height\": 572, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 877, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1833, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1295, \"height\": 2488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 442, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 905, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 904, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 920, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-14-738462-v1/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1852, \"height\": 356, \"label\": \"Table\"}]"
motivation: 解决外周血细胞分类黑箱问题，使模型决策符合临床形态学标准，便于审计验证。
method: 第一阶段用ConceptCLIP零样本计算细胞图像与70个形态概念的余弦相似度；第二阶段用软决策树基于概念得分分类，输出可解释决策路径。
result: "在BloodMNIST上准确率94.86%，仅低于黑箱模型3个百分点，决策路径符合血液学形态，并发现未监督的粒细胞亚型分离。"
conclusion: 概念瓶颈与软决策树结合能实现高精度可解释分类，并揭示超出标签粒度的临床意义。
---

## 摘要
动机：用于医学图像分析的深度学习分类器通常以黑箱方式运作，既不揭示其预测所依据的图像特征，也不说明每个决策的推理过程。外周血细胞分类体现了这一挑战：经验丰富的实验室专业人员通过结构化的形态学标准——细胞核形状、染色质纹理、核质比、颗粒度和染色特性——来识别细胞类型，然而现有的自动化系统无法以相同的术语表达其推理过程，从而阻碍了临床审核和验证。

结果：我们提出了一种两阶段的可解释流程，旨在解决这两个层面的不透明性。在第一阶段，一个冻结的领域自适应视觉-语言模型（ConceptCLIP）通过零样本余弦相似度将每个细胞图像投影到一个70维的形态学概念分数向量上，从而消除了对每张图像概念标注的需求。在第二阶段，一个软决策树（SDT）仅基于这些概念分数对细胞进行分类，为每个预测产生一个确定性的、基于概念的决策路径。在BloodMNIST数据集（八种细胞类型，3421张测试图像）上，完整流程达到了94.86%的测试准确率——比黑箱上限低约3个百分点——同时提供了完全可追溯的决策逻辑。训练后的组织学注释证实，学习到的路由逻辑与既定的血液学形态学标准一致，并揭示了未成熟粒细胞亚型（早幼粒细胞与中幼粒细胞）的无监督区分，这表明基于概念的决策树能够恢复超出训练标签粒度的临床意义区别。

可用性和实现：源代码、训练好的SDT权重、预计算的概念分数数据以及推理脚本可在https://github.com/aquamarineaqua/CLIP-CBM-SoftDecisionTree公开获取。

## Abstract
MotivationDeep learning classifiers for medical image analysis typically function as black boxes, disclosing neither the image features underlying their predictions nor the reasoning by which individual decisions are reached. Peripheral blood cell classification exemplifies this challenge: experienced laboratory professionals identify cell types through structured morphological criteria--nucleus shape, chromatin texture, nucleus-to-cytoplasm ratio, granularity, and staining properties--yet existing automated systems cannot express their reasoning in these same terms, impeding clinical audit and verification.

ResultsWe present a two-stage interpretable pipeline that addresses both levels of opacity. In the first stage, a frozen domain-adapted vision-language model (ConceptCLIP) projects each cell image onto a 70-dimensional vector of morphological concept scores via zero-shot cosine similarity, eliminating the need for per-image concept annotations. In the second stage, a Soft Decision Tree (SDT) classifies cells solely on these concept scores, producing a deterministic, concept-based decision path for each prediction. On BloodMNIST (eight cell types, 3,421 test images), the full pipeline achieves 94.86% test accuracy--approximately 3 percentage points below the black-box ceiling--while providing fully traceable decision logic. Post-training histological annotation confirms that the learned routing logic aligns with established hematological morphology criteria and reveals an emergent separation of immature granulocyte subtypes (promyelocyte versus metamyelocyte) without subtype supervision, demonstrating that concept-based decision trees can recover clinically meaningful distinctions beyond the granularity of the training labels.

Availability and implementationThe source code, trained SDT weights, precomputed concept score data, and inference scripts are publicly available at https://github.com/aquamarineaqua/CLIP-CBM-SoftDecisionTree.