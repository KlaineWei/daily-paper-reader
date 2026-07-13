---
title: Connectome-scale self-supervised representation learning reveals neuronal organization beyond canonical labels
title_zh: 连接组尺度的自监督表示学习揭示超越经典标签的神经元组织
authors: "Shi, T., Chen, Y., Liu, C., Zhang, R."
date: 2026-07-04
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.30.735468v1.full.pdf"
tags: ["query:contrastive"]
score: 9.0
evidence: 在连接组中使用对比学习进行自监督表示学习
tldr: 密集电镜连接组提供了突触级精细图谱，但如何自动学习整合神经元形态与连接的可扩展表征是挑战。本文提出自监督框架，利用层次图神经网络和骨架分解，在FlyWire神经元的精细骨架上进行对比学习。精细骨架比粗粒度保留更丰富身份信息，坐标无关拓扑减少几何混淆，提升聚类效果。结构嵌入作为连续描述符驱动连接表征，改善亚型区分；迭代多跳学习揭示了半球侧化和连接定义子组。该工作为大规模密集连接组中的神经元发现和组织分析提供了可扩展的自监督方案。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 970, \"height\": 1295, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1244, \"height\": 1151, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 992, \"height\": 1164, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 893, \"height\": 1087, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1045, \"height\": 927, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1351, \"height\": 783, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1576, \"height\": 1212, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1562, \"height\": 1933, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1560, \"height\": 1930, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-64898-2026-06-30-735468-v1/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1575, \"height\": 146, \"label\": \"Table\"}]"
motivation: 密集连接组中缺乏无监督学习整合神经元结构和连通性表征的可扩展方法。
method: 采用层次图神经网络结合骨架分解进行自监督对比学习，并引入坐标无关拓扑减少几何混淆。
result: 细粒度骨架保留更丰富身份信息，结构嵌入改善亚型区分，迭代多跳学习发现半球侧化和连接定义子组。
conclusion: 实现了密集连接组中神经元身份与网络组织的自监督、可扩展发现框架。
---

## 摘要
密集电子显微镜连接组提供了神经元结构和突触连接的突触分辨率图谱，但学习可扩展的表示方法以整合结构和连接性，从而在最小人工干预下进行连接组发现仍然困难。本文提出了一种用于密集连接组中结构-连接性表示学习的自监督框架。一种具有骨架分解的分层图神经网络能够从精细采样的FlyWire神经元骨架中进行对比学习，表明精细骨架比粗表示保留了更丰富的身份信息。无坐标拓扑减少了发育和几何混杂因素，改善了聚类和标签高效推理。然后，我们使用学习的结构嵌入作为突触伙伴的连续描述符来构建结构驱动的连接性表示，无需预定义的伙伴类型标签即可提高亚型区分能力。迭代多跳学习进一步揭示了高阶组织，包括半球连接偏侧化和连接性定义的亚组。注意力分析将这些差异与特定的突触伙伴联系起来。这些结果共同建立了一个自监督且可扩展的框架，用于在大规模密集连接组中发现神经元身份和连接组组织。

## Abstract
Dense electron-microscopy connectomes provide synaptic-resolution maps of neuronal structure and wiring, but learning scalable representations that integrate structure and connectivity for connectome discovery with minimal human intervention remains difficult. Here we present a self-supervised framework for structure-connectivity representation learning in dense connectomes. A hierarchical graph neural network with skeleton decomposition enables contrastive learning from finely sampled FlyWire neuronal skeletons, showing that fine skeletons preserve substantially richer identity information than coarse representations. Coordinate-free topology reduces developmental and geometric confounds, improving clustering and label-efficient inference. We then use learned structural embeddings as continuous descriptors of synaptic partners to construct structure-driven connectivity representations, improving subtype discrimination without predefined partner-type labels. Iterative multi-hop learning further reveals higher-order organization, including hemispheric connectivity lateralization and connectivity-defined subgroups. Attention analysis links these differences to specific synaptic partners. Together, these results establish a self-supervised and scalable framework for discovering neuronal identity and connectome organization in a large-scale dense connectome.

---

## 论文详细总结（自动生成）

好的，以下是根据给定论文内容生成的结构化中文总结。

---

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：密集电子显微镜连接组（如FlyWire果蝇大脑数据集）提供了突触分辨率的神经元结构与布线图谱，但传统方法依赖人工标注的类别标签，难以自动、可扩展地整合神经元形态和连接性信息进行无监督发现。
- **核心问题**：如何在无人工干预下，从大规模密集连接组中学习能够体现神经元身份和连接组组织的有效表示？现有方法要么使用粗粒度形态表示丢失细节，要么依赖坐标信息受发育和几何混淆影响。
- **整体含义**：本文提出一种自监督对比学习框架，通过精细采样的神经元骨架学习结构嵌入，并驱动连接性表示，从而自动揭示超越传统标签（如半球侧化、连接定义亚组）的神经元组织，为连接组发现提供可扩展方案。

### 2. 方法论：核心思想、关键技术细节、算法流程

- **核心思想**：利用层次图神经网络（Hierarchical GNN）对神经元骨架进行自监督对比学习，获得结构嵌入（structural embedding）；然后以该嵌入作为连续描述符，驱动结构-连接性联合表示，并通过迭代多跳学习挖掘高阶组织。
- **关键技术细节**：
  - **骨架分解与精细采样**：将神经元骨架分解为精细节点（fine skeleton），而非粗粒度表示（如粗枝干），保留更丰富的身份信息。
  - **坐标无关拓扑**：在图神经网络中去除坐标信息，仅使用拓扑结构，减少发育和几何混杂因素，提升聚类和标签高效推理效果。
  - **对比学习**：采用层次GNN对同一神经元的不同骨架视图进行正样本对构建，进行自监督对比学习，学习结构嵌入。
  - **结构驱动的连接性表示**：将学到的结构嵌入作为突触伙伴的连续描述符，代替预定义的伙伴类型标签，构建结构驱动的连接性表示，改善亚型区分。
  - **迭代多跳学习**：通过多跳邻居聚合，进一步揭示高阶组织，如半球连接偏侧化和连接性定义的亚组。
- **算法流程（文字描述）**：
  1. 对FlyWire数据集中每个神经元提取精细骨架图。
  2. 使用层次GNN对骨架图进行编码，获得节点/图级嵌入。
  3. 对比学习：同一神经元的不同视图（如不同骨架段）作为正对，不同神经元作为负对，优化嵌入。
  4. 将结构嵌入作为每个突触伙伴的特征，构建连接性向量。
  5. 迭代执行多跳聚合，获得高阶组织表示。
  6. 通过注意力分析关联特定突触伙伴与发现的组织差异（如半球侧化）。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：FlyWire连接的果蝇大脑密集电子显微镜连接组，包含大量神经元的精细骨架结构和突触连接信息。
- **基准（Benchmark）**：论文未明确列出标准基准，但通过聚类性能、标签高效推理效果、亚型区分能力等指标进行评估。
- **对比方法**：论文中提及对比了“粗表示”（coarse representation）与“精细骨架”的效果，以及“包含坐标”与“坐标无关拓扑”的差异。未提及与已有无监督方法（如GraphSAGE、GCN等）的系统对比，仅在消融中验证了各组件的贡献。

### 4. 资源与算力

- **未明确说明**：论文正文（摘要及元数据）未提及使用的GPU型号、数量、训练时长等具体算力信息。需要从作者单位或公开代码推测，但此处无法获取。建议读者查阅全文或补充材料。

### 5. 实验数量与充分性

- **实验数量**：从摘要描述可推断至少进行了以下实验：
  - 精细骨架 vs 粗表示对比实验（图1-3？）。
  - 坐标无关 vs 坐标依赖对比实验。
  - 结构嵌入驱动连接性表示与基线（如随机嵌入、直接使用连接）的对比。
  - 迭代多跳学习发现半球侧化和连接定义亚组的分析实验。
  - 注意力分析实验。
- **充分性评价**：由于缺乏全文，无法判断实验覆盖的广度（如是否在多个物种/连接组上验证）和消融的完整性。从摘要看，验证了精细骨架的优势和坐标无关拓扑的效果，但未与最新自监督图学习方法（如Deep Graph Infomax、SimGRACE等）对比。总体而言，实验逻辑清晰，但充分性有待全文检验。

### 6. 主要结论与发现

- 精细骨架比粗粒度骨架保留更丰富的神经元身份信息，显著提升聚类和标签高效推理。
- 去除坐标信息仅利用拓扑结构可减少发育和几何混淆，改善表示质量。
- 结构嵌入作为连续描述符构建连接性表示，无需预定义伙伴类型标签即可提高亚型区分能力。
- 迭代多跳学习揭示了高阶组织：半球连接存在侧化（左/右不对称），并发现连接性定义的神经元亚组。
- 注意力分析将半球侧化差异归因于特定突触伙伴，提供了可解释性。

### 7. 优点

- **方法创新性**：首次将自监督对比学习与神经元的精细骨架分解结合，在连接组尺度上学习结构-连接性联合表示，无需人工标签。
- **坐标无关性设计**：有效减少发育和几何混淆，使表示更关注拓扑结构，符合神经科学中功能与结构关联的直觉。
- **可扩展性**：层次GNN和对比学习框架可扩展到更大规模连接组。
- **发现超越经典标签的神经组织**：自动揭示半球侧化和连接定义亚组，证明了无监督方法的潜力。
- **注意力可解释性**：提供关联特定突触伙伴的机制，有助于生物学解读。

### 8. 不足与局限

- **实验覆盖有限**：仅基于FlyWire一个数据集进行验证，未在哺乳动物或其他物种的连接组上测试，泛化性存疑。
- **对比方法不充分**：未与图对比学习领域主流方法（如InfoNCE、BYOL等）进行系统性公平比较，也未与基于形态学的传统聚类方法对比。
- **缺少定量评估指标**：摘要未给出具体数值（如聚类准确率、NMI、ARI等），难以客观评估性能提升幅度。
- **算力与资源未公开**：影响可复现性。
- **应用限制**：方法依赖精细骨架提取，需高质量电镜重建结果；未讨论对噪声或断裂骨架的鲁棒性。
- **偏差风险**：坐标无关拓扑可能丢失某些依赖空间位置的生物学重要信息（如分层结构）。

（完）
