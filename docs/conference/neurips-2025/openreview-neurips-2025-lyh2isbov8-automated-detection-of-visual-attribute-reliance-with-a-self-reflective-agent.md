---
title: Automated Detection of Visual Attribute Reliance with a Self-Reflective Agent
title_zh: 使用自反射代理自动检测视觉属性依赖
authors: "Christy Li, Josep Lopez Camuñas, Jake Thomas Touchet, Jacob Andreas, Agata Lapedriza, Antonio Torralba, Tamar Rott Shaham"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=LyH2ISbOV8"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 自动检测视觉模型依赖的视觉属性，增强可解释性
tldr: 论文针对视觉模型可能依赖虚假相关性的问题，提出一个自动化框架，通过自反射代理系统性地生成和测试关于视觉属性的假设，利用自我评估协议验证解释是否准确，并不断迭代修正。该方法能够检测模型对特定视觉特征的意外依赖，提升了模型可解释性和鲁棒性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视觉模型可能依赖虚假特征，需要自动检测这种依赖性。
method: 提出自反射代理，迭代生成和测试视觉属性假设，并通过自我评估协议验证。
result: 有效检测视觉模型中的属性依赖。
conclusion: 该方法为模型可解释性提供了自动化的属性依赖检测工具。
---

## Abstract
When a vision model performs image recognition, which visual attributes drive its predictions? Detecting unintended reliance on specific visual features is critical for ensuring model robustness, preventing overfitting, and avoiding spurious correlations. We introduce an automated framework for detecting such dependencies in trained vision models. At the core of our method is a self-reflective agent that systematically generates and tests hypotheses about visual attributes that a model may rely on. This process is iterative: the agent refines its hypotheses based on experimental outcomes and uses a self-evaluation protocol to assess whether its findings accurately explain model behavior. When inconsistencies arise, the agent self-reflects over its findings and triggers a new cycle of experimentation. We evaluate our approach on a novel benchmark of 130 models designed to exhibit diverse visual attribute dependencies across 18 categories. Our results show that the agent's performance consistently improves with self-reflection, with a significant performance increase over non-reflective baselines. We further demonstrate that the agent identifies real-world visual attribute dependencies in state-of-the-art models, including CLIP's vision encoder and the YOLOv8 object detector.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

视觉模型在进行图像识别时，可能依赖某些视觉属性（如颜色、纹理、形状）做出预测。然而，这些属性中可能包含虚假相关性（spurious correlations），导致模型在部署时出现鲁棒性问题、过拟合或偏差。现有可解释性方法通常需要人工干预，难以自动化地发现模型意外依赖的视觉特征。为此，论文提出一个自动化框架，利用自反射代理（self-reflective agent）系统性地检测训练好的视觉模型对哪些视觉属性产生了依赖，从而提升模型可解释性和鲁棒性。

## 2. 方法论

- **核心思想**：构建一个能够自我反思和迭代的智能体，自动生成关于视觉属性的假设，通过实验测试假设，并用自我评估协议验证解释的准确性。若发现不一致，则触发新一轮实验。
- **关键技术细节**：
  1. **假设生成**：代理根据模型输出和已有知识，提出模型可能依赖的视觉属性（如“是否根据颜色判断类别”）。
  2. **实验执行**：通过设计输入扰动（如遮挡、颜色变化、纹理替换等）来测试模型对特定属性的敏感性。
  3. **自我评估**：代理评估实验结果是否一致地解释了模型行为；若存在矛盾，则进行自我反思，修正假设，并重新实验。
  4. **迭代循环**：重复“假设→实验→评估→反思”过程，直到解释与模型行为一致。
- **算法流程文字说明**：
  - 初始化：给定一个已训练的视觉模型和任务。
  - 代理生成初始属性假设。
  - 对于每个假设，设计并执行实验（如生成特定属性被移除或修改的测试图像）。
  - 收集模型在这些输入上的预测变化。
  - 代理使用自评估协议判断假设是否准确解释模型行为（例如，若模型预测完全依赖于该属性，则移除该属性应导致预测显著改变）。
  - 如果不一致，代理记录失败原因，调整假设，并重新实验。
  - 循环直到找到一组可靠的属性依赖或达到最大迭代次数。

（论文未提供具体公式，但上述文字描述了算法流程。）

## 3. 实验设计

- **数据集/场景**：构建了一个新的基准（benchmark），包含 **130个模型**，跨越 **18个类别**，这些模型被设计成表现出不同的视觉属性依赖（例如某些模型依赖颜色，某些依赖形状等）。
- **对比方法**：与没有自反射能力的基线（non-reflective baselines）进行对比，即代理不进行自我反思和迭代，仅进行单轮假设生成和实验。
- **评估指标**：主要比较模型检测属性依赖的准确率或一致性提升。

## 4. 资源与算力

论文中未明确说明使用的 GPU 型号、数量或训练时长。因此，资源与算力信息未知。

## 5. 实验数量与充分性

- **实验数量**：主要实验涉及130个模型、18个类别，并与非自反射基线对比。另外还展示了在真实先进模型（CLIP 视觉编码器和 YOLOv8 目标检测器）上的应用案例。
- **充分性**：基准设计较为系统，覆盖多种属性依赖场景，对比基线清晰。但缺少对不同类型代理（如使用不同反思策略）的消融实验，也未对代理的迭代次数敏感性进行详细分析。总体而言，实验足以证明自反射机制的提升，但深度上可进一步丰富。

## 6. 主要结论与发现

- 自反射代理的检测性能**持续提升**，且显著高于非自反射基线。
- 该方法能够有效识别真实世界先进模型（如 CLIP 和 YOLOv8）中存在的视觉属性依赖，说明其具备实用价值。
- 自我反思机制是提升检测准确性的关键，能够修正初始错误假设，逐步逼近真实依赖。

## 7. 优点

- **全自动**：无需人工标注或干预，即可自动发现模型依赖的视觉属性。
- **自省迭代**：代理能自我反思并修正假设，有效避免早期错误结论。
- **泛化性强**：在合成基准和真实先进模型上均有效。
- **可解释性增强**：输出的具体属性依赖可直接用于模型调试和鲁棒性改进。

## 8. 不足与局限

- **实验覆盖**：基准中的模型是人工设计的（可能包含了已知的依赖关系），实际应用中的复杂依赖（如高阶特征组合）可能未被覆盖。
- **偏差风险**：代理的初始假设生成可能受先验知识影响，导致偏向某些属性。
- **应用限制**：该方法目前主要针对图像分类和目标检测任务，对其他视觉任务（如分割、跟踪）的适用性未验证。
- **算力与可扩展性**：未报告计算成本；迭代过程可能在大规模模型上耗时较长。
- **资源缺失**：论文未公开代码或数据集，复现难度较大。

（完）
