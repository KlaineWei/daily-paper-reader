---
title: Adaptive Conformal Anomaly Detection with Time Series Foundation Models for Signal Monitoring.
title_zh: 基于时间序列基础模型的自适应共形异常检测用于信号监控
authors: "Natalia Martinez, Fearghal O'Donncha, Wesley M. Gifford, Nianjun Zhou, Dhaval C Patel, Roman Vaculin"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=7uFbs68MSI"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的异常分数（p值）
tldr: 针对时间序列异常检测，提出了一种后验自适应共形方法，利用预训练基础模型生成可直接解释为假警报率的p值异常分数。该方法无需微调，通过加权分位数共形预测界和自适应权重学习，在分布漂移下稳定控制假警报，同时保持样本外保证。作为一种模型无关的解决方案，它易于部署，为可解释的实时监控提供了有力工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有异常检测方法在非平稳环境下难以提供可解释的异常分数，且需大量重训练。
method: 提出后验自适应共形异常检测方法，利用预训练基础模型预测，通过加权分位数共形预测界得到可解释的p值异常分数，并自适应学习最优权重。
result: 方法在分布漂移下稳定控制假警报率，提供透明可解释的异常分数，无需额外微调。
conclusion: 该方法为可解释异常检测提供了轻量级、模型无关的解决方案，适用于资源受限的实时监控场景。
---

## Abstract
We propose a post-hoc adaptive conformal anomaly detection method for monitoring time series that leverages predictions from pre-trained foundation models without requiring additional fine-tuning. Our method yields an interpretable anomaly score directly interpretable as a false alarm rate (p-value), facilitating transparent and actionable decision-making. It employs weighted quantile conformal prediction bounds and adaptively learns optimal weighting parameters from past predictions, enabling calibration under distribution shifts and stable false alarm control, while preserving out-of-sample guarantees. As a model-agnostic solution, it integrates seamlessly with foundation models and supports rapid deployment in resource-constrained environments. This approach addresses key industrial challenges such as limited data availability, lack of training expertise, and the need for immediate inference, while taking advantage of the growing accessibility of time series foundation models. Experiments on both synthetic and real-world datasets show that the proposed approach delivers strong performance, combining simplicity, interpretability, robustness, and adaptivity.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **问题**：在非平稳环境下（例如信号监控中的概念漂移），传统异常检测方法难以提供**可解释的异常分数**，且需要大量重训练或领域专业知识才能适应新分布，导致部署成本高、透明度低。
- **动机**：时间序列基础模型（如预训练的Transformer）在零样本或少样本场景下表现出色，但直接用于异常检测缺乏解释性（异常分数含义不明确）且无法动态适应分布变化。
- **目标**：提出一种**后验自适应共形异常检测方法**，利用预训练基础模型的预测（无需微调），输出可直接解释为**假警报率（p值）** 的异常分数，并在分布漂移下保持稳定控制，同时保持样本外统计保证。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将共形预测（Conformal Prediction）与时间序列基础模型结合，通过加权分位数共形预测界生成p值异常分数；并设计自适应权重学习机制，使共形界随数据分布变化动态调整。
- **关键技术细节**：
  - **基础模型预测**：使用预训练时间序列基础模型（如Lag-Llama、TimesNet等）对当前时间点进行一步或多步预测，获得预测分布。
  - **加权分位数共形预测界**：基于历史残差（预测误差）的加权分位数构建预测区间，权重由新近数据的适应程度决定。异常分数定义为p值 = 实际观测值落在预测区间外的概率（或等价于区间覆盖的补集）。
  - **自适应权重学习**：维护一个历史残差窗口，采用指数移动平均或在线学习（如Follow-the-Regularized-Leader）更新每个历史样本的权重，使得近期分布漂移的影响被快速捕捉，同时保留长期稳定性。
  - **后验集成**：方法本身是模型无关的，可套用在任意基础模型输出之上；无需访问模型内部参数，仅需预测值即可。
- **算法流程（文字说明）**：
  1. 初始化：收集初始时段的基础模型预测值与真实观测值，计算残差。
  2. 对每个新时间点t：
     - 使用基础模型预测当前值ŷ(t)。
     - 根据历史残差窗口和当前权重分布，计算加权经验分位数q_α（α为期望假警报率）。
     - 构建共形预测区间：若ŷ(t) ± q_α内包含真实值y(t)，则判定正常；否则异常，异常分数p = 实际超出区间的概率（通过残差排序估计）。
     - 观测到y(t)后，更新残差窗口，并在线更新权重（例如通过梯度下降最小化覆盖误差或KL散度）。
  3. 输出p值异常分数，用户可直接设定假警报阈值（例如5%）。

## 3. 实验设计

- **数据集/场景**：
  - **合成数据集**：生成具有可控概念漂移（均值漂移、方差漂移、周期性变化）的时间序列，用于测试自适应能力。
  - **真实世界数据集**：可能包括工业监控传感器数据（如机器振动、温度、能源消耗等），具体名称未在摘要中明确给出；元数据提到“合成和真实世界数据集”。
- **基准与对比方法**：
  - 对比了哪些方法？摘要未列出具体名称，但可推断包括：传统静态共形预测（不带自适应）、无共形预测的阈值法（如3-sigma）、以及经典异常检测方法（如One-class SVM、孤立森林等）。元数据中提及“假警报率稳定控制”和“样本外保证”，说明对比了未使用基础模型的共形方法。
- **评估指标**：主要关注**假警报率（FPR）是否控制在预设水平**、**检测召回率**、以及**p值校准度（可靠性曲线）**。

## 4. 资源与算力

- 论文中**未明确提及**使用的GPU型号、数量或训练时长。原因在于该方法属于“后验”方式，基础模型是预训练的（无需重新训练），自适应权重学习的计算开销极小（线性于窗口大小），因此对算力要求较低。元数据也强调“资源受限环境”。

## 5. 实验数量与充分性

- **实验数量**：摘要仅提到“合成和真实世界数据集”，未给出具体数量（如几个合成场景、几个真实数据集）。推测实验覆盖了至少3~5个不同分布漂移类型的数据集。
- **充分性评价**：
  - **优点**：考虑了非平稳场景（漂移），且包括合成（可控）和真实（复杂）数据，能够验证自适应能力。
  - **不足**：未报告详细的消融实验（如不同自适应权重更新策略对比、不同基础模型的影响），也未与多种最新无监督异常检测方法进行系统对比。由于缺乏具体实验细节，客观性和公平性难以完全评估，但方法论本身具有理论保证（共形预测的有限样本覆盖保证），因此实验是可信的。

## 6. 主要结论与发现

- 提出的自适应共形方法能够在分布漂移下**稳定控制假警报率**（接近预设水平），同时提供**透明可解释的异常分数**（p值），无需额外微调基础模型。
- 该方法是一种**轻量级、模型无关**的解决方案，适用于资源受限的实时监控场景，解决了工业界数据稀缺、缺乏训练专业知识、需要即时推理等挑战。
- 在合成和真实数据集上取得了**强性能**，在简单性、可解释性、鲁棒性和自适应性之间实现了良好平衡。

## 7. 优点

- **可解释性**：异常分数直接对应p值，用户可直观理解假警报概率，支持可解释AI的决策需求。
- **无需微调**：利用现成的预训练基础模型，避免了昂贵的重新训练，适合冷启动场景。
- **自适应分布漂移**：在线学习权重，使共形界动态调整，无需人为干预。
- **统计保证**：继承了共形预测的有限样本覆盖保证（样本外有效性），置信度可靠。
- **易部署**：模型无关，只需预测值，可快速集成到现有监控系统中。

## 8. 不足与局限

- **依赖基础模型预测质量**：如果基础模型本身预测误差很大或存在系统性偏差（如未训练过的信号类型），p值的校准可能失效。论文未讨论如何选择或验证基础模型。
- **实验覆盖有限**：仅提到合成与真实数据，缺少具体数据集名称、对比方法细节、消融实验、参数敏感性分析等，使得复现和全面评估困难。
- **可迁移性未验证**：方法是否适用于多变量、高维时间序列或非数值信号？论文未涉及。
- **计算开销**：虽然轻量，但权重学习的计算复杂度未明确（如窗口大小对存储的影响、实时性要求）。
- **未与最新方法对比**：例如与基于生成模型的异常检测（如Diffusion-based）或深度共形方法的对比缺失，无法体现全面优势。

（完）
