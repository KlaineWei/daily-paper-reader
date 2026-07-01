---
title: "Real, Fake, or Manipulated? Detecting Machine-Influenced Text"
title_zh: 真实、伪造还是修改？检测机器影响文本
authors: "Yitong Wang, Zhongping Zhang, Margherita Piana, Zheng Zhou, Peter Gerstoft, Bryan A. Plummer"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.812.pdf"
tags: ["query:xai-objdet"]
score: 5.0
evidence: 层次化长度鲁棒的机器影响文本检测器
tldr: 针对现有机器生成文本检测仅区分人和机器的问题，提出HERO检测器，能区分人写、机器生成和机器修改三种类型。方法采用层次化结构并对长度鲁棒，实验表明在多类别检测上优于基线。但论文未提供检测结果的解释，因此与假新闻检测可解释性需求有一定差距。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1646, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 810, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 769, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 801, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 809, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 986, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1669, \"height\": 672, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1652, \"height\": 2267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.812/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1312, \"height\": 527, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.812/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1567, \"height\": 2268, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.812/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 939, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.812/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 724, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.812/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1550, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.812/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1393, \"height\": 267, \"label\": \"Table\"}]"
motivation: 现有机器文本检测忽略了机器修改文本，缺乏细粒度分类。
method: 提出层次化长度鲁棒检测器HERO，学习区分三种类型的文本。
result: 在多类别检测任务上取得了优于基线方法的性能。
conclusion: 提供了更细粒度的机器影响文本检测，但未探索可解释性。
---

## Abstract
Large Language Model (LLMs) can be used to write or modify documents, presenting a challenge for understanding the intent behind their use. For example, benign uses may involve using LLM on a human-written document to improve its grammar or to translate it into another language. However, a document entirely produced by a LLM may be more likely to be used to spread misinformation than simple translation (, from use by malicious actors or simply by hallucinating). Prior works in Machine Generated Text (MGT) detection mostly focus on simply identifying whether a document was human or machine written, ignoring these fine-grained uses. In this paper, we introduce a HiErarchical, length-RObust machine-influenced text detector (HERO), which learns to separate text samples of varying lengths from four primary types: human-written, machine-generated, machine-polished, and machine-translated. HERO accomplishes this by combining predictions from length-specialist models that have been trained with Subcategory Guidance. Specifically, for categories that are easily confused (, different source languages), our Subcategory Guidance module encourages separation of the fine-grained categories, boosting performance. Extensive experiments across five LLMs and six domains demonstrate the benefits of our HERO, outperforming the state-of-the-art by 2.5-3 mAP on average.

---

## 论文详细总结（自动生成）

# 论文详细总结：Real, Fake, or Manipulated? Detecting Machine-Influenced Text

## 1. 核心问题与整体含义（研究动机与背景）

- **问题**：现有机器生成文本（MGT）检测大多仅限于二分类（人类撰写 vs 机器生成），忽略了机器润色（机器改写人类文本）和机器翻译等细粒度类别。这些不同类别的文本可能反映不同的意图——例如，润色和翻译通常是良性使用，而完全由机器生成的文本更可能包含虚假信息或幻觉。
- **动机**：为了更准确地判断文本的潜在意图，需要区分机器影响的细粒度类型，包括人类撰写、机器生成、机器润色、机器翻译（及翻译源语言）。这不仅有助于识别恶意使用（如完全生成虚假信息），也能避免误判良性修改（如语法润色或翻译）。
- **整体含义**：本文首次将机器翻译及其源语言纳入细粒度MGT检测，扩展了检测维度，为内容审核提供更丰富的“意图”线索。

## 2. 方法论

### 核心思想
提出 **HERO（HiErarchical, length-RObust 检测器）**，一个层次化、对文本长度鲁棒的检测框架。它将分类任务组织为层次结构，并通过子类别指导模块和长度专家模型提升细粒度区分能力。

### 关键技术细节
- **类别层次**：共8个细粒度类别：人类撰写、机器生成、机器润色（Paraphrased）、机器人性化（Humanized）、以及来自中文、俄语、西班牙语、法语的机器翻译文本。
- **子类别指导模块（Subcategory Guidance）**：
  - 将易混淆的子类别分组：一组是“生成”和“人性化”，另一组是四种翻译文本。
  - 在训练时，对每个组的子类别计算额外的交叉熵损失（仅用该组的样本），引导共享特征空间更好地分离这些子类别。
  - 测试时这些模块被丢弃，不增加计算开销。
- **长度专家模型（Length Specialist Detectors）**：
  - 训练多个专家检测器，每个专注于一个特定文本长度范围（如128、256、512 tokens）。
  - 训练时使用长度裁剪（length cropping）加入其他长度样本以增强鲁棒性。
  - 测试时可直接使用最接近长度的专家，或对所有专家进行集成（平均预测）。
- **损失函数**：`L_total = L_CE + λ(L_GH + L_Trans)`，其中 `L_GH` 是生成/人性化子类别指导损失，`L_Trans` 是翻译子类别指导损失，`λ` 为可调超参数（实验取0.01）。
- **编码器**：使用 DistilBERT 作为共享特征提取器。

### 算法流程
1. 对每个输入文档，根据其token长度选择对应长度的专家模型。
2. 专家模型基于共享的DistilBERT提取特征。
3. 经过全连接层输出8类logits。
4. 训练时额外计算子类别指导损失，更新整个网络。
5. 测试时仅使用专家模型输出，不包含指导模块。

## 3. 实验设计

### 数据集 / 场景
- **训练集**：GoodNews（来自纽约时报文章2010-2018，筛选后8K训练/2K验证/2K测试）。
- **域内测试**：GoodNews。
- **域外测试**：
  - VisualNews（Guardian, BBC, USA Today, Washington Post）—— 相近域
  - WikiText（Wikipedia）—— 远程
  - WP（创意写作）、Reuters（新闻）、Essay（学生作文）—— 远程域
- **生成器**：域内（训练时用）为 Llama-3-8B；域外为 Qwen-1.5-7B, Qwen-2.5-12B, ChatGLM3-6B, StableLM-2-7B。
- **生成方式**：每种类别使用固定模板提示生成，如机器生成用“根据标题写文章”，润色用“改写文章”，翻译用“翻译文章”，人性化用“改写使其更像人类撰写”。翻译采用回译策略（先译成目标语言再译回英语），以控制内容一致性。

### Benchmark 与对比方法
- **对比方法**：
  - OpenAI-D（基于RoBERTa-large，在GPT-2输出上训练）
  - ChatGPT-D（在HC3数据集训练）
  - LLM-DetectAIve（使用DeBERTa，区分三类：人类、机器生成、机器润色）
  - DistilBERT（直接微调为8类分类）
- **评估指标**：
  - 平均精度均值（mAP）
  - 在5%假阳性率下的检测概率（PD at 5% FPR）
  - 部分实验报告F1分数

## 4. 资源与算力

- **训练设备**：单个GPU（如NVIDIA A40, L40S）。
- **训练时长**：每个数据集（如GoodNews）数据准备约60小时，模型训练约1小时。
- **骨干网络**：DistilBERT（较小、较快）。
- **说明**：论文明确提到了单GPU和训练时长，算力需求较低，具有实际部署可行性。

## 5. 实验数量与充分性

- **主实验**：Tab.1 覆盖6个数据集 × 5个LLM，共30种组合，报告mAP和PD。
- **消融实验**：
  - Tab.4：在VisualNews上比较基线（DistilBERT）、朴素粗到细、子类别指导、长度裁剪、长度专家、完整HERO。
  - Tab.2：不同输入长度下的性能对比。
  - Tab.3：按翻译质量（BLEU低/中/高）分组对比。
  - Tab.5：将翻译合并为单类后的性能。
  - Fig.5：多语言训练效果。
  - Fig.6：不同长度专家数量效果。
  - Fig.7：损失权重λ调参。
- **额外分析**：
  - 混淆矩阵（Fig.8-9）展示分类细节。
  - 润色程度实验（Fig.10）。
  - 人性化示例（Fig.12）。
- **充分性评价**：实验非常充分，覆盖了不同域、不同LLM、不同文本长度、不同翻译质量，以及全面的消融。对比方法均为领域内代表性方法，且设置公平（使用相同编码器或相近架构）。结论可靠。

## 6. 主要结论与发现

- HERO在几乎所有设置下平均mAP优于SOTA（2.5-3 mAP提升），尤其在域外数据上提升显著。
- 子类别指导模块比朴素粗到细方法更有效（Tab.4中平均mAP从31.53提升到45.97）。
- 长度专家模型显著改善了短文本检测困难问题（Tab.2中短文本性能远超基线）。
- 识别翻译源语言即使在不关心细分类时也能提升整体翻译检测性能（Tab.5中mAP提升约3）。
- 多语言训练存在饱和现象，但使用四种语言能达到最佳性能。
- 在域外LLM上性能仍低于域内，表明跨生成器泛化仍是挑战。

## 7. 优点

- **细粒度实用**：引入机器翻译及其源语言，提供更丰富的意图信息，更贴近实际应用场景。
- **高效设计**：子类别指导仅在训练时使用，不增加测试计算量，可扩展至大量细分类。
- **长度鲁棒**：长度专家集成有效缓解了短文本检测难题。
- **广泛评估**：涵盖6个域、5个LLM，包括域内和域外，实验全面、对比公平。
- **可复现**：提供代码链接（GitHub），数据生成过程详细，便于验证。

## 8. 不足与局限

- **域外泛化仍有限**：即使在HERO上，域外LLM（如ChatGLM3、Qwen系列）的性能仍显著低于域内（Llama-3）。模型对未见生成器的适应性需进一步改进。
- **翻译数据构造噪声**：使用回译策略，可能引入额外噪声或模式，使检测任务简化（翻译文本可能更容易被识别），实际表现可能高于真实场景。
- **未覆盖所有细分类**：仅探索了特定8类，未考虑部分润色、混合来源等更复杂情况。
- **骨干网络单一**：仅使用DistilBERT，未实验更大模型（如RoBERTa、DeBERTa）的兼容性。
- **需人类监督**：作者明确指出不推荐在无人类监督下用于正式检测（如抄袭检测），更适合作为辅助工具。
- **缺乏对生成源语言的深入分析**：仅包含四种语言，且均为高资源语言，低资源语言未涉及。

（完）
