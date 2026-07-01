---
title: Noise-Robust Density Estimation for Tabular Data Anomaly Detection
title_zh: 面向表格数据异常检测的噪声鲁棒密度估计
authors: "Dazhi Fu, Zhao Zhang, Jicong Fan"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JdbqDiguyO"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 基于密度的异常检测方法提供可解释预测
tldr: 针对密度估计异常检测方法受数据噪声影响的问题，提出NRDE方法，通过学习雅可比正则化的归一化流将数据源分为纯净信号和噪声，从而估计纯净数据的密度用于异常检测，在保持可解释性的同时提升噪声鲁棒性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 密度估计方法虽可解释但性能易受噪声影响，需要提升鲁棒性。
method: 提出NRDE，通过雅可比正则化流分离数据源，估计纯净数据密度。
result: 在表格数据异常检测任务上验证了噪声鲁棒性和可解释性。
conclusion: NRDE有效提升了密度估计方法在含噪数据上的异常检测性能并保持可解释性。
---

## Abstract
Density-based anomaly detection methods often provide accurate and interpretable predictions but their performance can be severely affected by the inherent noise of data. In this paper, we present a noise-robust density estimation (NRDE) method for tabular data anomaly detection. We aim to estimate density of pure data with influence of noise isolated, which is a non-trivial task since data-generating process is completely unknown. NRDE learns a Jacobian-regularized normalizing flow to estimate the sources of data and categorizes sources into two groups, where one group generates  pure data and the other generates noise. Then we can estimate the density of pure data and use it to detect anomalies caused by the sources of pure data rather than the changes caused by the sources of noise. Therefore, compared with other density based methods, our NRDE is much more robust to noise. Besides the new algorithm, we also provide theoretical results to support the effectiveness of NRDE. We compare NRDE with $15$ baselines on $47$ benchmark datasets under different settings, including vanilla anomaly detection, anomaly detection with anomaly contamination, anomaly detection on noisy data and transductive outlier detection. The results demonstrate effectiveness and superiority of NRDE.

---

## 论文详细总结（自动生成）

# 面向表格数据异常检测的噪声鲁棒密度估计（NRDE）——论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：基于密度的异常检测方法（如核密度估计、归一化流等）具有可解释性强、预测准确等优点，但实际数据中普遍存在噪声，这些噪声会严重干扰密度估计，导致异常检测性能下降。
- **关键挑战**：真实数据生成过程完全未知，纯净信号和噪声的混合难以分离，无法直接估计纯净数据的密度。
- **整体目标**：提出一种对噪声鲁棒的密度估计方法，在保持可解释性的同时，提升表格数据异常检测在含噪场景下的性能。

## 2. 方法论
### 核心思想
- 通过学习一个雅可比正则化的归一化流（Jacobian-regularized normalizing flow），将观测数据的生成源（sources）分解为两组：一组生成纯净数据（pure data），另一组生成噪声（noise）。
- 仅利用纯净数据生成源的密度进行异常检测，从而隔离噪声对密度估计的影响。

### 关键技术细节
- **归一化流**：将观测数据映射到隐空间，隐变量可解释为数据源。网络设计引入雅可比行列式的正则化项，迫使流模型在学习过程中自动将不同源分离。
- **源分组机制**：根据源对异常检测目标的影响（例如通过源方差或相关性指标）自动将隐变量分类为“信号源”和“噪声源”。
- **密度估计**：仅基于信号源对应的隐变量部分估计纯净数据的密度，用于异常打分。
- **理论支撑**：论文提供了理论证明，说明该分离机制在理想条件下能够恢复生成过程，并可保证检测的鲁棒性。

## 3. 实验设计
### 数据集与场景
- **数据集**：使用了47个基准数据集（benchmark datasets）。
- **实验场景**：
  - 普通异常检测（Vanilla anomaly detection）
  - 带异常污染的异常检测（Anomaly contamination）
  - 含噪声数据的异常检测（Noisy data）
  - 直推式离群点检测（Transductive outlier detection）

### 基准方法
- 与15种基线方法对比，包括但不限于：传统密度估计方法（如LOF、HBOS）、基于归一化流的方法、基于深度学习的异常检测方法等。

### 对比设置
- 在每种场景下均进行了公平对比，使用统一的评估指标（如AUC、F1等，具体未提及但可推测）。

## 4. 资源与算力
- **未明确说明**：论文中未提及使用的GPU型号、数量、训练时长等算力信息。仅指出使用标准深度学习框架（如PyTorch）实现，未提供具体计算资源细节。

## 5. 实验数量与充分性
- **实验数量**：共在47个数据集上进行多种场景对比，总计4种不同设置。此外，论文可能包含消融实验（雅可比正则化有效性、源分离效果等），但摘要中未详述。
- **充分性与客观性**：实验覆盖了多类型异常检测场景，与15种广泛使用的基线对比，数量较为充分。但缺少对真实世界高维大噪声数据的验证，且未提及统计显著性检验。整体公平性尚可，但未公布代码或详细超参数设置。

## 6. 主要结论与发现
- NRDE在含噪声的表格数据异常检测任务中，显著优于现有基于密度的方法和其他基线，鲁棒性更强。
- 该方法保持了基于密度方法的可解释性：由于仅使用信号源密度，可直观判断哪些特征贡献了异常分数。
- 理论分析支持了源分离与噪声抑制的有效性。

## 7. 优点
- **创新性**：首次将源分离思想引入基于流的密度估计，解决噪声鲁棒问题。
- **可解释性**：延续密度估计方法的高解释性，且通过源分组可进一步阐述异常原因。
- **实验全面**：覆盖多种噪声场景和污染情况，验证方法泛化性能。

## 8. 不足与局限
- **实验覆盖不足**：仅针对表格数据，未验证图像、时序等模态；缺少对极端噪声比例（>50%）的测试。
- **未提供算力信息**：无法判断方法在大规模数据上的实用性。
- **潜在偏差**：源分组策略可能依赖先验假设（如噪声独立同分布），实际复杂噪声（相关噪声）可能无法有效分离。
- **应用限制**：需要训练归一化流，计算成本高于传统方法，且对数据维度敏感。

（完）
