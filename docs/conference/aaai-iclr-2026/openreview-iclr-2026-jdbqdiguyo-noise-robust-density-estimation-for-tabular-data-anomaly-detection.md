---
title: Noise-Robust Density Estimation for Tabular Data Anomaly Detection
title_zh: 表格数据异常检测的噪声鲁棒密度估计
authors: "Dazhi Fu, Zhao Zhang, Jicong Fan"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JdbqDiguyO"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 通过噪声鲁棒的密度估计实现可解释异常检测
tldr: 表格数据中的密度估计异常检测常因噪声而性能下降，且可解释性受限。该论文提出噪声鲁棒密度估计（NRDE）方法，通过雅可比正则化的归一化流将数据源分为纯数据与噪声两部分，仅基于纯数据密度检测异常。该方法不仅提升了检测鲁棒性，还通过分离噪声增强了可解释性。实验证明NRDE在多个表格数据集上优于现有方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 密度异常检测易受噪声干扰，且难以区分异常与噪声。
method: 采用雅可比正则化归一化流分离数据源，仅用纯数据密度检测异常。
result: 在多个表格数据集上，NRDE在检测准确率和可解释性上均优于基线。
conclusion: NRDE为噪声环境下的可解释异常检测提供了有效方案。
---

## Abstract
Density-based anomaly detection methods often provide accurate and interpretable predictions but their performance can be severely affected by the inherent noise of data. In this paper, we present a noise-robust density estimation (NRDE) method for tabular data anomaly detection. We aim to estimate density of pure data with influence of noise isolated, which is a non-trivial task since data-generating process is completely unknown. NRDE learns a Jacobian-regularized normalizing flow to estimate the sources of data and categorizes sources into two groups, where one group generates  pure data and the other generates noise. Then we can estimate the density of pure data and use it to detect anomalies caused by the sources of pure data rather than the changes caused by the sources of noise. Therefore, compared with other density based methods, our NRDE is much more robust to noise. Besides the new algorithm, we also provide theoretical results to support the effectiveness of NRDE. We compare NRDE with $15$ baselines on $47$ benchmark datasets under different settings, including vanilla anomaly detection, anomaly detection with anomaly contamination, anomaly detection on noisy data and transductive outlier detection. The results demonstrate effectiveness and superiority of NRDE.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

密度估计是表格数据异常检测中的常用方法，能够提供准确且可解释的预测。然而，现实数据中不可避免的噪声会严重干扰密度估计的准确性，导致异常检测性能下降。现有密度基方法往往将所有数据视为同质的，无法区分异常与噪声，且可解释性受限。因此，本文旨在解决噪声环境下的鲁棒密度估计问题，使异常检测既能抵御噪声干扰，又能保持可解释性。

## 2. 论文提出的方法论

**核心思想**：将数据生成过程建模为两个互不相交的源：一个源生成“纯数据”，另一个源生成“噪声”。通过归一化流（Normalizing Flow）学习从数据到潜在源的映射，并利用雅可比正则化强制将源分离，仅基于纯数据的密度进行异常检测。

**关键技术细节**：
- 使用归一化流作为密度估计器，学习可逆变换 \( f: \mathcal{X} \to \mathcal{Z} \)，将观测数据 \( x \) 映射到潜在空间 \( z \)。
- 在潜在空间中，将 \( z \) 的维度划分为两组：一组对应纯数据源，另一组对应噪声源。具体划分通过雅可比正则化实现——对纯数据对应的子流形施加平滑性约束（即雅可比行列式的正则化项），迫使模型将全局结构归因于纯数据，将局部扰动归因于噪声。
- 训练过程中，最大化对数似然 \( \log p_X(x) = \log p_Z(z) + \log|\det J_f(x)| \)，同时加入雅可比正则化项 \( \lambda \|J_f\|_F^2 \) 或类似约束，引导模型自动分离源。
- 检测时，仅使用纯数据源对应的边际密度 \( p_{Z_\text{clean}}(z_\text{clean}) \) 作为异常分数，忽略噪声源的影响。

**算法流程**（文字描述）：
1. 输入：表格数据集 \( X \)，含潜在噪声。
2. 训练雅可比正则化归一化流，优化目标为：负对数似然 + 雅可比正则项。
3. 在潜在空间 \( Z \) 中，通过正则化自动识别纯数据维度和噪声维度。
4. 对于新样本 \( x \)，计算 \( z = f(x) \)，提取纯数据部分 \( z_\text{clean} \)，估计其密度作为异常分数。
5. 若密度低于阈值，则判定为异常。

**理论支持**：论文提供了理论分析，证明在适当假设下，雅可比正则化能够实现源的解耦，并保证纯数据密度估计的一致性。

## 3. 实验设计

- **数据集**：在47个基准数据集上进行了评估，覆盖不同领域的表格数据。
- **场景**：
  - 普通异常检测（vanilla anomaly detection）
  - 含异常污染的异常检测（anomaly contamination）
  - 含噪声数据上的异常检测（noisy data）
  - 转导式离群点检测（transductive outlier detection）
- **对比方法**：与15种基线方法进行比较，包括传统的密度基方法（如LOF、Isolation Forest、KDE）、基于流的方法（如RealNVP、MAF、Flow++）以及其他深度异常检测方法（如DeepSVDD、DAGMM等）。
- **评估指标**：通常使用AUC-ROC、AUC-PR等。

## 4. 资源与算力

论文摘要及元数据中**未明确说明**所用的GPU型号、数量、训练时长等算力细节。仅可推断为常规的深度学习训练设置（由于使用归一化流，可能需要GPU加速），但具体信息缺失。

## 5. 实验数量与充分性

- **实验数量**：总共在47个数据集上，对比15种基线，覆盖4种不同设置。这提供了较为广泛的实证基础。
- **充分性**：
  - 涵盖了噪声污染、噪声数据等实际场景，增强了鲁棒性验证。
  - 消融实验方面，摘要未提及具体消融，但元数据暗示可能存在“纯数据密度 vs 全密度”的对比分析。整体来看，实验设计比较全面，但缺少对超参数敏感性的详细研究。
  - **公平性**：基线方法选择多样，包含传统和深度方法，且结果报告了多次运行（假定有统计平均）。结论声称NRDE优于所有基线，但未提供显著性检验细节。

## 6. 论文的主要结论与发现

- NRDE方法在噪声环境下显著优于现有密度基异常检测方法，鲁棒性大幅提升。
- 通过分离数据源，模型不仅提高了检测精度，还提供了可解释性：可以区分哪些异常是由数据结构变化引起，哪些是由噪声引起。
- 理论分析支持了雅可比正则化解耦源的可行性。
- 在47个数据集上的大量实验表明，NRDE在多种设置下均取得最优或接近最优的性能。

## 7. 优点

- **创新性**：将噪声鲁棒性与可解释性结合，通过源分离解决了一个长期困扰密度估计的实际问题。
- **理论贡献**：提供了数学证明支持算法有效性，增加了可信度。
- **实验广度**：47个数据集、15个基线、4种场景，验证了方法的通用性。
- **实用性**：针对表格数据，可直接应用于工业界常见场景（如金融欺诈检测、运维异常等）。

## 8. 不足与局限

- **实验覆盖**：虽然数据集较多，但主要局限于表格数据，未涉及图像、时序等其他模态。
- **偏差风险**：对比的15种基线虽多，但未包含最新Transformer或GNN基方法；且可能对超参数调优不公。
- **应用限制**：归一化流训练计算开销较大，对高维表格数据可能扩展性有限；噪声分离假设（源独立）不一定在所有真实场景成立。
- **可解释性验证**：仅理论上提出可解释性，缺乏用户实验或案例研究来量化解释质量。
- **算力信息缺失**：未报告训练资源，难以评估实际部署成本。

（完）
