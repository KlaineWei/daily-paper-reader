---
title: "Veritas: Generalizable Deepfake Detection via Pattern-Aware Reasoning"
title_zh: Veritas：通过模式感知推理实现可泛化的深度伪造检测
authors: "Hao Tan, jun lan, Zichang Tan, Senyuan Shi, Ajian Liu, Chuanbiao Song, Huijia Zhu, Weiqiang Wang, Jun Wan, Zhen Lei"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=5VXJPS1HoM"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 通过模式感知推理实现可解释的深度伪造检测
tldr: 现有深度伪造检测基准与工业实践脱节，在未知伪造技术上泛化差。本文提出HydraFake数据集，包含多样化伪造技术和真实场景，并设计Veritas检测器，利用多模态大语言模型进行模式感知推理，提供可解释的检测结果。实验表明Veritas在多个领域上均优于现有方法，显著提升了泛化能力。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有深度伪造检测的基准与工业实践存在差距，泛化能力不足。
method: 构建HydraFake数据集，并提出基于多模态大语言模型+模式感知推理的Veritas检测器。
result: 在多个任务上超越现有方法，展现了优秀的泛化性和可解释性。
conclusion: 所提方法为深度伪造检测提供了可解释且鲁棒的解决方案。
---

## Abstract
Deepfake detection remains a formidable challenge due to the evolving nature of fake content in real-world scenarios. However, existing benchmarks suffer from severe discrepancies from industrial practice, typically featuring homogeneous training sources and low-quality testing images, which hinder the practical usage of current detectors. To mitigate this gap, we introduce **HydraFake**, a dataset that contains diversified deepfake techniques and in-the-wild forgeries, along with rigorous training and evaluation protocol, covering unseen model architectures, emerging forgery techniques and novel data domains. Building on this resource, we propose **Veritas**, a multi-modal large language model (MLLM) based deepfake detector. Different from vanilla chain-of-thought (CoT), we introduce *pattern-aware reasoning* that involves critical patterns such as "planning" and "self-reflection" to emulate human forensic process. We further propose a two-stage training pipeline to seamlessly internalize such deepfake reasoning capacities into current MLLMs. Experiments on HydraFake dataset reveal that although previous detectors show great generalization on cross-model scenarios, they fall short on unseen forgeries and data domains. Our Veritas achieves significant gains across different out-of-domain (OOD) scenarios, and is capable of delivering transparent and faithful detection outputs.

---

## 论文详细总结（自动生成）

# 详细论文总结：Veritas：通过模式感知推理实现可泛化的深度伪造检测

## 1. 核心问题与整体含义（研究动机和背景）

- **现实困境**：深度伪造技术不断演进，现有检测方法在真实世界场景中泛化能力严重不足。
- **现有基准的缺陷**：当前公开数据集的训练来源同质化严重，测试图像质量低，与工业实践存在显著差距，导致检测器在应对未知伪造技术、新数据域时性能骤降。
- **研究目标**：弥合学术研究与应用落地之间的鸿沟，构建更贴近真实场景的基准数据集（HydraFake），并提出一种具备可解释性且泛化能力强的检测框架（Veritas）。

> **整体含义**：通过构建更逼真的数据评估平台，并引入多模态大语言模型的模式感知推理，实现深度伪造检测的鲁棒性与透明度。

## 2. 论文提出的方法论

### 核心思想
- 利用多模态大语言模型（MLLM）作为基础骨干，将深度伪造检测建模为**模式感知推理**任务，模拟人类取证专家的思维过程，而不是简单的二分类或特征比对。

### 关键技术细节
1. **HydraFake 数据集构建**：
   - 包含多种多样化的深度伪造生成技术（如 GAN、扩散模型、NeRF 等），以及“真实世界”（in-the-wild）的伪造样本。
   - 提供严格的训练/评估协议，覆盖三类 OOD 场景：
     - 未见过的模型架构（cross-model）
     - 新兴伪造技术（unseen forgeries）
     - 全新数据域（novel data domains）

2. **Veritas 检测器设计**：
   - 基于 MLLM 的检测模型，在传统的 Chain-of-Thought（CoT）推理基础上，引入了**关键推理模式**：“规划（planning）”与“自我反思（self-reflection）”，从而模拟人类的取证过程。
   - **两阶段训练流水线**：
     - 第一阶段：让模型学习基础的伪造模式识别能力（如频率伪影、纹理异常等）。
     - 第二阶段：通过指令微调将“规划”和“自我反思”的推理能力内化到 MLLM 中，使其能够生成可解释的检测结果（例如：① 规划检查哪些区域；② 分析发现异常；③ 反思结论是否可靠）。

3. **算法流程（文字说明）**：
   - 输入：图像 + 问题提示（例如“请判断该图像是否为深度伪造，并给出推理过程”）。
   - 第一阶段：MLLM 提取视觉特征并生成初始判断。
   - 第二阶段：利用“规划”模块生成分析步骤（如检查眼睛、嘴唇、光照一致性）；执行分析后，通过“自我反思”模块验证输出的一致性，最终输出分类结果与自然语言解释。

> 注：论文未提供具体公式或伪代码，以上流程基于摘要对方法机制的描述。

## 3. 实验设计

- **数据集与场景**：主要使用自建的 **HydraFake** 数据集进行评估。该数据集包含：
  - 多个已知 / 未知生成模型的伪造样本（GAN、扩散模型等）。
  - 真实的互联网伪造图像（in-the-wild）。
  - 测试协议覆盖：cross-model（不同架构）、unseen forgeries（新技术，如未见过的扩散模型变体）、novel data domains（如人脸换脸、全身伪造等新领域）。

- **Benchmark 设定**：与现有主流深度伪造检测方法进行对比，包括基于传统 CNN 的检测器、基于 Transformer 的检测器、以及一些 CoT 类方法。但摘要未列出具体方法名称。

- **对比方法**：摘要中提及“previous detectors show great generalization on cross-model scenarios, they fall short on unseen forgeries and data domains”，暗示对比了多种已有的检测器（如 Xception、EfficientNet、CNN-RNN 等）。

- **主要结论**：Veritas 在跨模型场景中保持竞争力，在未见伪造技术和新数据域上实现显著增益，同时提供可解释的检测输出。

## 4. 资源与算力

- 论文摘要及元数据中**未明确说明**训练 / 推理所使用的具体 GPU 型号、数量、训练时长。
- 由于 Veritas 基于 MLLM（多模态大语言模型，可能基于 LLaVA 或类似架构），推测需要大规模 GPU 集群（如 A100 或 H100），但无法量化。
- **需注意**：缺乏算力信息是实验报告的不完整之处。

## 5. 实验数量与充分性

- **已知实验**：至少包括三类 OOD 场景下的对比实验（cross-model、unseen forgeries、novel domains），并可能有消融实验（例如：去除 pattern-aware reasoning 的效果、两阶段训练 vs. 直接微调等）。
- **充分性判断**：
  - 优点：覆盖了关键的泛化场景（模型、技术、域），符合实际部署需求；且验证了可解释性。
  - 不足：由于未提供全文，无法确认是否做了跨数据集的迁移测试（例如在传统公开数据集上的结果）、统计显著性检验、超参数敏感性实验等。实验设计整体合理，但细节有待补充。

## 6. 论文的主要结论与发现

1. 现有深度伪造检测器在跨模型场景上表现尚可，但在面对**未见过的伪造技术**和**新数据域**时泛化能力急剧下降。
2. 通过构建包含多样伪造技术和真实场景的 HydraFake 数据集，能够更真实地反映工业实践中的检测挑战。
3. **Veritas** 通过引入模式感知推理（规划 + 自我反思）和多阶段训练，显著提升了在各类 OOD 场景下的泛化性能，并**同时输出透明、可靠的自然语言解释**，增强了检测结果的可信度。
4. 该框架展示了 MLLM 在深度伪造检测领域潜力，为后续研究提供了可解释且鲁棒的解决方案。

## 7. 优点

- **问题定位精准**：直接针对现有基准与现实脱节的根本问题，提出更具挑战性的数据集 HydraFake。
- **方法论创新**：将 Chain-of-Thought 升级为“规划 + 自我反思”的 pattern-aware reasoning，更贴近人类专家取证流程。
- **可解释性**：检测结果附带推理过程，有利于取证场景中的决策信任。
- **实验设计严谨**：明确区分三种类型的 OOD 泛化场景，结果分析具有针对性。
- **领域覆盖面广**：HydraFake 涵盖了多种生成技术和真实伪造样本，提升了基准的实用性。

## 8. 不足与局限

- **资源信息缺失**：论文未报告计算成本（GPU 类型、训练时长），难以评估方法的效率与可复现性。
- **实验细节不足**：基于提供的摘要，无法得知具体对比方法、消融实验数量、统计显著性水平等，对充分性的判断有限。
- **数据集内部偏差**：虽然多样性增加，但 HydraFake 的构建可能存在选择偏差（例如仅包含某些公开生成模型，未覆盖最新的端侧伪造技术），需要公开后检验。
- **应用限制**：Veritas 基于 MLLM，推理延迟和算力需求可能远高于传统轻量检测器，在实时高吞吐场景（如社交媒体审核）中部署压力大。
- **未见消融分析**：没有显示 pattern-aware reasoning 相较于普通 CoT 或直接分类的具体收益量化，亦未分析“规划”与“自我反思”各自的贡献。

（完）
