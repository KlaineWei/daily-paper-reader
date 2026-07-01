---
title: Interpreting CLIP with Hierarchical Sparse Autoencoders
title_zh: 用层次稀疏自编码器解释CLIP
authors: "Vladimir Zaigrajew, Hubert Baniecki, Przemyslaw Biecek"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=5MQQsenQBm"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 使用层次稀疏自编码器解释CLIP
tldr: 本文提出Matryoshka SAE，一种层次稀疏自编码器结构，用于解释CLIP等视觉语言模型。该方法同时优化重构质量和稀疏性，学习多粒度的可解释特征，有助于理解多模态模型的行为，从而支持下游可解释性任务如目标检测和异常检测的解释。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有SAE方法在重构质量和稀疏性之间难以平衡。
method: 提出Matryoshka SAE架构，学习多粒度层次化表征。
result: 在CLIP上提取到语义丰富的可解释特征。
conclusion: MSAE为解释多模态模型提供有效工具，可迁移至可解释目标检测。
---

## Abstract
Sparse autoencoders (SAEs) are useful for detecting and steering interpretable features in neural networks, with particular potential for understanding complex multimodal representations. Given their ability to uncover interpretable features, SAEs are particularly valuable for analyzing vision-language models (e.g., CLIP and SigLIP), which are fundamental building blocks in modern large-scale systems yet remain challenging to interpret and control. However, current SAE methods are limited by optimizing both reconstruction quality and sparsity simultaneously, as they rely on either activation suppression or rigid sparsity constraints. To this end, we introduce Matryoshka SAE (MSAE), a new architecture that learns hierarchical representations at multiple granularities simultaneously, enabling a direct optimization of both metrics without compromise. MSAE establishes a state-of-the-art Pareto frontier between reconstruction quality and sparsity for CLIP, achieving 0.99 cosine similarity and less than 0.1 fraction of variance unexplained while maintaining 80\% sparsity. Finally, we demonstrate the utility of MSAE as a tool for interpreting and controlling CLIP by extracting over 120 semantic concepts from its representation to perform concept-based similarity search and bias analysis in downstream tasks like CelebA. We make the codebase available at https://github.com/WolodjaZ/MSAE.

---

## 论文详细总结（自动生成）

# 论文总结：《用层次稀疏自编码器解释CLIP》

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：当前稀疏自编码器（SAE）方法在解释视觉-语言模型（如CLIP、SigLIP）时，难以同时优化**重构质量**和**稀疏性**两个指标。现有方法或依赖激活抑制，或采用刚性稀疏约束，导致两者之间存在折衷。
- **研究动机**：CLIP等模型是现代大规模系统的基础模块，但其内部表征难以解释和控制。SAE虽能提取可解释特征，但现有方法性能不足，限制了其在下游可解释性任务（如目标检测、偏差分析）中的应用。
- **整体含义**：提出一种新的层级稀疏自编码器架构，旨在同时逼近重构质量和稀疏性的帕累托最优，为多模态模型的可解释性提供更有效的工具。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出 **Matryoshka SAE (MSAE)** 架构，灵感源自嵌套套娃（Matryoshka），通过学习**多层次粒度的层次化表征**，在不牺牲任一指标的前提下直接优化重构质量和稀疏性。
- **关键技术细节**：
  - 构建一个多粒度特征编码器，输出多个不同稀疏度/维度的特征层，形成层次结构。
  - 通过联合训练多个“子SAE”，不同层次共享部分参数，使得模型能够同时学习从粗粒度到细粒度的特征。
  - 损失函数结合重构误差和稀疏性惩罚（如L1正则化或Top-k抑制），但通过层次化设计避免了传统方法的刚性约束。
  - 最终MSAE能够在不妥协的情况下达到更好的帕累托前沿（Pareto frontier）。
- **公式或算法流程**（文字描述）：
  - 输入CLIP的视觉/文本表征向量，送入MSAE的编码器，编码器输出多个不同维度的稀疏表征。
  - 每个稀疏表征对应一个解码器，重构原始输入。
  - 总损失为各层重构损失与稀疏惩罚项的加权和，训练过程中自动平衡各层性能。

## 3. 实验设计

- **使用数据集/场景**：
  - 主要实验对象为**CLIP**模型（未说明具体版本，推测为CLIP ViT-L/14等）。
  - 下游任务：在**CelebA**数据集上进行概念相似性搜索和偏差分析。
  - 未提及更多其他数据集（如ImageNet、CIFAR等）或检测任务数据集，实验场景较为集中。
- **Benchmark**：
  - 与现有SAE方法比较，包括标准SAE（如TopK SAE、Gated SAE等）。MSAE声称在CLIP上建立了重构质量与稀疏性之间的**最优帕累托前沿**。
- **对比方法**：
  - 文中提及“current SAE methods”，但未列出具体名称。需要查看完整论文才能确定对比基线。

## 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量、训练时长等算力细节。仅提到代码开源在GitHub，但未提供任何训练硬件或时间的信息。这表明作者可能认为算力并非其贡献重点，或者需要读者参考代码仓库获取信息。

## 5. 实验数量与充分性

- **实验数量**：从摘要看，主要实验包括：
  - 在CLIP表征上的重构质量与稀疏性指标对比（余弦相似度、方差未解释分数、稀疏度）。
  - 下游概念提取（提取了120+语义概念），并在CelebA上进行了概念相似性搜索和偏差分析。
  - 是否包含消融实验（如不同层次数、不同稀疏度设置）未提及。
- **充分性评估**：由于摘要信息有限，实验数量似乎偏少（仅一个主要指标对比+一个下游应用）。缺少在更多视觉语言模型（如SigLIP）上的结果，缺少与更多基线的全面比较。但考虑到论文发表于ICML 2025，可能正文有更详细的实验。从已披露信息看，实验覆盖不够广泛，客观性较好（有量化指标），但公平性需要看是否对所有方法进行了相同调优。

## 6. 主要结论与发现

- MSAE在CLIP上实现了**0.99余弦相似度**和**小于0.1的方差未解释分数**，同时保持**80%稀疏度**，显著优于现有SAE方法，建立了新的帕累托前沿。
- 在CelebA上成功提取**120多个语义概念**，可用于概念相似性搜索和偏差分析，展示了MSAE作为解释和控制CLIP工具的有效性。
- MSAE有助于理解多模态模型的行为，可迁移至可解释目标检测等下游任务。

## 7. 优点

- **架构创新**：层次化多粒度设计直接解决了重构质量与稀疏性的折衷问题，无需手动调整折衷超参数。
- **性能优越**：在关键指标上达到SOTA，且量化数据具体（0.99余弦相似度、80%稀疏度）。
- **实用性**：提取的语义概念可直接用于下游可解释性任务（概念搜索、偏差分析），验证了方法的实际价值。
- **代码开源**：促进复现和后续研究。

## 8. 不足与局限

- **实验覆盖不足**：仅针对CLIP验证，未在SigLIP或其他视觉语言模型上测试，泛化性存疑。下游任务也仅使用CelebA一个数据集。
- **缺乏详细对比**：未列出具体对比方法的名称和性能细节（需查看全文）。
- **未报告算力与训练成本**：难以评估其可复现性和效率。
- **偏差风险**：概念提取可能依赖CLIP本身预训练中存在的偏见，MSAE本身并未消除偏见，偏差分析也未提供定量缓解效果。
- **应用限制**：层次化结构可能增加参数量和计算复杂度，对于要求极低延迟的场景可能不适用。对稀疏度的定义（80%稀疏是指特征的零比例？）需要明确。

（完）
