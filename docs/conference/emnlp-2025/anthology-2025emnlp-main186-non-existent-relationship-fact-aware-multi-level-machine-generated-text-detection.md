---
title: "Non-Existent Relationship: Fact-Aware Multi-Level Machine-Generated Text Detection"
title_zh: 不存在的关系：基于事实感知的多层级机器生成文本检测
authors: "Yang Wu, Ruijia Wang, Jie Wu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.186.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 基于事实感知的机器生成文本检测
tldr: 该论文针对机器生成文本检测中实体关系不一致的问题，提出了一种事实感知模型。模型通过图比较评估文本实体图与事实实体图之间的差异，并采用带门控单元的分层特征提取来全面分析上下文。该方法有效利用了LLM的幻觉特性进行伪造文本检测，为伪造检测提供了一种可解释的途径。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.186/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.186/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 717, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.186/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1646, \"height\": 976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.186/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.186/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 743, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.186/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1412, \"height\": 742, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.186/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.186/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 792, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.186/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.186/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.186/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 768, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.186/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 767, \"height\": 267, \"label\": \"Table\"}]"
motivation: 现有方法未充分利用实体图真实性这一关键判别特征，导致机器生成文本检测不准确。
method: 提出事实感知模型，通过比较文本实体图与事实实体图的差异，并使用分层门控特征提取。
result: 实验表明该方法能有效识别机器生成文本，尤其是利用事实不一致性。
conclusion: 利用事实知识图谱的实体关系不一致性可提升伪造文本检测的鲁棒性。
---

## Abstract
Machine-generated text detection is critical for preventing misuse of large language models (LLMs). Although LLMs have recently excelled at mimicking human writing styles, they still suffer from factual hallucinations manifested as entity-relation inconsistencies with real-world knowledge. Current detection methods inadequately address the authenticity of the entity graph, which is a key discriminative feature for identifying machine-generated content. To bridge this gap, we propose a fact-aware model that assesses discrepancies between textual and factual entity graphs through graph comparison. In order to holistically analyze context information, our approach employs hierarchical feature extraction with gating units, enabling the adaptive fusion of multi-grained features from entity, sentence, and document levels. Experimental results on three public datasets demonstrate that our approach outperforms the state-of-the-art methods. Interpretability analysis shows that our model can capture the differences in entity graphs between machine-generated and human-written texts.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：大语言模型（LLM）生成文本日益逼真，易被滥用于伪造新闻、垃圾信息、学术抄袭等。现有机器生成文本检测方法主要依赖统计特征、微调Transformer模型或捕捉上下文实体一致性。然而，这些方法存在两个局限：(1) 未充分利用**事实性**——人类文本中的实体关系通常与真实世界知识一致，而机器文本常因事实幻觉而产生不存在的实体关系；(2) 未充分处理**完整性**——LLM输入长度限制导致长文本信息丢失。
- **核心问题**：如何通过判别文本中实体关系与真实世界知识的一致性，提高机器生成文本检测的准确性和可解释性。
- **研究含义**：该问题不仅关乎检测性能，更揭示了LLM事实幻觉的本质，为未来可解释的文本检测提供了新视角。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：构建文本实体图与事实实体图，通过图比较获取事实感知的实体差异特征，再通过分层门控机制融合多粒度特征（实体、句子、文档级），最终判断文本来源。
- **关键技术细节**：
  - **特征提取模块**：
    - **文档与句子表示**：使用预训练RoBERTa提取文档CLS特征和句子初始特征矩阵。
    - **实体图构建**：利用REBEL模型提取文档中的三元组（主语、关系、宾语），构建**文本实体图**；将实体通过TAGME链接到Wikipedia，查询是否存在真实关系，构建**事实实体图**。两个图共享相同节点集，但边集不同。
    - **实体表示**：使用两层图卷积网络（GCN）分别编码文本图和事实图，初始节点嵌入采用预训练Word2Vec。
  - **特征融合模块**：
    - **实体比较**：计算文本与事实实体特征之差，并通过最大池化得到全局差异向量 \( h_{diff} \)（公式3-4）。
    - **实体到句子融合**：对每个句子中的实体特征进行平均池化，再利用门控单元与句子初始特征融合（公式5-7）。
    - **句子到文档融合**：将句子表示通过Transformer编码器更新（多头自注意力+FFN），再进行最大池化得到句子级表示；最后用门控单元与文档CLS特征融合（公式8-12）。
    - **预测**：拼接文档融合特征 \( h_D \) 与实体差异特征 \( h_{diff} \)，经全连接层和softmax输出二分类概率（公式13）。损失函数为交叉熵。

### 3. 实验设计：数据集、Benchmark、对比方法

- **数据集**：
  - **GROVER**：新闻风格，人类文本来自RealNews，机器文本由Grover-Mega生成；训练10,000，验证3,000，测试8,000。
  - **GPT-2**：WebText风格，人类文本来自WebText，机器文本由GPT-2 XLM-1542M生成；训练50,000，验证10,000，测试10,000。
  - **SemEval**：多源多模型，人类文本来自Wikipedia、Wikihow、Reddit，机器文本由davinci-003、ChatGPT、Cohere、Dolly-v2、BLOOMz、GPT-4生成；训练12,000，验证3,000，测试6,000。
- **Benchmark与对比方法**：分为三类——**统计方法**（GLTR、DetectGPT）、**知识方法**（CompareNet）、**Transformer方法**（XLNet、GPT-2、RoBERTa、FAST、COCO、USTC-BUPT）。评价指标为ACC和F1。

### 4. 资源与算力

- **文中明确说明**：模型在单张NVIDIA A100 GPU上训练与测试。使用AdamW优化器，学习率1e-5，batch size 16，最大训练30个epoch（早停）。总训练时间：GROVER约2.8小时，GPT-2约14.4小时，SemEval约2.4小时。未提及使用的GPU数量或型号细节（具体版本）。

### 5. 实验数量与充分性

- **实验组数**：主要包括三组主实验（三个数据集）；消融实验（5种变体：D、DF、DS、DSE、DSEF）；融合单元对比（门控、拼接、Add&Norm）；案例研究（可视化实体比较特征）。此外在附录中还有GCN与GAT对比、RoBERTa Base vs Large等补充实验。
- **充分性与公平性**：实验覆盖了多种主流baseline（统计、知识、微调、图增强），且在所有数据集上使用一致的设置（如RoBERTa-Large、相同分类头）。消融实验验证了每个模块的贡献。案例研究提供了可解释性证据。实验设计较为全面、客观。

### 6. 论文的主要结论与发现

- FAML在GROVER、GPT-2、SemEval三个数据集上均超越所有baseline，ACC和F1指标最优（例如GROVER上ACC 0.9340，F1 0.9339）。
- 门控融合机制优于直接拼接或Add&Norm，能够自适应调节粒度特征。
- 实体比较特征（\( h_{diff} \)）是区分人类与机器文本的关键：机器文本中差异值更大，人类文本更接近于零（见图5-6）。
- 多级特征融合（实体→句子→文档）逐步提升性能，说明细粒度信息对检测有帮助。

### 7. 优点

- **创新性**：首次将真实世界实体关系（事实性）引入机器生成文本检测，利用LLM事实幻觉的固有弱点。
- **方法论**：图比较+分层门控融合设计巧妙，兼顾局部实体差异与全局上下文，可解释性强。
- **实验丰富**：在三个不同规模/领域的数据集上验证，消融、融合单元、案例分析均完整。
- **可解释性**：通过可视化实体比较特征直观展示模型依据。

### 8. 不足与局限

- **依赖外部工具**：实体关系提取（REBEL）和实体链接（TAGME）质量影响性能，错误实体或关系会干扰学习。未来需探索更鲁棒的提取方法。
- **知识库不完整**：Wikipedia API频率限制及DBpedia本地知识库覆盖有限，可能导致事实图构建不全。不过论文指出适当不完整可能增强泛化。
- **适用范围窄**：仅针对实体关系幻觉，无法检测逻辑不一致、数值错误等其他类型的伪造文本。
- **未来挑战**：随着LLM知识图谱辅助训练的进步，事实幻觉可能减少，从而降低该方法的基础有效性，需要持续调整策略。

（完）
