---
title: "Identifying intervention strategies from machine learning models with COALA: a counterfactual optimization framework"
title_zh: 使用COALA从机器学习模型中识别干预策略：一个反事实优化框架
authors: "Han, B., Duan, Q., Hu, T."
date: 2026-07-07
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.18.664723v2.full.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 反事实优化框架，从机器学习模型生成可操作的解释，通用的XAI方法可应用于目标/异常/伪造检测
tldr: "机器学习模型黑箱问题限制了特征理解与个性化干预。现有可解释性方法难以识别特征交互和提供可操作建议。COALA框架通过反事实优化为每个样本寻找可实现的最正向预测变化，在NHANES数据上达到85.4%预测准确率，揭示了驱动样本最优反事实的关键特征，为个性化干预提供了新途径。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 937, \"height\": 1090}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1534, \"height\": 944}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 678}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1890, \"height\": 1094}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 926, \"height\": 646}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1898, \"height\": 882}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 656, \"height\": 237}]"
motivation: 现有可解释人工智能方法如SHAP只提供特征重要性，缺乏特征交互和个性化干预的可操作建议。
method: 提出COALA框架，通过反事实优化为每个样本识别可实现的最优改变，使预测结果正向变化最大。
result: "在NHANES数据上，约束特征可85.4%准确预测样本的最优反事实改变，揭示不同样本的个性化干预轮廓。"
conclusion: COALA能有效识别驱动最优反事实的关键特征，支持针对不同主体的可操作干预策略。
---

## 摘要
动机机器学习（ML）模型日益复杂，通常作为黑箱运行，限制了我们对有助于ML预测的特征的理解。常见的可解释人工智能（XAI）方法，如SHapley Additive exPlanations（SHAP），侧重于特征重要性，但在识别特征之间的相互作用以及指导有针对性的个性化干预方面存在不足。反事实是假设性事件，其中特定变量被改变以导致结果发生变化。这些因果陈述可以应用于AI模型，以识别针对人群中不同个体的可操作干预。

结果我们提出了可操作可解释人工智能的反事实优化框架（COALA）。COALA通过为每个个体识别最优反事实来解释模型，这些反事实被定义为导致预测结果最正向改变的可操作变化。当应用于基于美国国家健康与营养调查（NHANES）数据集训练的梯度提升树模型时，COALA识别出不同个体间的最优反事实概况。保持约束的特征能够以85.4%的准确率预测个体的最优反事实变化，揭示了驱动个体最优反事实的具体特征。

可用性和实现COALA实现的代码、合成数据、基于合成数据训练的模型以及复制结果和图形的代码可在https://github.com/brt-solo/COALA获取。NHANES 2017-2018数据集可从美国国家卫生统计中心（NCHS）公开获取。本研究中使用的弗雷明汉心脏研究数据集是一个公开可用的、源自弗雷明汉的数据集，通过麻省理工学院开放课程（MIT OCW）仓库分发。

## Abstract
MotivationMachine learning (ML) models have become increasingly complex, often functioning as black boxes that limit our understanding of the features contributing to ML predictions. Common explainable AI (XAI) methods such as SHapley Additive exPlanations (SHAP) focus on feature importance but fall short in identifying interactions among features and informing targeted, personalized interventions. Counterfactuals are hypothetical events where specific variables are altered to cause a change in outcome. These causal statements can be applied to AI models to identify actionable interventions for different subjects in a population.

ResultsWe propose the framework Counterfactual Optimization for Actionable interpretabiLity in AI (COALA). COALA interprets models by identifying optimal counterfactuals for each subject, which are defined as actionable changes that lead to the most positive change in predicted outcome. When applied to a gradient boosted tree model trained on the National Health and Nutrition Examination Survey (NHANES) dataset, COALA identifies different profiles of optimal counterfactuals across subjects. Features that remain constrained were able to predict the optimal counterfactual changes for a subject at 85.4%, revealing specific features that drive what a subjects optimal counterfactual is.

Availability and ImplementationCode for COALA implementation, synthetic data, models trained on synthetic data, and code to replicate results and figures are available at https://github.com/brt-solo/COALA. The NHANES 2017-2018 dataset is publicly available from the National Center for Health Statistics (NCHS). The Framingham Heart Study dataset used in this study is a publicly available, Framingham-derived dataset distributed through the Massachusetts Institute of Technology OpenCourseWare (MIT OCW) repository.