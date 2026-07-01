---
title: "OT-DETECTOR: Delving into Optimal Transport for Zero-shot Out-of-Distribution Detection"
title_zh: OT-DETECTOR：基于最优传输的零样本分布外检测
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0184.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 利用最优传输进行零样本分布外检测
tldr: 该论文提出OT-DETECTOR，利用最优传输理论进行零样本分布外（OOD）检测。方法通过计算测试样本与训练分布之间的传输距离来判断是否为OOD样本，无需重新训练。实验表明OT-DETECTOR在多个OOD检测基准上表现优异，且传输距离可提供一定的可解释性。该工作为异常检测提供了新思路。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-184/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 830, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-184/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 855, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-184/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1511, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-184/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 834, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-184/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 835, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-184/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 822, \"height\": 251, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-184/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 923, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-184/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1738, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-184/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 626, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-184/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1737, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-184/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 888, \"height\": 347, \"label\": \"Table\"}]"
motivation: 现有OOD检测依赖训练数据，泛化性不足且难以解释。
method: 基于最优传输距离进行零样本OOD判断。
result: 在多个OOD数据集上取得良好检测性能。
conclusion: 最优传输距离可作为OOD检测的有效度量并具有可解释潜力。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：在真实世界的开放环境中，机器学习模型经常遇到未知类别（分布外，OOD）样本，而传统的闭集分类无法检测它们。现有零样本 OOD 检测方法（如 MCM、NegLabel）主要依赖测试图像与 ID 标签之间的语义匹配，却忽略了分布层面的差异，尤其在处理与 ID 类在语义上高度相似的“硬 OOD”样本时表现不佳。
- **核心问题**：能否在不依赖外部知识（如额外数据集、大语言模型）的前提下，同时捕捉语义和分布层面的线索，以提升零样本 OOD 检测的鲁棒性？
- **整体含义**：本文提出利用最优传输（Optimal Transport, OT）理论量化测试样本与 ID 标签分布之间的差异，并将语义匹配与分布距离相结合，提出了一种无需训练、无需额外数据的零样本 OOD 检测框架，为 OOD 检测提供了新的理论视角。

### 2. 论文提出的方法论

- **核心思想**：借助 CLIP 的视觉-文本对齐能力，将 ID 文本标签作为 ID 图像分布的代理。通过 OT 计算测试样本特征集与 ID 文本特征集之间的最优传输方案，从而得到两种互补的 OOD 分数：**语义分数**（基于传输质量）和**分布分数**（基于传输成本）。同时，设计语义感知内容精炼（SaCR）模块，通过多视图增强和选择融合，放大 ID 与硬 OOD 之间的特征差异。
- **关键技术细节**：
    - **SaCR 模块**（算法 1）：
        1. 对输入图像进行 N 次随机裁剪生成 N 个视图。
        2. 利用 CLIP 预测每个视图的标签，仅保留与原始图像预测标签一致的视图。
        3. 计算每个保留视图的边际置信度（最大 logit 与第二大 logit 之差），选择 top-k 个视图。
        4. 将 top-k 视图的视觉特征按边际分数加权求和并 L2 归一化，得到精炼特征 \(f^r\)。
    - **OT 分数函数**：
        1. 设测试集精炼特征集 \(F^r\)，ID 文本特征 \(F^{text}\)，两者形成离散测度 \(\mu, \nu\)（均匀权重）。
        2. 定义成本矩阵 \(C = 1 - F^r (F^{text})^\top\)（余弦距离）。
        3. 求解熵正则化 OT 问题（式 14），得到最优传输计划 \(P^*\)。
        4. **语义分数**：\(S_{\text{sem}}(x_i) = \max_j p^*_{ij}\)，衡量样本与最近 ID 标签的语义对齐。
        5. **分布分数**：\(S_{\text{dist}}(x_i) = 1 - \sum_j p^*_{ij} c_{ij}\)，测量将样本特征传输到 ID 空间所需的成本。
        6. 最终分数 \(S_{OT} = \alpha S_{\text{sem}} + (1-\alpha) S_{\text{dist}}\)，\(\alpha\) 为平衡超参数。
- **算法流程**：输入测试图像 → 通过 SaCR 得到精炼特征 → 计算与所有 ID 文本特征的成本矩阵 → 求解 OT → 得到语义分数和分布分数 → 加权求和 → 与阈值比较判定 ID/OOD。

### 3. 实验设计

- **数据集**：
    - **ID 数据**：ImageNet-1K（1000 类）。
    - **OOD 数据**：四个大型数据集（iNaturalist、SUN、Places365、Texture）及三个硬 OOD 子集（ImageNet-10、ImageNet-20、ImageNet-100）。
- **基准**：ImageNet-1K OOD benchmark（Huang et al.，2021）及 MCM 提出的硬 OOD 任务。
- **对比方法**：
    - 需要训练/微调：MSP、Energy、Fort et al.、CLIPN。
    - 零样本：MCM、GL-MCM、EOE、NegLabel。
    - 所有方法均使用 CLIP-B/16 骨干网络，以公平比较。
- **评价指标**：FPR95（越低越好）和 AUROC（越高越好）。

### 4. 资源与算力

- 文中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力信息。由于方法完全基于预训练的 CLIP（ViT-B/16）且无额外训练，推理仅需 CLIP 前向传播和 OT 求解（Sinkhorn 算法），计算开销主要来自 SaCR 模块的 N=256 次图像编码。但具体硬件信息未提供。

### 5. 实验数量与充分性

- **实验组数**：
    - 主实验：Table 1（4 个 OOD 数据集 + 平均）和 Table 2（4 个硬 OOD 任务）。
    - 消融实验：Table 3（分析 SaCR、S_sem、S_dist 三个组件共 8 种组合）。
    - 超参数分析：Table 4（α 从 0 到 1 步长 0.1 在 4 个 OOD 数据集上的性能）；Figure 4（Top-k 从 1 到 100 的敏感度）。
    - 可视化：Figure 5（SaCR 对 ID/硬 OOD 的视图选择效果）、Figure 6（分数分布对比）。
- **充分性与公平性**：实验覆盖了主流的大规模 ID/OOD 场景和具有挑战性的硬 OOD 场景，对比了多种方法（包括需要额外数据的方法），消融和超参分析完整。但**缺少对不同 CLIP 骨干 （如 ViT-L） 的验证**，也未报告跨 ID 数据集（如 CIFAR 作为 ID）的实验，因此泛化性验证尚有不足。

### 6. 论文的主要结论与发现

- OT-DETECTOR 在 ImageNet-1K 上达到 **FPR95=23.65%、AUROC=94.49%**，超越所有对比方法，包括使用外部知识的 EOE 和 NegLabel。
- 在硬 OOD 任务上平均 **FPR95=7.98%、AUROC=98.41%**，相比 NegLabel 在 ImageNet-100→10 任务上 FPR95 下降 43.78%，AUROC 提升 6.61%。
- SaCR 模块能有效筛选出 ID 样本的判别性区域，同时使硬 OOD 样本的混淆区域更加突出，显著增大分布差异。
- OT 中的分布分数侧重全局分布差异，语义分数侧重单个样本对齐，两者互补；结合 SaCR 后性能大幅提升。

### 7. 优点

- **理论新颖**：首次将最优传输引入零样本 OOD 检测，利用 OT 自然捕获语义和分布两个层面的差异。
- **无需外部知识**：不需要额外 OOD 样本、负标签挖掘或大型语言模型，仅在 CLIP 基础上直接检测。
- **强健的硬 OOD 检测**：SaCR 模块通过多视图精炼有效放大了 ID 与硬 OOD 的区分度，显著提升了最具挑战性的场景的性能。
- **参数化灵活**：超参数 α 允许针对不同 OOD 数据集自适应调整，具有较强的泛化能力。
- **实验充分**：进行了全面的消融、超参分析及可视化，验证了各组件的贡献。

### 8. 不足与局限

- **计算开销**：N=256 次随机裁剪和图像编码，加上 OT 求解，推理时延较高，不适合实时应用。文中未讨论效率问题。
- **超参数敏感性**：α 需对每个 OOD 数据集单独调节（Table 4），且最佳值不同，实际部署中可能需要验证数据集。
- **依赖 CLIP 质量**：方法完全基于 CLIP 的对齐能力；若 CLIP 在特定领域（如医学图像）表现差，则检测性能会随之下降。
- **缺乏更多 ID 数据集验证**：仅以 ImageNet-1K 为 ID，未在 CIFAR、细粒度分类等场景中评估，限制了结论的普适性。
- **未讨论失败案例**：没有分析哪些类型的 OOD 样本仍被错误分类，也未提供错误模式分析。
- **未提及可复现性细节**：未给出随机种子、图像尺寸、裁剪策略等关键设置，可能影响结果复现。

（完）
