---
title: "Veritas: Generalizable Deepfake Detection via Pattern-Aware Reasoning"
title_zh: Veritas：基于模式感知推理的通用深度伪造检测
authors: "Hao Tan, jun lan, Zichang Tan, Senyuan Shi, Ajian Liu, Chuanbiao Song, Huijia Zhu, Weiqiang Wang, Jun Wan, Zhen Lei"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=5VXJPS1HoM"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 基于模式感知推理的深度伪造检测，具有可解释性
tldr: 针对深度伪造检测泛化性差，提出Veritas多模态大语言模型检测器。通过模式感知推理生成可解释判别依据，并构建了包含多样化伪造技术的HydraFake数据集。在多个跨域测试中显著超越现有方法，推理过程可解释。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有检测器难以泛化到新兴伪造技术。
method: 多模态大语言模型结合模式感知推理，利用HydraFake数据集训练。
result: 在多个跨域和未知伪造测试中达到SOTA。
conclusion: 模式感知推理提升深度伪造检测的泛化和可解释性。
---

## Abstract
Deepfake detection remains a formidable challenge due to the evolving nature of fake content in real-world scenarios. However, existing benchmarks suffer from severe discrepancies from industrial practice, typically featuring homogeneous training sources and low-quality testing images, which hinder the practical usage of current detectors. To mitigate this gap, we introduce **HydraFake**, a dataset that contains diversified deepfake techniques and in-the-wild forgeries, along with rigorous training and evaluation protocol, covering unseen model architectures, emerging forgery techniques and novel data domains. Building on this resource, we propose **Veritas**, a multi-modal large language model (MLLM) based deepfake detector. Different from vanilla chain-of-thought (CoT), we introduce *pattern-aware reasoning* that involves critical patterns such as "planning" and "self-reflection" to emulate human forensic process. We further propose a two-stage training pipeline to seamlessly internalize such deepfake reasoning capacities into current MLLMs. Experiments on HydraFake dataset reveal that although previous detectors show great generalization on cross-model scenarios, they fall short on unseen forgeries and data domains. Our Veritas achieves significant gains across different out-of-domain (OOD) scenarios, and is capable of delivering transparent and faithful detection outputs.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有深度伪造检测方法在真实场景中泛化能力不足，尤其在面对新兴伪造技术、未知模型架构和不同数据域时性能急剧下降。
- **研究背景**：当前基准测试存在严重缺陷——训练数据源同质化、测试图像质量低，导致模型实际部署效果与实验室评测严重脱节。
- **整体含义**：本文旨在弥合学术研究与工业实践之间的差距，通过构建更真实的基准和提出可解释、泛化性强的检测框架，推动深度伪造检测走向实用化。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用多模态大语言模型（MLLM）的推理能力，引入“模式感知推理”（Pattern-Aware Reasoning）模拟人类取证过程，从而提升检测的泛化性和可解释性。
- **关键技术细节**：
  - **Veritas架构**：基于MLLM（具体模型未说明，推测为视觉-语言联合模型）构建检测器，输出不仅是真伪标签，还包括可解释的判别依据。
  - **模式感知推理**：区别于传统链式思维（Chain-of-Thought, CoT），包含“规划”（planning）和“自我反思”（self-reflection）等关键步骤，模仿人类专家逐步分析伪造痕迹。
  - **两阶段训练流水线**：第一阶段可能学习基础视觉-语言对齐，第二阶段通过定制数据集（HydraFake）内化深度伪造推理能力。
- **无公式/算法流程文字说明**：输入图像→MLLM编码→模式感知推理链（规划、局部特征分析、矛盾检测、自我反思）→生成真伪判断与解释文本。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - **HydraFake**：自建数据集，包含多种深度伪造技术（GAN、扩散模型等）和野外伪造样本，覆盖未见模型架构、新兴伪造技术和新数据域。
  - 训练和评估协议严格：跨模型、跨伪造技术、跨数据域评估。
- **Benchmark**：HydraFake数据集本身作为主要评估基准，同时可能涉及现有公开数据集（但摘要未提及具体名称）。
- **对比方法**：未列出具体方法名称，但提到“previous detectors”在跨模型场景表现好，但在未见伪造和数据域上失败。Veritas在所有跨域场景（OOD）上取得显著提升。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据未提及GPU型号、数量、训练时长等计算资源信息。若需完整评估，需查阅全文。

## 5. 实验数量与充分性

- **实验数量**：至少包括三类OOD场景（跨模型、跨伪造技术、跨数据域）的对比实验，以及模式感知推理的消融分析（推测）。
- **充分性评估**：
  - 优点：覆盖多维度泛化挑战，且使用自建高质量数据集，评估协议严格。
  - 不足：摘要未给出具体数值（如准确率、AUC等），也未说明是否在多个现有基准上复现比较，可能缺乏与公开SOTA的全面对比。

## 6. 论文的主要结论与发现

- 现有检测器在跨模型场景下泛化尚可，但在未曾见过的伪造技术和数据域上表现较差。
- Veritas通过模式感知推理，在多类OOD场景下达到目前最优水平（SOTA）。
- 模型能够输出透明、可信的检测结果，具备可解释性，有助于实际应用中的信任建立。

## 7. 优点：方法或实验设计上的亮点

- **可解释性**：生成推理链而非简单二分类，符合人类取证逻辑，便于后续分析和模型审计。
- **泛化性**：训练数据HydraFake多样化，结合推理机制，有效应对未见伪造变体。
- **实用性导向**：主动解决学术界评估与现实部署的差异，数据集设计贴近工业场景。
- **创新推理范式**：模式感知推理比普通CoT更能捕获局部伪造模式，提升推理质量。

## 8. 不足与局限

- **计算成本**：MLLM推理复杂度高，可能不适合实时或资源受限场景。
- **数据集依赖**：HydraFake的覆盖面是否能代表未来所有新兴伪造技术仍存疑，存在过时风险。
- **实验透明度**：未提供具体性能指标和对比方法细节，无法独立复现验证结果。
- **消融分析不完整**：模式感知推理各组件（规划、自反思）的独立贡献未在摘要中量化。
- **领域限制**：仅针对图像/视频深度伪造，未涉及音频或多模态伪造。

（完）
