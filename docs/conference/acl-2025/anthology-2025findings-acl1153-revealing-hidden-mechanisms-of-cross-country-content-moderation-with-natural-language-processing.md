---
title: Revealing Hidden Mechanisms of Cross-Country Content Moderation with Natural Language Processing
title_zh: 利用自然语言处理揭示跨国内容审核的隐藏机制
authors: "Neemesh Yadav, Jiarui Liu, Francesco Ortu, Roya Ensafi, Zhijing Jin, Rada Mihalcea"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1153.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 使用Shapley值和LLM解释进行虚假检测的可解释性
tldr: 本文研究了内容审核决策中的隐藏机制，通过训练分类器逆向工程各国审核决策，并利用Shapley值和LLM生成解释来分析决策原因。主要贡献在于揭示了NLP方法在虚假新闻检测等任务中的可解释性，为跨国家的内容审核提供了透明性。该方法可直接应用于虚假检测的可解释性需求，提升了模型决策的透明度。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1153/fig-001.webp\", \"caption\": \"\", \"page\": 18, \"index\": 1, \"width\": 6040, \"height\": 3020}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1153/fig-002.webp\", \"caption\": \"\", \"page\": 18, \"index\": 2, \"width\": 6040, \"height\": 3020}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1153/fig-003.webp\", \"caption\": \"\", \"page\": 18, \"index\": 3, \"width\": 6040, \"height\": 3020}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1153/fig-004.webp\", \"caption\": \"\", \"page\": 18, \"index\": 4, \"width\": 6040, \"height\": 3020}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1153/fig-005.webp\", \"caption\": \"\", \"page\": 18, \"index\": 5, \"width\": 6040, \"height\": 3020}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1153/fig-006.webp\", \"caption\": \"\", \"page\": 18, \"index\": 6, \"width\": 6040, \"height\": 3020}]"
motivation: 当前内容审核方法缺乏可解释性，难以理解审核决策背后的原因。本文旨在通过NLP揭示跨国家内容审核的隐藏机制。
method: 训练分类器逆向工程审核决策，并利用Shapley值和LLM引导的解释来分析决策原因。
result: 实验结果表明该方法能够有效解释内容审核决策，提供了模型可解释性。
conclusion: 通过可解释性分析，增进了对内容审核机制的理解，为虚假检测等任务提供了透明化方法。
---

## Abstract
The ability of Natural Language Processing (NLP) methods to categorize text into multiple classes has motivated their use in online content moderation tasks, such as hate speech and fake news detection. However, there is limited understanding of how or why these methods make such decisions, or why certain content is moderated in the first place. To investigate the hidden mechanisms behind content moderation, we explore multiple directions: 1) training classifiers to reverse-engineer content moderation decisions across countries; 2) explaining content moderation decisions by analyzing Shapley values and LLM-guided explanations. Our primary focus is on content moderation decisions made across countries, using pre-existing corpora sampled from the Twitter Stream Grab. Our experiments reveal interesting patterns in censored posts, both across countries and over time. Through human evaluations of LLM-generated explanations across three LLMs, we assess the effectiveness of using LLMs in content moderation. Finally, we discuss potential future directions, as well as the limitations and ethical considerations of this work.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在线内容审核（如仇恨言论、虚假新闻检测）中，NLP 模型虽然被广泛使用，但其决策机制不透明，人们难以理解为什么某些内容被审核、模型如何做出判断。同时，不同国家的审核策略存在差异，缺乏系统性分析。
- **研究动机**：现有工作主要关注提升审核技术本身，很少系统分析审核决策背后的原因。作者希望像“调查记者”一样，利用 LLM 逆向工程并解释跨国的内容审核模式，揭示隐藏机制。
- **整体含义**：通过对五个国家（德国、法国、印度、土耳其、俄罗斯）2011–2020 年间 Twitter 被审查帖子的研究，本文首次大规模使用 LLM 进行跨国、跨时间的内容审核模式分析与解释，为提升审核透明度和可解释性提供了新视角。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将 LLM 作为自动调查工具，从两个层面分析内容审核：
  1. **逆向工程审核决策**（RQ1）：训练分类器预测一条帖子是否被审查，并归类到六种审查类型（政治、宗教、有害、企业、军事、其他）。
  2. **解释审核决策**（RQ2）：使用 Shapley 值找出对预测最重要的实体/词汇，并利用 LLM 生成可读的解释。

- **关键技术细节**：
  - **分类器训练**：使用多种编码器语言模型（BERT-Tiny, BERT Base, m-BERT, XLM-RoBERTa, RoBERTa Base）和小型解码器 LLM（Pythia 1B, Llama 3.2 1B）进行多标签分类（一条帖子可能被多个国家审查）。对比零样本设置下的大模型（Aya-23-8B, Llama-3.1-8B-Instruct, GPT-4o-mini, GPT-4o）。
  - **Shapley 值解释**：对最佳模型（Pythia 1B）计算每个 token 的 Shapley 值，识别每个国家最关键的实体。
  - **LLM 引导的解释**：提示 GPT-4o-mini 等 LLM 生成“为什么该帖子应该被审核”的推理，并进行人工评估。

- **公式/算法流程**（文字说明）：
  - 预处理：从 Twitter API 获取帖子文本及 `withheld_in_countries` 属性作为标签。
  - 训练：将帖子输入编码器/解码器模型，输出多标签分类（各国是否被审查）。损失函数为二分类交叉熵，训练 1 个 epoch。
  - 可解释性：使用 SHAP 库，对测试集每条帖子计算 token 贡献，汇总得到国家层面的重要实体；同时用 LLM 生成自然语言解释。

## 3. 实验设计：数据集、benchmark、对比方法

- **数据集**：
  - 来自 Twitter Stream Grab（1% 抽样）的帖子，时间跨度 2011–2020 年，仅包含英文帖子。
  - 原始数据来自 Elmas et al. (2021)，但本文重新通过 Twitter API 获取内容（因原数据仅提供 ID）。
  - 每个国家最多采样 500 条测试样本（共 5 国），确保类别平衡。训练集和验证集按原始分布划分（约为 80% 训练、12% 验证、8% 测试）。
- **六种审查类别**：政治、宗教、有害、企业、军事、其他。使用 GPT-4o-mini 自动标注，经人工抽样评估准确率接近完美（表 3，平均 92%）。

- **Benchmark**：无标准基准，本文构建了跨国家的内容审核预测任务。对比了多个预训练语言模型（表 4、5）。

- **对比方法**：
  - 小模型（微调）：BERT-Tiny, BERT Base, XLM-R, m-BERT, RoBERTa Base, Pythia 1B, Llama 3.2 1B。
  - 大模型（零样本）：Aya-23-8B, Llama-3.1-8B-Instruct, GPT-4o-mini, GPT-4o。

## 4. 资源与算力

- 论文明确提到实验在 **NVIDIA H100 和 A100 集群**上运行，使用 Huggingface Transformers 库。
- 训练细节：1 个 epoch，学习率 1e-5，dropout 0.1，batch size 8。
- 未说明具体的 GPU 数量、总训练时长或总计算量。对于 GPT-4o-mini/GPT-4o 的 API 调用，仅提及“因成本限制对每国只采样 500 条”。

## 5. 实验数量与充分性

- **实验数量**：
  - **逆向工程**：7 个微调模型 × 5 个国家（含聚合结果），以及 4 个零样本 LLM 的对比。
  - **类别分布分析**：对六类审查类型的分布和误分类模式进行了可视化（图 1）。
  - **Shapley 解释**：为每个国家生成了 top-20 重要实体图（图 5），并结合时间序列分析（图 2）和 t-SNE 可视化（图 3）。
  - **LLM 解释评估**：对 3 个 LLM（Aya-23, Llama-3.1, GPT-4o-mini），每个国家 15 个样本，共 45 个样本/国家 × 5 国 = 225 条解释，由 5 名专家按偏好、流畅度、有用性进行 5 分制评价，每份样本双人标注。

- **充分性评价**：
  - **优点**：实验覆盖了不同规模、不同语言的模型；进行了零样本和微调对比；评估了可解释性（Shapley + LLM 解释）并做了人工验证；还分析了时间趋势和事件关联。
  - **不足**：
    - 样本量相对较小（每国最多 500 条测试样本，尤其是印度和俄罗斯仅约 2% 的原始数据）。
    - 未进行严格的消融实验（如去掉某个模型组件的影响）。
    - 人工评估仅针对 15 条/国家/LLM，样本量有限，且未提及标注者间一致性指标（如 Cohen's Kappa）。
    - 未与更传统的可解释性方法（如 LIME）对比。

## 6. 论文的主要结论与发现

- **主要结论**：
  1. **审核决策可预测**：微调后的 Pythia 1B 等小型 LLM 能高精度（加权 F1 约 93%）逆向工程审核决策；但零样本大模型（GPT-4o 等）仅达约 50%，说明任务具有挑战性。
  2. **审核模式因国而异**：德国和法国相似（有害内容审查为主），印度和土耳其相似（政治审查为主），俄罗斯企业审查和“其他”类别较多。
  3. **时间模式与重大事件对齐**：Shapley 值提取的关键实体（如 Kavanaugh 听证会、After Daesh 等）与现实社会事件吻合；独特 token 数量随时间变化与各国政治/社会事件高峰一致。
  4. **LLM 能生成有用解释但不够完美**：人工评估显示，Aya-23 的解释最受偏好，但所有 LLM 的有用性平均分约为 3.6/5，说明仍需改进。LLM 在需深层地域知识时（如印度“MSG”相关实体）容易误判。
  5. **不同 LLM 的审核行为存在差异**（伦理讨论部分）：DeepSeek R1 和 GPT-4o-mini 在敏感提示测试中拒绝率不同，表明模型内置的审核策略受公司/训练数据影响。

## 7. 优点

- **问题新颖**：首次系统性地将可解释 AI（Shapley 值）与 LLM 结合，用于跨国、跨时间的内容审核分析，类似于自动调查记者。
- **方法论全面**：从预测（逆向工程）到解释（特征重要性 + 自然语言解释），完整覆盖了“是什么”和“为什么”。
- **人工验证**：对 LLM 生成的解释进行了双人标注、多维度评估，增加了结果的可信度。
- **伦理讨论深入**：特别讨论了 LLM 自身的审核偏见和数据隐私问题，并进行了实验对比（DeepSeek vs GPT），体现了对负责任研究的思考。
- **代码与数据开源**：提供了 GitHub 仓库，促进可复现性。

## 8. 不足与局限

- **数据方面**：
  - 仅使用英文帖子，可能无法反映多语言国家（如土耳其、印度、俄罗斯）的本地话语模式。
  - 数据集仅为 Twitter 1% 抽样，且因为 API 限制和用户删除，印度和俄罗斯样本极少（各约 2%），可能导致分析偏差。
  - 时间范围截至 2020 年，无法捕捉近期（如 2020 年后）的审核策略变化。

- **模型方面**：
  - 所有模型（包括 LLM）受训练数据影响，可能隐含文化或政治偏见。
  - Shapley 值解释只基于一个最佳模型（Pythia 1B），未验证不同模型下解释的稳定性。
  - 未与更简单的基线（如词频分析、规则方法）对比解释质量。

- **实验覆盖**：
  - 消融实验不足，未分析不同训练数据量、不同 epoch 的影响。
  - 人工评估样本量小（每国 15 条/LLM），且未报告标注者间一致性，可能影响可靠性。

- **应用限制**：
  - 研究本质是“调查性”而非“部署性”，结论不能直接用于实时审核系统。
  - 模型可能错误地将提及（mention）误判为使用（use），导致误伤正常讨论。
  - 伦理风险：可能被滥用于大规模监控或压制言论自由，作者已明确反对。

（完）
