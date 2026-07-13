---
title: "Identifying intervention strategies from machine learning models with COALA: a counterfactual optimization framework"
title_zh: 利用COALA从机器学习模型中识别干预策略：一个反事实优化框架
authors: "Han, B., Duan, Q., Hu, T."
date: 2026-07-07
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.18.664723v2.full.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 反事实可解释AI框架用于识别干预策略
tldr: "针对机器学习模型的黑箱问题，现有可解释性方法如SHAP仅关注特征重要性，无法识别特征交互和个性化干预。提出COALA框架，通过反事实优化为每个主体识别导致预测结果最积极变化的可操作改变，从而实现模型的可操作可解释性。在NHANES数据集上，COALA识别出不同主体的最优反事实轮廓，且约束特征能以85.4%的准确率预测最优反事实变化。该框架为精准干预提供了新思路，代码与数据已公开。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 937, \"height\": 1090}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1534, \"height\": 944}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 678}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1890, \"height\": 1094}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 926, \"height\": 646}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1898, \"height\": 882}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 656, \"height\": 237}]"
motivation: 现有XAI方法无法识别特征交互和个性化干预，需一种能提供可操作反事实解释的框架。
method: 提出COALA框架，通过优化寻找每个主体最优反事实改变，最大化预测结果正向变化。
result: "在NHANES数据集上，COALA识别不同主体最优反事实轮廓，约束特征预测最优反事实准确率达85.4%。"
conclusion: COALA通过反事实优化实现模型可操作可解释性，有助于个性化干预策略的制定。
---

## 摘要
动机：机器学习（ML）模型已变得越来越复杂，通常作为黑箱模型运行，限制了我们对特征如何影响模型预测的理解。常见的可解释人工智能（XAI）方法，如SHapley Additive exPlanations（SHAP），侧重于特征重要性，但未能识别特征之间的交互作用，也无法指导针对性的个性化干预。反事实是假设性事件，其中特定变量被改变以导致结果发生变化。这些因果陈述可应用于AI模型，以识别针对群体中不同个体的可操作干预措施。

结果：我们提出了可操作可解释性的人工智能反事实优化框架（COALA）。COALA通过为每个个体识别最优反事实来解释模型，这些反事实被定义为能带来预测结果最积极变化的可操作改变。当应用于基于国家健康与营养调查（NHANES）数据集训练的梯度提升树模型时，COALA识别出不同个体之间的最优反事实轮廓。那些保持受限的特征能够以85.4%的准确率预测个体的最优反事实变化，揭示了驱动个体最优反事实的具体特征。

可用性与实现：COALA实现的代码、合成数据、基于合成数据训练的模型以及复现结果和图形的代码可在https://github.com/brt-solo/COALA获取。NHANES 2017-2018数据集可从国家卫生统计中心（NCHS）公开获取。本研究中使用的弗雷明汉心脏研究数据集是公开可用的、衍生自弗雷明汉的数据集，通过麻省理工学院开放式课程（MIT OCW）存储库分发。

## Abstract
MotivationMachine learning (ML) models have become increasingly complex, often functioning as black boxes that limit our understanding of the features contributing to ML predictions. Common explainable AI (XAI) methods such as SHapley Additive exPlanations (SHAP) focus on feature importance but fall short in identifying interactions among features and informing targeted, personalized interventions. Counterfactuals are hypothetical events where specific variables are altered to cause a change in outcome. These causal statements can be applied to AI models to identify actionable interventions for different subjects in a population.

ResultsWe propose the framework Counterfactual Optimization for Actionable interpretabiLity in AI (COALA). COALA interprets models by identifying optimal counterfactuals for each subject, which are defined as actionable changes that lead to the most positive change in predicted outcome. When applied to a gradient boosted tree model trained on the National Health and Nutrition Examination Survey (NHANES) dataset, COALA identifies different profiles of optimal counterfactuals across subjects. Features that remain constrained were able to predict the optimal counterfactual changes for a subject at 85.4%, revealing specific features that drive what a subjects optimal counterfactual is.

Availability and ImplementationCode for COALA implementation, synthetic data, models trained on synthetic data, and code to replicate results and figures are available at https://github.com/brt-solo/COALA. The NHANES 2017-2018 dataset is publicly available from the National Center for Health Statistics (NCHS). The Framingham Heart Study dataset used in this study is a publicly available, Framingham-derived dataset distributed through the Massachusetts Institute of Technology OpenCourseWare (MIT OCW) repository.