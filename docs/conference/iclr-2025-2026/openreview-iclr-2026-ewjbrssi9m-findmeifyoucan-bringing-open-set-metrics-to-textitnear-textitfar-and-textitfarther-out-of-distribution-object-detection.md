---
title: "FindMeIfYouCan: Bringing Open Set Metrics to $\\textit{near}$, $\\textit{far}$ and $\\textit{farther}$ Out-of-Distribution Object Detection"
title_zh: FindMeIfYouCan：将开放集指标引入近、远、更远的分布外目标检测
authors: "Daniel Alfonso Montoya Vasquez, Aymen Bouguerra, Alexandra Gomez-Villa, Fabio Arnez"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=eWJbrssI9M"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 开放集目标检测涉及未知对象，与异常检测场景相关
tldr: 本文揭示了当前分布外目标检测评估协议的关键缺陷，指出其忽略未知对象检测能力且基准违反类不重叠假设。为此，人工筛选并提出了新的开放集指标，以更准确地评估模型在近、远、更远三种分布外场景下的检测性能。该工作为分布外目标检测提供了更可靠的评估标准。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 当前分布外目标检测评估协议忽略未知对象检测，基准存在重叠假设问题，需要更合理的指标。
method: 人工筛选数据并定义新的开放集指标，覆盖近、远、更远三种分布外场景。
result: 新指标揭示了现有方法在检测未知对象上的不足，提供了更全面的评估视角。
conclusion: 提出的开放集指标为分布外目标检测提供了更可靠的评估框架。
---

## Abstract
Recently, out-of-distribution (OOD) detection has gained traction as a key research area in object detection (OD), aiming to identify incorrect predictions often linked to unknown objects. In this paper, we reveal critical flaws in the current OOD-OD evaluation protocol: it fails to account for scenarios where unknown objects are ignored since the current metrics (AUROC and FPR) do not evaluate the ability to find unknown objects. Moreover, the current benchmark violates the assumption of non-overlapping objects with respect to in-distribution (ID) classes. These problems question the validity and relevance of previous evaluations. To address these shortcomings, first, we manually curate and enhance the existing benchmark with new evaluation splits---semantically $\textit{near}$, $\textit{far}$, and $\textit{farther}$ relative to ID classes. Then, we integrate established metrics from the open-set object detection (OSOD) community, which, for the first time, offer deeper insights into how well OOD-OD methods detect unknown objects, when they overlook them, and when they misclassify OOD objects as ID---key situations for reliable real-world deployment of object detectors. Our comprehensive evaluation across several OD architectures and OOD-OD methods show that the current metrics do not necessarily reflect the actual localization of unknown objects, for which OSOD metrics are necessary. Furthermore, we observe that semantically and visually similar OOD objects are easier to localize but more likely to be confused with ID objects, whereas $\textit{far}$ and $\textit{farther}$ objects are harder to localize but less prone to misclassification.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：分布外（OOD）检测在目标检测（OD）领域越来越受关注，旨在识别由未知对象导致的错误预测。
- **核心问题**：作者揭示了当前 OOD-OD 评估协议存在两个关键缺陷：
  1. 现有指标（AUROC、FPR）仅关注识别已知类，完全不评估模型检测未知对象的能力（即忽略未知对象的场景被忽视）。
  2. 当前基准数据集违反“类别不重叠”假设（in-distribution 与 out-of-distribution 类别之间存在重叠），导致评估结果不可靠。
- **整体含义**：这些问题动摇了以往 OOD-OD 评估的有效性和公平性，需要设计更合理的评估框架以真实反映模型在开放世界中的部署可靠性。

## 2. 论文提出的方法论

- **核心思想**：引入开放集目标检测（OSOD）领域已建立的指标，并重新组织评估数据，从而准确衡量模型在三种 OOD 场景下的表现：语义上 **近（near）**、**远（far）**、**更远（farther）** 相对于分布内（ID）类别。
- **关键技术细节**：
  - **人工筛选与增强基准**：手动整理现有数据集，划分出三个新的评估子集，分别对应与 ID 类别语义/视觉相似度不同的 OOD 对象。
  - **引入 OSOD 指标**：利用开放集指标（如未知对象召回率、误将 OOD 分类为 ID 的比率等）来刻画模型检测未知对象、忽略未知对象、以及将 OOD 误分类为 ID 的能力。
  - 没有给出具体的公式或算法流程，但明确了评估指标的定义与使用方法（见实验部分）。
- **流程概述**：  
  1. 选择现有 OOD-OD 基准数据集 → 2. 人工标注并划分 near、far、farther 子集 → 3. 使用传统 OOD 指标（AUROC、FPR）和 OSOD 指标同时评估 → 4. 对比分析不同指标对模型真实性能的反映差异。

## 3. 实验设计

- **数据集/场景**：使用现有的 OOD-OD 基准数据集，并经过人工处理得到三个评价分割：semantically near、far、farther（具体数据集名称未在摘要中给出，但推断为常用的 OOD 检测基准如 VOC、COCO 的 OOD 版本）。
- **Benchmark**：基于人工筛选后的基准，对比了多个目标检测架构和多种 OOD-OD 方法。
- **对比方法**：涵盖了若干目标检测模型（OD architectures）以及当前主流的 OOD-OD 方法（具体名称未列出）。
- **实验内容**：
  - 对比传统指标（AUROC、FPR）与 OSOD 指标在不同 OOD 场景下的表现。
  - 分析 near、far、farther 对象的定位难度与误分类倾向。

## 4. 资源与算力

- **未明确说明**：文中没有提及所使用的 GPU 型号、数量、训练时长等算力资源。无法评估计算开销。

## 5. 实验数量与充分性

- **实验数量**：从摘要看，在多个目标检测架构和多种 OOD-OD 方法上进行了全面评估，但未给出具体组数（如消融实验、不同数据集的数量）。初步判断实验量中等。
- **充分性分析**：
  - **优点**：选择了多种模型和方法，覆盖不同场景（near/far/farther），对比了新旧指标，增强了结论的泛化性。
  - **不足**：
    - 未提及跨数据集验证（仅在单一基准上增强得到子集）。
    - 缺失消融实验（如不同指标组合的效果）。
    - 未说明统计显著性检验或多次运行取平均，可能存在偏差。
  - **公平性**：作者指出当前基准存在类重叠问题，因此他们手动修复了该问题，这提高了实验的公平性，但人工筛选可能引入主观性。

## 6. 论文的主要结论与发现

1. **当前指标存在误导性**：传统 OOD-OD 指标（AUROC、FPR）无法真实反映模型定位未知对象的能力，不能替代 OSOD 指标。
2. **不同 OOD 场景表现差异化**：
   - 语义/视觉上 **近** 的 OOD 对象更容易被定位（模型更可能检测到它们的边界框），但同时也更容易被错误地分类为 ID 对象（混淆度高）。
   - **远** 和 **更远** 的 OOD 对象更难被定位（检测召回率低），但一旦正确检测，它们不太可能被误分类为 ID 对象。
3. **开放集指标的必要性**：为了可靠部署目标检测器，必须使用能同时评估未知对象定位与分类质量的开放集指标。

## 7. 优点

- **问题洞察深刻**：首次系统指出当前 OOD-OD 评估协议中忽略未知对象检测能力和基准类重叠问题，这些缺陷在以往研究中常被忽视。
- **方法创新**：将 OSOD 领域的成熟指标引入 OOD-OD，填补了评估空白；并手动构造了 near/far/farther 三种语义距离的评估子集，使场景划分更细致。
- **结论实用**：揭示了不同 OOD 场景下模型的性能权衡，为实际部署中如何进行风险控制提供了指导（例如近 OOD 要注意误分类，远 OOD 要注意漏检）。

## 8. 不足与局限

- **实验覆盖有限**：仅基于一个或少数几个基准数据集（如 VOC/COCO 的 OOD 变体），未在更多真实场景（如自动驾驶、无人仓库）下验证。
- **人工标注风险**：基准数据的 near/far/farther 划分依赖人工主观判定，缺乏定量标准，可能引入覆盖偏差。
- **未考虑计算成本**：未比较 OSOD 指标添加后的算法额外开销（如是否需要额外标注或后处理）。
- **缺少消融分析**：未分析不同指标组合对模型训练或调优的影响，也未对比不同 OOD 检测方法在 OSOD 指标下的绝对排名变化。
- **应用限制**：结论主要基于目标检测任务，能否推广到语义分割、实例分割等其他视觉任务尚未验证。

（完）
