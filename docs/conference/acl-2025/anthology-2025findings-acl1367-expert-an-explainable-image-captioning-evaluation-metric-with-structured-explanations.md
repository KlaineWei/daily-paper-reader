---
title: "EXPERT: An Explainable Image Captioning Evaluation Metric with Structured Explanations"
title_zh: EXPERT：具有结构化解释的可解释图像描述评估指标
authors: "Hyunjong Kim, Sangyeop Kim, Jongheon Jeong, Yeongjae Cho, Sungzoon Cho"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1367.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 图像描述的可解释评估指标
tldr: 针对现有图像描述评估指标缺乏可解释性的问题，本文提出EXPERT，一种无参考的可解释评估指标。它基于流畅性、相关性和描述性三个标准提供结构化解释。通过构建高质量解释数据集和两阶段评估模板，EXPERT在评分和解释生成上均达到最优。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1620, \"height\": 863, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 370, \"height\": 235, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 368, \"height\": 260, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 796, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 344, \"height\": 200, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1393, \"height\": 769, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 345, \"height\": 241, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 348, \"height\": 228, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 349, \"height\": 263, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 346, \"height\": 266, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 220, \"height\": 262, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1367/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 221, \"height\": 264, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 600, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 1000, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1655, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1653, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1653, \"height\": 228, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 555, \"height\": 448, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 569, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1367/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 799, \"height\": 463, \"label\": \"Table\"}]"
motivation: 现有图像描述评估指标生成解释时缺乏标准化标准，且解释质量未验证。
method: 提出基于三大标准的无参考可解释评估指标，构建解释数据集并设计两阶段评估模板。
result: EXPERT在评分和解释生成上均达到最先进水平。
conclusion: 该指标为图像描述评估提供了可解释的参考。
---

## Abstract
Recent advances in large language models and vision-language models have led to growing interest in explainable evaluation metrics for image captioning. However, these metrics generate explanations without standardized criteria, and the overall quality of the generated explanations remains unverified. In this paper, we propose EXPERT, a reference-free evaluation metric that provides structured explanations based on three fundamental criteria: fluency, relevance, and descriptiveness. By constructing large-scale datasets of high-quality structured explanations, we develop a two-stage evaluation template to effectively supervise a vision-language model for both scoring and explanation generation. EXPERT achieves state-of-the-art results on benchmark datasets while providing significantly higher-quality explanations than existing metrics, as validated through comprehensive human evaluation. Our code and datasets are available at https://github.com/hjkim811/EXPERT.

---

## 论文详细总结（自动生成）

# 论文总结：EXPERT：具有结构化解释的可解释图像描述评估指标

## 1. 核心问题与研究动机（背景）
- **问题**：现有图像描述评估指标在提供可解释性时，缺乏标准化标准，导致解释内容与结构不一致；同时，以往工作未对生成的解释质量进行系统验证。
- **动机**：随着大语言模型和视觉-语言模型的发展，对可解释评估指标需求增加，但现有方法（如FLEUR）生成的解释随意且质量未经检验。作者希望提出一种**无参考、可解释**的评估指标，提供基于三个基本准则（流畅性、相关性、描述性）的结构化解释，并严格验证解释质量。

## 2. 方法论
- **核心思想**：基于视觉-语言模型，通过构建大规模结构化解释数据集和两阶段评估模板，同时实现准确的评分和高质量的解释生成。
- **关键技术细节**：
  - **解释数据集构建**：在现有Polaris和Nebula人类评分数据集基础上，使用GPT-4o为每个图像-描述对生成符合三准则（流畅性、相关性、描述性）的结构化解释，得到Polaris-exp（16,014条）和Nebula-exp（26,152条）。通过4名母语者人类评估验证数据集质量（一致性3.72/4，事实性3.84/4，信息性3.72/4）。
  - **两阶段评估模板**：
    - **第一阶段（评分）**：提示模型对图像-描述对输出0.0~1.0的分数。采用**分数分箱**（score binning，bin size=0.10）将评分简化，提升学习效率。
    - **第二阶段（解释）**：提示模型基于三个准则提供结构化解释，附带准则描述和输出格式。
  - **监督微调（SFT）**：以LLaVA-1.5（13B）为基座模型，将合并后的训练集转换为两阶段模板进行微调。使用LoRA（r=128, alpha=256），学习率2e-5，余弦调度，批次8，1 epoch。
  - **推理**：使用贪心解码保证确定性；应用**分数平滑**（score smoothing）：对每个小数位计算数字0~9的概率加权和，得到更精细的分数 \( s = \sum_{j=1}^{2} 10^{-j} \sum_{i=0}^{9} i \times p(i,j) \)。

## 3. 实验设计
- **数据集与基准**：
  - **评分评估**：Flickr8k-EX（τc）、Flickr8k-CF（τb）、COMPOSITE（τc）、Polaris（τc）、Nebula（τc）、Pascal-50S（准确率，分HC/HI/HM/MM/Avg）。Polaris和Nebula使用测试分割。
  - **解释质量评估**：从Flickr8k-EX中按分数区间均匀抽取100个样本，使用一致性、事实性、信息性三个准则，4点Likert量表，4名母语者评估。
- **对比方法**：
  - **参考基**：BLEU-4, ROUGE-L, METEOR, CIDEr, SPICE, BERTScore, CLAIR, TIGEr, ViLBERTScore-F, RefCLIPScore, RefPAC-S, Polos, RefFLEUR, RefHICE-S, DENEB。
  - **无参考**：CLIPScore, PAC-S, InfoMetIC+, FLEUR, BRIDGE, HICE-S, **EXPERT**（提出）。
  - **LLM-as-a-judge**：GPT-4o直接打分。
- **主要实验结果（表2）**：EXPERT在所有六个数据集（除Pascal-50S HC/MM/Avg为第二）上达到无参考指标中的最佳结果；在Flickr8k-CF、COMPOSITE、Polaris、Nebula上甚至优于所有参考基指标。与GPT-4o相比，EXPERT在多数数据集上持平或更优。

## 4. 资源与算力
- **训练**：使用**两台NVIDIA A100 GPU（40GB内存）**，**训练约2小时**。
- **推理**：EXPERT得分+解释生成平均每样本3.80秒（A100），仅得分需0.36秒；FLEUR分别为2.76秒和0.32秒。
- **GPT-4o成本**：评估所有基准数据集花费约106美元。

## 5. 实验数量与充分性
- **数量**：覆盖6个广泛使用的图像描述评估基准（评分相关）+ 1个专门的人类解释评估（100样本×4名标注者）。还包括消融实验（分数分箱效果，表4）和错误分析（100个最大误差样本）。
- **充分性与公平性**：
  - 与多种传统、学习型、参考基与无参考指标全面对比，结果报告完整，基线结果来自原文或可复现。
  - 消融实验表明分数分箱一致提升性能。
  - 解释质量评估采用双盲设计（标注者不知道来源），且与FLEUR以及无SFT的EXPERT进行比较，差异统计显著（p<0.01）。
  - 实验设计客观、公平，但**仅在一个解释评估数据集（Flickr8k-EX样本）上进行人类评价**，泛化性可能受限。

## 6. 主要结论与发现
- EXPERT在**无参考评估指标**中达到新的SOTA，并在多个数据集上超越参考基指标。
- 生成的**结构化解释质量显著优于现有可解释指标**（FLEUR），人类评估中一致性、事实性、信息性均大幅领先。
- 分数分箱和分数平滑是提高评分准确性的有效技术。
- 标准化的结构化准则配合高质量解释数据监督是提升解释质量的关键。

## 7. 优点
- **可解释性强**：提供基于统一准则（流畅性、相关性、描述性）的结构化解释，支持细粒度分析。
- **无参考设计**：无需参考描述，更接近真实应用场景。
- **数据贡献**：构建并公开了包含超过42,000条结构化解释的数据集（Polaris-exp, Nebula-exp），促进后续研究。
- **方法简洁有效**：两阶段模板+分数分箱+分数平滑，在开源VLM上微调即可达到领先性能，无需复杂网络设计。
- **对人类评估的重视**：首次系统性地验证可解释图像描述评估指标的解释质量，并公开评估方法。

## 8. 不足与局限
- **错误分析**：主要错误类型为**对缺乏细节的描述过度惩罚**（45/100），以及高估含错误细节的描述（17/100）。模型难以捕捉图像中细粒度、区域特定的细节，这是视觉Transformer和VLM的固有挑战。
- **推理时间较长**：生成完整解释需约3.8秒/样本，比FLEUR慢，实用性受限制。
- **泛化性验证不足**：人类解释评估仅基于Flickr8k-EX一个数据集（100样本），可能无法代表其他数据集或真实场景。
- **依赖GPT-4o生成训练数据**：训练数据质量受限于GPT-4o，可能存在偏差或错误；尽管人类验证平均分高，但仍有改进空间。
- **仅使用LLaVA-1.5（13B）**：未尝试更大或更优的基座模型，可能限制上限。
- **分数范围有限**：输出分数为0~1，且仅通过分数平滑提供连续值，未探索更细粒度的评分尺度。

（完）
