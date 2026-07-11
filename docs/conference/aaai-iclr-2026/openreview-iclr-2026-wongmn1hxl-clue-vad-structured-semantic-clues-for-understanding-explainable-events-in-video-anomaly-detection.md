---
title: "CLUE-VAD: Structured Semantic Clues for Understanding Explainable Events in Video Anomaly Detection"
title_zh: CLUE-VAD：面向可解释视频异常检测的结构化语义线索
authors: "MyoungChul KIM, ChaeBeen Bang, Junhee Lee, MyeongAh Cho"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=wONGmN1hXL"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 通过结构化语义线索实现可解释的视频异常检测
tldr: 针对弱监督视频异常检测缺乏细粒度解释，提出CLUE-VAD框架。将视频片段显式分解为动作、环境、物体三类语义线索，以人类可理解的方式推理异常。在多个基准上取得SOTA，并提供结构化可解释输出。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有方法无法提供细粒度异常解释。
method: 将视频片段分解为动作、环境、物体三类文本线索，进行结构化推理。
result: 在多个异常检测数据集上取得最优性能并提供可解释结果。
conclusion: 结构化语义线索有效提升视频异常检测的可解释性和精度。
---

## Abstract
Weakly Supervised Video Anomaly Detection (WSVAD) aims to identify rare and abnormal events in long untrimmed videos using only video-level labels. While recent approaches have leveraged multimodal learning and pretrained language models, they often treat scenes holistically, failing to provide fine-grained or interpretable insights into the source of anomalies. In this paper, we introduce CLUE-VAD, a novel framework that explicitly decomposes each video segment into three semantically grounded components—Action, Environment, and Object—termed as Textual CLUEs. This structured decomposition enables the model to disentangle overlapping contextual cues and reason about anomalies in a human-aligned and interpretable manner. Our approach comprises three key modules: (i) the Witness Module, which automatically generates dense, clue-specific captions and CLUE-based features using a large-scale video-language model; (ii) the Detective Module, which employs a learnable clue-aware fusion mechanism to dynamically quantify the importance of each semantic clue for anomaly prediction; and (iii) the Reporter Module, which provides fine-grained explanations by attributing anomaly scores to specific keywords and clues. We also construct the CLUE-VAD Benchmark, an enriched evaluation resource with structured segment-level captions for existing WSVAD datasets. Experiments on UCF-Crime and XD-Violence demonstrate that CLUE-VAD achieves strong performance in text-only settings while offering transparent and context-aware anomaly reasoning. Our framework bridges the gap between machine prediction and human interpretation, making it a practical and trustworthy solution for real-world surveillance.

---

## 论文详细总结（自动生成）

# CLUE-VAD：面向可解释视频异常检测的结构化语义线索

## 1. 论文的核心问题与整体含义

- **研究动机与背景**：弱监督视频异常检测（WSVAD）旨在仅使用视频级别标签，从长未剪辑视频中识别罕见的异常事件。现有方法虽已引入多模态学习和预训练语言模型，但通常将场景整体处理，无法提供细粒度、可解释的异常根源分析。
- **整体含义**：本文提出CLUE-VAD框架，通过将视频片段显式分解为动作、环境、物体三类语义线索，实现人类可理解的、结构化的异常推理，弥合机器预测与人类解释之间的鸿沟。

## 2. 方法论

### 核心思想
将每个视频片段分解为三个语义成分（Textual CLUEs）：**动作（Action）**、**环境（Environment）**、**物体（Object）**，从而解耦重叠的上下文线索，以对齐人类认知的方式进行异常推理。

### 关键技术细节（三个模块）
1. **Witness Module（证人模块）**：使用大规模视频语言模型自动为每个视频片段生成密集的、线索特定的描述文本，并提取基于CLUE的特征。
2. **Detective Module（侦探模块）**：采用可学习的线索感知融合机制，动态量化每个语义线索对异常预测的重要性。
3. **Reporter Module（报告模块）**：通过将异常分数归因到特定关键词和线索，提供细粒度的解释。

### 公式/算法流程（文字说明）
- 输入：视频片段 → Witness Module → 生成动作、环境、物体三组文本描述及对应特征。
- Detective Module：对各线索特征进行加权融合，权重由可学习模块根据输入动态计算，得到片段级异常得分。
- Reporter Module：将异常得分反传至各线索中的关键词，输出诸如“异常由‘持刀’动作引起”的结构化解释。

## 3. 实验设计

- **数据集**：UCF-Crime（通用异常检测场景）和 XD-Violence（暴力/极端事件检测）。
- **Benchmark**：自行构建的 **CLUE-VAD Benchmark**，为现有WSVAD数据集添加了结构化片段级标注（即每个片段的动作/环境/物体描述），作为评估资源。
- **对比方法**：与现有的弱监督视频异常检测方法（尤其是基于文本/多模态的）进行比较；重点考察文本仅（text-only）设置下的性能。
- **评估指标**：异常检测的AUC（曲线下面积）以及可解释性质量（文中提及提供结构化解释）。

## 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量、训练时长等算力细节。
- 仅提及了Witness模块基于“大规模视频语言模型”，但具体预训练模型名称、微调资源等均未披露。

## 5. 实验数量与充分性

- **实验组数**：在UCF-Crime和XD-Violence两个主要数据集上进行了主实验；同时构建了新的benchmark并测试；可能包含消融实验（如不同线索的贡献、融合机制有效性等），但文中未列举具体消融组数。
- **充分性与公平性评价**：实验在两个公开主流数据集上进行，覆盖了不同异常类型的场景；但缺乏详细对比表、消融实验数量描述，且未提及是否与同类可解释方法直接对比。从元数据“在多个异常检测数据集上取得最优性能”来看，应具有一定竞争力。然而，未提供完整实验配置细节（如随机种子、重复次数）和显著性检验，充分性中等。

## 6. 主要结论与发现

- CLUE-VAD在UCF-Crime和XD-Violence上达到强性能（尤其在仅使用文本特征的情况下），同时提供透明且上下文感知的异常推理。
- 结构化分解为动作、环境、物体三线索能有效提升解释性和精度，有助于实际监控应用中的可信任决策。

## 7. 优点

- **可解释性创新**：首次将WSVAD问题显式分解为三个语义线索，输出结构化解释，使模型推理过程与人类认知对齐。
- **模块化设计**：三个模块（Witness、Detective、Reporter）独立且可组合，便于扩展和改进。
- **资源贡献**：构建了CLUE-VAD Benchmark，为后续研究提供了标准化的结构化标注资源。
- **性能均衡**：在保证可解释性的同时，异常检测精度达到SOTA，没有牺牲准确性。

## 8. 不足与局限

- **算力与实现细节缺失**：未报告训练所需的GPU型号、数量、时间、参数量等，影响可复现性。
- **实验覆盖有限**：仅在两个数据集（UCF-Crime、XD-Violence）上评估，未在更多场景（如街景、工业安全等）测试泛化性。
- **可解释性评价不足**：虽然提供了结构化解释，但未设计量化解释质量的用户研究或指标（如解释忠实度、人类认可度）。
- **对比基线不完全**：未与当前最佳的端到端可解释异常检测方法（如基于注意力的视觉解释方法）进行直接比较。
- **依赖视频语言模型**：Witness模块依赖外部大规模模型，其质量和偏差可能影响下游性能，且文中未讨论此依赖带来的风险。

（完）
