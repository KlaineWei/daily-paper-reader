---
title: "PromptMoE: Generalizable Zero-Shot Anomaly Detection via Visually-Guided Prompt Mixtures"
title_zh: PromptMoE：基于视觉引导提示混合的通用零样本异常检测
authors: "Yuheng Shao, Lizhang Wang, Changhao Li, Peixian Chen, Qinyuan Liu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37842/41804"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 零样本异常检测提示混合方法
tldr: 零样本异常检测中，现有基于视觉语言模型的提示策略存在表示瓶颈和过拟合问题。本文提出PromptMoE，通过学习一个提示专家池，以组合方式构建多样化的提示表示，增强对未见异常的泛化能力。在多个基准上，PromptMoE显著优于现有方法，为异常检测的零样本泛化提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37842/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37842/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 871, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37842/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1383, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37842/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 880, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37842/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37842/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 814, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37842/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 795, \"height\": 449, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37842/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1791, \"height\": 1157, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37842/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 769, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37842/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 264, \"label\": \"Table\"}]"
motivation: 单固定、可学习或密集动态提示存在表示瓶颈，无法泛化到多样未见异常。
method: 学习一个提示专家池，通过视觉引导混合生成组合提示，增强表示多样性。
result: 在零样本异常检测任务上大幅超越现有方法，泛化性显著提升。
conclusion: 组合式提示学习是提升异常检测泛化能力的关键。
---

## Abstract
Zero-Shot Anomaly Detection (ZSAD) aims to identify and localize anomalous regions in images of unseen object classes. While recent methods based on vision-language models like CLIP show promise, their performance is constrained by existing prompt engineering strategies. Current approaches, whether relying on single fixed, learnable, or dense dynamic prompts, suffer from a representational bottleneck and are prone to overfitting on auxiliary data, failing to generalize to the complexity and diversity of unseen anomalies. To overcome these limitations, we propose PromptMoE. Our core insight is that robust ZSAD requires a compositional approach to prompt learning. Instead of learning monolithic prompts, PromptMoE learns a pool of expert prompts, which serve as a basis set of composable semantic primitives, and a visually-guided Mixture-of-Experts (MoE) mechanism to dynamically combine them for each instance.
Our framework materializes this concept through a Visually-Guided Mixture of Prompt (VGMoP) that employs an image-gated sparse MoE to aggregate diverse normal and abnormal expert state prompts, generating semantically rich textual representations with strong generalization. Extensive experiments across 15 datasets in industrial and medical domains demonstrate the effectiveness and state-of-the-art performance of PromptMoE.

---

## 论文详细总结（自动生成）

# 论文 `PromptMoE: Generalizable Zero-Shot Anomaly Detection via Visually-Guided Prompt Mixtures` 详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究任务**：零样本异常检测（Zero-Shot Anomaly Detection, ZSAD），即在训练阶段未见过的物体类别上，检测并定位图像中的异常区域。
- **现有局限**：
  - 基于视觉语言模型（如CLIP）的提示方法（单一固定提示、可学习提示或密集动态提示）存在**表示瓶颈**——单个提示向量难以覆盖未见类别的多样正常/异常模式。
  - 增加静态提示数量容易导致**过拟合**到辅助数据集，泛化能力差。
  - 动态提示方法（如AdaCLIP、VCP-CLIP）依赖单一映射网络处理所有视觉变化，难以生成针对细粒度异常模式的专用提示。
- **核心洞察**：解决ZSAD需要**组合式提示学习**（compositional prompt learning），即不是学习一个整体提示，而是学习一组可组合的语义基元（专家提示），并通过视觉实例动态组合它们。

## 2. 论文提出的方法论

### 2.1 核心思想
- **PromptMoE**：将提示学习从“单体式”范式转变为“组合式”范式。学习一个专家提示池（expert prompt pool），每个专家代表一个可复用的语义基元，再利用视觉引导的混合专家（MoE）机制为每个实例动态组合出特定于该实例的正常/异常文本提示。

### 2.2 关键技术：Visually-Guided Mixture of Prompt（VGMoP）

- **结构**：为每个视觉实例构建两种混合文本提示：
  - 正常提示：`[S_n_agg][cls][Q_ctx]`
  - 异常提示：`[S_n_agg][S_a_agg][cls][Q_ctx]`
  - 其中 `S_n_agg` 和 `S_a_agg` 是由MoE动态聚合得到的正常/异常状态嵌入，`Q_ctx` 是共享可学习上下文。

- **视觉引导的稀疏路由**：
  - 对每个视觉层，使用可学习查询向量与图像块特征进行交叉注意力（Cross-Attention），提取与状态相关的视觉表示 `r^(l)`。
  - 将 `r^(l)` 输入一个两层的图像门控稀疏路由器（image-gated sparse router），产生路由logits，从中选出 top-k 个专家，用 softmax 归一化的权重加权聚合得到状态嵌入（公式(2)(3)）。

- **正常/异常独立专家池**：分别维护正常专家池 `E_n` 和异常专家池 `E_a`，提供专门的表征空间。

- **辅助损失**：
  - **负载均衡损失（L_balance）**：鼓励路由器在批次内均匀选择所有专家，避免某些专家被过度选择导致池退化（公式(4)）。
  - **专家解耦损失（L_decouple）**：通过强制专家中心嵌入之间的正交性，促进专家多样性（公式(5)）。

### 2.3 训练与推理流程
- 使用预训练CLIP（冻结参数），从多个层（6,12,18,24）提取视觉特征。
- 对每层相似度图进行上采样并求和得到像素级异常图（公式(6)）；图像级分数结合异常图最大值和全局特征相似度（公式(7)）。
- 总损失包含分类损失（BCE）、辅助损失、分割损失（Dice + Focal）（公式(8)）。

## 3. 实验设计

- **数据集**：共15个真实世界数据集，涵盖工业制造（7个）和医学诊断（8个）：
  - 工业：MVTec AD、VisA、MPDD、BTAD、SDD、DAGM、DTD-Synthetic。
  - 医疗：HeadCT、BrainMRI、Br35H、ISIC、CVC-ColonDB、CVC-ClinicDB、Kvasir、Endo。
- **基准设置**：标准零样本设定——主要在MVTec AD上训练，然后在其余14个数据集上零样本推理；评估MVTec AD自身时，在VisA上训练。
- **对比方法**：CLIP基线、WinCLIP、APRIL-GAN、AnomalyCLIP、AdaCLIP、FAPrompt。
- **度量指标**：图像级AUROC和AP；像素级AUROC和PRO。

## 4. 资源与算力

- 文中明确提到：所有实验在单块 **RTX 3090** 上使用 **PyTorch 1.13.1** 进行，训练 **15个epoch**，批量大小 **16**，学习率0.001（前3个epoch warm-up）。
- **未说明**：训练的总耗时（如小时数）、是否使用多卡并行、推理速度等。

## 5. 实验数量与充分性

- **实验数量充分**：包含15个数据集的完整定量比较（表1）、定性可视化对比（图5）、专家激活模式分析（图6）、以及多组消融实验：
  - 表2：从静态提示逐步构建到完整PromptMoE的消融。
  - 图7：专家解耦损失的影响（训练动态）。
  - 表3：负载均衡损失系数α的消融。
- **客观性与公平性**：所有对比结果均引用自原论文或使用官方代码统一复现（缺失值自行复现），设置保持一致。消融实验控制变量，结论可信。
- **局限性**：未在更多跨领域（如自然图像异常）上评估；未与其他类型的MoE（如视觉特征层面的MoE）对比；对超参数（如专家数、top-k）的敏感性分析不够深入。

## 6. 论文的主要结论与发现

- 组合式提示学习（PromptMoE）在ZSAD上显著优于现有的静态、动态单体提示方法，在15个数据集上的多项指标达到SOTA。
- 专家池的稀疏激活能够提升泛化能力并缓解过拟合，正常状态路由更稳定，异常状态路由更动态（图6）。
- 负载均衡损失和专家解耦损失协同作用：解耦损失保证专家多样性，从而使得负载均衡损失能有效工作（图7）。

## 7. 优点

1. **创新性**：首次将MoE机制应用于提示学习，以组合方式替代单体式提示，克服表示瓶颈和过拟合。
2. **通用性**：方法在工业与医疗两种差异显著的领域均表现优异，证明了学习到的语义基元具有跨领域可迁移性。
3. **设计精巧**：通过交叉注意力提取状态相关视觉特征、独立专家池、辅助损失正则化等设计，每个组件都有明确作用。
4. **实验严谨**：在大量标准数据集上公平对比，消融实验充分验证各模块贡献。
5. **计算效率**：虽然学习专家池但仅稀疏激活，推理时增加的计算量较小（k=4选8个专家）。

## 8. 不足与局限

- **依赖预训练CLIP**：方法性能严重受限于CLIP视觉编码器的质量，若更换更强或更弱的预训练模型，效果可能变化。
- **未讨论极端异常**：实验数据集的异常通常比较明显，对于极其细微或语义复杂的异常（如逻辑异常），泛化能力有待检验。
- **超参数敏感性**：专家数量（E=8）、top-k（k=4）、查询数量（Nq=8）等是手动设定，未提供鲁棒性分析。
- **训练数据单一**：主要使用MVTec AD训练，尽管零样本泛化良好，但不同辅助数据集的影响未探索。
- **未见计算开销分析**：未报告训练/推理时间或参数量与对比方法的比较。
- **可解释性不足**：虽然分析了专家激活频率，但未解释每个专家代表的语义到底是什么（如是否可对应“纹理异常”、“形状异常”等）。

（完）
