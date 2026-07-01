---
title: "MVP-CBM: Multi-layer Visual Preference-enhanced Concept Bottleneck Model for Explainable Medical Image Classification"
title_zh: MVP-CBM：用于可解释医学图像分类的多层视觉偏好增强概念瓶颈模型
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0060.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 通过概念瓶颈模型实现可解释的医学图像分类，可解释性方法
tldr: 该论文针对医学图像分类的可解释性需求，提出了多层视觉偏好增强的概念瓶颈模型（MVP-CBM）。通过将视觉偏好融入概念学习，模型在保持分类精度的同时提供了可理解的决策依据。实验表明，该方法在多个医学图像数据集上取得了良好性能，为可解释视觉分析提供了借鉴，但任务为图像分类而非目标检测。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-60/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 895, \"height\": 776, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-60/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1835, \"height\": 670, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-60/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 320, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-60/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-60/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 888, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-60/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 895, \"height\": 749, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-60/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1840, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-60/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-60/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 893, \"height\": 551, \"label\": \"Table\"}]"
motivation: 医学图像分类需要可解释的决策过程。
method: 提出多层概念瓶颈模型，融合视觉偏好信息实现可解释分类。
result: 在医学图像分类任务上达到了高精度且具有可解释性。
conclusion: MVP-CBM提供了有效的可解释分类框架，可迁移至目标检测场景。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：医学图像分类中深度神经网络的黑箱特性缺乏透明度，尤其在癌症诊断等高风险场景中威胁可信度。概念瓶颈模型（CBM）通过将预测链接到人类可理解的概念来提升可解释性，但现有方法通常仅使用视觉编码器的最后一层特征与概念对应，忽略了**概念偏好变化现象**（concept preference variation）——不同视觉层对特定概念的关联能力存在差异，仅依赖最后一层会削弱特征与概念的准确匹配，损害可解释性。
- **整体含义**：本文旨在通过显式建模各视觉层对不同概念的内在偏好，并跨层稀疏融合概念激活，解决上述问题，从而同时提升模型的可解释性和分类性能。

### 2. 论文提出的方法论

- **核心思想**：利用视觉Transformer（ViT）的多层结构，为每个概念动态选择最相关的视觉层，并稀疏聚合跨层概念激活。
- **关键技术细节**：
  - **Intra-layer Concept Preference Modeling (ICPM)**：
    - 对每个属性（包含多个概念），用文本编码器将属性内所有概念拼接得到全局属性特征 \(T_i\)。
    - 对每一视觉层 ℓ，计算其类别令牌 \(v^{cls}_\ell\) 与各 \(T_i\) 的余弦相似度，经Sigmoid和带可学习温度 \(\tau_1\) 的Softmax归一化，得到偏好值 \(p_{\ell,i}\)，表示层 ℓ 对属性 i 的偏好程度。
  - **Multi-layer Concept Sparse Activation Fusion (MCSAF)**：
    - 对每层 ℓ 的补丁令牌进行自适应平均池化，得到与属性 i 相关的局部特征 \(v^{pool}_{\ell,i}\)。
    - 计算每个概念 j 在层 ℓ 的激活得分 \(s_{(i,j),\ell} = p_{\ell,i} \cdot \cos(v^{pool}_{\ell,i}, t_j^i)\)。
    - 通过可学习参数 \(\tau_2\) 和自适应阈值 \(\theta_\ell\) 生成硬掩码，得到稀疏权重 \(w^{sparse}_{(i,j),\ell}\)，仅保留最相关的层。
    - 跨层加权求和得到最终概念激活 \(s^{agg}_{(i,j)}\)。
  - **损失函数**：\(\mathcal{L} = \mathcal{L}_{ce}(y,\hat{y}) + \lambda_1 \mathcal{L}_{ce}(y_c, s_c) + \lambda_2 \mathcal{L}_{sparse}\)，其中 \(\mathcal{L}_{sparse}\) 约束激活层数稀疏。
- **公式/算法流程**：见论文公式(6)-(18)，语言描述如上。

### 3. 实验设计

- **数据集**：7个公开医学数据集 —— ISIC2018（皮肤病变）、NCT-CRC-HE（结直肠组织）、IDRiD（糖尿病视网膜病变）、BUSI（乳腺超声）、CMMD（乳腺X线）、Cardiomegaly（胸部X线）、SIIM-ACR Pneumothorax（气胸X线）。
- **基准**：对比三类方法：
  - 零样本模型：CLIP、MedCLIP、BiomedCLIP；
  - 黑盒模型：ResNet50、ViT-Base；
  - 可解释模型：LaBo、PCBM、Explicd（当时SOTA CBM方法）。
- **指标**：平衡准确率（BMAC）和准确率（ACC）。

### 4. 资源与算力

- 论文在“Implementation Details”中提及：使用PyTorch，**单张Nvidia 4090 GPU**。未明确说明训练时长、总GPU数量或分布式设置，因此无法量化总计算开销。

### 5. 实验数量与充分性

- **主实验**：在7个数据集上各运行5次取均值标准差，对比9种方法（含本文），结果全面。
- **消融实验**：在ISIC2018上进行了10组消融（表3），逐一验证ICPM、概念损失、稀疏损失、替代模块（Q-former、软掩码、LAWF、MHAM）以及超参数 \(\tau_1, \tau_2\) 的作用。
- **定性分析**：概念偏好可视化（图4）、稀疏激活对比（图5）、可解释性案例（图6）。
- **充分性评价**：实验较为充分，覆盖多种模态（皮肤镜、组织病理、眼底、超声、X线），消融设计合理。但消融仅在一个数据集上执行，未在其他6个数据集上重复验证模块泛化性；未进行统计显著性检验（如t检验）。

### 6. 论文的主要结论与发现

- MVP-CBM在全部7个数据集上的BMAC和ACC均达到**最优或接近最优**，显著优于现有CBM方法及黑盒模型。
- 概念偏好可视化证实：不同概念在不同视觉层的激活强度存在明显差异，且最后一层并非总是最优。
- 稀疏激活机制有效去除了冗余噪声，使模型聚焦于最关键的概念。
- 可解释性案例显示：MVP-CBM能正确突出与真实诊断一致的概念，而对比方法Explicd有时错误聚焦。

### 7. 优点

- **创新性**：首次发现并系统利用CBM中的概念偏好变化问题，提出两模块解决方案。
- **性能领先**：在7个数据集上全面超越SOTA，同时提升准确率和可解释性。
- **自动概念生成**：利用LLM（GPT-o1）生成诊断概念，减少人工标注成本。
- **设计巧妙**：稀疏激活机制既降低层间冗余，又增强了表示的简洁性和可解释性。
- **实验充分**：多数据集、多基线、多消融分支，结果可信。

### 8. 不足与局限

- **消融覆盖不全面**：仅在一个数据集（ISIC2018）上验证各模块贡献，其他数据集上的泛化性未确认。
- **计算开销**：需要提取并处理所有中间层特征，相比单层CBM增加了内存和计算负担。
- **阈值自适应稳定性**：稀疏阈值 \(\theta_\ell\) 依赖层内权重范围，若分布极端可能使硬掩码不稳定。
- **概念质量依赖**：生成的诊断概念可能不完整或含偏见，未系统评估概念集合的覆盖度和医学准确性。
- **对比方法**：未与最新的概念发现/编辑方法（如ConceptSHAP）对比。
- **统计检验缺失**：未报告方差分析或显著性检验，难以判断提升是否统计显著。
- **数据集规模**：部分数据集较小（如BUSI仅780张），结果可能受随机波动影响。

（完）
