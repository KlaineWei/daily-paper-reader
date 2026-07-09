---
title: "Identifying intervention strategies from machine learning models with COALA: a counterfactual optimization framework"
title_zh: 使用COALA从机器学习模型中识别干预策略：一个反事实优化框架
authors: "Han, B., Duan, Q., Hu, T."
date: 2026-07-07
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.18.664723v2.full.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 反事实优化用于可解释机器学习，可应用于目标检测可解释性分析
tldr: "机器学习模型的黑箱特性限制了对其预测依据的理解，现有可解释性方法如SHAP难以识别特征交互和指导个性化干预。COALA框架通过反事实优化寻找每个样本的最优干预策略，即在约束特征不变的情况下预测结果正向变化最大的可行动改变。在NHANES梯度提升树模型上，COALA揭示了不同样本的差异化最优反事实，且利用受约束特征能以85.4%准确率预测样本应改变的特征，为针对性干预提供了可解释依据。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 937, \"height\": 1090, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1534, \"height\": 944, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 678, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1890, \"height\": 1094, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 926, \"height\": 646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1898, \"height\": 882, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 656, \"height\": 237, \"label\": \"Table\"}]"
motivation: 现有可解释AI方法难以识别特征交互及生成个性化干预方案，反事实分析可提供因果层面的 actionable 建议。
method: 提出 COALA 框架，通过优化目标函数为每个样本找出约束特征下使预测结果正向变化最大的反事实改变。
result: "在NHANES梯度提升树模型上，COALA发现不同样本的最优反事实存在差异，且受约束特征能以85.4%准确率预测最优反事实。"
conclusion: COALA能识别驱动最优干预的关键特征，为个性化决策提供可操作的可解释性。
---

## 摘要
动机
机器学习（ML）模型日益复杂，常作为黑箱运行，限制了我们对特征如何影响模型预测的理解。常见的可解释人工智能（XAI）方法如SHapley Additive exPlanations（SHAP）关注特征重要性，但未能识别特征间的相互作用，也无法指导有针对性的个性化干预。反事实是假设事件，其中改变特定变量会导致结果变化。这些因果陈述可应用于AI模型，为人群中的不同个体识别可行的干预措施。

结果
我们提出了可操作的AI可解释性反事实优化框架（COALA）。COALA通过为每个个体识别最优反事实来解释模型，这些反事实定义为导致预测结果最积极变化的可操作改变。当应用于基于国家健康与营养调查（NHANES）数据集训练的梯度提升树模型时，COALA识别出不同个体间最优反事实的不同配置。保持约束的特征能够以85.4%的准确率预测个体的最优反事实变化，揭示了驱动个体最优反事实的特定特征。

可用性和实现
COALA实现的代码、合成数据、基于合成数据训练的模型，以及复现结果和图形的代码可在https://github.com/brt-solo/COALA获取。NHANES 2017-2018数据集可从国家健康统计中心（NCHS）公开获取。本研究中使用的弗雷明汉心脏研究数据集是一个公开可用的、由弗雷明汉衍生并通过麻省理工学院开放课程（MIT OCW）仓库分发的数据集。

## Abstract
MotivationMachine learning (ML) models have become increasingly complex, often functioning as black boxes that limit our understanding of the features contributing to ML predictions. Common explainable AI (XAI) methods such as SHapley Additive exPlanations (SHAP) focus on feature importance but fall short in identifying interactions among features and informing targeted, personalized interventions. Counterfactuals are hypothetical events where specific variables are altered to cause a change in outcome. These causal statements can be applied to AI models to identify actionable interventions for different subjects in a population.

ResultsWe propose the framework Counterfactual Optimization for Actionable interpretabiLity in AI (COALA). COALA interprets models by identifying optimal counterfactuals for each subject, which are defined as actionable changes that lead to the most positive change in predicted outcome. When applied to a gradient boosted tree model trained on the National Health and Nutrition Examination Survey (NHANES) dataset, COALA identifies different profiles of optimal counterfactuals across subjects. Features that remain constrained were able to predict the optimal counterfactual changes for a subject at 85.4%, revealing specific features that drive what a subjects optimal counterfactual is.

Availability and ImplementationCode for COALA implementation, synthetic data, models trained on synthetic data, and code to replicate results and figures are available at https://github.com/brt-solo/COALA. The NHANES 2017-2018 dataset is publicly available from the National Center for Health Statistics (NCHS). The Framingham Heart Study dataset used in this study is a publicly available, Framingham-derived dataset distributed through the Massachusetts Institute of Technology OpenCourseWare (MIT OCW) repository.