---
title: "MoSEs: Uncertainty-Aware AI-Generated Text Detection via Mixture of Stylistics Experts with Conditional Thresholds"
title_zh: MoSEs：基于风格专家混合与条件阈值的AI生成文本不确定性检测
authors: "Junxi Wu, Jinpeng Wang, Zheng Liu, Bin Chen, Dongjian Hu, Hao Wu, Shu-Tao Xia"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.294.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: AI生成文本检测与不确定性量化
tldr: AI生成文本检测多忽视风格建模和静态阈值问题。MoSEs提出风格专家混合框架，包含风格库、路由器和条件阈值估计器，实现风格感知的不确定性量化，显著提升检测性能。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.294/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1572, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.294/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 801, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.294/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1591, \"height\": 978, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.294/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 776, \"height\": 501, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 702, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 700, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 781, \"height\": 566, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 997, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 815, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 696, \"height\": 430, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 967, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1637, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1020, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1475, \"height\": 629, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1603, \"height\": 887, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1613, \"height\": 294, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1586, \"height\": 1993, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1580, \"height\": 2342, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1584, \"height\": 2199, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1580, \"height\": 2352, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.294/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1582, \"height\": 1273, \"label\": \"Table\"}]"
motivation: 现有AI文本检测忽略风格建模且使用静态阈值，限制性能。
method: 提出风格专家混合框架，包含风格参考库、风格感知路由器和条件阈值估计器。
result: 在多个基准上优于现有方法。
conclusion: 风格感知和不确定性量化对AI文本检测至关重要。
---

## Abstract
The rapid advancement of large language models has intensified public concerns about the potential misuse. Therefore, it is important to build trustworthy AI-generated text detection systems. Existing methods neglect stylistic modeling and mostly rely on static thresholds, which greatly limits the detection performance. In this paper, we propose the Mixture of Stylistic Experts (MoSEs) framework that enables stylistics-aware uncertainty quantification through conditional threshold estimation. MoSEs contain three core components, namely, the Stylistics Reference Repository (SRR), the Stylistics-Aware Router (SAR), and the Conditional Threshold Estimator (CTE). For input text, SRR can activate the appropriate reference data in SRR and provide them to CTE. Subsequently, CTE jointly models the linguistic statistical properties and semantic features to dynamically determine the optimal threshold. With a discrimination score, MoSEs yields prediction labels with the corresponding confidence level. Our framework achieves an average improvement 11.34% in detection performance compared to baselines. More inspiringly, MoSEs shows a more evident improvement 39.15% in the low-resource case. Our code is available at https://github.com/creator-xi/MoSEs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：大型语言模型（LLM）的广泛应用引发了对AI生成文本滥用的担忧，急需可靠的检测系统。
- **现有问题**：当前方法忽略了对文本风格（如新闻、学术论文、评论等专业领域的写作习惯）的建模，且大多使用静态阈值进行决策，无法适应不同风格文本的分布差异，导致检测性能受限。
- **整体目标**：提出一种**风格感知且能进行不确定性量化**的AI文本检测框架，通过动态阈值估计提升检测的准确性和鲁棒性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将文本风格显式建模，通过**风格专家混合**方式，根据输入文本的语义特征动态选择合适的参考样本，并联合语言统计属性与语义特征**自适应估计最优分类阈值**，输出预测标签及置信度。
- **三个核心组件**：
  - **风格参考库（SRR）**：包含多种风格（新闻、故事、学术论文等）的已标注文本，每个样本附有二元标签（人类/AI）以及多维条件特征（如文本长度、log概率均值/方差、n-gram重复率、类型-符号比、深度语义嵌入）。
  - **风格感知路由器（SAR）**：基于预训练语言编码器（如BGE-M3）构建语义潜空间，对各风格样本进行**原型聚类**（使用Sinkhorn-Knopp算法求解最优运输问题）；输入新文本时，通过**m近邻原型检索**动态激活SRR中的相关参考样本组。
  - **条件阈值估计器（CTE）**：利用激活的参考样本，联合建模语言统计属性和降维后的语义特征（经PCA压缩至32维），训练一个分类器（逻辑回归或XGBoost）来学习从条件特征到最优阈值的映射。分类概率定义为 \( P(y=1|C,\tau) = \sigma(C\beta - \tau) \)，其中\(C\)为条件特征，\(\tau\)为判别得分。通过最小化加权负对数似然优化参数，并提供**理论误差分析**证明估计阈值具有渐近无偏性（误差服从零均值高斯分布）。

### 3. 实验设计：数据集、Benchmark与对比方法

- **数据集**：基于MAGE构建8个数据集，分为两类：
  - **主数据集**（各2000样本，1800参考+200测试）：CMV（辩论）、XSum（新闻）、WP（故事）、SciXGen（学术论文），由GPT-3.5 Turbo和LLaMA 65B生成。
  - **低资源数据集**（各400样本，200参考+200测试）：CNN/Daily Mail（新闻邮件）、DialogSum（对话）、IMDB（影评）、PubMedQA（生物医学问答），由GPT-4生成。
- **基准方法**：**静态阈值**（在参考集上最大化约登指数得到固定阈值）和**最近投票**（取输入文本判别得分最近的k=100个参考样本的多数标签）。
- **对比方法**：在**三种判别得分模型**（RoBERTa-base、Fast-DetectGPT、Lastde）上分别应用上述两种基准和本文提出的MoSEs-lr（CTE为逻辑回归）和MoSEs-xg（CTE为XGBoost）。
- **评估指标**：Accuracy和F1-score。

### 4. 资源与算力

- 论文明确提及计算硬件：**Intel Xeon(R) Gold 6226R CPU + NVIDIA GeForce RTX 3090 GPU**。
- 训练/推理时间（主数据集上）：
  - MoSEs-lr：训练0.18s，推理0.06ms。
  - MoSEs-xg：训练0.13s，推理1.04ms。
- 未说明使用的GPU数量及更细粒度的训练时长（如epoch数），仅给出了整体时序。

### 5. 实验数量与充分性

- **实验组数丰富**：包含4组主实验（3种得分模型×4个数据集）、4组低资源实验、消融实验（选择策略、SAR有无、条件特征逐项移除、PCA维度）、OOD实验（未见风格、未见LLM）、不同prompt生成方式实验，以及计算效率分析。
- **充分性评价**：实验覆盖了标准场景、低资源场景、域外泛化场景，消融逐个验证了各组件和特征的有效性，对比在同一判别模型上公平进行。McNemar检验表明改进显著（p值极小）。整体设计合理、全面，结论可信。

### 6. 论文的主要结论与发现

- MoSEs-xg在主数据集上平均Accuracy比静态阈值高**11.34%**，在低资源场景下提升达**39.15%**。
- 风格感知路由（SAR）和条件特征（尤其是文本长度、log概率均值、2-gram重复率、类型-符号比）均对性能有正向贡献。
- 基于XGBoost的CTE优于逻辑回归，能够捕捉非线性交互。
- 在未见风格和未见LLM的OOD测试中，MoSEs仍保持优势，说明具有良好的泛化能力。
- 计算效率方面，MoSEs-lr推理速度接近静态阈值，MoSEs-xg稍慢但远低于判别得分模型本身，可接受。

### 7. 优点：方法或实验设计上的亮点

- **创新性**：首次将专业写作风格（habitus）显式融入AI文本检测，提出原型聚类+动态检索机制避免预定义风格类别。
- **实用性**：条件阈值估计实现了自适应决策，附带置信度输出；低资源下性能突出，适合数据稀缺场景。
- **严谨性**：提供阈值估计的理论误差分析（渐近无偏性）；消融实验全面，逐特征验证重要性；OOD实验证明泛化能力。
- **开源可复现**：代码已公开。

### 8. 不足与局限

- **PCA压缩风险**：过度压缩可能丢失深层语义，保留过高维度又会引入噪声，需调参平衡。
- **推理速度**：MoSEs-xg推理时间（1.04ms）比静态阈值（0.02ms）慢一个数量级，在实时性要求极高的场景中可能受限。
- **二分类局限**：当前仅支持人类/AI二元检测，虽然论文指出可扩展至多源检测（如SeqXGPT、DART），但未实现验证。
- **特征冗余**：部分语言统计属性可能存在共线性，论文虽说明可由CTE自动学习权重，但未深入分析冗余对训练稳定性的影响。
- **低资源实验规模**：低资源数据集仅200参考样本，虽已显示优势，但未探索更极端情况（如<100样本）的表现。

（完）
