---
title: "WISE: Weak-Supervision-Guided Step-by-Step Explanations for Multimodal LLMs in Image Classification"
title_zh: WISE：弱监督引导的多模态大语言模型逐步解释方法（用于图像分类）
authors: "Yiwen Jiang, Deval Mehta, Siyuan Yan, Yaling Shen, Zimu Wang, Zongyuan Ge"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.741.pdf"
tags: ["query:xai-objdet"]
score: 5.0
evidence: 为多模态大模型在图像分类中提供弱监督逐步解释
tldr: 针对现有多模态链式思维提示因依赖强标注数据集且忽视类内语义理解的问题，提出WISE方法。该方法利用概念瓶颈模型将概念表示转化为可解释的推理链，仅需弱监督即可为图像分类生成逐步解释。在十个数据集上验证了生成解释的质量和模型性能，表明该方法可推广到其他视觉任务。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.741/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.741/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1570, \"height\": 812, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.741/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1339, \"height\": 819, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.741/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.741/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 655, \"height\": 326, \"label\": \"Table\"}]"
motivation: 现有MCoT方法依赖丰富标注数据集且忽视类内语义，限制了图像分类的可解释性。
method: 通过概念瓶颈模型将概念表示重构为弱监督下的可解释推理链，生成逐步解释。
result: 在十个数据集上生成的高质量解释提升了多模态大模型的可解释性和分类性能。
conclusion: WISE为图像分类提供了一种高效的可解释方法，可推广到其他视觉任务。
---

## Abstract
Multimodal Large Language Models (MLLMs) have shown promise in visual-textual reasoning, with Multimodal Chain-of-Thought (MCoT) prompting significantly enhancing interpretability. However, existing MCoT methods rely on rationale-rich datasets and largely focus on inter-object reasoning, overlooking the intra-object understanding crucial for image classification. To address this gap, we propose WISE, a Weak-supervision-guided Step-by-step Explanation method that augments any image classification dataset with MCoTs by reformulating the concept-based representations from Concept Bottleneck Models (CBMs) into concise, interpretable reasoning chains under weak supervision. Experiments across ten datasets show that our generated MCoTs not only improve interpretability by 37% but also lead to gains in classification accuracy when used to fine-tune MLLMs. Our work bridges concept-based interpretability and generative MCoT reasoning, providing a generalizable framework for enhancing MLLMs in fine-grained visual understanding.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有MCoT（多模态链式思维）方法通常依赖人工标注或自动生成的 rationale 数据集，成本高且难以保证质量；同时它们主要关注对象间推理（inter-object reasoning），忽略了图像分类所需的对象内语义理解（intra-object understanding）。
- **核心问题**：如何自动为图像分类数据集生成高质量、可解释的自然语言推理链（MCoT），以增强多模态大语言模型（MLLM）在细粒度分类中的可解释性与准确性。
- **整体意义**：论文提出WISE方法，首次将概念瓶颈模型（CBM）的概念表示转化为弱监督引导的逐步解释，桥接了概念可解释性与生成式MCoT推理两个范式，为提升MLLM在细粒度视觉理解中的能力提供通用框架。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用多个弱监督模型（CLIP、CBM、决策树、朴素贝叶斯）对图像进行概念评分，从而构建两类决策树（类别典型性树与实例区分性树），将其合并为结构化推理路径，再通过模板转化为自然语言MCoT，最终以课程学习方式微调MLLM。
- **关键技术步骤**：
  1. **概念评分与视觉显著性筛选**：使用CLIP计算图像与概念库中每个概念的余弦相似度，得到概念得分向量；再训练softmax分类器得到每个类别对概念的权重，并确定概念极性；最终通过逻辑回归与阈值筛选出最显著的概念。
  2. **类别典型性树（Prior Tree）**：基于类别-概念先验分布P(c_m|y_n)，对每一类选择先验概率>0.5的概念，使用决策树（Gini不纯度）学习区分该类别与其他类别的最短决策路径。
  3. **实例区分性树**：分为肯定树和消除树。  
     - 肯定树：结合Prior Tree中出现在实例中的概念与实例特有的其他正概念，进一步支持分类。  
     - 消除树：当肯定树叶子仍有混淆类时，利用实例中缺失但混淆类中频繁出现的概念（负概念）来排除错误选项。  
  4. **MCoT生成**：将肯定树路径与消除树路径拼接，通过模板生成自然语言逐步推理链。
  5. **MLLM微调**：采用两阶段课程学习：第一阶段训练模型回答概念级QA对；第二阶段基于生成的MCoT进行端到端微调。

- **公式/算法**（文字说明）：通过贝叶斯先验公式P(c_m|y_n)计算类别-概念关联；决策树使用Gini不纯度递归分裂；最终MCoT路径表示为T_MCoT = T_a^+ ∥ T_e^-。

## 3. 实验设计：数据集、基准与对比方法

- **数据集**：共10个细粒度图像分类数据集：
  - 有概念标注的：CUB（200种鸟，312概念）、SkinCon（3类和9类，48概念）、LAD（5个子集：动物、电子产品、发型、水果、车辆，共230类359概念）。
  - 无概念标注的：Oxford-Flowers（102类）、Oxford-Pets（37类），概念库由GPT-4o自动构建。
- **基准与对比方法**：
  - 弱监督基线：CLIP零样本、CLIP-based CBM、CLIP-based决策树、CLIP-based朴素贝叶斯。
  - MLLM基线：零样本输入输出（ZS-IO）、零样本MCoT（ZS-MCoT，添加“Let's think step by step”及概念指导）、指令微调无MCoT（IT-IO）。
  - 目标MLLM：Qwen2-VL-7B-Instruct。
- **评估指标**：分类准确率（acc.）和可解释性（intp.，即推理链中概念极性与专家标注的一致率，相当于概念精度）。

## 4. 资源与算力

- 文中明确说明：全部实验使用4张NVIDIA RTX A5000 GPU。
- 微调细节：LoRA（秩8），训练10个epoch，batch size=16，学习率1e-4。
- 弱监督模型使用CLIP ViT-L/14（参数量约为目标MLLM的5%），SkinCon使用领域预训练模型MAKE。

## 5. 实验数量与充分性

- **实验数量**：主表（表1）覆盖8个有概念标注的数据集，每个数据集报告了弱监督（4种）和MLLM（4种）的准确率与可解释性；表2分析了MCoT的正负概念精度及效率；表3在CUB上进行了5组消融实验（去除显著性、打乱顺序、替换为描述、仅实例树、仅类别树）；此外还评估了2个无概念标注数据集。
- **充分性与公平性**：实验设计较为全面，涵盖了多种弱监督与MLLM设置，消融实验验证了各组件的必要性。但是缺少与其他同类MCoT生成方法的直接对比（如与CoMT等），仅与自身变体比较；同时仅在单一MLLM架构（Qwen2-VL-7B）上验证，未评估泛化到其他模型（如LLaVA等）。总体上实验充分，但存在一定局限性。

## 6. 论文的主要结论与发现

- WISE生成的MCoT将MLLM的可解释性平均提升37%（从零样本MCoT的50.75%提升到87.83%），同时分类准确率平均提高0.69%（相比无MCoT的指令微调）。
- 弱监督（尤其是决策树）能有效引导MLLM习得概念驱动推理；MCoT的正负概念精度分别达到83%和87%，表明模型平衡使用支持性与反事实推理。
- 推理链非常高效：每张图像平均仅使用8个概念进行推理，但动态覆盖95%的概念库，避免了CBM静态全概念评分的冗余。
- 消融实验表明：视觉显著性选择、概念顺序、树结构都对可解释性至关重要，而简单的描述式MCoT无效。

## 7. 优点

1. **创新性**：首次桥接CBM与MCoT，利用弱监督自动生成推理链，无需人工标注rationale。
2. **通用性**：可应用于任何图像分类数据集（仅需类别标签），并通过LLM自动构建概念库。
3. **高效性**：推理链极简（平均8概念），动态选择概念，可扩展性强。
4. **可解释性与准确性兼得**：不同于CBM通常牺牲准确率换取可解释性，WISE在提升解释性的同时小幅提升了准确率。
5. **人类对齐**：推理链模仿人类先典型后区分、结合正反证据的判决过程，具有透明性。

## 8. 不足与局限

1. **依赖概念库质量**：对无标注数据集使用LLM生成概念，若概念覆盖不全或存在冗余，将限制区分能力（尤其SkinCon中疾病共享相似概念模式）。
2. **数据集标签空间固定**：当整合多个数据集时可能产生概念冲突（如在某一数据集中不存在的类别在另一数据集中作为干扰项出现）。
3. **模型泛化性不足**：实验仅在Qwen2-VL-7B上执行，未验证在其他MLLM（如LLaVA、GPT-4V等）上的效果。
4. **零样本MCoT baseline较弱**：文中零样本MCoT可解释性仅50.75%，但实际应用中更好的提示工程或更大模型可能改善，因而37%的提升幅度可能被高估。
5. **幻觉风险**：当概念级精度下降到50.75%时（如某些数据集），推理链可能引入错误信息并传播到最终分类。
6. **未与最新MCoT生成方法对比**：仅与自身变体及简单基线比较，缺乏与如CoMT等专门针对MCoT生成的工作的直接比较。

（完）
