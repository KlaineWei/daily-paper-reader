---
title: "Text Meets Topology: Rethinking Out-of-distribution Detection in Text-Rich Networks"
title_zh: 文本遇见拓扑：重新思考文本丰富网络中的分布外检测
authors: "Danny Wang, Ruihong Qiu, Guangdong Bai, Zi Huang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.280.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 文本丰富网络中的分布外检测视为异常检测
tldr: 文本丰富网络中的分布外检测面临文本与结构多样性挑战。TextTopoOOD框架评估属性级和结构级偏移场景，为网络异常检测提供基准。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.280/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.280/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.280/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1614, \"height\": 395, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1609, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 952, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 441, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 840, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 825, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1692, \"height\": 723, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1493, \"height\": 806, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 805, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 705, \"height\": 766, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 800, \"height\": 980, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 799, \"height\": 1039, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 809, \"height\": 550, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 808, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1646, \"height\": 1968, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1648, \"height\": 2008, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1647, \"height\": 2031, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1646, \"height\": 1598, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1646, \"height\": 1670, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1647, \"height\": 1573, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1647, \"height\": 1950, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1646, \"height\": 1963, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1645, \"height\": 1880, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1646, \"height\": 1990, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.280/table-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1647, \"height\": 1978, \"label\": \"Table\"}]"
motivation: 现有方法忽视文本-结构多样性，分布外检测性能有限。
method: 提出TextTopoOOD框架，涵盖属性级和结构级偏移场景。
result: 揭示了现有方法在复杂分布外场景中的不足。
conclusion: 需要更全面的分布外检测方法应对文本网络多样性。
---

## Abstract
Out-of-distribution (OOD) detection remains challenging in text-rich networks, where textual features intertwine with topological structures. Existing methods primarily address label shifts or rudimentary domain-based splits, overlooking the intricate textual-structural diversity. For example, in social networks, where users represent nodes with textual features (name, bio) while edges indicate friendship status, OOD may stem from the distinct language patterns between bot and normal users. To address this gap, we introduce the TextTopoOOD framework for evaluating detection across diverse OOD scenarios: (1) attribute-level shifts via text augmentations and embedding perturbations; (2) structural shifts through edge rewiring and semantic connections; (3) thematically-guided label shifts; and (4) domain-based divisions. Furthermore, we propose TNT-OOD to model the complex interplay between Text aNd Topology using: 1) a novel cross-attention module to fuse local structure into node-level text representations, and 2) a HyperNetwork to generate node-specific transformation parameters. This aligns topological and semantic features of ID nodes, enhancing ID/OOD distinction across structural and textual shifts. Experiments on 11 datasets across four OOD scenarios demonstrate the nuanced challenge of TextTopoOOD for evaluating OOD detection in text-rich networks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：文本丰富网络（TrN）中，节点包含文本特征（如用户简介、产品描述），边表示拓扑结构（如社交关系、共购关系）。现有OOD检测方法主要关注标签偏移或简单的领域划分，忽略了文本与拓扑之间的复杂交互和多样偏移类型。例如，社交网络中机器人与正常用户的语言模式差异可能导致OOD；产品网络中描述术语变化而购买关系不变也会形成分布偏移。
- **整体含义**：本文旨在系统性地定义和评估TrN中的多种OOD场景，并提出一种能够联合建模文本与拓扑信息的新检测方法，以提升OOD检测的鲁棒性。

## 2. 方法论：核心思想、关键技术细节
### 核心思想
- 提出**TextTopoOOD框架**——首个涵盖四类OOD场景的综合评估基准：属性级偏移（文本增强、嵌入扰动）、结构级偏移（边重连、语义连接、文本交换）、主题引导的标签偏移、基于领域的分割（如时间偏移）。
- 提出**TNT-OOD检测模型**：通过交叉注意力融合文本与图结构信息，并利用超网络（HyperNetwork）生成节点特定的投影参数，实现异构对齐。

### 关键技术细节
1. **结构编码**：使用GCN对节点进行邻居聚合，得到结构感知嵌入 $g$。
2. **交叉注意力融合**：对每个节点，以结构嵌入为查询（Query），文本嵌入为键（Key）和值（Value），对邻居文本进行加权聚合，得到融合表示 $z_i$。
3. **超网络投影**：由融合表示 $z_i$ 生成节点特定的投影权重 $W_i$（或低秩分解 $L_i, R_i$），将文本嵌入 $x_i$ 投影到共享空间 $p_i^t = W_i x_i$，实现节点级自适应。
4. **对比学习与分类**：对投影后的文本表示 $P_t$ 和结构嵌入 $\tilde{g}$ 施加对称对比损失 $L_{cont}$，同时使用分类损失 $L_{cls}$，联合优化。
5. **OOD分数**：综合能量分数与对齐分数（$s_{E\text{-}lign} = e_{energy} - T \cdot s_{align}$），再经图传播平滑得到最终分数。

## 3. 实验设计
### 数据集与场景
- **11个数据集**：涵盖引用网络（Cora、Citeseer、DBLP、Arxiv、PubMed）、知识/社交网络（Reddit、WikiCS）、电商网络（Bookhis、Bookchild、Elephoto、Elecomp）。
- **OOD场景**：每种场景包含多种噪声水平或模式，共生成大量子任务（如特征混合 $\alpha=\{0.5,0.7,0.9\}$；结构重连 mild/medium/strong；语义连接三个阈值；文本交换三种策略；标签偏移三类选择等）。

### 基准方法
- **后处理方法**：Maha、MSP、ODIN、NECO、Energy。
- **图专用方法**：GNNSafe、NodeSafe（带分数传播）。
- **LLM零样本检测**：GPT-4o mini、Gemini-2.5-flash（仅标签偏移场景）。

### 评估指标
- AUROC（↑）、AUPR（↑）、FPR95（↓）、ID Accuracy。

## 4. 资源与算力
- 文中提及使用**单张NVIDIA RTX A6000 GPU（48GB）**，但未明确说明训练总时长。从附录表13可看到各数据集训练时间：Cora约11.85秒（完整TNT-OOD），Arxiv约276.48秒（带批量），Bookhis约49.82秒。整体训练效率低于基线，但推理速度相近。

## 5. 实验数量与充分性
- **实验数量**：对比了7种基线 + 2种LLM，在11个数据集×多种OOD子场景下重复3次，报告均值和标准差。另包含消融实验（表3）、超参数分析（λ, τ）、文本编码器替换（表14）、耦合偏移分析（表6）、与LLM对比（表5）、传播效果分析（表4）等。
- **充分性与公平性**：
  - 基线使用相同分类器配置（ID准确率一致），超参数网格搜索，分三种子并报告标准差，统计严谨。
  - 考虑不同规模、不同域的数据集，覆盖全面。
  - 消融实验验证了交叉注意力、超网络、对比损失、对齐分数各组件贡献。
  - 传递性：文中注明排除了直推式方法（如GRASP），保持归纳设置，对比公平。

## 6. 主要结论与发现
- TNT-OOD在大多数数据集和场景下优于所有基线，尤其在引用网络（Cora FPR95降至25.71%）、知识/社交网络（Reddit AUROC提升13%以上）、电商网络（最低FPR95）上表现显著。
- TextTopoOOD框架揭示了不同场景的难度差异：Arxiv等大规模数据集上传播方法失效，说明现有方法仍存在盲点。
- 超网络与交叉注意力机制有效提升了文本-结构对齐，能量-对齐联合分数比单独能量分数更鲁棒。
- LLM在标签偏移上表现不如TNT-OOD（如Cora的FPR从34.89%降至25.29%）。
- 耦合偏移（结构+特征）可放大ID/OOD分离，导致检测更易。

## 7. 优点
- **基准创新**：首次系统定义并评估了文本丰富网络中多种维度（文本、结构、标签、时间）的OOD场景，填补了该领域空白。
- **方法新颖**：交叉注意力融合 + 超网络生成节点特定投影，能够捕捉文本与拓扑的异构交互，较静态投影头更具表达能力。
- **实验充分**：大规模多域数据集、多场景、多指标、多基线比较，消融与可视化（t-SNE）完备。
- **可扩展性**：低秩分解降低了超网络的计算开销，支持更大规模网络。
- **开源代码**：便于复现和后续研究。

## 8. 不足与局限
- **计算成本**：交叉注意力和超网络带来额外内存和训练时间（尤其在Arxiv上OOM），尽管有低秩设计，但整体效率仍低于简单后处理方法。
- **文本编码器固定**：未微调预训练语言模型，可能限制了文本表示质量。
- **仅节点级OOD**：未扩展至图级或边级OOD检测，应用范围有限。
- **硬件限制**：单GPU 48GB，对超大规模网络（>100k节点）可能仍需进一步优化。
- **场景选择性**：仅测试了部分配置（如α值、β参数），未穷举所有可能的偏移组合，可能存在偏差。
- **LLM对比有限**：仅对比标签偏移，未在其他场景（如文本增强）与LLM比较，且LLM作为零样本检测器时无法输出连续分数，对比存在不公平因素。
- **无理论保证**：方法为启发式，缺乏泛化误差界或OOD可检测性的理论分析。

（完）
