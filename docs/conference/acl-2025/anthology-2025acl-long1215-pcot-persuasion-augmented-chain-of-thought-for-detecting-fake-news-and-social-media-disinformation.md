---
title: "PCoT: Persuasion-Augmented Chain of Thought for Detecting Fake News and Social Media Disinformation"
title_zh: PCoT：基于说服增强思维链的虚假新闻与社交媒体虚假信息检测
authors: "Arkadiusz Modzelewski, Witold Sosnowski, Tiziano Labruna, Adam Wierzbicki, Giovanni Da San Martino"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1215.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 利用说服增强思维链进行可解释的虚假检测
tldr: 本文提出PCoT方法，利用说服知识增强思维链，在零样本设置下检测虚假新闻和社交媒体虚假信息。通过链式推理过程，模型提供可解释的检测理由。在多个数据集上的实验表明，该方法显著提升了虚假检测的准确性和可解释性。贡献在于将心理学说服知识融入大模型推理，增强了模型的可信度。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 815, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 790, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 769, \"height\": 244, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 773, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 774, \"height\": 250, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 772, \"height\": 249, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 776, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 775, \"height\": 246, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 772, \"height\": 248, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1619, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1570, \"height\": 1344, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1215/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1583, \"height\": 927, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 700, \"height\": 174, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 487, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 612, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1660, \"height\": 853, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 737, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 791, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 505, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 667, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 677, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 620, \"height\": 180, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 721, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 746, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1634, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 466, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 517, \"height\": 528, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1614, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1222, \"height\": 621, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1468, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1461, \"height\": 730, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 661, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 659, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 660, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 360, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1215/table-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 361, \"height\": 311, \"label\": \"Table\"}]"
motivation: 现有虚假检测方法缺乏可解释性，而心理学研究表明说服知识有助于人类识别虚假信息，因此探索将说服知识融入大模型。
method: 提出说服增强思维链PCoT，在零样本分类中利用大语言模型和说服知识进行虚假检测。
result: 在新构建的数据集上评估，PCoT显著优于基线方法，同时提供了可解释的推理过程。
conclusion: 证明说服知识增强思维链能有效提升虚假检测的性能和可解释性。
---

## Abstract
Disinformation detection is a key aspect of media literacy. Psychological studies have shown that knowledge of persuasive fallacies helps individuals detect disinformation. Inspired by these findings, we experimented with large language models (LLMs) to test whether infusing persuasion knowledge enhances disinformation detection. As a result, we introduce the Persuasion-Augmented Chain of Thought (PCoT), a novel approach that leverages persuasion to improve disinformation detection in zero-shot classification. We extensively evaluate PCoT on online news and social media posts. Moreover, we publish two novel, up-to-date disinformation datasets: EUDisinfo and MultiDis. These datasets enable the evaluation of PCoT on content entirely unseen by the LLMs used in our experiments, as the content was published after the models’ knowledge cutoffs. We show that, on average, PCoT outperforms competitive methods by 15% across five LLMs and five datasets. These findings highlight the value of persuasion in strengthening zero-shot disinformation detection.

---

## 论文详细总结（自动生成）

### 论文中文总结

#### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：社交媒体的虚假信息传播对民主、公众信任构成严重威胁。传统监督方法面临标注数据稀缺和泛化能力差的问题，促使研究者探索零样本检测。
- **核心问题**：心理学研究表明，教导人们识别**说服谬误**能提高其辨别真假新闻的能力。那么，将说服知识注入大语言模型（LLM）能否增强其零样本虚假信息检测性能？
- **整体含义**：论文提出**说服增强思维链（PCoT）** 方法，通过显式建模文本中的说服策略，引导LLM进行可解释的推理，显著提升零样本虚假信息检测的准确性和可信度。

#### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：利用“说服”作为中间推理线索，先分析文本中的说服策略，再将分析结果用于最终虚假判断，使检测过程兼具可解释性和准确性。
- **两阶段架构**：
  - **第一阶段：说服检测（Persuasion Detection）**  
    - 任务：多标签多分类 + 解释生成。输入文本 \(T\)，注入说服知识 \(K_P\)、上下文身份 \(I_P\) 和任务指令 \(G_P\)。  
    - 输出：对6种说服策略（攻击声誉、正当化、简化、转移注意力、呼吁、操纵性措辞）给出二元标签 \(y_{p_i}\) 及解释 \(E_{p_i}\)。  
    - 提示设计：采用 **DMT（Detailed Multitask）** 单提示框架，包含策略定义及下属技术细节（基于Piskorski等人的分类体系）。
  - **第二阶段：虚假信息检测**  
    - 输入：原始文本 \(T\)、第一阶段输出的分析 \(A_T\)、新指令 \(G_D\) 和上下文 \(I_D\)。  
    - 输出：二元标签 \(Y_T\)（是否虚假信息）。  
    - 提示适应性：将三种基础提示（VaN、Z-CoT、DeF-SpeC）修改为接收并利用第一阶段分析。
- **公式表示**：
  - 第一阶段：\(A_T \sim M(T, I_P, K_P, G_P)\)  
  - 第二阶段：\(Y_T \sim M(T, I_D, A_T, G_D)\)
- **关键差异**：与传统零样本直接检测相比，PCoT通过显式说服推理引入了中间可解释步骤。

#### 3. 实验设计：数据集、benchmark与对比方法
- **数据集**：
  - **已有数据集（可能重叠预训练数据）**：CoAID（COVID-19 misinformation）、ISOT Fake News、ECTF（COVID-19虚假推文）。
  - **新构建的post-cutoff数据集**：  
    - **MultiDis**：约2000篇英文文章，涵盖8个主题，由事实核查专家标注，文章发表于2024年之后。  
    - **EUDisinfo**：约400篇英文文章，源自EUvsDisinfo数据库，专注于亲克里姆林宫虚假信息，发表于2024年之后。
  - 测试集均为随机抽取的400-500条样本，保证模型未见。
- **LLMs**：GPT-4o Mini、Gemini 1.5 Flash、Claude 3 Haiku、Llama 3.3 70B、Llama 3.1 8B。温度设为0，确保确定性。
- **对比方法**：
  - **基础方法**：VaN（vanilla prompt）、Z-CoT（零样本思维链）、DeF-SpeC（上下文/演绎/溯因推理）——选自Lucas et al. (2023)在人类标注数据上的最佳方法。
  - **额外比较**：CoT、RaR（Rephrase and Respond）、CoVe（Chain-of-Verification）、以及OpenAI的o1-mini、o3-mini推理模型。
  - **消融实验**：单步PCoT、无解释版本、基础说服版本（仅一般说服定义）、移除具体策略定义等。
- **评估指标**：F1分数，使用McNemar检验统计显著性（显著性水平0.01）。

#### 4. 资源与算力
- **未明确全面说明**：大部分实验通过API调用完成（OpenAI、Google、Anthropic、DeepInfra），未说明具体GPU型号与训练时长。
- **仅有一处提及**：对BERT模型的微调使用了NVIDIA L40 GPU，但论文主要依赖推理而非训练，因此未提供整体算力统计。

#### 5. 实验数量与充分性
- **实验数量**：  
  - 5个LLM × 5个数据集 × 3种基础提示方法 = 75组核心对比实验。  
  - 加上消融实验（单步、无解释、基础版本）、与其他提示方法对比（CoT、RaR、CoVe）、推理模型对比、说服策略相关性分析、McNemar检验等，总计超过100组实验。
- **充分性与公平性**：  
  - 覆盖新闻文章和社交媒体帖子两种文本类型。  
  - 特意使用post-cutoff数据集消除数据泄露风险，并对比了不同大小、不同来源的LLM（闭源+开源）。  
  - 统计显著性检验确保结论可靠。  
  - **不足**：仅限英语，未覆盖其他语言；数据集主题有限（欧洲/COVID-19/政治）；说服策略分类体系单一。

#### 6. 论文的主要结论与发现
- **性能提升**：PCoT在所有模型和数据集上平均提升15% F1分数，对长文章提升18%，对社交媒体帖子提升8%。  
- **未见数据优势**：在post-cutoff（2024年后）数据集上提升16%，表明说服知识有助于模型泛化到新内容。  
- **说服策略相关性**：四种策略（攻击声誉、简化、转移注意力、操纵性措辞）与虚假信息强相关，而“正当化”和“呼吁”在真假内容中频率相当。  
- **可解释性价值**：加入说服解释进一步提升了性能，尤其在小模型上效果显著。  
- **零样本优于监督**：LLM零样本（含PCoT）显著优于在有限数据上微调的BERT，验证了零样本方法的潜力。

#### 7. 优点
- **创新性**：首次将心理学说服知识系统性地融入LLM零样本虚假检测，形成可解释的推理链条。  
- **方法论完整**：两阶段设计、充分的提示工程优化（DMT优于单任务提示）、提供公开数据集和代码。  
- **实验严谨**：包含post-cutoff数据集确保公平评估，多个模型/数据集/基线对比，统计显著性检验，消融实验覆盖全面。  
- **实用性**：公开MultiDis和EUDisinfo数据集，包含中间标签，有助于未来研究。  
- **可解释性**：PCoT不仅输出分类，还提供说服分析的理由，增加了模型决策的可信度。

#### 8. 不足与局限
- **语言局限**：仅评估英文文本，未探索多语言场景。  
- **主题覆盖**：数据集主要聚焦于欧洲/亲俄/COVID-19/政治主题，可能不全面代表所有虚假信息类型。  
- **分类体系依赖**：说服策略仅基于Piskorski等人单一分类法，未动态选择最相关的策略。  
- **标注偏差**：MultiDis虽经多轮培训审核，但人工标注仍有主观性；EUDisinfo依赖已有数据库，继承其偏差。  
- **计算资源不透明**：未报告API调用的具体能耗与成本，仅提及用于教育目的的GPU。  
- **方法局限**：仍需要注入固定知识，未来可探索动态说服策略选择；未测试在长尾或低资源语言上的表现。

（完）
