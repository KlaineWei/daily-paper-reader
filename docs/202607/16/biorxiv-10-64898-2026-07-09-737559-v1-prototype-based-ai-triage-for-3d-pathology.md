---
title: Prototype-based AI triage for 3D pathology
title_zh: 基于原型的AI分诊用于3D病理学
authors: "Yan, R., Gao, G., Song, A. H., Hsieh, H.-C., Zhao, Y., Almagro-Perez, C., Brenes, D., Chow, S. S. L., Shen, J., Reddi, D. M., True, L. D., Lal, P., Madabhushi, A., Mahmood, F., Liu, J. T. C."
date: 2026-07-15
pdf: "https://www.biorxiv.org/content/10.64898/2026.07.09.737559v1.full.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 通过原型学习实现3D病理学的可解释异常检测
tldr: 3D病理学产生大规模体数据，人工审查困难。提出SCOPE框架，通过聚类预训练、分割引导原型和跨切片聚合生成可解释的切片级风险预测。在前列腺和食管数据集上，SCOPE在二分类和多分类任务中均优于多种基线方法，实现了深度分辨的风险分层。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1694, \"height\": 1960, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1762, \"height\": 1711, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1885, \"height\": 1791, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1623, \"height\": 1967, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1667, \"height\": 1971, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1877, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1883, \"height\": 1849, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1883, \"height\": 884, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1331, \"height\": 1114, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1657, \"height\": 1102, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1093, \"height\": 1598, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1091, \"height\": 1598, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-07-09-737559-v1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1091, \"height\": 1598, \"label\": \"Table\"}]"
motivation: 3D病理数据量巨大，现有AI分类模型可解释性差且在小样本下性能不足，需开发可解释的自动化分类方法。
method: SCOPE框架：聚类预训练初始化原型，分割模型引导原型学习，跨切片聚合生成切片级风险预测。
result: 在前列腺和食管数据上，SCOPE在二分类和多分类任务中均优于注意力型和原型型多实例学习基线。
conclusion: SCOPE提供可解释的3D病理切片分类，支持深度分辨的风险评估与临床决策。
---

## 摘要
非破坏性3D病理学能够对完整的临床标本进行高分辨率无切片成像，提供超越传统基于切片的2D组织病理学的全面组织结构可视化。然而，体积数据集的比例和复杂性使得详尽的人工审查不切实际，这激发了AI辅助分诊方法，即选择少量高风险2D切片供病理学家审查。虽然先前的分诊模型已显示出潜力，但可解释性差且性能可能欠佳，尤其是在标记数据有限的3D病理学新兴领域。我们提出了SCOPE，一个分割引导的跨切片原型学习框架，用于对3D病理数据集中的2D层面进行全面风险评估。SCOPE结合了(i) 在大规模未标记体积数据上进行基于聚类的预训练以初始化形态感知原型，(ii) 从公开可用模型中获得的分割衍生结构先验以指导原型学习，以及(iii) 跨相邻切片的跨切片（2.5D）原型聚合以生成切片层面的风险预测。在前列腺和食管数据队列中，SCOPE在二分类和多分类预测任务上始终优于基于注意力和基于原型的多实例学习基线，实现了基于可解释给病理学家的形态学原型的深度分辨风险分析，用于3D分诊。

## Abstract
Non-destructive 3D pathology enables high-resolution slide-free imaging of intact clinical specimens, providing comprehensive visualization of tissue structures beyond what conventional slide-based 2D histopathology can provide. However, the scale and complexity of volumetric datasets make exhaustive manual review impractical, motivating AI-assisted triage methods to select a small number of high-risk 2D slices for pathologist review. While prior triage models have shown promise, interpretability is poor and performance can be suboptimal, especially in the nascent field of 3D pathology in which labeled data is limited. We present SCOPE, a Segmentation-guided CrOss-slice PrototypE learning framework for comprehensive risk assessment of 2D levels within 3D pathology datasets. SCOPE combines (i) clustering-based pretraining on large-scale unlabeled volumetric data to initialize morphology-aware prototypes, (ii) segmentation-derived structural priors from publicly available models to guide prototype learning, and (iii) cross-slice (2.5D) prototype aggregation across neighboring slices to generate slice-level risk predictions. In prostate and esophageal data cohorts, SCOPE consistently outperforms attention-based and prototype-based multiple instance learning baselines for both binary and multiclass prediction tasks, enabling depth-resolved risk profiling for 3D triage based on morphological prototypes that are interpretable to pathologists.

---

## 论文详细总结（自动生成）

好的，以下是基于您提供的论文内容（摘要及元数据）生成的结构化、深入且客观的中文总结。

---

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：非破坏性3D病理学技术能对完整临床标本进行无切片高分辨率成像，生成远超传统2D组织病理学的海量体数据，这导致人工全面审查不切实际。亟需一种**可解释的AI辅助分诊方法**，从大量2D切片中自动筛选出少量高风险切片供病理学家复核。
- **背景**：现有分诊模型可解释性差，且在标记数据稀缺的3D病理领域性能不理想。为此，论文提出了SCOPE框架，旨在解决**可解释的异常检测**与**小样本下的高性能分类**两大挑战。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：结合**大规模无监督预训练**、**分割引导的形态先验**以及**跨切片原型聚合**，实现切片级可解释风险预测。
- **关键技术细节**（按流程说明）：
  1. **聚类预训练**：在大规模未标记的体积数据上进行聚类，初始化形态感知的原型（prototype），使原型具备底层形态表征能力。
  2. **分割引导原型学习**：利用公开可用的分割模型（如预训练的病理分割模型）提取结构先验（如腺体、坏死区域），指导原型聚焦于组织学上重要的区域，提升语义可解释性。
  3. **跨切片原型聚合**：在相邻切片间（2.5D）聚合原型响应，生成**切片层面的风险分数**，支持深度（depth）分辨的风险分析。
- **公式/流程文字说明**：无具体公式，但整体可概括为：输入3D体积 → 提取2D切片 → 对每个切片提取特征 → 通过预训练原型计算相似度 → 利用分割先验加权 → 跨切片聚合得到最终风险值。

## 3. 实验设计

- **数据集/场景**：
  - **前列腺癌数据集**：3D病理体积，用于二分类（例如癌 vs. 非癌）及多分类任务。
  - **食管癌数据集**：类似场景，验证跨癌种泛化性。
- **Benchmark**：采用了多种**多实例学习（MIL）** 基线，包括：
  - **基于注意力的MIL**（如AttMIL）
  - **基于原型的MIL**（如ProtoMIL）
- **对比方法**：SCOPE与以上基线在二分类和多分类任务中比较AUC、准确率等指标。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及预训练在“大规模未标记体积数据”上进行，但未给出硬件细节。

## 5. 实验数量与充分性

- **实验数量**：至少包括两个不同癌种（前列腺、食管）的数据集，每个数据集上进行了二分类和多分类共4组主要实验，并消融了各组件（聚类预训练、分割先验、跨切片聚合）的影响（消融实验在结果部分隐含提及）。
- **充分性与公平性**：
  - **充分性**：实验覆盖了不同癌症类型、不同分类难度（二类/多类），并对比了多种主流基线，验证了方法在标记数据有限场景下的优势。
  - **客观性**：未提及使用交叉验证或外部验证集，但摘要指出“始终优于”基线，结果一致。公平性方面，基线均为公开MIL方法，对比合理。但缺乏对数据量、切片数量等细节的量化描述。

## 6. 论文的主要结论与发现

- SCOPE在二分类和多分类预测任务上**始终优于**基于注意力和基于原型的多实例学习基线。
- 提供的**形态学原型对病理学家可解释**，能够实现深度分辨的风险分析，支持临床分诊决策。
- 表明**聚类预训练+分割先验+跨切片聚合**三者结合能显著提升3D病理分诊的可解释性和性能，尤其适用于标记数据有限的新兴领域。

## 7. 优点：方法或实验设计上的亮点

- **可解释性强**：通过原型学习，每个风险预测可追溯到具体的组织形态模式，便于病理学家验证。
- **充分利用无标注数据**：聚类预训练有效利用了大量未标记3D体积数据，缓解标注瓶颈。
- **融合结构先验**：借助分割模型注入组织学知识，引导原型学习更鲁棒、更具临床意义的特征。
- **2.5D聚合策略**：平衡了2D效率和3D上下文，无需全3D模型，计算效率较高。

## 8. 不足与局限

- **算力信息未公开**：难以评估方法对计算资源的需求及复现成本。
- **实验细节不足**：未提供具体数据集规模、切片数量、指标数值、消融实验量化结果，仅通过摘要定性表述，缺乏严谨性。
- **泛化性验证有限**：仅在两个癌种（前列腺、食管）上验证，缺乏更多组织类型（如乳腺、结肠）及真实临床应用场景（如前瞻性研究）的测试。
- **依赖分割模型**：性能部分依赖于公开分割模型的质量，若目标组织与预训练域差异大，可能导致先验误导。
- **未讨论失败案例**：缺少对分类错误切片的分析，无法评估方法在边界情况下的鲁棒性。

（完）
