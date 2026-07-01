---
title: "GCAD: Anomaly Detection in Multivariate Time Series from the Perspective of Granger Causality"
title_zh: GCAD：基于格兰杰因果视角的多变量时间序列异常检测
authors: "Zehao Liu, Mengzhou Gao, Pengfei Jiao"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/34096/36251"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 使用格兰杰因果实现可解释异常检测
tldr: 针对现有图神经网络异常检测方法缺乏可解释性的问题，提出GCAD框架，通过格兰杰因果建模变量间可解释的因果关系，并利用因果模式的变化检测异常。实验在多个时间序列基准上验证了其有效性。该方法为时间序列异常检测提供了因果层面的可解释性，有助于理解异常根源。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34096/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1495, \"height\": 793, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34096/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34096/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 816, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34096/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 871, \"height\": 438, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-34096/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 741, \"height\": 616, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-34096/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 833, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-34096/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 745, \"height\": 300, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-34096/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1797, \"height\": 480, \"label\": \"Table\"}]"
motivation: 现有图方法仅学习序列嵌入的相似性，缺乏对图结构影响时间序列演化的可解释性。
method: 设计基于格兰杰因果的可解释因果图建模空间依赖，并通过因果模式变化检测异常。
result: 在多个基准数据集上取得先进结果，提供了可解释的异常检测。
conclusion: 通过可解释因果建模，有效提升了异常检测的透明度和准确性。
---

## Abstract
Multivariate time series anomaly detection has numerous real-world applications and is being extensively studied. Modeling pairwise correlations between variables is crucial. Existing methods employ learnable graph structures and graph neural networks to explicitly model the spatial dependencies between variables. However, these methods are primarily based on prediction or reconstruction tasks, which can only learn similarity relationships between sequence embeddings and lack interpretability in how graph structures affect time series evolution. In this paper, we designed a framework that models spatial dependencies using interpretable causal relationships and detects anomalies through changes in causal patterns. Specifically, we propose a method to dynamically discover Granger causality using gradients in nonlinear deep predictors and employ a simple sparsification strategy to obtain a Granger causality graph, detecting anomalies from a causal perspective. Experiments on real-world datasets demonstrate that the proposed model achieves more accurate anomaly detection compared to baseline methods.

---

## 论文详细总结（自动生成）

# GCAD：基于格兰杰因果视角的多变量时间序列异常检测

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：多变量时间序列异常检测在工业系统（如供水、航天、服务器）中至关重要。现有基于图神经网络的方法通过可学习图结构建模变量间空间依赖，但这些方法依赖于预测或重构任务，仅能学习序列嵌入的相似性，缺乏对图结构如何影响时间序列演化的可解释性。实际场景中，异常往往伴随依赖结构的变化（如管道泄漏导致压力因果关系改变），因此需要从因果角度建模。
- **核心问题**：如何利用可解释的因果关系（格兰杰因果）动态建模变量间依赖，并通过因果模式的变化来检测异常。
- **整体含义**：提出GCAD框架，首次将深度模型与格兰杰因果结合用于时间序列异常检测，实现可解释的因果图建模，并在多个真实数据集上取得最优性能。

## 2. 论文提出的方法论

### 核心思想
利用非线性深度预测器的梯度动态发现格兰杰因果关系，通过因果模式的偏离检测异常。

### 关键技术细节
- **预测器**：使用Mixer Predictor（多层堆叠的时序混合和特征混合MLP）对滑动窗口进行预测。
- **通道分离梯度生成器**：对每个变量计算预测误差，通过反向传播获得梯度张量 \( G_t \in \mathbb{R}^{N \times N \times \tau} \)（N为变量数，τ为最大时滞）。
- **格兰杰因果发现**：将因果效应量化为梯度在时滞上的积分：\( a_{i,j} = \int_{t-\tau}^{t-1} \left| \frac{\partial L_{t,j}}{\partial x_{\phi,i}} \right| P(x_{\phi,i}) dx_{\phi,i} \)，形成因果矩阵 \( A \in \mathbb{R}^{N \times N} \)。
- **因果图稀疏化**：通过对称性稀疏消除双向边，保留单向因果：\( \tilde{A}_{i,j} = \max(0, A_{i,j} - A_{i,j}^T) \)，并设定阈值 \( h \) 去除噪声。
- **异常评分**：
  - 从训练集采样得到典型正常因果模式 \( A_{\text{norm}} \)
  - 计算测试窗口的因果偏差 \( S_c = \sum \frac{|\tilde{A}_{\text{test}} - A_{\text{norm}}|}{A_{\text{norm}} + \epsilon} \)
  - 加入时序模式偏差 \( S_t \)（利用主对角线元素）
  - 最终评分：\( S = S_c + \beta S_t \)

### 算法流程
1. **训练阶段**：在正常数据上训练预测器（最小化MSE损失）。
2. **采样阶段**：对训练集窗口按伯努利分布采样，计算各窗口因果图并求平均得正常模式。
3. **测试阶段**：对每个测试窗口计算因果图，与正常模式比较得到异常评分，通过阈值判定异常。

## 3. 实验设计

- **数据集**：5个真实世界基准数据集：
  - SWaT（水处理系统，51个变量）
  - SMD（服务器监测，38个变量）
  - MSL（火星科学实验室，55个变量）
  - SMAP（土壤水分主动被动，25个变量）
  - PSM（池化服务器监测，25个变量）
- **对比方法**：6种基线方法：
  - DAGMM、USAD、GDN、AnomalyTransformer（AT）、GANF、MEMTO
- **评估指标**：AUROC和AUPRC（阈值无关）
- **实验设置**：80%正常数据训练，20%验证，测试集包含标注异常。

## 4. 资源与算力

论文未明确提及所使用的GPU型号、数量或训练时长等算力信息。仅提到所有实验重复10次取平均结果。

## 5. 实验数量与充分性

- **总体实验**：在5个数据集上各进行10次重复实验，统计平均性能。
- **消融实验**：在SWaT和SMD上进行了3组消融：
  - 去除因果图稀疏化（-Spars）
  - 去除格兰杰因果（-GC）
  - 去除时序模式偏差（-TC）
- **参数敏感性**：在SWaT上分析了最大时滞τ和稀疏化阈值h的影响。
- **案例研究**：针对SWaT的真实攻击事件，可视化了因果模式偏差矩阵，并分析受影响传感器。
- **充分性评估**：实验覆盖多种规模的数据集和多种基线方法，消融和参数分析较全面，但未提供统计显著性检验，且仅使用两个消融数据集略显不足。整体较为充分客观。

## 6. 论文的主要结论与发现

- GCAD在5个数据集中的12个指标（5×2）上，有9个取得最优（AUROC或AUPRC第一），综合性能优于所有基线。
- 格兰杰因果的引入显著提升了异常检测性能（消融时-GC下降明显）。
- 因果图稀疏化有助于减少噪声，提升效果。
- 时序模式偏差的加入进一步增强了模型对时域依赖的捕获能力。
- 案例表明GCAD能有效检测因果结构变化，即使在序列本身无明显波动时也能通过因果模式偏离识别异常。

## 7. 优点

- **可解释性**：首次将格兰杰因果与深度模型结合，提供了因果级别的可解释性，有助于理解异常根源。
- **计算高效**：训练后测试阶段无需在线优化，只需一次前向和梯度计算，适合流式数据。
- **稀疏化策略**：简洁有效的对称性稀疏方法消除双向相似性，保留单向因果。
- **融合时空偏差**：异常评分同时包含因果模式偏差和时序模式偏差，更全面。
- **实验充分**：在多个真实数据集上对比多种基线，消融和参数分析完整。

## 8. 不足与局限

- **二元因果局限**：只能捕获变量间的二元因果对，无法建模多变量间的复杂交互（如联合因果或高阶交互），论文也承认此局限。
- **无GPU资源说明**：未报告实验硬件配置，影响可复现性评估。
- **消融实验范围有限**：仅在两个数据集上进行了完整消融，其他三个数据集未报告，可能遗漏数据集依赖的结论。
- **统计检验缺失**：未报告方差或显著性检验（如t检验），无法确认性能差异的统计显著性。
- **稀疏化阈值选择依赖人工**：阈值h需手动设定，缺乏自动化方法，可能影响泛化。
- **仅考虑线性因果假设的扩展**：虽使用非线性预测器，但格兰杰因果本质上基于预测误差，可能无法捕捉非线性因果方向反转等情况。

（完）
