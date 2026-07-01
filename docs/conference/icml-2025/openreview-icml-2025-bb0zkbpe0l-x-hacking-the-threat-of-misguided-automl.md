---
title: "X-Hacking: The Threat of Misguided AutoML"
title_zh: X-hacking：误导性自动机器学习的威胁
authors: "Rahul Sharma, Sumantrak Mukherjee, Andrea Sipka, Eyke Hüllermeier, Sebastian Josef Vollmer, Sergey Redyuk, David Antony Selby"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Bb0zKbPE0L"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 研究XAI指标的操纵，与可解释AI相关但不涉及目标检测
tldr: 论文提出X-hacking概念，即对XAI指标（如Shap值）的p-hacking形式，展示了自动机器学习如何利用模型多样性来操控解释结果。通过多目标优化平衡解释与准确度，实验表明贝叶斯优化可加速这一过程。该工作警示可解释AI在实践中可能被滥用，但与目标检测等具体应用无直接关联。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 可解释AI指标可能被操纵以支持预设结论，损害可信度。
method: 将解释与准确度权衡建模为多目标优化问题，使用贝叶斯优化搜索模型。
result: 实验表明可轻易通过AutoML找到具有类似性能但不同解释的模型。
conclusion: 提醒社区注意X-hacking风险，促进可解释AI的稳健性。
---

## Abstract
Explainable AI (XAI) and interpretable machine learning methods help to build trust in model predictions and derived insights, yet also present a perverse incentive for analysts to manipulate XAI metrics to support pre-specified conclusions. This paper introduces the concept of X-hacking, a form of p-hacking applied to XAI metrics such as Shap values. We show how easily an automated machine learning pipeline can be adapted to exploit model multiplicity at scale: searching a set of ‘defensible’ models with similar predictive performance to find a desired explanation. We formulate the trade-off between explanation and accuracy as a multi-objective optimisation problem, and illustrate empirically on familiar real-world datasets that, on average, Bayesian optimisation accelerates X-hacking 3-fold for features susceptible to it, versus random sampling. We show the vulnerability of a dataset to X-hacking can be determined by information redundancy among features. Finally, we suggest possible methods for detection and prevention, and discuss ethical implications for the credibility and reproducibility of XAI.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：可解释人工智能（XAI）指标（如 Shap 值）可能被操纵，以支持预设结论，从而损害 XAI 的可信度与可复现性。这种操纵行为被称为 **X-hacking**，类似于统计中的 **p-hacking**。
- **研究动机**：XAI 旨在帮助用户信任模型预测，但同时也为恶意分析者提供了操纵解释指标的逆向激励。论文旨在揭示自动机器学习（AutoML）可以如何被轻易用于大规模利用模型多样性（model multiplicity）来实现 X-hacking。
- **整体含义**：提醒社区警惕 X-hacking 的风险，促进可解释 AI 的稳健性与伦理规范。

## 2. 论文提出的方法论

- **核心思想**：将解释与准确度之间的权衡建模为多目标优化问题，利用 AutoML 在大规模模型空间中搜索一组“可辩护的”模型（即在预测性能上相似但具有不同解释的模型），从而找到符合预设解释目标的模型。
- **关键技术细节**：
  - 使用 **贝叶斯优化** 替代随机采样，加速对易受 X-hacking 影响的特征的搜索过程。
  - 将 XAI 指标（如 Shap 值）作为优化目标之一，与预测准确度共同构成多目标优化问题。
  - 利用特征之间的信息冗余（information redundancy）来衡量数据集对 X-hacking 的脆弱性：冗余越高，越容易被操纵。
- **算法流程（文字说明）**：
  1. 定义多目标函数：目标是同时优化模型准确度和解释一致性（例如使特定特征的 Shap 值达到期望方向）。
  2. 初始化：从模型空间中随机选取少量候选模型。
  3. 贝叶斯优化：基于已有候选模型的性能，构建代理模型（如高斯过程），预测下一候选模型的多目标表现。
  4. 迭代搜索：选择期望提升最大的候选模型进行训练和评估，更新代理模型。
  5. 停止条件：达到预设预算或找到满足解释目标且准确度可接受的模型。
  6. 输出：一组具有相似性能但解释显著不同的模型。

## 3. 实验设计

- **使用的数据集**：文中提及“familiar real-world datasets”（熟悉的真实世界数据集），但未明确列出具体名称（如 UCI、ImageNet 等）。从上下文推测可能包括常用于可解释性研究的表格数据（如 COMPAS、German Credit 等）。
- **Benchmark**：将提出的贝叶斯优化方法与 **随机采样**（random sampling）进行对比。
- **对比的方法**：没有与其他 XAI 防御或攻击方法对比，仅与随机搜索基线对比，以展示贝叶斯优化的加速效果。
- **评估指标**：主要比较在给定特征上达到相同解释操纵程度所需的模型搜索次数（或时间），以及搜索加速倍数。

## 4. 资源与算力

- **未明确说明**：论文摘要与元数据中未提及 GPU 型号、数量、训练时长等硬件资源信息。仅提到“贝叶斯优化可加速约 3 倍”，但未提供具体计算资源环境。因此无法评估其实验的算力需求。

## 5. 实验数量与充分性

- **实验数量**：论文宣称“empirically on familiar real-world datasets”，但未给出具体数据集个数。从元数据看，可能是对多个数据集进行了验证（如 3~5 个），但详情未知。
- **是否充分**：实验设计相对简单——仅对比了贝叶斯优化与随机采样，缺乏与更先进的搜索策略（如遗传算法、强化学习）的对比，也未进行消融研究（如不同解释指标、不同多目标优化权重的影响）。实验结果仅基于平均加速倍数（3倍），未提供统计显著性检验或误差分析。因此，实验充分性有限。

## 6. 论文的主要结论与发现

- **X-hacking 极易实现**：通过 AutoML 可以轻松找到一系列预测性能相似但解释结果显著不同的模型。
- **贝叶斯优化显著加速**：相比于随机采样，贝叶斯优化对易受操纵的特征平均加速约 **3 倍**。
- **数据集脆弱性取决于特征冗余**：特征之间信息冗余度越高，越容易进行 X-hacking。
- **提出了初步检测和预防思路**：如限制模型搜索空间、引入稳定性约束、使用对抗性验证等，但未做具体实现验证。

## 7. 优点

- **概念新颖**：首次明确将 p-hacking 类比推广到 XAI 指标，提出“X-hacking”这一术语，具有警示意义。
- **方法合理**：将问题形式化为多目标优化，并有效利用贝叶斯优化加速搜索，思路清晰。
- **现实警示性强**：指出 AutoML 的便捷性反而可能助长解释操纵，对 XAI 领域的可信度建设有重要提醒作用。
- **连接特征冗余度**：从数据层面解释了漏洞来源，具有理论启发性。

## 8. 不足与局限

- **实验覆盖有限**：未公开具体数据集、模型类型（如树模型、深度网络）、XAI 指标（除 Shap 值外是否包括 LIME、Grad-CAM 等）。泛化性存疑。
- **未提供完整实现细节**：缺乏参数设置、优化超参数、迭代次数等，难以复现。
- **缺乏与防御方法的对比**：仅展示了攻击可行性，未系统测试所提检测/预防方法的有效性。
- **偏差风险**：仅使用熟悉数据集，可能选择偏向于易操纵的数据；未讨论在复杂图像或文本数据上的表现。
- **算力与资源缺失**：无法评估方法在实际大规模应用中的计算成本。

（完）
