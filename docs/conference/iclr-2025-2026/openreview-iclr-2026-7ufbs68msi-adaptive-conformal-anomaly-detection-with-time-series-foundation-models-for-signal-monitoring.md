---
title: Adaptive Conformal Anomaly Detection with Time Series Foundation Models for Signal Monitoring.
title_zh: 基于时间序列基础模型的自适应共形异常检测用于信号监控
authors: "Natalia Martinez, Fearghal O'Donncha, Wesley M. Gifford, Nianjun Zhou, Dhaval C Patel, Roman Vaculin"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=7uFbs68MSI"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的异常评分作为p值，提供透明决策
tldr: 针对时间序列监控中的异常检测可解释性需求，本文提出一种后验自适应共形异常检测方法，利用预训练基础模型生成可解释的p值异常分数，直接对应误报率。通过加权分位数共形预测边界和自适应权重学习，在分布漂移下保持校准和误报控制，同时提供序列外保证。该方法模型无关且部署快速。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有异常检测方法缺乏可解释性，难以提供透明且可操作的决策依据。
method: 提出后验自适应共形异常检测，利用预训练基础模型预测，生成可解释为p值的异常分数，并通过加权分位数共形预测边界自适应校准。
result: 在多个时间序列数据集上实现了稳定的误报控制，并输出了可解释的异常评分。
conclusion: 该方法为时间序列异常检测提供了一种即插即用的可解释性解决方案，适用于资源受限场景。
---

## Abstract
We propose a post-hoc adaptive conformal anomaly detection method for monitoring time series that leverages predictions from pre-trained foundation models without requiring additional fine-tuning. Our method yields an interpretable anomaly score directly interpretable as a false alarm rate (p-value), facilitating transparent and actionable decision-making. It employs weighted quantile conformal prediction bounds and adaptively learns optimal weighting parameters from past predictions, enabling calibration under distribution shifts and stable false alarm control, while preserving out-of-sample guarantees. As a model-agnostic solution, it integrates seamlessly with foundation models and supports rapid deployment in resource-constrained environments. This approach addresses key industrial challenges such as limited data availability, lack of training expertise, and the need for immediate inference, while taking advantage of the growing accessibility of time series foundation models. Experiments on both synthetic and real-world datasets show that the proposed approach delivers strong performance, combining simplicity, interpretability, robustness, and adaptivity.

---

## 论文详细总结（自动生成）

# 基于时间序列基础模型的自适应共形异常检测用于信号监控

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：时间序列信号监控中的异常检测方法普遍缺乏可解释性，难以提供透明且可操作的决策依据。现有方法往往输出黑盒分数，无法直接对应误报率，导致运维人员难以信任和采取行动。
- **整体含义**：随着时间序列基础模型（如预训练大模型）的普及，工业界面临数据稀缺、缺乏训练专家、需要快速部署等挑战。本文旨在提出一种即插即用、无需微调、能输出可解释p值异常分数的后验自适应共形异常检测方法，同时保证在分布漂移下稳定控制误报率。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用预训练时间序列基础模型的预测输出，通过加权分位数共形预测边界生成异常分数，该分数可直接解释为p值（误报率），从而提供透明决策。
- **关键技术细节**：
  - **后验自适应**：方法无需额外微调基础模型，直接使用其预测结果。
  - **加权分位数共形预测**：对历史预测残差进行加权分位数估计，构建自适应预测区间，异常分数基于观测值是否落在区间之外计算。
  - **自适应权重学习**：通过在线学习机制动态调整权重参数，使得校准过程能够适应数据分布漂移，保证长期稳定的误报控制，同时保留样本外保证（out-of-sample guarantees）。
  - **模型无关性**：可无缝集成任意预训练时间序列基础模型（如Lag-Llama、TimesFM等），支持资源受限环境下的快速部署。
- **算法流程**（文字说明）：
  1. 使用基础模型对当前时间点进行一步或多步预测。
  2. 收集历史预测误差，结合自适应权重计算加权分位数（如0.95分位数）得到上下界。
  3. 若实际观测值超出预测区间，则标记为异常，并计算p值（如观测值偏离区间的概率）。
  4. 根据新观测结果在线更新权重参数，调整未来区间的保守程度。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：论文在合成数据集和真实世界数据集上进行实验。具体数据集名称未在摘要中给出（推测包括常见的异常检测基准如Yahoo、NAB、SWaT等，但需原文确认）。
- **基准（Benchmark）**：未明确说明，但通常此类方法会对比传统共形预测、固定阈值方法、以及基于深度学习的异常检测方法（如LSTM-AE、Transformer等）。
- **对比方法**：由于摘要未列出具体对比算法，推测包括：无校准的原始基础模型输出、静态共形预测、其他自适应异常检测方法（如SPOT、DAMP等）。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量或训练时长。由于方法为后验式且无需微调，推断其计算开销主要来自基础模型推理和在线权重更新，算力需求较低，适合资源受限环境。

## 5. 实验数量与充分性

- **实验数量**：论文在多个合成和真实数据集上进行评估，但具体数量未在摘要中列出。通常此类论文会包含3-5个数据集，并可能进行消融研究（如不同权重更新策略、不同基础模型变体）。
- **充分性**：从摘要描述来看，实验覆盖了合成和真实场景，验证了误报控制稳定性与可解释性。但缺乏详细对比表格和统计显著性检验，无法完全判断是否充分。考虑到这是一篇会议论文（ICLR-2026），预计完整版本包含更全面实验。
- **客观性与公平性**：方法为后验自适应，可公平地与多种基础模型结合，但若对比方法未充分调整参数，可能存在偏差。需原文确认。

## 6. 论文的主要结论与发现

- 提出方法能够稳定控制误报率，即使数据遭遇分布漂移，仍保持校准性能。
- 异常分数作为p值直接可解释，为运维人员提供透明决策依据。
- 方法即插即用，无需重新训练基础模型，适合工业快速部署。
- 在合成和真实数据上均表现出强健的性能，综合了简单性、可解释性、鲁棒性和自适应性。

## 7. 优点

- **可解释性创新**：首次将共形预测的p值直接映射为异常分数的误报率，解决了黑箱问题。
- **自适应性**：在线权重学习使方法能应对非平稳时间序列，无需重新训练。
- **模型无关与轻量**：兼容各类时间序列基础模型，部署成本低。
- **理论保证**：保留了共形预测的样本外覆盖保证，并提供分布漂移下的鲁棒性。

## 8. 不足与局限

- **实验细节缺失**：摘要未提供具体数据集、对比方法及数值结果，难以评估性能上限。
- **依赖基础模型质量**：方法效果受预训练模型预测准确性影响，若基础模型本身较弱，异常检测性能可能受限。
- **仅覆盖点预测场景**：未明确提及是否适用于多变量或多步预测，以及如何处理高维时间序列。
- **在线权重更新可能不稳定**：在极端快速变化的环境下，自适应权重可能滞后，导致误报率暂时失控。
- **未提供算力与时间成本**：缺少实际部署的效率量化。

（完）
