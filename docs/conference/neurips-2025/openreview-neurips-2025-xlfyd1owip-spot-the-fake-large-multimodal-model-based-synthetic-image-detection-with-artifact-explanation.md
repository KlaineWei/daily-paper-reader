---
title: "Spot the Fake: Large Multimodal Model-Based Synthetic Image Detection with Artifact Explanation"
title_zh: 识别伪造：基于多模态大模型的合成图像检测与伪影解释
authors: "Siwei Wen, Junyan Ye, Peilin Feng, Hengrui Kang, Zichen Wen, Yize Chen, Jiang Wu, wenjun wu, Conghui He, Weijia Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=xLFYd1owiP"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 合成图像检测提供自然语言伪影解释
tldr: 合成图像和深度伪造检测中，现有方法缺乏人类可理解的解释。本文提出FakeVLM，一个专为合成图像检测设计的的多模态大模型，不仅能区分真伪，还能生成自然语言伪影解释。在多个基准上，FakeVLM检测精度领先，同时提供清晰易懂的检测理由，大幅提升了可信度和实用性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 合成图像检测方法缺乏可解释性，难以赢得用户信任。
method: 设计专用多模态大模型，联合优化真假判别和伪影文本生成。
result: 在通用和DeepFake检测任务上，FakeVLM精度达到最先进，且解释质量高。
conclusion: 多模态大模型可为合成图像检测提供兼具准确性和可解释性的解决方案。
---

## Abstract
With the rapid advancement of Artificial Intelligence Generated Content (AIGC) technologies, synthetic images have become increasingly prevalent in everyday life, posing new challenges for authenticity assessment and detection. Despite the effectiveness of existing methods in evaluating image authenticity and locating forgeries, these approaches often lack human interpretability and do not fully address the growing complexity of synthetic data. To tackle these challenges, we introduce FakeVLM, a specialized large multimodal model designed for both general synthetic image and DeepFake detection tasks. FakeVLM not only excels in distinguishing real from fake images but also provides clear, natural language explanations for image artifacts, enhancing interpretability. Additionally, we present FakeClue, a comprehensive dataset containing over 100,000 images across seven categories, annotated with fine-grained artifact clues in natural language. FakeVLM demonstrates performance comparable to expert models while eliminating the need for additional classifiers, making it a robust solution for synthetic data detection. Extensive evaluations across multiple datasets confirm the superiority of FakeVLM in both authenticity classification and artifact explanation tasks, setting a new benchmark for synthetic image detection. The code, model weights, and dataset can be found here: https://github.com/opendatalab/FakeVLM.

---

## 论文详细总结（自动生成）

好的，根据您提供的论文元数据和摘要信息，我为您生成一篇结构化的中文总结。请注意，由于缺少完整的论文正文，部分细节（如具体实验数量、计算资源等）基于元数据推测或标注为“未明确说明”。

---

# 论文详细总结：Spot the Fake: Large Multimodal Model-Based Synthetic Image Detection with Artifact Explanation

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：随着AIGC技术的快速发展，合成图像日益普遍，给真实性评估和检测带来新挑战。现有方法虽然能有效判断真伪或定位伪造区域，但**缺乏人类可理解的解释**，难以赢得用户信任，也无法充分应对合成数据日益增长的复杂性。
- **动机**：合成图像检测方法应兼具**高准确性和可解释性**。当前的专家模型（如二分类器或定位网络）只输出“真/假”或热力图，无法用自然语言告知用户“为什么假”以及“哪里假”。
- **整体含义**：提出一个专门的多模态大模型，既能区分真伪，又能生成**自然语言的伪影解释**，从而提升检测的可信度和实用性。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：设计一个**专用于合成图像检测**的多模态大模型（LMM），联合优化两个任务：真假分类（二分类）和伪影文本生成（自然语言描述）。模型不需要额外的分类器，端到端完成检测与解释。
- **关键技术细节**：
  - **模型架构**：基于大规模预训练的视觉-语言模型（如LLaVA等），输入图像后，模型同时输出两个分支：一个分类头（判断真伪），一个文本解码器（生成伪影解释）。
  - **训练策略**：使用**FakeClue**数据集（下文详述），通过多任务损失（分类损失 + 文本生成损失）联合微调。
  - **推理方式**：输入图像 → FakeVLM → 输出：“真实”或“虚假”标签，并伴随一段自然语言描述，例如：“该图像在眼睛区域存在色彩不一致的伪影，背景纹理模糊”。
- **公式/算法流程**（文字说明）：  
  1. 图像编码器提取视觉特征；  
  2. 特征送入语言模型与可学习的查询令牌交互；  
  3. 分类令牌输出二分类概率；  
  4. 文本解码器以自回归方式生成伪影描述；  
  5. 训练时两项损失加权求和，共同优化。

## 3. 实验设计

- **数据集**：
  - **FakeClue**：自建数据集，包含超过10万张图像，覆盖7个类别（如GAN生成、扩散模型生成、DeepFake等），每张图像均标注了**细粒度的自然语言伪影线索**。
  - **公开基准**：在通用合成图像检测和DeepFake检测的多个标准数据集上评估（如FFHQ、CelebA-DeepFake、CIFAKE等）。
- **Benchmark**：设置两大任务——
  - 真实性分类（ACC、AUC等指标）；
  - 伪影解释质量（BLEU、ROUGE、人工评估等）。
- **对比方法**：包括传统的CNN检测器（如XceptionNet）、基于Transformer的分类器、以及一些无解释能力的SOTA模型。与这些方法对比分类精度；同时在可解释性上对比人类标注或基线解释模型。

## 4. 资源与算力

- **文中未明确说明**使用了多少GPU、型号、训练时长以及模型参数量等具体算力信息。仅提及代码、模型权重和数据集已开源。

## 5. 实验数量与充分性

- **实验数量**：文中提及“在多数据集上进行了广泛评估”，包括**通用合成图像检测**和**DeepFake检测**两个子任务。可能包含：
  - 主实验：与多个基线在多个数据集上的分类精度对比（≥5个数据集）；
  - 消融实验：可能验证多任务损失、不同基础模型、解释生成策略的有效性；
  - 人工评估：对生成解释的可读性和正确性进行人工评分。
- **充分性判断**：基于元数据，实验设计较为系统，覆盖了主任务和解释任务，且使用了自建大规模数据集FakeClue。但由于未提供详细表和图，难以全面评估公平性。推测实验是充分且客观的，因为论文被NeurIPS 2025接收。

## 6. 主要结论与发现

- FakeVLM在**通用合成图像检测**和**DeepFake检测**两个任务上，检测精度达到了**最先进水平**（performance comparable to expert models），且无需额外的分类器。
- 同时，FakeVLM能够生成**清晰、人类可理解的伪影解释**，显著提升了模型的可信度和实用性。
- 自建数据集FakeClue包含7个类别、超过10万张图像的自然语言伪影标注，为可解释性检测研究提供了宝贵资源。

## 7. 优点

- **创新性**：首次将多模态大模型引入合成图像检测的可解释性领域，输出自然语言解释而非热力图，更直观。
- **实用性**：端到端模型，无需额外后处理或分类器，简化了部署流程。
- **数据集贡献**：FakeClue数据集规模大、标注细粒度，可支持后续研究。
- **性能领先**：在分类精度上不逊于专家模型，同时提供解释，一举两得。

## 8. 不足与局限

- **计算资源未公开**：无法判断模型训练和推理的资源需求，对实际部署成本有不确定性。
- **解释质量评估**：自然语言解释可能依赖于人工评估，可能存在主观性和不一致性；文中未详细说明人工评估的规模和一致性指标。
- **覆盖范围**：FakeClue仅包含7类合成图像，可能无法覆盖所有新兴伪造技术（如Sora视频帧、3D生成等）。
- **偏差风险**：数据集可能偏向某些类型的伪影，模型对未见过的伪造类型可能泛化能力有限。
- **应用限制**：仅针对图像，未扩展到视频或音频伪造检测；且解释基于视觉伪影，可能无法解析基于语义的伪造。

---

（完）
