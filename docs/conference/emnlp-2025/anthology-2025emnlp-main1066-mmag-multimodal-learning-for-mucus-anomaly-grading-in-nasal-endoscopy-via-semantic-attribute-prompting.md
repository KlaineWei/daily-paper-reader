---
title: "MMAG: Multimodal Learning for Mucus Anomaly Grading in Nasal Endoscopy via Semantic Attribute Prompting"
title_zh: MMAG：基于语义属性提示的鼻内窥镜黏液异常分级多模态学习
authors: "Xinpan Yuan, Mingzhu Huang, Liujie Hua, Jianuo Ju, Xu Zhang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1066.pdf"
tags: ["query:xai-objdet"]
score: 5.0
evidence: 医学图像异常分级与多模态学习
tldr: 黏液异常分级因分泌物外观模糊而困难。MMAG利用临床属性提示与排序感知的视觉语言模型，实现联合检测与分级，在鼻内窥镜数据集上达到高准确率。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1066/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 789, \"height\": 855, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1066/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1628, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1066/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1463, \"height\": 900, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1066/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1618, \"height\": 883, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1066/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 791, \"height\": 388, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1066/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1066/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1066/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1658, \"height\": 866, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1066/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1066/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1066/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 271, \"label\": \"Table\"}]"
motivation: 鼻腔分泌物外观模糊且结构多变，自动分级困难。
method: 构建临床属性提示，与多级视觉特征对齐，进行联合检测与分级。
result: 在异常分级任务中取得最优性能。
conclusion: 结构化提示能有效提升医学图像异常分级的准确性和可解释性。
---

## Abstract
Accurate grading of rhinitis severity in nasal endoscopy relies heavily on the characterization of key secretion types, notably clear nasal discharge (CND) and purulent nasal secretion (PUS). However, both exhibit ambiguous appearance and high structural variability, posing challenges to automated grading under weak supervision. To address this, we propose Multimodal Learning for Mucus Anomaly Grading (MMAG), which integrates structured prompts with rank-aware vision-language modeling for joint detection and grading. Attribute prompts are constructed from clinical descriptors (e.g., secretion type, severity, location) and aligned with multi-level visual features via a dual-branch encoder. During inference, the model localizes mucus anomalies and maps the input image to severity-specific prompts (e.g., “moderate pus”), projecting them into a rank-aware feature space for progressive similarity scoring.Extensive evaluations on CND and PUS datasets show that our method achieves consistent gains over Baseline, improving AUC by 6.31% and 4.79%, and F1 score by 12.85% and 6.03%, respectively.This framework enables interpretable, annotation-efficient, and semantically grounded assessment of rhinitis severity based on mucus anomalies.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：鼻内窥镜检查中，黏液异常（清涕CND和脓涕PUS）是评估鼻炎严重程度的关键指标，但其外观模糊、结构多变，在弱监督条件下自动分级非常困难。
- **现有方法不足**：传统的分类方法将严重程度视为固定类别（如no/mild/moderate/severe），忽略了疾病的序数（ordinal）渐进性；已有的视觉语言模型（如CLIP）缺乏空间感知和序数建模能力，导致相邻严重等级混淆。
- **动机**：提出一种结合结构化属性提示和排序感知视觉语言建模的框架（MMAG），实现从检测到分级的端到端联合学习，提升可解释性和标注效率。

## 2. 论文提出的方法论
- **核心思想**：构建临床属性提示（例如“分泌类型为PUS”），与多级视觉特征对齐，先定位异常区域，再将局部特征与严重度排序提示进行对齐，从而在弱监督下实现空间感知的分级。
- **三个关键模块**：
  1. **属性提示构建（APC）**：将临床属性（炎症、分泌类型、颜色、体积、附着、位置）转化为自然语言句子，嵌入到模板“a photo of the [Attribute]”中，通过图像-属性对比损失（IAC）和匹配损失（IAM）进行细粒度跨模态对齐。
  2. **异常感知区域对齐（AARA）**：
     - 使用冻结的CLIP视觉编码器提取多级特征（S1-S3），通过轻量适配器（MVFA）调整。
     - 计算图像特征与文本提示的余弦相似度，最大化对齐损失L_align。
     - 双分支推理：零样本分支（直接图像-文本相似度）和少样本分支（基于记忆库的余弦距离），加权集成得到最终分类和定位得分（C_pred, S_pred）。
  3. **排序感知严重度评估（RSA）**：
     - 建立排序感知特征空间，将局部特征与严重度排序提示（如“moderate pus”）对齐。
     - 使用左排序损失L_left和右排序损失L_right，强制预测相似度满足序数关系（例如当前类得分 > 相邻类得分）。
     - 总排序损失L_rank = average(L_right + L_left) over所有样本。

- **整体流程**：输入图像 → APC生成属性提示 → AARA提取多级视觉特征并与提示对齐 → 双分支预测异常分类和定位 → RSA将定位特征投影到排序空间，输出最终严重度等级。

## 3. 实验设计
- **数据集与场景**：
  - 鼻内窥镜数据集：CND（清涕）和PUS（脓涕），各1000张高清图像（1920×1080），由两位ENT专家独立标注，7:2:1划分训练/验证/测试。
  - 迁移场景：Hyper-Kvasir（胃肠道黏液子集）、CVC_ColonDB（息肉）、CVC_ClinicDB（息肉），用于检验泛化能力。
- **基准方法**：GDRNet、CLIP、OrdinalCLIP、CLIP-DR，以及各自加上MMAG模块的变体。
- **评估指标**：检测指标（AC-AUC、AS-AUC）和分级指标（ACC、F1、AUC），全在0-100%范围。
- **对比结果**：MMAG在各数据集上全面优于基线，CND上ACC提升至71.97%，F1提升至69.78%；PUS上ACC达84.13%，F1达85.93%。

## 4. 资源与算力
- 文中明确说明：使用单个NVIDIA Tesla V100 GPU（16GB内存），输入分辨率240×240，AdamW优化器（lr=0.0001），batch size=16，训练100 epochs。
- **未明确说明**：GPU数量（仅提及单个）、总训练时长、具体参数数量等。

## 5. 实验数量与充分性
- **实验组数**：
  - 主要对比实验：2个数据集 × 4个基线方法 × 每个方法加MMAG = 共16组结果（表2）。
  - 迁移实验：3个外部数据集（表3）。
  - 消融实验：零样本消融（表4，4个组件逐步增加）、少样本消融（表5，6种样本量）、双分支消融（表6，3种设置）。
  - 可视化：定性比较（图3-5）及相似度矩阵分析（图4）。
- **充分性评价**：实验设计较为全面，涵盖了多数据集、多方法对比、多角度消融、零/少样本以及迁移泛化。实验公平性较好（所有方法在同一划分和评估标准下），但未进行统计学显著性检验（如多次重复实验报告方差）。总体而言，实验充分且客观。

## 6. 论文的主要结论与发现
- MMAG在鼻内窥镜黏液异常分级任务上显著优于现有方法，AUC最高提升6.31%，F1提升12.85%。
- 属性提示能有效引导视觉定位，排序损失强制序数一致性，减少了相邻等级混淆。
- 少样本实验表明，仅需少量标注样本即可获得良好性能（16-shot时F1达78.54%），证明了框架的标注效率。
- 迁移实验显示模型能从鼻内窥镜泛化到结肠镜息肉和黏液场景，具有较好的领域适应性。
- 可视化分析证明热图能准确定位异常区域，且随严重度增加而增强，具备临床可解释性。

## 7. 优点
- **方法创新**：首次将结构化属性提示与排序感知视觉语言建模结合用于医学黏液异常分级，形成“检测-分级”范式。
- **弱监督能力**：在无/少标注条件下仍能实现高精度定位和分级，实用性强。
- **双分支集成设计**：零样本和少样本互补，提升鲁棒性。
- **轻量适配器**：只更新少量参数，避免过拟合，保持模型泛化性。
- **可解释性**：热图和相似度矩阵可直观展示模型决策依据，便于临床理解。
- **迁移性好**：在结肠镜数据集上也取得不错结果，验证了框架通用性。

## 8. 不足与局限
- **极低光照盲区**：暗鼻腔中透明或低对比度黏液可能被漏检或误判为无异常，影响严重程度评估。
- **数据集单一性**：仅使用了自身收集的鼻内窥镜数据（CND/PUS），缺乏多中心、多设备、大样本验证，可能存在偏差风险。
- **临床验证缺失**：实验仅停留在算法指标层面，未在真实临床流程中验证其决策支持价值。
- **计算开销**：虽提及GPU型号，但未详细分析推理速度或参数量，无法评估实际部署成本。
- **泛化边界**：迁移实验仅涉及结肠镜黏液/息肉，尚未测试其他解剖部位（如喉镜、支气管镜）。

（完）
