---
title: "TABARD: A Novel Benchmark for Tabular Anomaly Analysis, Reasoning and Detection"
title_zh: TABARD：表格异常分析、推理与检测的新基准
authors: "Manan Roy Choudhury, Anirudh Iyengar Kaniyar Narayana Iyengar, Shikhhar Siingh, Sugeeth Puranam, Vivek Gupta"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1189.pdf"
tags: ["query:xai-objdet"]
score: 5.0
evidence: 使用LLM的表格异常检测基准
tldr: 表格数据异常检测缺乏细粒度基准。TABARD通过扰动多种表格构建包含八类异常的基准，评估LLM在直接、间接和思维链提示下的表现，揭示了标准提示的局限性。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1618, \"height\": 595, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1448, \"height\": 694, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 646, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 808, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1412, \"height\": 659, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1476, \"height\": 1162, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1653, \"height\": 1292, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1413, \"height\": 626, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1478, \"height\": 840, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 815, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1476, \"height\": 2168, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1476, \"height\": 2168, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1477, \"height\": 1485, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1648, \"height\": 531, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1189/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1649, \"height\": 500, \"label\": \"Table\"}]"
motivation: 现有基准未覆盖细粒度表格异常类型。
method: 构建包含事实、逻辑、时间等八类异常的表格基准，评估多种提示策略。
result: LLM在细粒度异常检测上存在显著不足。
conclusion: 需要专门为表格异常设计更好的方法。
---

## Abstract
We study the capabilities of large language models (LLMs) in detecting fine-grained anomalies in tabular data. Specifically, we examine: (1) how well LLMs can identify diverse anomaly types including factual, logical, temporal, and value-based errors; (2) the impact of prompt design and prompting strategies; and (3) the effect of table structure and anomaly type on detection accuracy. To this end, we introduce TABARD, a new benchmark constructed by perturbing tables from WikiTQ, FeTaQA, Spider, and BEAVER. The dataset spans multiple domains and eight anomaly categories, including paired clean and corrupted tables. We evaluate LLMs using direct, indirect, and Chain-of-Thought (CoT) prompting. Our results reveal notable limitations in standard prompting, especially for complex reasoning tasks and longer tables. To overcome these issues, we propose a unified framework combining multi-step prompting, self-verification, and constraint-based rule execution. Our approach significantly improves precision and recall, offering a promising direction for robust and interpretable anomaly detection in tables.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：表格数据在金融、医疗、科研等领域广泛应用，但常存在噪声、不一致等异常。现有异常检测工作多聚焦于非结构化或半结构化数据（文本、图像），对关系型表格的**细粒度（cell-level）异常检测**关注不足，缺乏标准化基准和系统性评估。
- **目标**：探索大语言模型（LLMs）能否识别表格中的细粒度异常（如事实、逻辑、时间、数值错误），并分析提示设计、表格结构、异常类型对检测精度的影响。
- **意义**：为LLM在结构化数据上的可靠性和可解释性提供评估基础，推动表格异常检测的方法发展。

## 2. 方法论：核心思想、关键技术细节
### 2.1 整体框架
- 将表格异常检测视为**二分类任务**：对每个单元格判断是否含有异常（标签1/0）。
- 构建**TABARD基准**：通过扰动四个公开表格数据集（WikiTQ, FeTaQA, Spider, BEAVER）生成含八类异常的表，同时保留清洁版本用于监督评估。

### 2.2 异常类型（8类）
1. **Value Anomaly**：域约束违反（如负数量）。
2. **Factual Anomaly**：与真实世界知识冲突（如“Atlantis”作为地点）。
3. **Logical Anomaly**：列间逻辑关系违背（如订单日期晚于发货日期）。
4. **Temporal Anomaly**：时间数据不合逻辑（如年份1600在电商数据中）。
5. **Calculation Anomaly**：算术计算错误（如总价≠单价×数量）。
6. **Security Anomaly**：敏感信息泄露（如未加密信用卡号）。
7. **Normalization Anomaly**：数据库范式违反（如重复组、传递依赖）。
8. **Data Consistency Anomaly**：格式或表示不一致（如同ID不同写法）。

### 2.3 提示策略
- **四个级别（L1-L4）**：从仅提及“问题”到明确指定异常类型并给出示例。每个级别分**带CoT（Chain-of-Thought）**和**不带CoT**两种。
- **直接 vs. 间接**：L1-L2为间接（不直接说“异常”），L3-L4为直接。

### 2.4 提出的三个增强方法
1. **MUSEVE（Multi-Reasoning Self Verification）**：
   - 生成多个独立推理路径，每条使用CoT+自验证。
   - 多数投票确认异常，最后重新阅读并CoT精炼。
2. **SEVCOT（Self Verification Chain of Thoughts）**：
   - 单CoT推理 + 自验证 + 重新阅读（无多路径多数投票）。
3. **NSCM（Neuro-Symbolic Constraint Method）**：
   - LLM基于表结构和部分样本生成校验约束（域、逻辑、时间等）。
   - 约束转为Python代码，在增强数据上确定性执行，标记违规单元格。
   - 可整合外部知识（如事实验证），提高可解释性和召回率。

### 2.5 生成过程
- 使用GPT-4o（temperature=0.7，max_tokens=1000）生成扰动，动态分块处理长表。
- 人验证15%样本，Cohen Kappa约94%，Jaccard系数约93%，表明扰动质量高。

## 3. 实验设计
### 3.1 数据集 / 场景
- **表格来源**：WikiTQ（短表）、FeTaQA（短表）、Spider（长表）、BEAVER（长表）。
- **统计**：共5295张表，平均行数33，平均列数5。长表变异大（最大30000行）。
- **每个表平均注入 ceil(0.5 * 行数) 个异常**（至少一个），部分表保留清洁。

### 3.2 评估指标
- **Precision（P）和Recall（R）**（F1在附录）。
- 所有评估假设当前时间为2025年5月。

### 3.3 对比方法
- **基线**：四个提示级别（L1-L4），每个带/不带CoT。
- **增强方法**：MUSEVE, SEVCOT, NSCM（仅在ChatGPT-4o和Gemini-1.5-Pro上运行，因其他模型缺乏外部工具支持）。
- **模型**：ChatGPT-4o, Gemini-1.5-Pro, LLaMA 3.1 70B Instruct, DeepSeek-V3。

### 3.4 实验数量与充分性
- **大量实验**：论文在4个数据集×3个主要模型×多种提示策略（L1-L4、MUSEVE、SEVCOT、NSCM）上报告结果。附录进一步涵盖LLaMA和DeepSeek的对比、类别级分析、合并表实验、三种变体采样等。
- **充分性**：覆盖了不同表长、不同提示复杂度、不同模型，并进行了人验证评估扰动质量。类别级分析（表4）显示不同异常类型难度不同，实验设计较为全面。
- **客观性**：使用标准指标，对比基线公平。但需注意NSCM仅能在支持代码执行的模型上运行，对比条件略有差异。

## 4. 资源与算力
- **未明确说明**：论文未提及GPU型号、数量、训练时长。主要使用LLM API（GPT-4o, Gemini-1.5-Pro等）进行推理，并调用LLM生成约束和代码执行。推断实验在云API上完成，未进行微调，算力需求相对较低（主要开销在API调用次数）。附录中提到使用Gemini 1.5 Flash生成元数据。

## 5. 主要结论与发现
- **TABARD具有挑战性**：所有模型在所有数据集上精度和召回率均不理想，特别是事实和时间异常。
- **CoT提升召回率**：但有时轻微降低精度。对短表（FeTaQA, WikiTQ）提升更明显。
- **增强方法各有优势**：
  - MUSEVE和SEVCOT提升精度。
  - NSCM大幅提升召回率（尤其在值、计算、安全异常上），但精度较低（假阳性）。
- **类别难度差异大**：值异常最易检测（召回率最高），事实和时间异常最难。
- **模型差异**：Gemini-1.5-Pro表现更稳定，DeepSeek-V3在提示复杂度深化时表现优于LLaMA。
- **长表更困难**：Spider+BEAVER（长表）性能普遍低于短表数据集。

## 6. 优点
- **首个细粒度表格异常检测基准**：覆盖8类异常，来源多样，经人验证，质量高。
- **系统性的提示策略比较**：从简单到复杂，带/不带CoT，全面评估。
- **提出创新方法**：MUSEVE, SEVCOT, NSCM，特别是NSCM结合符号执行，提高可解释性和覆盖率。
- **分析细致**：类别级性能、表长影响、模型间对比，揭示深入见解。
- **开源数据集和代码**，促进可重复性。

## 7. 不足与局限
- **单表局限**：仅处理单表内的异常，未涉及多表关联异常（如外键不一致、跨表逻辑矛盾）。现实场景常涉及多表。
- **依赖完整表**：假设表格无缺失值，未处理缺失数据（文中提到可未来扩展）。
- **未探索微调**：仅使用提示策略，未微调LLM（可能进一步提升性能）。
- **NSCM假阳性高**：约束生成过于保守，基于少量样本可能过度泛化，导致误报。论文提出未来可通过反馈优化或元模型缓解。
- **仅限英文表**：数据集主要来自英文语种（WikiTQ等），未验证多语言泛化性。
- **评估指标有限**：未使用ROC-AUC等排序指标（但二分类场景下P/R足够）。
- **模型版本固定**：实验时使用特定版本（2025年5月），后续模型更新可能改变结论。

（完）
