---
title: "LLMAD-mini: Efficient Distilling Hierarchical Chain-of-Thought for Interpretable Log Anomaly Reasoning and Detection using Large Language Model"
title_zh: LLMAD-mini：高效蒸馏分层思维链实现可解释日志异常推理与检测
authors: "Yuanyuan Zhang, Jianjun Jeff Zhu, Yunwen Bai, Heng Hao, Seungjai Min"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=W9CaFkRUeQ"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释日志异常检测，使用LLM和思维链
tldr: 本文提出LLMAD-mini，一个轻量级大模型，通过知识蒸馏和LoRA微调，结合分层思维链生成可解释的日志异常推理。该模型解决了现有方法仅输出二分类结果、缺乏根因解释的问题。实验表明，在保持检测性能的同时显著降低了部署成本，为生产环境提供了可解释的异常检测方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有日志异常检测缺乏解释和根因定位。
method: 结合知识蒸馏与LoRA微调，使用分层思维链推理。
result: 轻量级模型保持强推理能力，降低部署成本。
conclusion: 为可解释日志异常检测提供高效解决方案。
---

## Abstract
Log anomaly detection is critical for system reliability, yet most existing methods focus only on binary detection without providing explanations or identifying root causes, which limits their usefulness in production environments. To address these challenges, we propose LLMAD-mini, a lightweight LLM-based model that combines knowledge distillation with Low-Rank Adaptation (LoRA) fine-tuning to deliver strong reasoning and comprehensive log understanding. Large language models (LLMs) with human-interpretable descriptions can be tuned for specialized logs via supervised fine-tuning, but the high cost of training and deployment remains a major barrier. To achieve efficient adaption on small in-domain dataset on LLMs, we introduce a hierarchical Chain-of-Thought mechanism that significantly enhances reasoning capability with limited data. Evaluated on different system log datasets, LLMAD-mini surpasses traditional anomaly detection methods in detection accuracy and provides far better reasoning than much larger LLMs. Notably, it achieves a 3.2× improvement on reasoning quality compared to a LLM with 30× more parameters. Furthermore, our experiments on out-of-domain logs demonstrate LLMAD-mini’s ability to generalize across diverse systems with the improvement of 40% of accuracy on anomaly detection and improve the Bleu-4 from 0.01 to 0.49 while diagnosing failures, making it a practical and efficient solution for real-world deployment.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：现有日志异常检测方法大多仅输出二分类结果（正常/异常），缺乏可解释性，无法定位根因，限制了在生产环境中的实际应用。
- **背景**：大型语言模型（LLM）具有可解释性描述能力，可通过有监督微调适配特定日志，但训练和部署成本高昂。亟需一种轻量级、高效且具备可解释推理能力的日志异常检测方案。
- **研究动机**：在保持检测精度的前提下，降低模型规模和部署成本，同时提供异常根因的推理解释。

## 2. 方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出LLMAD-mini，一个轻量级LLM模型，结合**知识蒸馏（Knowledge Distillation）**和**LoRA微调**，并通过**分层思维链（Hierarchical Chain-of-Thought, HCoT）**机制增强推理能力，实现可解释的日志异常检测与根因定位。
- **关键技术细节**：
  - **知识蒸馏**：利用一个大教师LLM（参数为LLMAD-mini的30倍）生成高质量的分层思维链推理样本，用于蒸馏学生模型LLMAD-mini。
  - **LoRA微调**：在小型LLM（如Qwen2.5-3B等）上使用低秩适应技术进行高效参数微调，减少训练成本。
  - **分层思维链（HCoT）**：将推理过程分为多个层次，包括异常事件识别、原因链条推导、根因结论等，逐步生成解释，增强在有限数据下的推理能力。
- **算法流程（文字说明）**：
  1. 教师LLM对正常/异常日志生成分层思维链注解（包含异常描述、中间推理步骤、根因）。
  2. 使用蒸馏数据对学生LLM进行有监督微调（SFT），结合LoRA。
  3. 推理时，输入日志序列，学生模型输出异常判断及其分层推理链。

## 3. 实验设计
- **数据集与场景**：多个系统日志数据集（具体名称未在摘要中列出，但提及不同系统日志数据集，包括域内和域外日志）。
- **Benchmark**：与传统异常检测方法（如基于统计、机器学习的方法）以及更大规模的LLM（如30倍参数的教师模型）进行比较。
- **对比方法**：
  - 传统异常检测方法（未具体列出名称）。
  - 大LLM（教师模型，参数约为LLMAD-mini的30倍）。
- **评估指标**：异常检测准确率；推理质量通过BLEU-4等指标衡量（域外诊断时）。

## 4. 资源与算力
- **未明确说明**：论文摘要中未提及使用的GPU型号、数量、训练时长等具体算力信息。仅指出LLMAD-mini是轻量级模型，部署成本显著降低，但未给出训练资源细节。

## 5. 实验数量与充分性
- **实验规模**：涉及多个系统日志数据集（域内和域外），以及消融实验（通过对比有无蒸馏、有无HCoT等验证方法有效性）。具体实验组数未详细列出，但至少包括：
  - 域内日志上的异常检测准确率对比（与传统方法、大LLM）。
  - 域外日志上的泛化能力测试（准确率提升40%，BLEU-4从0.01提升至0.49）。
  - 推理质量比较（与30倍参数LLM相比，提升3.2倍）。
- **充分性评价**：实验覆盖域内和域外场景，对比方法类型丰富，且包含推理质量评估，较充分。但缺乏对更多数据集（如不同规模、噪声水平）的验证，也未提供消融实验的详细表格，公平性方面未提及是否统一实验环境。

## 6. 主要结论与发现
- **检测性能**：LLMAD-mini在域内日志上超越传统异常检测方法，在域外日志上准确率提升40%。
- **推理质量**：与30倍参数的大LLM相比，LLMAD-mini推理质量提升3.2倍（BLEU-4从0.01提升至0.49在域外诊断中）。
- **部署成本**：轻量级模型显著降低部署成本，同时保持强推理能力，为生产环境提供可解释异常检测方案。

## 7. 优点（方法或实验设计上的亮点）
- **方法创新**：
  - 首次将知识蒸馏与LoRA结合用于日志异常检测的可解释推理，兼顾效率与效果。
  - 提出分层思维链机制，在有限数据下显著提升推理能力。
- **实验设计**：
  - 同时评估域内和域外泛化能力，证明模型实用性强。
  - 使用BLEU-4等客观指标量化推理质量，对比大参数模型，数据有说服力。

## 8. 不足与局限
- **实验覆盖**：仅提及“不同系统日志数据集”，未公开具体数据集名称和规模，第三方复现困难。可能只覆盖少数系统类型。
- **偏差风险**：蒸馏数据依赖教师LLM，教师LLM的偏见可能被继承；HCoT设计可能偏向特定日志模式。
- **应用限制**：虽然轻量，但仍需GPU推理；对于极低资源设备可能仍有挑战。未讨论在线推理延迟和资源占用。
- **消融实验细节缺失**：未提供移除蒸馏或HCoT后的性能对比数据，无法量化各组件贡献。

（完）
