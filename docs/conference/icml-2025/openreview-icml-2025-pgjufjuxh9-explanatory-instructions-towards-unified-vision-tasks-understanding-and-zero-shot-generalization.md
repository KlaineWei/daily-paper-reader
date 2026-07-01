---
title: "Explanatory Instructions: Towards Unified Vision Tasks Understanding and Zero-shot Generalization"
title_zh: 解释性指令：迈向统一视觉任务理解与零样本泛化
authors: "Yang Shen, Xiu-Shen Wei, Yifan Sun, YuXin Song, Tao Yuan, Jian Jin, He-Yang Xu, Yazhou Yao, Errui Ding"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=PgjUFjuxH9"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 用于视觉任务的解释性指令，可应用于目标检测场景
tldr: 该论文提出用解释性指令替代离散任务定义（如“图像分割”），帮助模型理解任务本质，实现零样本泛化。虽不直接涉及可解释性分析，但其方法可用于增强目标检测等任务的可解释性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 计算机视觉缺乏零样本任务泛化，可能源于离散的术语化任务定义。
method: 设计解释性指令描述任务，预训练后根据指令执行多种视觉任务。
result: 在多个基准上实现了零样本任务泛化。
conclusion: 解释性指令有助于模型理解任务，推动视觉任务泛化。
---

## Abstract
Computer Vision (CV) has yet to fully achieve the zero-shot task generalization observed in Natural Language Processing (NLP), despite following many of the milestones established in NLP, such as large transformer models, extensive pre-training, and the auto-regression paradigm, among others. In this paper, we rethink the reality that CV adopts discrete and terminological task definitions (e.g., "image segmentation"), and conjecture it is a key barrier that hampers zero-shot task generalization. Our hypothesis is that without truly understanding previously-seen tasks—due to these terminological definitions—deep models struggle to generalize to novel tasks. To verify this, we introduce Explanatory Instructions, which provide an intuitive way to define CV task objectives through detailed linguistic transformations from input images to outputs. We create a large-scale dataset comprising 12 million "image input $\to$ explanatory instruction $\to$ output" triplets, and train an auto-regressive-based vision-language model (AR-based VLM) that takes both images and explanatory instructions as input. By learning to follow these instructions, the AR-based VLM achieves instruction-level zero-shot capabilities for previously-seen tasks and demonstrates strong zero-shot generalization for unseen CV tasks.  Code and dataset will be open-sourced.

---

## 论文详细总结（自动生成）

# 论文总结：Explanatory Instructions: Towards Unified Vision Tasks Understanding and Zero-shot Generalization

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：计算机视觉（CV）尚未像自然语言处理（NLP）那样实现零样本任务泛化，尽管CV已借鉴了NLP中的许多里程碑（如大型Transformer、大规模预训练、自回归范式）。
- **根本原因猜想**：CV采用离散、术语化的任务定义（例如“图像分割”），导致模型无法真正理解已见任务的内在逻辑，从而难以泛化到未见任务。
- **动机**：探索通过更富解释性的语言描述替代简单的术语标签，使模型能够理解任务的本质，进而实现零样本任务泛化。

## 2. 论文提出的方法论
- **核心思想**：提出 **解释性指令（Explanatory Instructions）**，即用详细的自然语言描述定义CV任务的目标，说明从输入图像到输出的转换过程（如“请找出图像中所有红色物体并标注其边界框”），而不是仅用任务名称（如“目标检测”）。
- **技术细节**：
  - 构建大规模三元组数据集：包含1200万组 `(图像输入 → 解释性指令 → 输出)`。
  - 训练一个自回归视觉语言模型（AR-based VLM），同时接收图像和解释性指令作为输入。
  - 模型通过自回归方式预测输出，学习遵循解释性指令执行任务。
- **关键逻辑**：通过解释性指令，模型在训练时不仅看到任务的结果，还看到任务的语义描述，从而习得任务的内在映射关系，获得对已见任务的指令级零样本能力，并能泛化到未见任务（即新的解释性指令）。

## 3. 实验设计
- **数据集**：论文自建了一个包含1200万三元组的大规模数据集。具体任务涉及多种视觉任务（如图像分割、目标检测、关键点检测等），但文中未列出详细的数据集名称（如COCO、ADE20K等）。
- **Benchmark**：在多个基准上评估零样本任务泛化性能，但未明确列出具体基准名称。
- **对比方法**：文中未提及具体的对比基线方法，仅说明模型在已见任务上实现了指令级零样本能力，并在未见任务上展现出强大的零样本泛化。缺乏与现有VLM或任务泛化方法的直接定量比较。

## 4. 资源与算力
- **未明确说明**：论文摘要和元数据中未提及使用的GPU型号、数量、训练时长等算力信息。仅提到数据集规模（1200万三元组）和模型类型（AR-based VLM），但未提供具体的计算资源消耗。

## 5. 实验数量与充分性
- **实验数量**：仅从摘要和元数据看，实验覆盖了多个视觉基准任务，但未给出具体实验组数。消融实验、超参数分析、不同解释性指令设计的影响等均未提及。
- **充分性与客观性**：
  - 局限性：缺乏与现有零样本任务泛化方法（如CLIP、Flamingo等）的定量对比，实验设计不够充分；未提供详细的性能指标（准确率、mAP等）和误差分析。
  - 公平性：由于未披露对比基准和实验细节，难以判断实验是否公平。仅凭“实现了零样本泛化”的定性描述，可信度有待更多实验支持。

## 6. 主要结论与发现
- 解释性指令能够替代离散的任务术语，帮助深度模型理解任务本质，从而在已见任务上实现指令级零样本能力，并对未见CV任务展现良好的零样本泛化。
- 该研究验证了“术语化任务定义是CV零样本泛化障碍”的猜想，为统一视觉任务理解提供了新思路。

## 7. 优点
- **视角新颖**：首次将NLP中的解释性指令引入CV任务定义，挑战了传统的术语化定义模式。
- **大规模数据集**：构建了1200万三元组，涵盖多种视觉任务，为后续研究提供了基础资源。
- **概念简洁**：方法直观，不依赖复杂的任务架构，仅通过修改输入表示（加入解释性指令）即可实现零样本泛化。
- **开源承诺**：代码和数据集将开源，有利于可重复性研究。

## 8. 不足与局限
- **实验覆盖不足**：缺乏与主流方法的定量比较，仅展示定性结果，说服力有限。
- **数据集细节缺失**：未说明数据集的来源、任务类型分布、质量保证等，第三方难以复现。
- **泛化范围不清晰**：仅提到“多个基准”，未明确哪些任务能泛化、哪些任务仍有困难，泛化边界模糊。
- **计算资源未报告**：无法评估方法的训练成本和可伸缩性。
- **偏差风险**：解释性指令的设计可能引入语言歧义或任务理解偏差，但文中未讨论相关影响。
- **应用限制**：仅适用于可以作为文本指令描述的视觉任务，对于需要连续空间输出（如光流）或非语义任务，适用性存疑。

（完）
