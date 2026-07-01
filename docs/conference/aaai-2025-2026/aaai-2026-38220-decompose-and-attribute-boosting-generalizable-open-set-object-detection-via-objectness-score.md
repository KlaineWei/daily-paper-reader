---
title: "Decompose and Attribute: Boosting Generalizable Open-Set Object Detection via Objectness Score"
title_zh: 分解与归因：通过目标性分数提升可泛化开放集目标检测
authors: "Yuxuan Yuan, Lichen Wei, Luyao Tang, Chaoqi Chen, Zheyuan Cai, Yue Huang, Xinghao Ding"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38220/42182"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 开放集目标检测分解归因可解释性
tldr: 开放集目标检测面临域偏移和未知类别挑战，现有方法混淆域风格与语义内容。本文提出DOAT框架，利用小波分解分离域特定风格与语义结构，并通过归因机制提升可解释性。在多个跨域和开放集检测基准上，DOAT有效提升了泛化性能，同时提供了可解释的分解归因，为可解释目标检测提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 845, \"height\": 515, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1828, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1732, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 863, \"height\": 297, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1842, \"height\": 1030, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 731, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1831, \"height\": 365, \"label\": \"Table\"}]"
motivation: 域风格与语义纠缠导致泛化能力差，且缺乏可解释性。
method: 采用小波特征分解分离风格与语义，并通过归因机制提升可解释性。
result: 在多个跨域和开放集检测任务上取得最优，同时提供可解释性分析。
conclusion: 分解归因框架有效增强了目标检测的泛化性和可解释性。
---

## Abstract
Open-set object detection (OSOD) aims to recognize known object categories while localizing previously unseen instances. However, real-world scenarios often involve co-occurring domain shifts and novel object categories. Existing OSOD methods typically overlook domain shifts, relying on source-trained representations that entangle domain-specific style with semantic content, thereby hindering generalization to both unseen domains and novel categories. To address this challenge, we propose a unified framework, termed DecOmpose and ATtribute (DOAT), which disentangles domain-specific style from semantic structure, thereby facilitating generalizable object detection. DOAT employs wavelet-based feature decomposition to separate style information from high-frequency structural details, thus enabling an explicit separation of domain and category shifts. To account for domain shift, the low-frequency components are perturbed within a style subspace to simulate diverse domain appearances. For unknown object discovery, the high-frequency components are utilized to estimate objectness scores via an attribution mechanism that fuses wavelet energy with semantic distance to known-category prototypes. Extensive experiments on standard open-set benchmarks have demonstrated the superior generalization performance of DOAT.

---

## 论文详细总结（自动生成）

# 论文总结：Decompose and Attribute: Boosting Generalizable Open-Set Object Detection via Objectness Score

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：开放集目标检测（OSOD）在实际部署中同时面临**域偏移**（如光照、天气变化）和**未知类别**（训练时未出现的物体）。现有OSOD方法大多忽略域偏移，使用源域训练的特征表示往往将**域特定的风格**与**语义内容**纠缠在一起，导致在未见过的域和未知类别上泛化能力差。
- **研究背景**：现有方法如OW-DETR、PROB、CAT等虽然能检测未知物体，但在域偏移下，因特征纠缠而性能严重下降——容易把未知物体误判为已知类别，或者把背景当作物体。
- **论文目标**：提出一个统一框架DOAT，通过显式分离域特定风格与语义结构，实现在域偏移下的鲁棒开放集检测，同时提升可解释性。

## 2. 方法论

### 2.1 核心思想
- 利用**小波变换**将特征图分解为**低频分量**（编码域敏感的样式信息）和**高频分量**（编码域不变的结构细节）。低频分量用于风格扰动以模拟域变化，高频分量用于估计类别无关的目标性分数。
- 设计**目标性归因机制**，结合能量引导和语义引导，无需显式建模未知类别即可发现未知物体。

### 2.2 关键技术细节

1. **频率特征分解**（Discrete Wavelet Transform, DWT）：  
   使用 Haar 小波基（LL, LH, HL, HH 四个滤波器）对 backbone 各层特征图进行卷积分解，得到低频子带 \( f_{LL} \) 和高频子带 \( f_{LH}, f_{HL}, f_{HH} \)。相比 FFT，DWT 保留空间局部性和方向信息，更适合目标检测。

2. **低频谱风格多样化（LFSD）**：  
   - 仅对低频特征 \( f_{LL} \) 进行扰动。  
   - 构建风格子空间：对源域特征的均值-标准差对（μ, σ）采用**最远点采样（FPS）** 选择 K 个代表性风格基。  
   - 从 Dirichlet 分布采样权重组合基，生成新的风格统计量 \( \mu_H, \sigma_H \)，通过 AdaIN 风格归一化公式合成新特征：  
     \[
     \tilde{f}_{LL} = \sigma_H \cdot \frac{f_{LL} - \mu(f_{LL})}{\sigma(f_{LL})} + \mu_H
     \]  
   - 该操作模拟多样域外观，同时保持语义内容不变。

3. **未知物体发现目标性归因**：  
   - **能量引导归因（EGA）**：对每个查询框区域，提取所有尺度上的高频子带能量，生成能量嵌入 \( E(q_i) \)，反映结构丰富度。  
   - **语义引导归因（SGA）**：维护一个已知类查询的原型 \( \hat{q} \)（EMA更新），计算查询与原型之间的归一化欧氏距离，得到软分数：  
     \[
     s_{q_i} = \exp\left(-\frac{\text{dist}(q_i, \hat{q})}{\tau}\right) \cdot \hat{E}(q_i)
     \]  
   - 该分数作为伪标签训练**目标性头**，采用二分类交叉熵损失 \( \mathcal{L}_{\text{obj}} \)。  
   - 最终分类概率分解为：\( p(c|q) = p(c|o=1,q) \cdot p(o=1|q) \)，从而避免对未知类别显式建模。

## 3. 实验设计

### 3.1 使用的数据集 / 场景
- **Cityscapes → Foggy Cityscapes**：12 种设置，按语义重叠（het-sem, hom-sem）和实例频率（freq-dec, freq-inc）以及未知类别数量（3/4/5）划分。
- **Cityscapes → BDD100K**：同样按 het-sem 和未知类别数量划分。
- **Pascal VOC → Clipart1K**：按未知类别数量（6/8/10）划分。

### 3.2 Benchmark 与对比方法
- **基检测器**：Deformable DETR（D-DETR）。
- **对比方法**：D-DETR（基线）、OpenDet、OW-DETR、PROB、CAT、SOMA、SS-OWFormer。所有方法在统一设置下复现。
- **评估指标**：基类性能用 mAP\(_k\)；未知类性能用 AR\(_u\)、Wilderness Impact (WI)、Absolute Open-Set Error (AOSE)。

## 4. 资源与算力

- **硬件**：单块 NVIDIA A40 GPU（文中仅提到 “on an NVIDIA A40 GPU”）。
- **训练配置**：80 个 epoch，batch size 4，AdamW 优化器（初始学习率 2×10⁻⁴，权重衰减 5×10⁻⁴）。
- **未明确说明**：GPU 数量、总训练时间、显存占用等细节未提供。

## 5. 实验数量与充分性

- **实验组数**：
  - Cityscapes → Foggy：12 组设置（4 种任务 × 3 种未知类别数）。
  - Cityscapes → BDD100K：3 组（het-sem 下 3 种未知类别数）。
  - Pascal VOC → Clipart：3 组（6/8/10 未知类别）。
  - 消融实验：表4、表5、图5 等，共约 5 组以上的消融分析（分解/归因/风格策略/损失权重等）。
- **充分性评估**：
  - **充足**：覆盖多种域迁移和类别偏移设置，并在三个跨域基准上验证，对比了 6 种主流方法。
  - **公平性**：所有方法在同一检测框架下复现，评估指标统一。
  - **客观性**：结果报告了平均指标，并提供了可视化 t-SNE 和定性比较。

## 6. 主要结论与发现

- DOAT 在 **12 组 Foggy 设置**上**一致取得最佳**未知类检测性能（高 AR\(_u\)，低 WI/AOSE），同时保持甚至提升基类 mAP\(_k\)。
- 在 Pascal VOC → Clipart 大域偏移场景下，DOAT 显著领先，AR\(_u\) 最高提升约 10 个百分点。
- 在更具挑战的 Cityscapes → BDD100K 场景下，虽然增益有限，但仍优于所有对比方法。
- **消融实验**证明：
  - 频率分解和目标性归因均至关重要。
  - FPS 风格采样优于随机插值或随机扰动。
  - 在低频特征上扰动比在全特征上扰动效果更好。
  - 目标性头预测的分数在前景/背景上呈现可区分的高斯分布，说明结构化学习。
- 验证了**显式分离域风格与语义结构**能够显著提升开放集检测在域偏移下的泛化能力。

## 7. 优点

- **方法创新**：将频域分解（小波）与开放集检测结合，利用低频/高频的不同特性分别处理域偏移和未知物体发现，思路清晰且合理。
- **可解释性**：通过能量引导和语义引导的归因机制，为目标性分数提供了物理含义（结构显著性和语义距离），有助于理解模型行为。
- **简洁有效**：无需生成伪标签或显式建模未知类，仅通过类别无关的目标性分数实现未知检测，降低训练复杂度。
- **实验充分**：在 3 个跨域基准、12+3+3 种设置下验证，消融实验覆盖关键组件，对比方法涵盖近年主流。

## 8. 不足与局限

- **实验覆盖有限**：仅使用了自动驾驶和自然图像跨域场景（Cityscapes, BDD100K, Clipart），未在更广泛的安全关键场景（如医疗、工业质检）中验证。
- **算力细节缺失**：未报告 GPU 数量、训练总时长，可重复性有所欠缺。
- **局限性讨论**：
  - 高纹理背景（如建筑物、植被）可能被能量引导归因误判为物体（文中已提及）。
  - 在 BDD100K 这种低光照、运动模糊严重的场景下，高频结构线索受限，性能增益较小，表明方法对图像质量有一定依赖。
  - 风格多样化仅依赖源域内插值，可能无法覆盖目标域的极端风格（如极端雾气、夜间），存在外推风险。
  - 基类性能（mAP\(_k\)）在部分场景下提升不大，说明未知检测的增益可能以基类稳定性为代价（尽管文中未显著下降）。
- **未进行用户研究或可解释性量化评估**：虽声称提升可解释性，但缺乏定量指标（如特征归因的忠实度）。

（完）
