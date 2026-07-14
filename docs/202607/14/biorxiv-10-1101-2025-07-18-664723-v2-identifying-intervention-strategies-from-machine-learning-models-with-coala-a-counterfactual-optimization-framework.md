---
title: "Identifying intervention strategies from machine learning models with COALA: a counterfactual optimization framework"
title_zh: 使用COALA从机器学习模型中识别干预策略：一个反事实优化框架
authors: "Han, B., Duan, Q., Hu, T."
date: 2026-07-07
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.18.664723v2.full.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 可应用于目标检测、异常检测、伪造检测的反事实优化可解释AI框架
tldr: "机器学习模型常被视为黑箱，现有可解释性方法如SHAP侧重于特征重要性，但缺乏对特征交互和个性化干预的洞察。本文提出COALA框架，通过反事实优化为每个个体识别能最大程度提升预测结果的可行动干预策略。在NHANES数据集上训练的梯度提升树模型中，COALA揭示了不同个体的最优反事实剖面，且利用约束特征可预测这些反事实变化，准确率达85.4%。该方法为从复杂模型中提取个性化干预策略提供了新途径。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 937, \"height\": 1090}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1534, \"height\": 944}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 678}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1890, \"height\": 1094}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 926, \"height\": 646}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1898, \"height\": 882}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 656, \"height\": 237}]"
motivation: 现有可解释AI方法仅关注特征重要性，未能识别特征交互并提供个性化干预。反事实分析可用于生成可行动干预策略。
method: 提出COALA框架，通过优化反事实识别每个个体能最大改善预测结果的可行动变量变化，进而解释模型预测。
result: "在NHANES数据集上，COALA识别出不同个体的最优反事实剖面，且约束特征可预测这些变化，准确率85.4%。"
conclusion: COALA能有效从黑箱模型中提取个性化干预策略，并揭示驱动干预的特定特征。
---

## 摘要
动机：机器学习模型日益复杂，常作为黑箱运作，限制了我们对特征如何影响模型预测的理解。常见的可解释人工智能方法如SHAP（Shapley加法解释）专注于特征重要性，但未能识别特征间的交互，也无法指导针对性的个性化干预。反事实是假设性事件，通过改变特定变量来导致结果变化。这些因果陈述可应用于AI模型，以识别针对群体中不同个体的可操作干预措施。

结果：我们提出了AI中可操作可解释性的反事实优化框架（COALA）。COALA通过为每个个体识别最优反事实来解释模型，这些反事实被定义为能够导致预测结果最积极变化的可操作改变。当应用于基于国家健康与营养调查（NHANES）数据集训练的梯度提升树模型时，COALA识别出不同个体间的最优反事实轮廓。能够保持约束的特征以85.4%的准确率预测了个体的最优反事实变化，揭示了驱动个体最优反事实的具体特征。

可用性与实现：COALA实现的代码、合成数据、基于合成数据训练的模型以及复现结果和图形的代码可在https://github.com/brt-solo/COALA获取。NHANES 2017-2018数据集可从国家健康统计中心（NCHS）公开获取。本研究中使用的弗雷明汉心脏研究数据集是通过麻省理工学院开放式课程（MIT OCW）存储库分发的公开可用的弗雷明汉衍生数据集。

## Abstract
MotivationMachine learning (ML) models have become increasingly complex, often functioning as black boxes that limit our understanding of the features contributing to ML predictions. Common explainable AI (XAI) methods such as SHapley Additive exPlanations (SHAP) focus on feature importance but fall short in identifying interactions among features and informing targeted, personalized interventions. Counterfactuals are hypothetical events where specific variables are altered to cause a change in outcome. These causal statements can be applied to AI models to identify actionable interventions for different subjects in a population.

ResultsWe propose the framework Counterfactual Optimization for Actionable interpretabiLity in AI (COALA). COALA interprets models by identifying optimal counterfactuals for each subject, which are defined as actionable changes that lead to the most positive change in predicted outcome. When applied to a gradient boosted tree model trained on the National Health and Nutrition Examination Survey (NHANES) dataset, COALA identifies different profiles of optimal counterfactuals across subjects. Features that remain constrained were able to predict the optimal counterfactual changes for a subject at 85.4%, revealing specific features that drive what a subjects optimal counterfactual is.

Availability and ImplementationCode for COALA implementation, synthetic data, models trained on synthetic data, and code to replicate results and figures are available at https://github.com/brt-solo/COALA. The NHANES 2017-2018 dataset is publicly available from the National Center for Health Statistics (NCHS). The Framingham Heart Study dataset used in this study is a publicly available, Framingham-derived dataset distributed through the Massachusetts Institute of Technology OpenCourseWare (MIT OCW) repository.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：机器学习模型（如XGBoost、MLP）在生物医学应用中日益复杂，但通常作为“黑箱”运行，无法提供关于特征如何影响预测的透明解释。现有可解释AI（XAI）方法（如SHAP）虽能给出特征重要性，但无法识别特征之间的交互作用，也无法为个体提供可操作的干预策略。
- **反事实的潜力**：反事实（“如果改变X，结果会变为Y”）能够提供因果性陈述，可用于指导个性化干预。然而，现有反事实方法在生物医学领域面临三大挑战：①预测模型性能有限，个体反事实不可靠；②生物因素相互关联，需同时改变多个特征；③存在无数可能反事实，缺乏统一选择标准，难以比较个体间差异。
- **目标**：提出一种在群体层面识别最优反事实的框架，并揭示哪些约束特征决定了每个个体的最优反事实，从而实现个性化干预策略。

## 2. 方法论
### 核心思想
- **COALA（Counterfactual Optimization for Actionable interpretabiLity in AI）**：基于多样性进化算法（MAP-Elites），将反事实搜索空间划分为由“可变的特征类别”定义的单元格（cells），在每个单元格内独立搜索最优反事实。最优反事实定义为：通过改变指定类别中的特征，能使模型预测结果（或分类概率）取得最大改善的候选解。

### 技术细节
- **特征分类**：用户根据领域知识将全部特征划分为若干互斥的类别（如“遗传”、“环境”、“饮食”等）。每个单元格对应一对类别（即同时可变的特征集）。
- **搜索过程**（Algorithm 1）：
  - 初始化阶段：在每个单元格内随机生成一批反事实候选（对连续特征在观测范围内均匀采样，对二值特征随机赋值）。
  - 优化阶段：迭代进行，每次随机选择一个单元格，从该单元格中选取一个精英解（当前最优）和一个随机解作为父代，通过均匀交叉产生后代，再评估后代并更新该单元格的精英解。
  - 独立为每个输入样本重复上述过程，得到该样本在每个单元格中的最优反事实。
- **群体分析**：
  - 对所有样本的最优反事实中的可变特征值进行K-means聚类（z-score标准化后），通过轮廓系数确定最佳聚类数。
  - 对可变特征和约束特征分别做ANOVA，计算η²（组间平方和/总平方和），η²≥0.14视为大效应，表明该约束特征驱动了最优反事实的差异。
  - 使用PCA可视化反事实分布，并构建样本间的相似性网络（欧氏距离）。

## 3. 实验设计
### 数据集
- **合成数据集**：n=1000，9个特征，分为四个视图（遗传、环境、营养、代谢），包含显式交互项（如G1·E1、G2·M2·N2）。连续输出y。
- **NHANES 2017-2018**：真实生物医学数据，用于预测糖尿病（HbA1c≥6.5%）。包含人口统计学、临床、饮食等变量。
- **Framingham Heart Study (FHS)**：心血管疾病风险数据集，结果见于补充材料。

### 基准与对比方法
- **对比方法**：SHAP聚类——先计算每个样本在可变特征上的SHAP值，然后基于SHAP值进行层次聚类（Ward linkage），聚类数与COALA相同。
- **评估指标**：
  - 聚类质量：轮廓系数、Davies-Bouldin指数、Calinski-Harabasz指数。
  - 预测能力：用随机森林基于各样本的约束特征值预测聚类标签，计算平衡准确率（交叉验证和holdout验证）。
  - 可视化：PCA、相似性网络。

### 模型
- 合成数据：线性回归（仅捕捉加法关系）、MLP（可捕捉非线性/交互）、ground truth生成模型。
- 真实数据：XGBoost（梯度提升树）。
- 训练/测试分割：80/20。

## 4. 资源与算力
- 文中未明确提及使用的GPU型号、数量、训练时长等具体计算资源信息。
- 仅指出：COALA作为进化算法，计算成本与样本量呈线性增长；未来可探索降低计算开销的策略。

## 5. 实验数量与充分性
- **实验组数**：
  - 合成数据上：ground truth模型、线性回归模型、MLP模型各做一组COALA分析（共3组），并做了预期效果验证。
  - NHANES数据上：1组COALA分析 + 1组SHAP对比分析，并进行了聚类数选择、ANOVA检验、预测准确率比较。
  - FHS数据：补充材料中报告了类似比较（COALA 100% holdout准确率 vs SHAP 53.3%）。
- **充分性评价**：实验覆盖不同复杂度模型和多个数据集，验证了COALA在已知交互下的恢复能力（合成数据）、真实场景下的应用（NHANES）和泛化能力（FHS）。但缺少对进化算法超参数（种群大小、迭代次数、突变率等）的敏感性分析，也未对聚类数选择做更深入消融。总体较为充分，对比方法（SHAP）公平。

## 6. 主要结论与发现
- COALA能够识别出由约束特征（如腰围、遗传因子G1/G2）驱动的**不同最优反事实轮廓**，并准确揭示这些约束特征如何调制可变特征对预测结果的影响。
- 在NHANES上，腰围是驱动饮食干预策略差异的最主要约束特征（η²大），蛋白质、总糖、饱和脂肪是区分不同干预组的关键可变特征。
- 约束特征对COALA聚类标签的预测准确率远高于SHAP聚类（NHANES: 85.4% vs 32.4%；FHS: 100% vs 53.3%），表明COALA产生的群体结构更紧密地与个体的“固定属性”相关，更适合个性化干预。
- 合成数据实验证实COALA能恢复已知交互模式，并能诊断ML模型是否准确学习了交互（如MLP模型错误地让E2产生了不应有的效应）。

## 7. 优点
- **模型无关**：仅需模型预测函数，可应用于任何黑箱模型（XGBoost、MLP等）。
- **揭示特征交互**：通过分析约束特征对最优反事实的影响，直接揭示特征间的交互作用。
- **群体级可操作解释**：产生可聚类的反事实群体，直接对应不同亚组的干预策略，比SHAP值聚类更贴近实际干预需求。
- **允许领域知识融入**：用户定义特征类别，使搜索空间结构化、可解释。
- **内置模型诊断功能**：通过对比预期 vs 实际反事实分布，可评估模型是否学到了正确的交互模式。

## 8. 不足与局限
- **计算成本**：进化算法对每个样本独立搜索，成本随样本数线性增长，大规模人群应用时可能受限。
- **反事实可行性不足**：未考虑现实可行性约束（如饮食建议需符合健康指南），可能输出不切实际的建议（如>3000kcal能量摄入）。未来需融入领域约束。
- **因果性局限**：反事实仅解释模型行为，不保证反映真实生物学因果关系。若模型有偏，结论也会偏。
- **特征类别定义主观**：用户需预先指定特征类别，不同归类方式可能影响结果；潜在的主观性。
- **模型性能依赖**：当模型预测性能较低（如NHANES上AUROC=0.754）时，反事实可靠性有限，解释需谨慎。
- **聚类数选择**：使用k-means和轮廓系数可能无法捕捉真实连续谱（如NHANES中呈连续梯度而非离散群），聚类结果有近似性。

（完）
