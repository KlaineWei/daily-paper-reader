---
title: "Identifying intervention strategies from machine learning models with COALA: a counterfactual optimization framework"
title_zh: 通过COALA从机器学习模型中识别干预策略：一个反事实优化框架
authors: "Han, B., Duan, Q., Hu, T."
date: 2026-07-07
pdf: "https://www.biorxiv.org/content/10.1101/2025.07.18.664723v2.full.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 反事实优化框架用于可解释AI，可应用于多种场景
tldr: "机器学习模型常被视为黑箱，现有可解释性方法如SHAP仅关注特征重要性，难以指导个性化干预。COALA框架通过反事实优化，为每个样本寻找最有利预测结果的可操作改变，从而识别干预策略。在NHANES数据集上，COALA揭示了不同主体的最优反事实剖面，且受约束特征能以85.4%的准确率预测最优改变。该方法为模型可解释性与个性化干预提供了新工具。"
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 937, \"height\": 1090}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1534, \"height\": 944}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 901, \"height\": 678}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1890, \"height\": 1094}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 926, \"height\": 646}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1898, \"height\": 882}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-07-18-664723-v2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 656, \"height\": 237}]"
motivation: 现有XAI方法缺乏对特征交互和个性化干预的指导，需要能识别可操作反事实的框架。
method: COALA通过优化每个样本的反事实，找到导致预测结果最正向变化且可行的特征变更路径。
result: "在梯度提升树模型上，COALA识别出不同主体的独特反事实剖面，约束特征预测准确率达85.4%。"
conclusion: COALA为机器学习模型提供了一种可操作的、个性化的可解释性方法，有望促进临床决策等领域的干预设计。
---

## 摘要
动机：机器学习（ML）模型变得越来越复杂，通常作为黑箱运行，限制了我们对其预测特征的理解。常见的可解释人工智能（XAI）方法如SHapley Additive exPlanations（SHAP）侧重于特征重要性，但在识别特征间的交互以及指导有针对性的个性化干预方面存在不足。反事实是指改变特定变量以导致结果发生变化的情境假设。这些因果陈述可应用于AI模型，以识别对不同个体可操作的干预措施。

结果：我们提出了反事实优化以实现AI可操作可解释性（COALA）框架。COALA通过为每个个体识别最优反事实来解释模型，这些反事实被定义为能导致预测结果最具积极变化的可操作改变。当应用于在National Health and Nutrition Examination Survey（NHANES）数据集上训练的梯度提升树模型时，COALA识别出不同个体的最优反事实轮廓。受到约束的特征能够以85.4%的准确率预测个体的最优反事实变化，揭示了个体最优反事实的驱动特征。

可用性与实现：COALA实现的代码、合成数据、在合成数据上训练的模型以及复现结果和图表的代码可在https://github.com/brt-solo/COALA获取。NHANES 2017-2018数据集可从国家卫生统计中心（NCHS）公开获取。本研究中使用的Framingham心脏研究数据集是通过麻省理工学院开放式课件（MIT OCW）仓库分发的公开可用的Framingham衍生数据集。

## Abstract
MotivationMachine learning (ML) models have become increasingly complex, often functioning as black boxes that limit our understanding of the features contributing to ML predictions. Common explainable AI (XAI) methods such as SHapley Additive exPlanations (SHAP) focus on feature importance but fall short in identifying interactions among features and informing targeted, personalized interventions. Counterfactuals are hypothetical events where specific variables are altered to cause a change in outcome. These causal statements can be applied to AI models to identify actionable interventions for different subjects in a population.

ResultsWe propose the framework Counterfactual Optimization for Actionable interpretabiLity in AI (COALA). COALA interprets models by identifying optimal counterfactuals for each subject, which are defined as actionable changes that lead to the most positive change in predicted outcome. When applied to a gradient boosted tree model trained on the National Health and Nutrition Examination Survey (NHANES) dataset, COALA identifies different profiles of optimal counterfactuals across subjects. Features that remain constrained were able to predict the optimal counterfactual changes for a subject at 85.4%, revealing specific features that drive what a subjects optimal counterfactual is.

Availability and ImplementationCode for COALA implementation, synthetic data, models trained on synthetic data, and code to replicate results and figures are available at https://github.com/brt-solo/COALA. The NHANES 2017-2018 dataset is publicly available from the National Center for Health Statistics (NCHS). The Framingham Heart Study dataset used in this study is a publicly available, Framingham-derived dataset distributed through the Massachusetts Institute of Technology OpenCourseWare (MIT OCW) repository.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：机器学习模型（尤其是黑箱模型）预测能力强，但可解释性差。常见的可解释AI方法（如SHAP）仅能给出特征重要性评分，无法回答“改变哪些特征、如何改变才能获得更好的预测结果”这一关键问题，也无法捕获特征间的交互效应。这限制了模型在个性化干预（如精准医疗）中的应用。
- **背景**：反事实（counterfactual）是一种“若改变某变量，结果会如何改变”的假想陈述，天然具有因果性，可用于指导干预。但现有反事实方法存在三大挑战：① 生物医学模型性能通常有限，单样本的反事实不可靠，需要人群级分析；② 特征间存在交互，需同时改变多个特征；③ 反事实空间无限，需定义“最优”标准进行筛选。
- **整体含义**：作者提出COALA框架，通过进化优化为每个样本寻找“最优反事实”（即能带来最大正面预测变化且可操作的特征改变），从而提供个性化干预策略，并揭示哪些约束特征（如遗传、生理）决定了最优方案。

## 2. 论文提出的方法论

### 核心思想
- 基于MAP-Elites多样化进化算法，将反事实搜索空间划分为多个“细胞”（cell），每个细胞对应一组可改变的特征类别组合。在每个细胞中独立搜索最优反事实（即预测结果改善最大的那个候选解）。
- 用户可指定哪些特征类别是可变的（mutable），哪些是固定的（constraint）。固定特征称为“约束特征”，其差异会通过模型内生的交互效应导致不同个体的最优反事实不同。

### 关键技术与算法流程
1. **特征分类**：将全部特征 \( F \) 划分为 \( N \) 个不相交的类别（如：饮食类、基因类、代谢类）。定义细胞集合 \( C = \{ (i,j) | 1 \leq i \leq j \leq N \} \)，每个细胞对应一对特征类别（即只改变这两个类别中的特征）。
2. **初始化**：为每个细胞维护一个精英解（当前最优反事实）和其性能。首先进行随机初始化（前 \( G \) 次迭代）：随机选择一个细胞，在其对应的可变特征上，连续特征从观测范围内均匀采样，二值特征随机赋值，生成初始候选解。
3. **优化阶段**：每次迭代随机选择一个细胞，从该细胞中选出精英解（best-performing）和另一个随机候选解作为父代，通过交叉（crossover，文中采用均匀交叉）产生子代，并评估其预测性能（fitness）。如果子代性能优于当前精英，则替换。
4. **输出**：对每个样本独立运行以上过程，得到每个细胞中的一个最优反事实。
5. **事后分析**：
   - 对某一细胞（例如仅饮食特征可变），对所有样本的最优反事实进行K-means聚类（使用z-score标准化后的可变特征值），得到干预组。
   - 通过ANOVA计算可变特征和约束特征的解释方差比例 \( \eta^2 \)（Cohen's large effect threshold: \( \eta^2 \ge 0.14 \)），找出哪些约束特征驱动了最优反事实的差异。
   - 构建相似性网络（Euclidean距离），可视化子群结构。

### 公式与算法（文字说明）
- 候选解生成公式（初始化阶段）：连续特征 \( x'_k \sim U(\min_k, \max_k) \)。
- 优化阶段：通过精英与随机父代交叉产生新解，保留各细胞最优解。

## 3. 实验设计

### 数据集
1. **合成数据集**：1000个样本，9个特征分为4个视图（遗传、环境、营养、代谢），连续输出 \( y \) 由加性项和三项交互（\( G1·E1 \)、\( G2·M2·N2 \)）生成。用于验证COALA能否恢复已知交互模式。
2. **NHANES 2017-2018数据集**：真实人群调查数据，包括人口学、临床、生活方式、饮食等变量，二分类结果变量为糖尿病（HbA1c ≥ 6.5%）。模型为XGBoost（AUROC=0.7541）。
3. **Framingham心脏研究数据**（补充材料）：心血管疾病风险预测，类似流程验证。

### 基准模型
- 对合成数据：线性回归（仅捕获加性关系）和MLP（可捕捉非线性交互）。
- 对真实数据：XGBoost。

### 对比方法
- **SHAP聚类分析**：对每个样本计算可变特征的SHAP值，然后基于SHAP值进行层次聚类（Ward连接，Euclidean距离）。与COALA比较两组指标：
  - 聚类质量（轮廓系数、Davies-Bouldin、Calinski-Harabasz）。
  - **约束特征预测聚类成员的准确率**：训练随机森林分类器，用约束特征预测COALA或SHAP的聚类标签，计算平衡准确率（交叉验证和holdout验证）。**该指标衡量聚类是否由约束特征解释，即是否具备个性化干预的潜力**。

### 其他实验
- 对合成数据的地面真实模型（数据生成函数作为模型）也应用COALA，验证能否恢复8种预期最优反事实。
- 对线性回归模型应用COALA，检验其是否无法产生差异（因为无交互）。

## 4. 资源与算力

- **论文未明确说明使用的GPU型号、数量或训练时长**。仅提到COALA的进化算法计算代价随样本量线性增长。作者也指出未来可探索降低计算开销的策略。

## 5. 实验数量与充分性

- **实验组数**：
  - 合成数据：3个模型（地面真实模型、线性回归、MLP），每个模型下分别运行COALA和SHAP（但SHAP仅对MLP部分展示）。
  - NHANES：XGBoost模型，COALA和SHAP对比。
  - Framingham（补充材料）：XGBoost模型，COALA和SHAP对比。
- **消融与验证**：
  - 在地面真实模型上验证COALA能否恢复已知交互结构（8簇预期）。
  - 验证线性模型上COALA无差异（正确）。
  - 对NHANES进行聚类数选择（轮廓系数），并用 \( \eta^2 \) 分析特征组差异。
  - 比较COALA与SHAP的聚类可预测性（约束特征预测准确率）。
- **充分性评价**：实验设计较充分，覆盖了合成数据（控制条件）和两个真实数据集，对比了不同复杂度的模型（线性、MLP、XGBoost）。主要局限在于真实数据上模型性能中等（AUROC 0.754），但作者明确指出了这一点，并将其作为模型行为分析而非真实因果的界限。SHAP对比实验设计合理，主指标（约束特征可预测性）直接对应个性化干预能力。

## 6. 论文的主要结论与发现

1. **COALA能恢复已知交互模式**：对合成数据的地面真实模型，COALA正确识别出8种不同最优反事实，且仅与包含交互的遗传约束特征相关，与无交互的特征无关。
2. **线性模型下无差异**：当模型只含加性效应时，COALA对所有样本给出相同最优反事实，符合预期。
3. **NHANES应用发现腰围是主要驱动因素**：仅饮食特征可变时，最优反事实聚类显示腰围的 \( \eta^2 \) 最大，表明腰围调节了最优饮食干预方向。这与腰围是糖尿病强预测因子的现有证据一致。
4. **COALA在约束特征可预测性上远优于SHAP**：在NHANES上，约束特征预测COALA聚类标签的holdout准确率为85.4%，而SHAP仅32.4%；在Framingham上为100% vs 53.3%。说明COALA识别的干预组更符合个性化逻辑（即受个体固有特征驱动）。
5. **相似性网络揭示非线性结构**：即使相同腰围，不同个体最优反事实可能不同，提示需更精细的建模（如年龄等）。

## 7. 优点

- **创新性**：将MAP-Elites多样化进化算法应用于反事实搜索，同时考虑了可行性和个性化。无需梯度信息，适合高维、非凸、不可微的搜索空间。
- **可操作性**：输出为“改变哪些特征”的具体建议，可直接用于设计干预方案；用户可自定义可变特征类别（如仅改变饮食），贴近实际应用。
- **可解释性**：通过聚类和方差分析，自动识别哪些约束特征（如遗传、生理）决定了个体最优干预，提供了“为什么这个人的最优方案不同”的洞察。
- **模型无关性**：仅需预测函数，适用于任何黑箱模型。
- **对比SHAP体现优势**：SHAP只能回顾性解释“哪些特征重要”，无法前瞻性回答“改变后结果如何”；COALA直接优化干预结果，且约束特征可预测性高，证明其确实捕捉到了特征交互导致的个性化差异。

## 8. 不足与局限

- **计算成本**：进化算法为每个样本独立运行，计算量随样本量线性增长。文中未给出运行时间，也未与SHAP的计算费用对比。
- **可行性忽略现实约束**：当前反事实仅限制在特征观测范围内，未考虑可操作性的现实边界（如饮食改变不能超过每日能量推荐上限、突变幅度不能过大等）。作者举例最优反事实中能量摄入>3000kcal可能不现实。
- **依赖模型可靠性**：COALA解释的是模型行为，而非真实生物机制。如果模型存在偏差或未学到真实交互（如MLP在合成数据上误将E2作为交互特征），COALA输出也可能误导。作者将其作为模型验证工具的建议很好，但也提醒需谨慎解读。
- **仅适用于表格数据**：文中未提及对图像、文本等非结构化数据的适配性。
- **聚类数的选择**：NHANES中轮廓分数建议10个簇，但作者为解释性选择了3个簇，存在一定主观性。虽然文中解释了原因，但不同聚类数可能影响后续分析。
- **SHAP对比的局限性**：SHAP聚类本质是风险分组而非干预分组，直接比较约束特征可预测性可能不完全公平。但作者明确区分了“风险组”与“干预组”，并论证了COALA更适合后者。
- **实验规模有限**：仅使用两个真实数据集，且NHANES模型性能中等。需要更多领域、更好性能的模型验证。

（完）
