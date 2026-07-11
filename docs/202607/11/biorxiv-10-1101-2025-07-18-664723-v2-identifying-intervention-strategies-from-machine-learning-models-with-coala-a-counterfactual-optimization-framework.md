---
title: "Identifying intervention strategies from machine learning models with COALA: a counterfactual optimization framework"
title_zh: 使用COALA从机器学习模型中识别干预策略：一种反事实优化框架
authors: "Han, B., Duan, Q., Hu, T."
date: 2026-07-07
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.18.664723v2.full.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 反事实可解释AI框架用于识别干预策略，可应用于可解释异常/伪造检测
tldr: "机器学习模型的黑箱性限制了对其预测的个性化干预。现有可解释方法如SHAP难以识别特征交互和可操作改变。为此提出COALA框架，通过反事实优化为每个个体找到导致预测结果最积极变化的干预策略。在NHANES数据集上，COALA识别出不同个体的最优反事实轮廓，且受限特征能以85.4%准确率预测最优反事实。该框架提供了基于反事实的可操作可解释性，支持个性化干预。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 937, \"height\": 1090}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1534, \"height\": 944}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 678}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1890, \"height\": 1094}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 926, \"height\": 646}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1898, \"height\": 882}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 656, \"height\": 237}]"
motivation: 机器学习模型缺乏可解释性，现有方法无法识别特征交互和个性化干预，需要可操作的反事实解释。
method: 提出COALA框架，通过反事实优化为每个个体寻找预测结果提升最大的可行动干预。
result: "应用于NHANES数据集，COALA发现不同个体最优反事实不同，受限特征以85.4%准确率预测最优反事实。"
conclusion: COALA实现了基于反事实的可操作可解释AI，有助于个性化干预策略的制定。
---

## 摘要
动机机器学习（ML）模型已变得日益复杂，往往作为黑箱运行，限制了我们对哪些特征影响模型预测的理解。常见的可解释人工智能（XAI）方法，如SHAP（Shapley加法解释），侧重于特征重要性，但在识别特征间交互以及指导针对性、个性化干预方面存在不足。反事实是假设性事件，其中改变特定变量以导致结果变化。这些因果陈述可应用于AI模型，以识别对群体中不同个体可执行的干预措施。

结果我们提出了“反事实优化实现AI可操作可解释性”（COALA）框架。COALA通过为每个个体识别最优反事实来解释模型，这些反事实被定义为能带来预测结果最积极变化的可操作改变。当应用于基于国家健康与营养调查（NHANES）数据集训练的梯度提升树模型时，COALA识别出不同个体间的最优反事实概况。保持受限的特征能够以85.4%的准确率预测个体的最优反事实变化，揭示了驱动个体最优反事实的具体特征。

可用性与实现COALA实现的代码、合成数据、基于合成数据训练的模型以及复现结果和图形的代码可在https://github.com/brt-solo/COALA获取。NHANES 2017-2018数据集可从国家健康统计中心（NCHS）公开获取。本研究使用的弗雷明汉心脏研究数据集是一个公开可用的、源自弗雷明汉的数据集，通过麻省理工学院开放课程（MIT OCW）仓库分发。

## Abstract
MotivationMachine learning (ML) models have become increasingly complex, often functioning as black boxes that limit our understanding of the features contributing to ML predictions. Common explainable AI (XAI) methods such as SHapley Additive exPlanations (SHAP) focus on feature importance but fall short in identifying interactions among features and informing targeted, personalized interventions. Counterfactuals are hypothetical events where specific variables are altered to cause a change in outcome. These causal statements can be applied to AI models to identify actionable interventions for different subjects in a population.

ResultsWe propose the framework Counterfactual Optimization for Actionable interpretabiLity in AI (COALA). COALA interprets models by identifying optimal counterfactuals for each subject, which are defined as actionable changes that lead to the most positive change in predicted outcome. When applied to a gradient boosted tree model trained on the National Health and Nutrition Examination Survey (NHANES) dataset, COALA identifies different profiles of optimal counterfactuals across subjects. Features that remain constrained were able to predict the optimal counterfactual changes for a subject at 85.4%, revealing specific features that drive what a subjects optimal counterfactual is.

Availability and ImplementationCode for COALA implementation, synthetic data, models trained on synthetic data, and code to replicate results and figures are available at https://github.com/brt-solo/COALA. The NHANES 2017-2018 dataset is publicly available from the National Center for Health Statistics (NCHS). The Framingham Heart Study dataset used in this study is a publicly available, Framingham-derived dataset distributed through the Massachusetts Institute of Technology OpenCourseWare (MIT OCW) repository.