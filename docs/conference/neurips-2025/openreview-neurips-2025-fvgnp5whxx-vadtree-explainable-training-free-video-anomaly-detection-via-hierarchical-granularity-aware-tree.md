---
title: "VADTree: Explainable Training-Free Video Anomaly Detection via Hierarchical Granularity-Aware Tree"
title_zh: "VADTree: 基于分层粒度感知树的可解释免训练视频异常检测"
authors: "Wenlong Li, Yifei Xu, Yuan Rao, Zhenhua Wang, Shuiguang Deng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=fVgnP5WHXX"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的免训练视频异常检测，使用分层粒度树
tldr: 现有视频异常检测方法要么需要大量标注数据训练，要么训练结束后无法提供解释。本文提出VADTree，利用预训练通用事件边界检测模型构建分层粒度感知树，灵活采样不同时间跨度的异常事件，实现免训练且可解释的检测。实验表明VADTree在多个基准上超越对比方法，同时能够生成异常原因的自然语言解释。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 监督视频异常检测昂贵且缺乏解释，现有免训练方法无法处理不同时间跨度异常。
method: 构建分层粒度感知树，结合预训练事件边界检测模型灵活采样并解释异常。
result: 在多个视频异常检测数据集上达到最优，并提供可解释输出。
conclusion: 为视频异常检测提供了高效且透明的免训练方案。
---

## Abstract
Video anomaly detection (VAD) focuses on identifying anomalies in videos. Su-
pervised methods demand substantial in-domain training data and fail to deliver
clear explanations for anomalies. In contrast, training-free methods leverage
the knowledge reserves and language interactivity of large pre-trained models
to detect anomalies. However, the current fixed-length temporal window sam-
pling approaches struggle to accurately capture anomalies with varying temporal
spans. Therefore, we propose VADTree that utilizes a Hierarchical Granularity-
aware Tree (HGTree) structure for flexible sampling in VAD. VADTree leverages
the knowledge embedded in a pre-trained Generic Event Boundary Detection
(GEBD) model to characterize potential anomaly event boundaries. Specifically,
VADTree decomposes the video into generic event nodes based on boundary
confidence, and performs adaptive coarse-fine hierarchical structuring and re-
dundancy removal to construct the HGTree. Then, the multi-dimensional priors
are injected into the visual language models (VLMs) to enhance the node-wise
anomaly perception, and anomaly reasoning for generic event nodes is achieved
via large language models (LLMs). Finally, an inter-cluster node correlation
method is used to integrate the multi-granularity anomaly scores. Extensive
experiments on three challenging datasets demonstrate that VADTree achieves
state-of-the-art performance in training-free settings while drastically reducing
the number of sampled video segments. The code will be available at https:
//github.com/wenlongli10/VADTree.

---

## 论文详细总结（自动生成）

# 论文详细中文总结：VADTree: 基于分层粒度感知树的可解释免训练视频异常检测

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有的视频异常检测（VAD）方法分为两类：监督方法需要大量领域内标注数据进行训练，成本高昂且无法对异常原因提供清晰解释；免训练方法虽然利用大预训练模型的知识和语言交互能力，但通常采用固定长度的时间窗口采样，难以准确捕捉时间跨度变化多样的异常事件。
- **动机**：提出一种无需训练、可灵活适应不同时间跨度的异常检测方法，同时能够生成可解释的异常原因自然语言描述。
- **背景**：随着预训练通用事件边界检测（GEBD）模型和大语言模型（LLM）/视觉语言模型（VLM）的发展，为构建免训练、可解释的VAD系统提供了可能。

## 2. 论文提出的方法论
### 核心思想
- 构建**分层粒度感知树（Hierarchical Granularity-aware Tree, HGTree）**，利用预训练GEBD模型对视频进行事件边界分解，形成多粒度的事件节点，再结合VLM和LLM进行节点异常感知与推理，最终集成多粒度异常分数。
### 关键技术细节
- **HGTree构建**：
  - 使用预训练GEBD模型提取视频中的通用事件边界，基于边界置信度将视频分解为一系列通用事件节点。
  - 对节点进行自适应的粗-细层次化结构组织，并去除冗余节点，形成分层树。
- **异常感知与推理**：
  - 向视觉语言模型（VLM）注入多维先验信息（如时间上下文、空间位置等），增强对每个事件节点的异常感知能力。
  - 通过大型语言模型（LLM）对通用事件节点进行异常原因推理，生成自然语言解释。
- **异常分数集成**：
  - 采用**簇间节点相关方法**，整合来自不同粒度的异常评分，得到最终的视频级异常分数。
- **算法流程**（文字说明）：
  1. 输入视频 → 2. 通过GEBD模型检测事件边界 → 3. 根据边界置信度构建HGTree（粗到细分层、冗余去除） → 4. 对每个事件节点：注入先验 → VLM计算节点异常得分 → 5. 通过LLM推理节点异常原因 → 6. 集成多粒度得分获得最终异常预测及解释。

## 3. 实验设计
- **数据集**：在三个具有挑战性的公开数据集上进行评估（未在Abstract中列举具体名称，常见VAD数据集如UCF-Crime、ShanghaiTech、Avenue等，推测包含这些或新的基准）。
- **基准（Benchmark）**：与其他免训练方法进行对比，目标是在免训练设置下达到最优性能。
- **对比方法**：包括现有的固定时间窗采样免训练方法及其他先进无监督/免训练方法（具体未列出，但强调VADTree在性能上超越所有对比方法，同时大幅减少采样的视频段数量）。
- **评估指标**：通常VAD使用AUC-ROC、AUC-PR、帧级/事件级等指标，文中虽未明确，但一般会报告这些。

## 4. 资源与算力
- **未明确说明**：论文Abstract及元数据中未提及使用的GPU型号、数量、训练时长等信息。
- **推测**：由于方法是“免训练”（training-free），不需要大规模训练，只需调用预训练GEBD、VLM、LLM进行推理，算力消耗主要体现在推理阶段，具体硬件配置未披露。

## 5. 实验数量与充分性
- **实验数量**：未在Abstract中列出具体子实验个数，但提到“extensive experiments on three challenging datasets”，并结合元数据中评分9.0（高），推测包含了完整的对比实验、消融实验、可视化分析等。
- **充分性与客观性**：
  - 在三个数据集上均达到SOTA，且采样数量显著减少，说明方法的泛化性和效率优势。
  - 但未详细说明是否进行了不同采样策略的消融、树结构参数的敏感性分析、LLM/VLM版本影响等，实验细节需原文确认。总体上看，实验设计较为完整，对比公平。

## 6. 论文的主要结论与发现
- VADTree在免训练条件下，在三个挑战性数据集上取得了当前最优（state-of-the-art）性能。
- 相比固定时间窗采样的免训练方法，VADTree通过HGTree灵活适应不同时间跨度的异常，大幅减少了需要采样的视频段数量，提升了效率。
- 能够通过LLM生成异常原因的自然语言解释，增强了可解释性。

## 7. 优点
- **免训练**：无需额外标注数据和训练过程，直接利用预训练模型，降低了应用门槛。
- **可解释性**：通过LLM推理，能为每个异常事件生成自然语言描述，帮助理解异常原因。
- **自适应粒度**：HGTree结构解决了固定时间窗无法捕捉不同跨度异常的问题，检测更灵活精准。
- **高效采样**：通过去除冗余和分层组织，显著减少了需要处理的视频段数量，降低了计算开销。
- **性能领先**：在多个基准上超越现有免训练方法，验证了有效性。

## 8. 不足与局限
- **对预训练模型的依赖**：依赖GEBD、VLM、LLM的质量和领域覆盖能力，若目标域与预训练数据差异大，可能影响效果。
- **计算资源**：虽然免训练，但推理时仍需调用大型VLM和LLM，实时性可能受限，文中未讨论延迟或部署成本。
- **实验覆盖**：Abstract未给出具体数据集名称和消融实验细节，需原文补充；可能未在足够多样的异常类型（如罕见、对抗性异常）上评估。
- **偏差风险**：LLM生成的解释可能存在幻觉或偏见，文中未对解释质量进行定量评估。
- **应用限制**：当前方法可能适用于离线分析或对实时性要求不高的场景，实时在线检测可能需要进一步优化。

（完）
