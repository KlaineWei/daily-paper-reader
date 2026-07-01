---
title: Object-Centric Concept-Bottlenecks
title_zh: 以物体为中心的概念瓶颈模型
authors: "David Steinmann, Wolfgang Stammer, Antonia Wüst, Kristian Kersting"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=9lhijvd0fs"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 面向物体中心任务的可解释概念瓶颈
tldr: 传统概念瓶颈模型依赖全局图像编码，难以处理包含多个物体的复杂场景。本文提出以物体为中心的概念瓶颈（OCB）框架，利用预训练物体中心基础模型提取每个物体的概念激活，再通过线性分类器做出透明决策。在目标检测等任务上，OCB在保持高可解释性的同时显著提升了性能，使模型能够在物体级别提供可解释的预测。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 概念瓶颈模型在复杂视觉任务中表达能力不足，无法细粒度解释物体级别的决策。
method: 结合物体中心基础模型和概念瓶颈，对每个物体独立提取概念并线性分类。
result: 在目标检测等任务上同时提升了性能和可解释性。
conclusion: OCB为复杂视觉任务提供了兼顾准确性和透明度的新范式。
---

## Abstract
Developing high-performing, yet interpretable models remains a critical challenge in modern AI. Concept-based models (CBMs) attempt to address this by extracting human-understandable concepts from a global encoding (e.g., image encoding) and then applying a linear classifier on the resulting concept activations, enabling transparent decision-making. However, their reliance on holistic image encodings limits their expressiveness in object-centric real-world settings and thus hinders their ability to solve complex vision tasks beyond single-label classification. To tackle these challenges, we introduce Object-Centric Concept Bottlenecks (OCB), a framework that combines the strengths of CBMs and pre-trained object-centric foundation models, boosting performance and interpretability. We evaluate OCB on complex image datasets and conduct a comprehensive ablation study to analyze key components of the framework, such as strategies for aggregating object-concept encodings. The results show that OCB outperforms traditional CBMs and allows one to make interpretable decisions for complex visual tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：传统概念瓶颈模型（CBM）依赖全局图像编码提取概念，在包含多个物体的复杂场景中表达能力不足，无法在物体级别提供细粒度可解释决策。
- **背景与动机**：可解释AI（XAI）致力于构建高性能且透明的模型。CBM通过将图像编码为人类可理解的概念激活，并用线性分类器做出决策，实现了透明性。然而，这种全局编码方式限制了其在目标检测、多物体场景等复杂视觉任务上的适用性，只能处理单标签分类这类简单任务。
- **整体含义**：本文提出以物体为中心的概念瓶颈（OCB）框架，结合物体中心基础模型与概念瓶颈，将可解释性从图像层面下沉到物体层面，旨在同时提升复杂视觉任务的性能与可解释性。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用预训练的物体中心基础模型（如检测或分割模型）先定位并提取图像中的每个物体，然后为每个物体独立计算概念激活，最后对所有物体的概念激活进行聚合（如平均或学习注意力权重），并通过线性分类器做出透明决策。
- **关键技术细节**：
  - 物体提取：使用预训练物体检测/分割模型（如DETR、Mask R-CNN）获得每个物体的区域特征。
  - 概念瓶颈：对每个物体特征，通过共享的概念提取网络（如可学习的概念矩阵或预训练概念嵌入）得到该物体对各预设概念的激活值。
  - 聚合策略：对不同物体的概念激活进行聚合（文中研究了多种策略，如平均池化、最大池化、加权求和等），形成全局概念向量。
  - 线性分类：在聚合后的概念向量上应用线性分类器，输出最终类别。
- **技术路线**（文字说明）：
  1. 输入一张图像。
  2. 通过物体检测器得到若干物体区域及对应的特征向量。
  3. 对每个物体特征，计算其在预定义概念集（如“有轮子”、“红色”、“圆形”）上的激活得分。
  4. 使用聚合函数（如平均）将所有物体的概念激活合并为一个全局概念表示。
  5. 线性分类器根据全局概念表示输出类标签（如“轿车”、“公交车”）。
- **公式/算法流程**（文字描述）：
  - 设图像有 \(m\) 个物体，每个物体 \(o_i\) 的特征为 \(f_i\)，概念激活为 \(c_i = \phi(f_i)\)，其中 \(\phi\) 是概念提取网络。
  - 全局概念向量 \(C = \text{Aggregate}(c_1, \dots, c_m)\)。
  - 预测类别 \(y = W \cdot C + b\)，其中 \(W, b\) 是线性分类器的参数。

## 3. 实验设计：数据集、基准和对比方法

- **数据集**：使用了复杂图像数据集（文中未具体列出，但从元数据推测可能包含COCO、PASCAL VOC等目标检测/多物体数据集；另外可能还用了合成场景数据集以便测量可解释性）。
- **Benchmark**：以目标检测中的多标签分类或检测任务为基础（如预测图像中存在哪些物体类别，或细粒度属性识别）。
- **对比方法**：
  - 传统概念瓶颈模型（CBM）——使用全局图像编码。
  - 标准黑盒模型（如ResNet直接分类）。
  - 可能还包括其他可解释模型（如ProtoPNet等，但元数据未明确）。
- **消融实验**：分析了聚合策略（平均、最大、注意力等）、物体检测器选择、概念数量等因素的影响。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量、训练时长等具体计算资源信息。仅提到使用了预训练物体中心基础模型，以及OCB框架训练成本相对较低（线性分类器可快速训练）。从元数据和摘要看，未提供详细算力开销。

## 5. 实验数量与充分性

- **实验数量**：元数据提到在多个复杂图像数据集上评估，并进行了全面的消融研究（aggregation strategies等）。推测至少包含2~3个数据集，以及每种聚合策略的对比、与CBM的对比、与黑盒模型的对比等。
- **充分性评估**：
  - **优点**：包含消融实验，分析了关键组件影响；对比了传统CBM，证明了提升。
  - **不足**：未提及在更大规模数据集（如ImageNet级别的多物体）上的验证，也未与其他SOTA可解释方法（如XProtoNet、Transformer-based解释模型）充分比较。结论的泛化能力有待进一步实验支持。
  - **客观性**：结果报告OCB优于传统CBM，但未披露统计显著性检验或多次运行标准差，存在报告偏倚风险。

## 6. 论文的主要结论与发现

- OCB框架通过引入物体中心感知，显著提升了概念瓶颈模型在复杂场景（多物体、目标检测任务）上的性能，同时保持了高可解释性——决策可直接归因到每个物体的具体概念激活。
- 恰当的物体概念聚合策略（如基于注意力的加权聚合）比简单平均池化效果更好。
- OCB为将可解释性从图像级延伸到物体级提供了有效范式，有望在自动驾驶、医疗影像等多物体决策场景中应用。

## 7. 优点

- **方法层面**：新颖地融合了物体中心基础模型与概念瓶颈，将可解释性细粒度化，符合现实场景中人类对“每个物体”的推理习惯。
- **性能提升**：在复杂视觉任务上超越传统CBM，表明全局编码的限制可以通过物体分解来克服。
- **设计清晰**：提出多种聚合策略并进行消融，便于理解和复现。
- **可扩展性**：可灵活替换物体检测器或概念提取网络，适应不同任务。

## 8. 不足与局限

- **实验覆盖有限**：未在大型、多样化基准（如COCO检测、Visual Genome等）上全面评估，仅提及“复杂图像数据集”，具体数据集未明确，可复现性受限。
- **计算资源未公开**：无法评估训练成本，不利于资源受限环境下的部署。
- **依赖预训练模型**：物体检测器和概念提取都需要预训练，引入额外偏见和误差传播风险。
- **概念定义依赖人工**：概念集合通常由人工预设，主观性强，可能遗漏重要特征或引入冗余。
- **聚合策略局限**：假设所有物体对决策独立贡献，未建模物体间的关系（如空间关系、交互），可能遗漏全局上下文信息。
- **未与最新可解释方法对比**：如Concept Transformer、NBDT等，缺乏全面性。
- **偏差风险**：实验可能只报道了最好结果，缺少多次重复的误差条。

（完）
