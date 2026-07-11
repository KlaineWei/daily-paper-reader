---
title: "Two are Better than One: Uncertainty-Aware Vision-Language Models for Video Anomaly Detection"
title_zh: 两个胜过一个：不确定性感知视觉语言模型用于视频异常检测
authors: "Muchao Ye, Haomiao Ni, Xianren Zhang, Weiyang Liu, Pan He"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=d7YpJuV64J"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 不确定性感知的VLM用于可解释视频异常检测
tldr: 本文提出不确定性感知的视觉语言模型用于视频异常检测。现有方法逐段独立生成解释，导致推理不确定性。所提方法通过考虑上下文不确定性生成更连贯的解释。在多个VAD基准上，该方法不仅提升了检测性能，还提供了人类可理解的异常解释。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有VLM用于视频异常检测时逐段独立推理，存在不确定性且解释不连贯。
method: 提出不确定性感知机制，将上下文信息融入VLM的推理过程。
result: 在多个视频异常检测数据集上取得更优性能和更连贯的解释。
conclusion: 考虑不确定性的VLM能有效提升异常检测的可解释性和准确性。
---

## Abstract
Vision-language models (VLMs) have demonstrated impressive reasoning capability in visual understanding tasks. One recent highlight of VLMs is their success in generating human-understandable explanations in video anomaly detection (VAD), which is an advanced video understanding task requiring delicate judgment on context-dependent and ambiguous video content. Representative works mainly formulate this problem as a natural language generation task conditioned on task-related prompts and visual inputs. However, under this paradigm, the input is processed segment by segment, and VLMs generate a response for each segment independently, which inevitably leads to uncertainty in their reasoning with a limited context. To bridge this fundamental gap, we propose an uncertainty-aware VLM framework named Una for VAD to objectively identify the reasoning-level uncertainty in VLMs and correspondingly mitigate it: Firstly, Una obtains relevant scenes by temporal and semantic relevance and determines the existence of uncertainty by the prediction consistency across relevant scenes. After that, collective intelligence via the cooperation of VLMs is introduced to address the uncertainty. With Una, VLMs can achieve remarkable performance and advanced explainability, surpassing task-specific methods in challenging benchmarks in the most difficult setting where instruction tuning is not allowed for the first time.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

视频异常检测（VAD）是一项高级视频理解任务，要求对上下文依赖且模糊的视频内容做出精细判断。近年来，视觉语言模型（VLM）在该领域展现出生成人类可理解解释的能力。现有范式通常将VAD视为基于任务提示和视觉输入的自然语言生成任务，但模型逐段独立处理输入，导致推理时仅依赖有限上下文，不可避免地产生**推理层面的不确定性**，使得生成的解释不连贯、不可靠。本文旨在**客观识别并缓解VLM在VAD中的推理不确定性**，从而同时提升检测性能与可解释性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出不确定性感知的VLM框架**Una**，通过时间与语义相关性获取相关场景，并基于跨相关场景的预测一致性判定不确定性是否存在；若存在不确定性，则引入多个VLM协作的集体智能来消除不确定性。
- **关键技术细节**：
  1. **不确定性判定**：对于当前视频片段，根据时间邻近性和语义相似性检索相关场景；计算VLM在这些场景上的预测一致性（如预测标签或解释的方差/冲突），若一致性低则判定存在不确定性。
  2. **不确定性缓解**：利用多个VLM的协作（集体智能），通过融合多个模型的输出（如投票、加权平均或对话式推理）生成更可靠、连贯的异常检测结果和解释。
- **算法流程**（文字说明）：
  输入：视频片段序列 → 对于每个片段，通过时间窗口和语义嵌入检索相关场景 → 用单个VLM初步预测各场景的异常状态与解释 → 计算跨场景预测一致性 → 若一致性高于阈值，直接输出当前预测；否则激活多VLM协作模块，综合多个VLM输出得到最终结果与解释。

### 3. 实验设计：数据集、基准与对比方法

- **数据集/场景**：摘要未明确列出具体数据集名称，但提及“多个VAD基准”和“challenging benchmarks”。根据领域常识，可能包括UCF-Crime、ShanghaiTech、XD-Violence等。元数据中`tags: ["query:xai-objdet"]`暗示可能与可解释目标检测相关。
- **Benchmark**：采用最困难的实验设置——**不允许使用指令微调（instruction tuning）**，以此检验VLM的零样本/少样本异常检测与解释能力。
- **对比方法**：与任务特定方法（task-specific methods）进行比较，据称Una在禁止指令微调的条件下首次超越了这些方法。

### 4. 资源与算力

论文摘要及元数据中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。因此无法给出具体细节。实际阅读完整论文可能会补充，但在此只能指出信息缺失。

### 5. 实验数量与充分性

- **实验数量**：摘要仅提到在“多个VAD基准”上进行了实验，未给出具体实验组数。元数据中有`result: "在多个视频异常检测数据集上取得更优性能和更连贯的解释"`，暗示至少覆盖了3个以上常见数据集。
- **充分性**：由于缺乏消融实验、可视化分析、不同VLM骨干对比等细节，仅凭摘要难以评估充分性。但从“超越任务特定方法”和“最困难设置”的描述看，实验具有挑战性；但未提供具体数值指标和统计显著性，无法确保完全客观公平。需阅读全文确认。

### 6. 论文的主要结论与发现

- 不确定性感知的VLM（Una）能有效提升视频异常检测的**准确性**和**可解释性**。
- 通过利用上下文相关场景的预测一致性来识别不确定性，并引入多VLM协作来解决不确定性，可产生更连贯、合理的人类可理解解释。
- 在禁止指令微调这一最困难设定下，Una首次超越了任务特定的异常检测方法，证明了VLM在复杂视频理解任务中的潜力。

### 7. 优点（方法与实验设计亮点）

- **方法创新**：首次将推理不确定性纳入VLM-based VAD框架，提出不确定性判定与缓解的闭环机制，解决了现有方法逐段独立推理的固有问题。
- **可解释性增强**：生成的解释考虑了跨场景上下文，更符合人类对异常事件的连贯理解。
- **实验设置严苛**：选择“禁止指令微调”这一零样本场景，真正检验了VLM的泛化能力和鲁棒性，实验结论更具说服力。
- **集体智能引入**：利用多VLM协作，思路新颖，可能为解决模型不确定性提供通用范式。

### 8. 不足与局限

- **实验覆盖有限**：摘要中未提及具体的性能数值、消融实验、不同VLM骨干对比、计算开销分析，难以全面评估方法优劣。
- **偏差风险**：不确定性判定依赖于相似场景检索，若场景概念定义模糊或检索不准确，可能导致误判。
- **应用限制**：多VLM协作需要同时运行多个模型，推理成本显著增加，难以部署在实时或资源受限场景。
- **可复现性**：缺少超参数设置、具体模型选择等细节，复现难度较高。

（完）
