---
title: Feature-Level Insights into Artificial Text Detection with Sparse Autoencoders
title_zh: 基于稀疏自编码器的人工文本检测特征级洞察
authors: "Kristian Kuznetsov, Laida Kushnareva, Anton Razzhigaev, Polina Druzhinina, Anastasia Voznyuk, Irina Piontkovskaya, Evgeny Burnaev, Serguei Barannikov"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1321.pdf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 利用稀疏自编码器增强人工文本检测的可解释性，匹配伪造检测解释性
tldr: 为提升人工文本检测的可解释性，利用稀疏自编码器从Gemma-2-2B残差流中提取可解释且高效的特征，并通过引导和人工/LLM解读分析语义。实验表明该方法能有效识别与生成模型相关的特征，为理解文本检测提供深入洞察。该工作推动了可解释性在伪造检测中的应用。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1647, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1639, \"height\": 435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 952, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 782, \"height\": 628, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1610, \"height\": 986, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1614, \"height\": 1020, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1623, \"height\": 1076, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 778, \"height\": 1033, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1633, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1637, \"height\": 627, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1611, \"height\": 1008, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1321/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1643, \"height\": 1090, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 842, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 829, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1620, \"height\": 2431, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1647, \"height\": 541, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1653, \"height\": 540, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1673, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1650, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1620, \"height\": 2034, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1594, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1597, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1591, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1618, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1602, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1609, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1321/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1581, \"height\": 2244, \"label\": \"Table\"}]"
motivation: 现有文本检测方法缺乏可解释性，影响泛化。
method: 使用稀疏自编码器提取残差流特征，结合引导和解读分析。
result: 识别出可解释且高效的特征，揭示了检测机制。
conclusion: 可解释特征是提升文本检测泛化的关键。
---

## Abstract
Artificial Text Detection (ATD) is becoming increasingly important with the rise of advanced Large Language Models (LLMs). Despite numerous efforts, no single algorithm performs consistently well across different types of unseen text or guarantees effective generalization to new LLMs. Interpretability plays a crucial role in achieving this goal. In this study, we enhance ATD interpretability by using Sparse Autoencoders (SAE) to extract features from Gemma-2-2B’s residual stream. We identify both interpretable and efficient features, analyzing their semantics and relevance through domain- and model-specific statistics, a steering approach, and manual or LLM-based interpretation of obtained features. Our methods offer valuable insights into how texts from various models differ from human-written content. We show that modern LLMs have a distinct writing style, especially in information-dense domains, even though they can produce human-like outputs with personalized prompts. The code for this paper is available at https://github.com/pyashy/SAE_ATD.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 1. 核心问题与整体含义（研究动机和背景）
- **问题**：随着大语言模型（LLM）的广泛应用，人工文本检测（ATD）变得日益重要，但现有方法缺乏可解释性，难以泛化到未见过的文本类型或新模型。
- **目标**：通过引入稀疏自编码器（Sparse Autoencoder, SAE）提取可解释特征，增强ATD的可解释性，揭示人类与AI生成文本的本质差异，并提升检测器的泛化能力。

### 2. 方法论
#### 核心思想
- 利用SAE从Gemma-2-2B模型的残差流中分解出稀疏、单义的潜在特征，从而将复杂激活转化为可解释的“特征”，并通过这些特征进行人工文本检测与语义分析。

#### 关键技术细节
- **SAE提取特征**：使用预训练的Gemma-Scope SAE（16k个潜在特征），对每个偶数层的残差流激活提取特征向量 `f(x) = σ(W_enc x + b_enc)`，并对文本所有token的特征进行求和，得到文本级特征向量 `f = Σ_i f^{(l)}(x_i^{(l)})`。
- **分类器**：
  - 采用XGBoost对所有SAE特征进行训练，评估特征集的整体表现，并筛选重要特征。
  - 对单个特征使用阈值分类器（`I[f_j > τ]`），通过逻辑回归确定最优阈值 `τ*`，并与零阈值（`I0`，即特征是否激活）对比。
- **特征解读方法**：
  - **手动分析**：查看高激活文本样本。
  - **特征引导（Steering）**：通过修改隐藏状态 `x' = x + λ A_max d_i`，观察生成文本的变化，并由GPT-4o自动分析语义影响。
  - **自动解释**：利用GPT-4o对引导结果进行结构化描述。

#### 公式或算法流程（文字说明）
1. 从Gemma-2-2B的偶数层提取残差激活 `x^{(l)}`。
2. 通过SAE编码器得到稀疏特征向量 `f^{(l)}(x_i)`，对文本所有token求和得 `f`。
3. 使用XGBoost训练二分类器（人类 vs AI生成）。
4. 针对每个重要特征，训练单特征阈值分类器，并分析其跨域/跨模型表现。
5. 通过引导实验观察特征增减对生成文本风格和内容的影响，结合GPT-4o进行语义标注。

### 3. 实验设计
#### 数据集
- **主数据集**：COLING 2025 GenAI Content Detection Task 1数据集（简称COLING），包含多种模型（如GPT-4o、LLaMA-3、OPT、Bloom等）的生成文本，覆盖金融、医学、Reddit等多个领域。
- **鲁棒性数据集**：RAID数据集，包含GPT-4、ChatGPT等模型的生成文本，并施加多种攻击（如拼写错误、同形字、改写、空格插入等）。

#### Benchmark
- 对比方法：XGBoost在**平均池化激活**上的表现；与先前SOTA方法（MTL模型）比较（第16层SAE特征超越MTL）。
- 额外对比：在LLaMA-3.1-8B（LLaMA Scope）和Pythia-160M-deduped上训练的SAE特征。

#### 对比方法
- 自身对照：不同层、不同特征组合、不同阈值策略（`Iτ*` vs `I0`）。
- 跨域/跨模型交叉验证：在某一域/模型上训练，在其他域/模型上测试。

### 4. 资源与算力
- **未明确说明**：论文未提及使用的GPU型号、数量、训练时长等具体算力信息。仅公开了代码仓库。

### 5. 实验数量与充分性
- **实验数量**：较为丰富，包括：
  - 全部偶数层（2-20层）的XGBoost对比实验（图2）。
  - 单特征阈值分类器跨域/跨模型性能（图3-4，图8-10，表5-7）。
  - 特征对长度、句法异常、攻击的敏感性分析（表2，表4）。
  - 零阈值与最优阈值对比（表7）。
  - 三个不同SAE架构（Gemma、LLaMA、Pythia）的对比（图11）。
  - 特征引导实验及GPT-4o解读（表8-12）。
- **充分性评价**：实验设计较为系统，覆盖了域内、跨域、跨模型、鲁棒性等多个维度。但缺乏对更多攻击类型和未来新模型的验证，且仅基于Gemma-2-2B一个基础模型。

### 6. 主要结论与发现
- **通用特征**：如特征3608（过度复杂句法）、4645（断言性陈述）、6587（冗长开头）等，能在多个域和模型上有效检测AI文本，尤其对GPT-3.5+、LLaMA、Gemma等现代LLM效果显著。
- **模型特定特征**：如特征8689（过度同义词替换）专门检测GPT系列；特征8264（概念重复）检测GPT-4o。
- **域特定特征**：如特征12390（复杂句法）用于arXiv；特征1416（丢失数学公式）用于WikiHow；特征14953（形式化语气）用于医学等。
- **检测难度**：当模型使用非正式、个性化提示时（如Yelp评论、Outfoxessay），AI文本更难检测。信息密集域（金融、医学）更容易检测。
- **SAE对分类的帮助**：SAE特征比原始平均池化激活表现更好，说明解耦叠加效应后，分类器能关注更本质的特征。

### 7. 优点
- **创新性**：首次系统地将SAE用于ATD可解释性分析，提供了特征级细粒度洞察。
- **方法论全面**：结合XGBoost、阈值分类、特征引导、手动/自动解读，形成完整分析框架。
- **跨域/跨模型评估**：在多样化数据集上验证通用性与特异性，结果可信度高。
- **开源代码**：促进可复现研究和后续工作。

### 8. 不足与局限
- **模型单一**：仅使用Gemma-2-2B作为基础模型（SAE也基于该模型），其他SAE探索较浅（LLaMA/Pythia仅进行简单实验）。
- **特征可解释性不完整**：部分SAE特征仍难以解读，可能存在多语义或特征吸收现象。
- **数据集偏差**：COLING数据集中存在一些浅层伪影（如异常标点、长度差异），可能影响特征真实性的判断（尽管论文进行了分析）。
- **攻击覆盖有限**：仅测试了RAID中部分攻击，未覆盖未来可能出现的新对抗策略。
- **算力信息缺失**：未报告计算资源，不利于复现成本评估。

（完）
