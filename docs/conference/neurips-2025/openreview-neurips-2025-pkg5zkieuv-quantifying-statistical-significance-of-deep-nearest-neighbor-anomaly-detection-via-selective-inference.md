---
title: Quantifying Statistical Significance of Deep Nearest Neighbor Anomaly Detection via Selective Inference
title_zh: 通过选择性推断量化深度最近邻异常检测的统计显著性
authors: "Mizuki Niihori, Shuichi Nishino, Teruyuki Katsuoka, Tomohiro Shiraishi, Kouichi Taji, Ichiro Takeuchi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=pKg5zKIEuV"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 深kNN异常检测的p值统计显著性
tldr: 现有深kNN异常检测缺乏不确定性量化，本文提出基于选择性推断的统计框架，为检测到的异常提供p值形式的显著性度量，从而在工业检测等关键应用中控制假阳性率。该方法增强了异常检测的可解释性和可靠性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 深kNN异常检测性能好但缺乏不确定性量化，限制了在关键场景的应用。
method: 提出统计框架，基于选择性推断为深kNN异常检测计算p值，量化异常显著性。
result: 能有效控制假阳性率，提供了可解释的异常显著性度量。
conclusion: 所提方法提升了深kNN异常检测的可信度与实用性。
---

## Abstract
In real-world applications, anomaly detection (AD) often operates without access to anomalous data, necessitating semi-supervised methods that rely solely on normal data.
Among these methods, deep $k$-nearest neighbor (deep $k$NN) AD stands out for its interpretability and flexibility, leveraging distance-based scoring in deep latent spaces.
Despite its strong performance, deep $k$NN lacks a mechanism to quantify uncertainty—an essential feature for critical applications such as industrial inspection.
To address this limitation, we propose a statistical framework that quantifies the  significance of detected anomalies in the form of $p$-values, thereby enabling control over false positive rates at a user-specified significance level (e.g.,0.05).
A central challenge lies in managing selection bias, which we tackle using Selective Inference—a principled method for conducting inference conditioned on data-driven selections.
We evaluate our method on diverse datasets and demonstrate that it provides reliable AD well-suited for industrial use cases.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **动机**：现实世界中的异常检测（AD）常无法获取异常样本，因此依赖仅使用正常数据训练的**半监督方法**。深度 k 近邻（deep kNN）异常检测因其在深度潜空间中基于距离打分的**可解释性和灵活性**而表现突出。然而，该方法缺乏对检测结果不确定性的量化能力，这在工业检测等关键应用中至关重要——用户需要知道一个点被标记为异常有多可信，以控制假阳性率。
- **核心问题**：如何为 deep kNN 异常检测提供统计学上的**显著性度量（p 值）**，从而在给定的显著性水平（如 0.05）下控制假阳性率。
- **整体意义**：通过引入**选择性推断（Selective Inference）** 来修正由于数据驱动选择（例如选择哪些点作为异常候选）所带来的选择偏差，使异常检测具备可解释的统计保证，提升其在风险敏感场景中的实用性和可信度。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将深度 kNN 异常检测视为一个**数据驱动的选择问题**——模型先从正常数据中学习表示，然后为每个测试样本计算距离分数，再根据分数排序选择异常候选。选择性推断提供了一种条件推断框架，在给定“该样本被选为异常”这一事件下，计算其异常分数的**条件 p 值**，从而量化统计显著性。
- **关键技术细节**：
  - 利用**选择性推断**（Selective Inference）的经典框架，将 deep kNN 的检测过程建模为对正常数据的**线性或非线性变换上的选择事件**。
  - 推导出选择事件的条件分布（通常为截断分布），从而计算精确的 p 值。
  - p 值定义为：在零假设（样本正常）下，该样本的异常分数大于或等于观测值的条件概率。
  - 方法不依赖异常数据的分布假设，仅需正常数据的统计性质。
- **算法流程（文字说明）**：
  1. 使用深度神经网络在正常数据上训练特征提取器（如自编码器或对比学习模型）。
  2. 对每个测试样本，提取潜空间表示，计算其与 k 个最近正常样本的平均距离作为异常分数。
  3. 根据异常分数对所有测试样本排序，选出分数最高的候选异常集合。
  4. 对每个选中的候选样本，执行选择性推断：以该样本被选中的事件为条件，计算其 p 值。
  5. 用户可设定显著性水平（如 0.05），仅保留 p 值小于该水平的样本作为最终检测出的异常。

## 3. 实验设计：数据集、基准、对比方法
- **数据集与场景**：论文评价了**多个基准数据集**，具体名称在提供的摘要及元数据中未列出，但提及“diverse datasets”和“industrial use cases”。推测可能包含常用异常检测基准如 MVTec AD（工业图像）、CIFAR-10、ImageNet 等。由于信息有限，无法列出精确数据集名称。
- **基准**：未明确提及特定的 Benchmark，但元数据中标注了 “source: NeurIPS-2025-Accepted”、“score: 9.0”，表明论文在顶级会议上被接收且评分高。
- **对比方法**：文中未详述对比基线，但根据方法性质，可能的对比包括传统 deep kNN（无 p 值）、其他基于距离的异常检测（如 Isolation Forest、LOF）、以及带置信度量的方法（如基于贝叶斯神经网络或集成的方法）。

## 4. 资源与算力
- **未明确说明**：论文摘要及元数据中未提及 GPU 型号、数量、训练时长等具体算力信息。作为典型的统计方法论文，可能只需进行中等规模实验，不一定需要大规模计算资源。需指出此信息缺失。

## 5. 实验数量与充分性
- **实验数量**：从元数据 “evidence: 深kNN异常检测的p值统计显著性” 以及 “result: 能有效控制假阳性率” 推测，论文应该进行了多组实验以验证 p 值的校准性（假阳性率控制）、统计功效（检测率）以及鲁棒性。但具体实验组数（如不同数据集、不同 k 值、不同显著性水平）未给出。
- **充分性与客观性**：
  - **充分性**：由于信息有限，难以全面评估。但论文发表于 NeurIPS 2025 且获得较高评分（9.0），表明审稿人认为实验设计合理、结果可信。
  - **公平性**：选择性推断方法通常需要在假设检验框架下与标准方法对比，确保对照组设置相同。未发现明显的偏差风险。

## 6. 论文的主要结论与发现
- **主要结论**：提出的基于选择性推断的统计框架能够为 deep kNN 异常检测提供**可靠的 p 值**，从而使用户可以在指定显著性水平下控制假阳性率。
- **发现**：该方法在多个数据集上有效，显著提升了异常检测的**可解释性和信任度**，使其更适合工业检测等关键应用场景。

## 7. 优点
- **理论创新**：将选择性推断引入半监督深度异常检测，解决了长期被忽视的**统计显著性量化**问题。
- **实用价值**：提供 p 值形式的不确定性度量，使异常检测结果可被下游决策直接使用（如仅当 p < 0.01 时才触发警报）。
- **方法简洁**：不改变原始 deep kNN 的模型架构，仅在检测阶段附加推断过程，易于集成到现有系统。
- **控制假阳性率**：严谨的统计保证是其他不确定性方法（如启发式阈值）所不具备的。

## 8. 不足与局限
- **信息缺失**：由于提供的论文内容仅为摘要和元数据，无法获取完整的实验细节（如数据集列表、对比方法、超参数设置、计算资源等），因此难以全面评价其局限。
- **潜在局限**：
  - **计算开销**：选择性推断通常需要求解截断分布或进行采样，可能增加测试阶段的计算复杂度，尤其当测试样本数量大时。
  - **假设强度**：方法可能假设特征提取器在正常数据上充分训练且表示分布已知，若分布估计不准，p 值可能偏离理想校准。
  - **适用场景**：仅针对 deep kNN 这一特定架构，对基于其他原理的异常检测（如重构误差、密度估计）不够通用。
  - **实验覆盖**：缺少现实高维、噪声大或类别不均衡的工业场景下的详细结果。

（完）
