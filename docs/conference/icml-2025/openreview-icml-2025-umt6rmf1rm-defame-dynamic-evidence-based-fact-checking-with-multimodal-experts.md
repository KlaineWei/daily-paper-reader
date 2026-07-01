---
title: "DEFAME: Dynamic Evidence-based FAct-checking with Multimodal Experts"
title_zh: DEFAME：基于动态证据的多模态专家事实核查
authors: "Tobias Braun, Mark Rothermel, Marcus Rohrbach, Anna Rohrbach"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=umT6rMf1Rm"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 多模态假新闻检测并生成可解释报告
tldr: 虚假信息泛滥需要可靠的事实核查。本文提出DEFAME，一种零样本多模态大模型流水线，用于开放域图文声明验证。其六阶段流程动态选择工具和搜索深度，提取并评估文本和视觉证据，生成结构化多模态报告，克服了现有方法缺乏可解释性的问题。在VERITE等基准上超越前人。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有事实核查方法缺乏可解释性，且多局限于文本。
method: 设计零样本MLLM流水线，动态选择工具进行图文证据提取与评估。
result: 在VERITE、AVeriTeC和MOCHEG上超越先前方法。
conclusion: DEFAME提供可解释的多模态事实核查，适用于假检测场景。
---

## Abstract
The proliferation of disinformation demands reliable and scalable fact-checking solutions. We present **D**ynamic **E**vidence-based **FA**ct-checking with **M**ultimodal **E**xperts (DEFAME), a modular, zero-shot MLLM pipeline for open-domain, text-image claim verification. DEFAME operates in a six-stage process, dynamically selecting the tools and search depth to extract and evaluate textual and visual evidence. Unlike prior approaches that are text-only, lack explainability, or rely solely on parametric knowledge, DEFAME performs end-to-end verification, accounting for images in claims *and* evidence while generating structured, multimodal reports. Evaluation on the popular benchmarks VERITE, AVeriTeC, and MOCHEG shows that DEFAME surpasses all previous methods, establishing itself as the new general state-of-the-art fact-checking system for uni- and multimodal fact-checking. Moreover, we introduce a new multimodal benchmark, ClaimReview2024+, featuring claims after the knowledge cutoff of GPT-4o, avoiding data leakage. Here, DEFAME drastically outperforms the GPT-4o baselines, showing temporal generalizability and the potential for real-time fact-checking.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）
- **背景**：虚假信息泛滥，迫切需要可靠、可扩展的事实核查方案。
- **现有不足**：大多数事实核查方法局限于文本，缺乏可解释性，或仅依赖参量化知识（如大语言模型内部记忆），难以处理同时包含文本和图像的开放域声明。
- **核心问题**：如何实现对图文结合的开放域声明进行零样本、可解释、动态证据驱动的事实核查？
- **整体含义**：DEFAME 提出一种模块化、零样本的多模态大语言模型（MLLM）流水线，通过动态选择工具和搜索深度，提取并评估文本与视觉证据，生成结构化多模态报告，从而提升事实核查的准确性与可解释性。

## 2. 方法论
- **核心思想**：采用六阶段流水线设计，动态选择证据提取工具与搜索深度，结合多模态专家进行端到端验证，兼顾图像在声明和证据中的作用，并输出结构化多模态报告。
- **关键技术细节**：
  - 零样本（zero-shot）模式：无需针对特定任务微调，直接利用预训练 MLLM 的通用能力。
  - 动态工具选择：根据声明内容自动选择合适的文本和图像证据检索工具（如搜索引擎、图像识别 API 等）。
  - 证据提取与评估：分别处理文本和视觉证据，交叉验证一致性。
  - 报告生成：输出包含结构化证据链和推理过程的多模态报告，增强可解释性。
- **算法流程**（文字说明）：
  1. 接收图文联合声明。
  2. 分解声明，确定关键实体与视觉元素。
  3. 动态规划搜索策略（选择搜索引擎/图像数据库、设定搜索深度）。
  4. 并行或顺序提取文本证据与图像证据。
  5. 对每项证据进行可信度评估与逻辑推理。
  6. 综合所有证据判断声明真实性，并生成结构化报告（含引用和图像来源）。

## 3. 实验设计
- **使用的数据集/场景**：
  - **VERITE**：多模态事实核查基准。
  - **AVeriTeC**：包含图像证据的声明验证数据集。
  - **MOCHEG**：多模态常识推理与事实核查数据集。
  - **ClaimReview2024+**：新提出的基准，包含 GPT-4o 知识截止日期之后的声明，用于测试时间泛化能力，避免数据泄露。
- **对比方法**：与所有先前方法（包括仅文本、无解释性、依赖参数量知识的方法）以及 GPT-4o 基线模型进行对比。
- **基准（Benchmark）**：上述四个数据集上的准确率、F1 等指标，以及报告可解释性评估。

## 4. 资源与算力
- **文中未明确提及**：摘要和元数据中未说明使用的 GPU 型号、数量或训练时长。由于该方法是零样本流水线（不涉及微调），主要依赖推理算力，但具体消耗未披露。

## 5. 实验数量与充分性
- **实验数量**：在三个公开多模态基准（VERITE, AVeriTeC, MOCHEG）上进行了评估，并额外引入一个新基准 ClaimReview2024+。至少包含 4 组主要实验对比。
- **充分性与公平性**：
  - 覆盖了多模态和单模态场景，并与前人方法及 GPT-4o 基线比较，结果均超越先前方法。
  - 新基准设计用于测试时间泛化性，避免了数据泄露，增强了实验客观性。
  - 但未提及消融实验或对不同工具选择策略的深入分析，可能不够全面。

## 6. 主要结论与发现
- DEFAME 在所有测试基准上均超越先前方法，成为通用单模态与多模态事实核查的新 SOTA。
- 在新基准 ClaimReview2024+ 上，DEFAME 大幅超越 GPT-4o 基线，证明其具有时间泛化能力和实时事实核查潜力。
- 模块化、零样本、动态证据选择的设计能有效处理图文联合声明，并输出结构化可解释报告。

## 7. 优点
- **方法亮点**：
  - 零样本设计，无需领域微调，易于部署到新场景。
  - 动态工具选择与搜索深度自适应，避免固定搜索带来的效率或精度问题。
  - 可解释性强：生成结构化多模态报告，明确展示证据来源和推理过程。
  - 首次系统性地同时处理图像在声明和证据中的角色。
- **实验亮点**：
  - 提出新基准 ClaimReview2024+，专门测试时间泛化性，避免数据泄露。
  - 在多个公开基准上取得显著领先，验证了方法的通用性。

## 8. 不足与局限
- **实验覆盖**：未提供消融实验（如去除动态工具选择、仅文本或仅图像证据）来分析各组件贡献。
- **偏差风险**：零样本 MLLM 可能存在对特定语言或文化的偏见，文中未讨论。
- **应用限制**：
  - 依赖外部工具（搜索引擎、图像 API）的可用性和质量。
  - 实时性可能受动态搜索深度影响，难以保证极低延迟。
  - 结构化报告的可解释性依赖于 MLLM 的推理能力，复杂声明可能存在推理错误。
- **算力成本**：未说明推理时的计算开销，对实际部署的经济性缺乏评估。

（完）
