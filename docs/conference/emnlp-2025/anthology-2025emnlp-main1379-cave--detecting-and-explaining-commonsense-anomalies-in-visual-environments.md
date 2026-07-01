---
title: "CAVE : Detecting and Explaining Commonsense Anomalies in Visual Environments"
title_zh: CAVE：检测与解释视觉环境中的常识异常
authors: "Rishika Bhagwatkar, Syrielle Montariol, Angelika Romanou, Beatriz Borges, Irina Rish, Antoine Bosselut"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1379.pdf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 首个真实世界视觉异常基准，支持描述、解释和证明任务
tldr: 针对计算机视觉中异常检测局限于工业缺陷或合成异常的问题，提出CAVE基准，包含真实世界视觉异常。该基准支持异常描述、解释和证明三个开放任务，并提供细粒度标注，包括视觉定位、异常分类等。为可解释的异常检测提供了标准和数据，直接满足异常检测可解释性需求。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 908, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 546, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1662, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 817, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1654, \"height\": 750, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1660, \"height\": 1646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1660, \"height\": 981, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 792, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 244, \"height\": 274, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 385, \"height\": 272, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 453, \"height\": 274, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 454, \"height\": 274, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 776, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 773, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 771, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 813, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1628, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1650, \"height\": 1118, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1616, \"height\": 1200, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 642, \"height\": 840, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 647, \"height\": 840, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 639, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 635, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 640, \"height\": 834, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1379/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 640, \"height\": 1112, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1589, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 778, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1151, \"height\": 629, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 746, \"height\": 265, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 667, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 202, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 763, \"height\": 545, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1518, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1470, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1554, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 786, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1665, \"height\": 794, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1379/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 734, \"height\": 363, \"label\": \"Table\"}]"
motivation: 现有异常检测基准局限于合成或工业缺陷，缺乏真实世界异常及其解释。
method: 构建真实世界视觉异常数据集CAVE，包含多任务标注（描述、解释、证明），并借鉴认知科学设计。
result: 提供了首个真实世界异常基准，支持全面的可解释异常检测评估。
conclusion: CAVE推动了可解释视觉异常检测的发展，弥合了与人类认知的差距。
---

## Abstract
Humans can naturally identify, reason about, and explain anomalies in their environment. In computer vision, this long-standing challenge remains limited to industrial defects or unrealistic, synthetically generated anomalies, failing to capture the richness and unpredictability of real-world anomalies. In this work, we introduce CAVE, the first benchmark of real-world visual anomalies. CAVE supports three open-ended tasks: anomaly description, explanation, and justification; with fine-grained annotations for visual grounding and categorizing anomalies based on their visual manifestations, their complexity, severity, and commonness. These annotations draw inspiration from cognitive science research on how humans identify and resolve anomalies, providing a comprehensive framework for evaluating Vision-Language Models (VLMs) in detecting and understanding anomalies. We show that state-of-the-art VLMs struggle with visual anomaly perception and commonsense reasoning, even with advanced prompting strategies. By offering a realistic and cognitively grounded benchmark, CAVE serves as a valuable resource for advancing research in anomaly detection and commonsense reasoning in VLMs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：当前计算机视觉中的异常检测主要局限于**工业缺陷检测**（如 MVTec AD）或**合成生成的异常**（如 WHOOPS、ROME），这些方法无法捕捉真实世界异常的多样性、不可预测性和现实性。同时，现有异常数据集缺乏对异常的**可解释性**评估（为什么异常、如何发生）。
- **背景**：人类能自然地识别、推理并解释环境中的异常，而视觉-语言模型（VLM）在异常检测和常识推理方面仍有显著不足，尤其在真实场景中。
- **目标**：构建首个**真实世界视觉异常基准** CAVE，并设计一套基于认知科学的评估框架，用于系统评价 VLM 的异常检测、解释和证明能力。

## 2. 论文提出的方法论

### 核心思想
- 借鉴认知科学文献，将人类识别和理解异常的过程分解为三个开放任务：
  - **异常描述（Anomaly Description, AD）**：识别并描述异常是什么。
  - **异常解释（Anomaly Explanation, AE）**：说明为什么该情况是异常的（基于常识知识）。
  - **异常证明（Anomaly Justification, AJ）**：提供真实合理的假设，解释异常如何发生。
- 异常的表现形式分为六类：实体存在/缺失、属性异常、空间关系异常、均匀性破坏、文本异常。
- 每个异常附加三个数值属性：严重性（1-5）、惊奇度（1-5）、复杂度（1-5）。

### 数据集构建
- **数据来源**：从 Reddit 四个子版块（r/ocdtriggers, r/mildlyconfusing, r/mildlyinfuriating, r/OSHA）爬取 top 1000 帖子，经自动和手动过滤后保留 361 张图像。
- **标注流程**：
  1. **MTurk 初标注**：每张图 5 名工人标注是否存在异常、描述、预期正确版本、分类。
  2. **专家验证与补充**：专家整合、修正文本标注，并添加边界框、分类、数值评分（3 名专家独立打分）。
- **最终数据集**：309 张异常图 + 52 张正常图，共 334 个异常（每张最多 3 个），每个异常包含边界框（平均占图 24% 面积）。

### 评估方法
- **AD**：使用 GPT-4o 作为裁判将模型输出与真实描述进行成对匹配（验证准确率 90%），计算精确率、召回率、F1。
- **AL**：给定真实描述，让模型预测边界框，计算 IoU。
- **AE**：给定真实描述，用 LLM 裁判比较模型解释与真实解释（验证准确率 89%）。
- **AJ**：因主观性，采用人工评估（3 人），比较模型输出与人类输出在 plausibility、relevance、creativity 上的优劣。

## 3. 实验设计
### 数据集 / 场景
- 仅使用 **CAVE 基准**（361 张图像，334 个异常）。额外在**合成基准** WHOOPS 和 COCO-OOC 上进行了对比实验（附录 C）。

### 对比方法
- **3 个闭源模型**：GPT-4o (2024-11-20)、o1 (2024-12-17)、Claude-3.5-Sonnet (2024-10-22)
- **5 个开源模型**：Llama3.2 90B、LlavaOneVision 72B、InternVL2.5 38B/78B、Qwen2.5-VL 72B

### 提示策略
- Vanilla（基线）、Chain-of-thought (CoT)、Set-of-Marks (SoM，使用 GroundingDINO 检测目标）、CoT+SoM、Multi-step CoT (MS CoT)、CoT + Self-consistency（3 次生成，多数投票）
- 所有评估为**零样本**，temperature 为 0（除 self-consistency 使用 0.5）。

### 实验内容
- AD 主实验（F1 对比）、AE 实验、AJ 实验（仅 GPT-4o 和 InternVL）。
- 按数值特征（严重性、惊奇度、复杂度）和异常类别分析模型表现。
- 错误类型分析（感知错误 vs 推理错误）。
- 文化偏差分析。
- 额外合成基准对比（Appendix C）。

## 4. 资源与算力
- **推理**：使用 4 块 A100 80GB GPU，每个大型开放模型完整跑完 CAVE 需要最多 **3 小时**。
- **未提及训练**：所有实验均为零样本推理，无需训练。
- 闭源模型通过 API 调用，未说明具体算力消耗。

## 5. 实验数量与充分性
- **数量**：涵盖了 8 个模型的 6 种提示策略，并针对每个任务（AD、AE、AJ、AL）进行了多组实验。数值分析和类别分析也较为全面。
- **充分性**：实验设计系统、客观。对 AD 评估使用了 LLM 裁判并验证了准确率（90%）；对 AE 也验证了 89% 准确率；对 AJ 使用人工评估。此外进行了统计显著性检验（bootstrap）和裁判偏差分析（用 Claude 作为独立裁判）。
- **公平性**：对比模型覆盖主流开源和闭源，提示策略一致；消融实验（如 self-consistency 对 F1 提升）表明了改进有效性。但 CAVE 数据集较小，可能限制泛化结论。

## 6. 主要结论与发现
- **最佳模型**：GPT-4o 在 AD 上仅达到 **57% F1**（使用 MS CoT 提示），仍有大量提升空间。
- **提示策略效果有限**：CoT + self-consistency 平均提升最大（+4.83%），但 SoM 和 CoT+SoM 甚至在部分模型上降级（因 GroundingDINO 引入噪声）。
- **模型擅长解释但弱于感知**：所有模型在 AE 上准确率 >80%（即使 AD 为 FN 时），说明模型具备常识知识，但视觉感知能力不足导致检测失败。
- **定位能力极差**：GPT-4o 仅 21.7% 预测框 IoU ≥ 0.1，且倾向于低估异常区域。
- **错误类型**：Vanilla 提示下约 49% FP 为推理错误，44% 为感知错误；MS CoT 将推理错误降至 32%，但感知错误升至 68%。
- **难度差异**：模型在**高严重性、高惊奇度、低复杂度**的异常上表现更好；在**空间关系**和**均匀性破坏**类别上困难最大。
- **存在轻微文化偏差**：4 例异常具有西方中心偏向，模型倾向于将其视为异常。

## 7. 优点
- **首个真实世界异常基准**：填补了合成/工业数据集与真实需求之间的空白。
- **认知科学驱动的框架**：将异常理解拆解为描述、解释、证明三个开放任务，更贴近人类认知过程。
- **细粒度多维度标注**：包含异常类别、边界框、严重性/惊奇度/复杂度等数值属性，支持深入分析。
- **全面的评估体系**：结合自动评估（LLM-as-judge）与人工评估，并验证了裁判可靠性。
- **对模型弱点的深入分析**：通过错误类型、数值特征、类别特征等剖析了 VLMs 失败的模式。

## 8. 不足与局限
- **数据集规模偏小**：仅 361 张图像、334 个异常，可能不足以覆盖现实世界中所有异常类型。
- **文化偏差**：数据仅来自 Reddit（用户群体偏向西方），标注者和图像内容可能存在系统性文化偏向。虽采取了多样标注团队、多轮标注等措施，仍可能影响基准的全球适用性。
- **标注完整性假设**：评估假设所有异常已被人类标注，可能遗漏某些细微或争议性异常，影响召回率计算。
- **LLM 裁判可靠性**：尽管验证了高准确率，但使用 GPT-4o 作为裁判可能对自身输出有偏（论文补充分析显示偏差不显著，但仍有风险）。
- **定位任务评估粗糙**：仅用 IoU ≥ 0.1 作为阈值，且未在开源模型上完整测试定位。
- **仅零样本评估**：未探索微调或适应策略，因数据量小不可行；未来工作可考虑少样本或检索增强方法。

（完）
