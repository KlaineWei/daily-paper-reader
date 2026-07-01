---
title: Can LLMs Find a Needle in a Haystack? A Look at Anomaly Detection Language Modeling
title_zh: 大语言模型能否在数据中找到异常？——基于异常检测语言模型的视角
authors: "Leslie Barrett, Vikram Sunil Bajaj, Robert John Kingan"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.341.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: LLMs用于异常检测，可扩展至可解释性
tldr: 该论文针对文本异常检测问题，提出了基于大型预训练语言模型的三模态方法。实验表明，LLM在将异常检测作为不平衡分类任务处理时击败了基线。尽管未明确涉及可解释性，但该方法为后续可解释异常检测研究提供了基础。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.341/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 366, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.341/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1663, \"height\": 600, \"label\": \"Table\"}]"
motivation: 现有的文本异常检测方法在预训练时间和领域适应性上存在不足。
method: 采用大型预训练语言模型，从三种模态进行异常检测。
result: 在多个数据集上，LLM方法在不平衡分类设定下优于现有基线。
conclusion: LLM可作为文本异常检测的有效工具，但可解释性有待进一步研究。
---

## Abstract
Anomaly detection (AD), also known as Outlier Detection, is a longstanding problem in machine learning, which has recently been applied to text data. In these datasets, a textual anomaly is a part of the text that does not fit the overall topic of the text. Some recent approaches to textual AD have used transformer models, achieving positive results but with trade-offs in pre-training time and inflexibility with respect to new domains. Others have used linear models which are fast and more flexible but not always competitive on certain datasets. We introduce a new approach based on Large Pre-trained Language Models in three modalities. Our findings indicate that LLMs beat baselines when AD is presented as an imbalanced classification problem regardless of the concentration of anomalous samples. However, their performance is markedly worse on unsupervised AD, suggesting that the concept of “anomaly” may somehow elude the LLM reasoning process.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
文本异常检测（Anomaly Detection, AD）旨在识别文档中与整体主题不符的文本片段（如主题入侵）。传统方法包括基于近邻的模型、非负矩阵分解（NMF）和 Transformer 等，但存在预训练时间长、领域迁移不灵活等问题。近年来大语言模型（LLM）在分类任务中表现出色，但在文本AD上的应用尚不充分，且对类别不平衡的鲁棒性存疑。本文研究 LLM 能否在文本异常检测中超越现有基线，并探索不同任务形式（有监督 vs 无标签）下 LLM 的性能差异。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：利用预训练 LLM 的直接推理能力，通过三种不同的提示策略（不进行微调）来检测文本异常。
- **三种模态（Modalities）**：
  - **Binary Outlier Detection（二值异常检测）**：给定主题列表（内类主题和异常类主题），零样本提示模型输出“内类”或“异常”标签。
  - **Multi-class Topic Detection（多类主题检测）**：给定所有可能的主题标签（不区分内/异常），通过少量示例（few-shot）让模型直接预测文本所属主题，再根据真实主题判断是否为异常。
  - **Unlabeled Outlier Discovery（无标签异常发现）**：将所有文本混合（保持原有异常浓度），零样本提示模型直接从列表中识别出“不属于整体”的句子，不提供任何主题先验。
- **提示与输出**：所有提示要求模型输出 JSON 格式（包含分类、推理等），温度参数设置为 0.1（GPT-4o/Claude 3.5 Sonnet）或 1（o1-preview），采用核采样（top_p 默认）。
- **未使用公式或复杂算法**：不涉及模型训练，完全依靠 LLM 的已有能力进行推理。

### 3. 实验设计：数据集、场景、benchmark、对比方法
- **数据集**：
  - **20Newsgroups**：新闻组邮件，选取 pc/mac 硬件为内类，comp.os 或 comp.windows.x 为异常类。
  - **Reuters-21578**：路透社新闻，内类为 earn+acq，异常类为 interest 或 trade。
  - **WikiPeople**：维基百科人物传记，内类为“Life”段落，异常类为“Career”段落。
- **异常浓度**：0.01、0.025、0.05（基于稀有事件分析），共构成 12 个数据配置（如表2所示）。
- **对比方法**：
  - 非 LLM 基线：**DATE**（基于 Transformer 的自监督方法，SOTA）；**R-NMF**（基于非负矩阵分解的重构方法）。
  - LLM 模型：**GPT-4o**、**Claude 3.5 Sonnet**（用于所有模态）；**OpenAI o1-preview**（仅用于无标签模态）。
- **评价指标**：AUROC（Area Under ROC Curve），用于衡量排序能力。

### 4. 资源与算力
- **LLM 实验**：未提及具体 GPU 资源，推测通过 API 调用（不涉及本地训练）。温度、top_p 等超参数固定。
- **DATE 基线**：使用 2 个 Tesla V100 GPU（各 32GB RAM）和 6 个 CPU 核心，训练至收敛（平均 5000 步）。
- **R-NMF 基线**：使用 3 个 CPU 核心和 8GB RAM，进行超参数扫描（k 范围 [1,128]，α 范围 [1,16]）。

### 5. 实验数量与充分性
- **实验数量**：总共执行了 3 个 LLM（其中 o1 仅参与无标签模态）× 3 种模态 × 12 个数据配置 = 大约 96 个实验（不考虑重复）。每个基线也在所有 12 个配置上运行。结果汇总于表1。
- **充分性分析**：
  - **优点**：覆盖多种主题、多种领域（邮件、新闻、百科），并考虑了三种不同浓度的异常，实验设计较为系统。
  - **不足**：
    - 数据集规模较小（最大约 6000 样本），未在更大或更多样化的真实场景中验证。
    - 每个配置只运行单次，未报告方差（如多次采样），统计显著性未知。
    - 消融实验有限：未比较不同提示模板、不同温度或是否使用系统指令的差异。
    - 仅使用三个 LLM，且 o1 只参与一个模态，对比不够全面。
    - 未对 LLM 的推理错误进行深入分析（仅附录中给出少量例子）。

### 6. 论文的主要结论与发现
- **在二值异常检测和多类主题检测模态下**，GPT-4o 和 Claude 3.5 Sonnet 均超越基线（R-NMF 和 DATE），AUROC 多数达到 0.95 以上，且表现稳定。
- **在无标签异常发现模态下**，所有 LLM 表现极差，AUROC 普遍接近 0.5（随机猜测），甚至低于基线（如 GPT-4o 在多个数据集上精确率为 0）。模型倾向于关注句法、货币名称等非主题特征，无法理解“主题异常”的概念。
- **异常浓度**（0.01/0.025/0.05）对模型性能影响不显著，与以往研究（Zhang et al., 2024）认为 LLM 对不平衡数据敏感的观点不一致。
- **LLM 适合作为有监督（需提供内/异常主题）的文本异常分类器，但不适合无监督的开放性异常发现。

### 7. 优点：方法或实验设计上的亮点
- **创新性**：首次系统地在三种不同任务形式下评估 LLM 在文本异常检测中的能力，并与多种基线在同一基准上比较。
- **提示策略简单有效**：零样本/少样本提示，无需微调，即插即用，具有实际部署价值。
- **覆盖多个领域**：使用新闻、邮件、百科三种不同类型文本，增加了结论的泛化能力。
- **结果清晰揭示 LLM 的局限**：无标签模态的失败为后续研究指明了方向（如何让 LLM 理解“主题性”）。
- **附录提供了详细的提示模板和错误案例**，便于复现和理解。

### 8. 不足与局限
- **数据集规模小且局限**：仅使用三个公开数据集，且样本量有限（最大 6095 个），未在真实金融/工业日志等场景验证。
- **缺乏统计显著性分析**：未报告多次运行的均值和标准差，难以判断结果是否具有偶然性。
- **无标签模态的成功率几乎为零**，但论文未深入探究失败原因（如是否提示措辞不够明确、模型对“主题”的定义偏差等），仅推测为词汇频率偏差。
- **消融实验不足**：未对提示模板、温度参数、是否使用 CoT 等进行系统性消融，无法确定哪些因素影响性能。
- **算力资源不透明**：LLM 实验未描述调用 API 的具体成本和重复次数，可复现性受限。
- **伦理与局限性讨论简短**：仅提及分类错误可能导致用户被误封或不良内容漏检，未讨论更广泛的偏见或安全风险。

（完）
