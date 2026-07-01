---
title: "EVICheck: Evidence-Driven Independent Reasoning and Combined Verification Method for Fact-Checking"
title_zh: "EVICheck: 基于证据的独立推理与组合验证方法用于事实核查"
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0376.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 事实核查论文，采用证据驱动推理，支持可解释性
tldr: 针对事实核查中缺乏可解释性推理的问题，本文提出了EVICheck方法，通过证据驱动的独立推理模块和组合验证策略，提升了虚假信息检测的透明度。实验结果表明，该方法在多个数据集上取得了先进的准确率，同时提供了可解释的推理路径，有助于理解模型决策过程。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 896, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 887, \"height\": 898, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 879, \"height\": 426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 906, \"height\": 264, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 899, \"height\": 244, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 893, \"height\": 250, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 890, \"height\": 111, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 895, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 897, \"height\": 811, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-376/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 893, \"height\": 490, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-376/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 678, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-376/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 892, \"height\": 474, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-376/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 635, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-376/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 867, \"height\": 587, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-376/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 633, \"height\": 302, \"label\": \"Table\"}]"
motivation: 当前事实核查方法缺乏独立证据推理，本文提出结合独立推理与组合验证的框架。
method: 提出EVICheck方法，利用证据驱动的独立推理模块，并进行组合验证。
result: 实验结果表明该方法在标准事实核查数据集上达到先进水平。
conclusion: EVICheck通过推理与验证的结合提升了事实核查的准确性和可解释性。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

# 论文结构化总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **问题**：现有自动事实核查方法主要依赖大语言模型（LLM）和检索增强生成（RAG），但存在两大缺陷：
  - **证据利用不充分**（IEU）：多数方法将多份证据聚合后进行集体推理，而非独立分析每份证据，导致信息未被充分挖掘。
  - **缺乏明确的验证标准**：仅使用简单提示或少量样本进行可信度判断，在处理复杂、模糊声明时可靠性不足。
- **目标**：提出一种新颖方法，通过独立推理每份证据、引入细粒度真值标准，提升事实核查的准确性和可解释性。

## 2. 论文提出的方法论
- **核心思想**：将事实核查分为两个主要模块：**证据获取与初步推理**、**基于细粒度真值标准的组合验证**。
- **关键技术细节**：
  - **证据获取与初步推理**：
    1. 从声明中提取核心要素，生成多个验证问题。
    2. 选择与声明最相关的问题（基于LLM评分）。
    3. 使用搜索API（SerpApi）检索网页内容，并对每份检索结果进行独立初步推理（包括背景、证据、因果关系分析、结论）。
    4. 根据前一轮推理结果生成新的验证问题，循环进行多轮（论文设置为2轮），以全面收集证据。
  - **组合验证**：
    - 将多轮推理结果（问题-推理对）聚合。
    - 基于人工设计的**细粒度真值标准**（表1），对三类标签（True、False、Half）分别给出定义和约束条件（如False包括因果关系错误、证据不支持、未核实、官方直接否认、关键信息缺失等）。
    - 使用微调后的Llama-3-8B-Instruct模型作为`f_combined_verification`，对聚合证据和标准进行最终判决。
- **算法流程**（见Algorithm 1）：
  - 输入声明x，循环次数max_loops。
  - 生成问题 -> 选最优问题 -> 检索 -> 初步推理 -> 存储结果 -> 生成新问题 -> 循环 -> 组合验证 -> 输出最终预测和解释。

## 3. 实验设计
- **数据集**：RAWFC（英文假新闻数据集），包含三类标签：True、False、Half。总计2012条数据，其中训练1612、测试200、验证200。数据来自Snopes，附有人工标注的“黄金解释”。
- **基准方法**：
  - 监督方法：GenFE、SentHAN、SBERT、CofCED。
  - LLM方法（基于GPT-3.5）：CoT、Standard Prompt、Hiss、RAFTS。
- **评估指标**：Macro平均精确率（P）、召回率（R）、F1值。此外使用混淆矩阵分析分类错误模式。

## 4. 资源与算力
- 论文未明确说明使用的GPU型号、数量及训练时长。
- 仅提及细节：
  - 微调采用Llama-3-8B-Instruct模型，使用LoRA（低秩适配）方法，冻结除LoRA适配器外的所有参数，训练3个epoch。
  - 推理时使用GPT-3.5、GPT-4作为部分模块（如问题选择、初步推理），并调用SerpApi作为搜索接口。
- 因此，算力资源细节缺失，无法评估计算成本。

## 5. 实验数量与充分性
- **实验组别**：
  1. **整体性能对比**：在测试集上比较7种基准方法与EVICheck的4种变体（不同LLM组合），共11组结果（表3）。
  2. **消融实验**（图4）：3组消融——去除微调、去除初步推理、去除细粒度真值标准，分析对F1的影响。
  3. **循环轮数与问题数量优化**：在12个随机样本上测试循环轮数（1~4轮）和问题数量（1~7个）对得分率的影响（图5、图6）。
  4. **人类评估**：3位专家对12个样本的RAWFC解释与EVICheck解释进行5点量表评分（覆盖性、可读性、准确性、简洁性、可信度）。
  5. **案例分析**：展示一个具体声明从问题生成到最终判决的完整过程。
- **充分性评价**：实验设计较全面，覆盖了性能对比、消融、参数探索、人类评估，但存在以下不足：
  - **数据集单一**：仅使用RAWFC一个数据集，缺乏跨领域、跨语言验证。
  - **测试集规模小**：仅200条测试样本，可能影响统计可靠性。
  - **循环/问题优化实验样本量过小**（12个），结论稳健性存疑。
  - **人类评估样本量小**（12个），且未报告评分者间信度。

## 6. 论文的主要结论与发现
- EVICheck在所有评估指标上超越现有SOTA方法，特别是使用GPT-4 + 微调Llama-3时，**F1达0.633**，相比最优基线（RAFTS的0.573）提升约6.0%。
- 消融实验表明：
  - 去除初步推理导致F1下降7.77%。
  - 去除细粒度真值标准导致F1下降10.08%。
  - 模型微调带来3.47%的提升。
- 混淆矩阵分析显示：GPT-4存在负向偏见（更倾向于判False），而微调的Llama-3更加均衡，对Half和True的判别改善明显。
- 人类评估表明：EVICheck在覆盖性、可读性、准确性和可信度上优于RAWFC原始解释，但简洁性较低（因包含多轮推理细节）。

## 7. 优点
- **方法创新**：独立推理每份证据，避免聚合造成的语义损失；细粒度真值标准为模型提供了结构化指导，显著提升复杂声明的判别可靠性。
- **可解释性强**：提供多轮推理步骤，包括背景、证据、因果关系分析，支持透明验证。
- **性能提升显著**：在RAWFC上达到SOTA，且消融实验清晰验证各模块贡献。
- **实际应用潜力**：集成实时搜索API，可处理最新信息；人类评估证实其实用性优于原数据集解释。

## 8. 不足与局限
- **实验覆盖不足**：
  - 仅使用单数据集（RAWFC），且测试集仅200条，统计效力有限。
  - 循环轮数和问题数量优化实验样本量极小（12个），且未在完整测试集上验证。
  - 未在更多元的数据集（如FEVER、PolitiFact）上评估泛化能力。
- **计算成本高**：每次验证需要多次API调用（搜索+LLM），且多轮推理增加延迟和成本，实践中可能受限。
- **对非正式声明和多媒体声明仍有困难**：论文自述在处理社交媒体非正式声明和图文/视频型声明时存在不足。
- **简洁性不足**：人类评估显示解释较长，可能影响实际用户体验。
- **潜在偏见**：GPT-4在实验中表现出明显的False倾向，虽经微调缓解，但模型固有偏见未完全消除。
- **缺少算力报告**：未提供训练/推理的GPU规格和时长，难以评估资源需求。

（完）
