---
title: A layer-resolved diagnostic identifies bias-driven decisions in deep neural networks
title_zh: 一种分层诊断方法识别深度神经网络中偏差驱动的决策
authors: "Nakuci, J."
date: 2026-07-16
pdf: "https://www.biorxiv.org/content/10.1101/2025.09.16.676625v7.full.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 层分辨率神经网络可解释性诊断
tldr: 深度神经网络在高置信度下仍可能做出偏差驱动的决策，但现有指标无法区分置信度的来源。本文提出偏差主导指数（BDI），通过逐层分解网络输出为特征依赖项和输入无关偏移项，量化偏移对决策边际的贡献。在卷积网络、Vision Transformer和Transformer语言模型上，BDI发现高置信度常伴随偏差驱动决策，且偏移成分在读出权重退化时能稳定性能。BDI作为通用诊断工具，可区分特征支持与偏差驱动决策，支持机制感知的模型审计与分流。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1714, \"height\": 911, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1715, \"height\": 1346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1723, \"height\": 748, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1705, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1723, \"height\": 1168, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1724, \"height\": 729, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1720, \"height\": 810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1723, \"height\": 1626, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1783, \"height\": 481, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1624, \"height\": 897, \"label\": \"Table\"}]"
motivation: 现有置信度指标无法区分决策是源于输入特征支持还是模型固有偏差，导致难以评估决策的合理性。
method: 提出偏差主导指数（BDI），逐层分解神经网络输出为输入依赖的特征支持与输入无关的偏移支持，量化偏移对决策边际的相对贡献。
result: 在CNN、ViT和Transformer语言模型上，BDI揭示高置信度常伴随偏差驱动决策；偏移成分在读出权重退化时稳定性能。
conclusion: BDI作为通用诊断，可区分特征支持与偏差驱动决策，支持机制感知的模型审计与分流。
---

## 摘要
现代AI系统可以准确且自信，但这本身并不能揭示决策是否得到了输入的良好支持。这造成了信任问题，因为置信度报告的是模型有多么确定，而不是什么支撑了这种确定。在这里，我们展示神经网络置信度可以分解为依赖于输入的特征支持和与输入无关的偏移支持。我们通过偏差主导指数（BDI）形式化了这种分解，BDI是一种分层度量，量化了与输入无关的偏移对决策边界的相对贡献，揭示了置信度主要是特征支持还是偏差驱动。在卷积神经网络、视觉Transformer和Transformer语言模型上，BDI显示高置信度可以与偏差驱动的决策共存。分层分析映射了偏差驱动支持在网络深度上的分布。扰动分析进一步表明，当读出权重退化时，偏差分量可以稳定性能。最后，我们将决策组成操作化为一个接受规则，该规则结合了置信度和BDI，用于机制感知的审计和分类。总之，这些结果将BDI定位为决策组成的一般诊断工具，能够区分不同模型家族中特征支持的决策和偏差驱动的决策。

## Abstract
Modern AI systems can be accurate and confident, but this alone does not reveal whether a decision is well supported by the input. This creates a trust problem because confidence reports how decisive a model is, but not what supports that decisiveness. Here we show that neural-network confidence can be decomposed into input-dependent feature support and input-independent offset support. We formalize this decomposition through the Bias Dominance Index (BDI), a layer-resolved measure quantifying the relative contribution of input-independent offsets to the decision margin, revealing whether confidence is primarily feature-supported or bias-driven. Across convolutional neural networks, a vision transformer and a transformer language model, BDI shows that high confidence can coexist with bias-driven decisions. Layer-resolved analyses map where bias-driven support across network depth. Perturbation analyses further show that the bias component can stabilize performance when readout weights are degraded. Finally, we operationalize decision composition into an acceptance rule that combines confidence and BDI for mechanism-aware auditing and triage. Together, these results position BDI as a general diagnostic of decision composition that distinguishes feature-supported from bias-driven decisions across model families.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义（研究动机和背景）

- **核心问题**：深度神经网络（DNN）即使在高置信度下也可能做出“偏差驱动”的决策——即决策边界主要由模型内部的输入无关偏移（如偏置项、归一化偏移）支撑，而非来自输入特征的有效证据。现有信任评估指标（如置信度、校准度、归因方法）无法揭示决策的**计算组成**，即置信度到底来源于特征支持还是偏差支持。
- **整体含义**：高置信度不等同于可信赖。需要一种机制感知的诊断工具，区分“特征支持的决策”和“偏差驱动的决策”，以提升AI系统在部署中的可审计性和可靠性。

## 论文提出的方法论

- **核心思想**：将决策边界（logit差值）分解为输入依赖的特征分量和输入无关的偏差分量，定义**偏差主导指数（BDI）**量化偏差对边界的相对贡献。
- **关键技术细节**：
  - 对于输入 \(x\)，输出 logits 为 \(z_k(x) = w_k^\top a + b_k\)。定义决策边界 \(\Delta z = z_t - z_r\)（目标类与次高类之差）。
  - 分解：\(\Delta z = (w_t - w_r)^\top a \quad\text{(特征分量)} + (b_t - b_r) \quad\text{(偏差分量)}\)。
  - BDI = \(|C_{\text{bias}}| / (|C_{\text{bias}}| + |C_{\text{feat}}|)\)，范围 [0,1]，>0.5 表示偏差主导。
  - **分层（layer-resolved）BDI**：对每一层（卷积、线性、LayerNorm等），将预激活输出分解为特征分量和偏差分量，利用梯度加权内积得到该层对决策边界的贡献，再计算 BDI。同时定义整体 BDI_all（各层绝对值累加）。
  - 支持**无标签**模式：使用 top-1 vs top-2 logit 差值定义边界，无需真实标签。
  - 涵盖多种模型：CNN（AlexNet, VGG-16）、Vision Transformer（ViT-b/16）、BERT。对 Transformer 额外考虑 LayerNorm 偏移和注意力的值投影偏置。
- **算法流程**（文字说明）：
  1. 前向传播获取各层预激活和最终 logits。
  2. 确定决策边界（top-1 vs top-2 或标签指定）。
  3. 对于输出层：直接计算特征和偏差分量，得到 BDI。
  4. 对于中间层：计算决策边界对层输出的梯度，分别与特征和偏差分量做内积，得到分层贡献，再计算层 BDI 和整体 BDI_all。

## 实验设计

- **数据集与场景**：
  1. **点辨别任务**（dot-discrimination task）：自制红蓝点图像，二分类（红色/蓝色主导），与人类行为数据对比。使用 5 个修改的 AlexNet（卷积层固定、全连接层训练）。
  2. **Tiny ImageNet**（200 类子集）：10,000 张验证集图像，用于 AlexNet、VGG-16、ViT-b/16 评估。
  3. **Tiny ImageNet-C**：加入高斯噪声（5级严重程度）的 Tiny ImageNet 图像，用于鲁棒性测试。
  4. **BERT 掩码补全任务**：使用提示句子，分析 top-1 和 top-2 token 之间的决策边界。
- **基准与对比方法**：
  - 与**人类表现**对比（点辨别任务，50名受试者数据）。
  - 与**归因方法**（DeepLIFT）定性对比。
  - 与**仅使用置信度阈值**的接受策略对比。
- **消融与扰动实验**：
  - 对点辨别任务：对中间层激活或读出权重添加高斯噪声（σ=0.1~1.0），比较保留/移除偏差分量时的准确率。
  - 逐层偏置归零（bias-clamp）分析，观察决策边界变化。

## 资源与算力

- **明确说明**：点辨别任务中 5 个 CNN 模型在 Google Colab 上使用 NVIDIA A100 GPU 训练和测试。其他预训练模型（AlexNet, VGG-16, ViT-b/16, BERT）直接从 PyTorch 加载，仅进行推理分析。
- **未明确说明**：未报告训练时长、具体 GPU 数量、能耗等细节。

## 实验数量与充分性

- **实验数量**：
  - 点辨别任务：5 个模型 × 1000 测试图像，附噪声扰动（σ=0.1~1.0，共10个等级）。
  - Tiny ImageNet：3 个模型（AlexNet, VGG-16, ViT-b/16）× 10,000 图像 → 30,000 次推理。
  - Tiny ImageNet-C：3 模型 × 5,000 图像（5级×1000）。
  - BERT：示例分析（表2提供3个例子，补充表1更多）。
  - 置信度-BDI 接受策略：覆盖 (τ,γ) 网格分析。
- **充分性评估**：
  - 覆盖 CNN、Vision Transformer、Transformer 语言模型，具有代表性。
  - 包含干净数据、有噪数据、分布偏移场景。
  - 进行了逐层归零消融和噪声扰动消融。
  - **不足**：BERT 分析仅提供定性示例，缺乏大规模定量评估；未在更大规模语言模型（如 GPT、LLaMA）上验证；未测试其他类型偏差（如数据集偏差）。

## 论文主要结论与发现

1. **置信度无法唯一决定决策支持类型**：相同置信度的决策可能分别由特征或偏差主导，高置信度可与高 BDI 共存。
2. **BDI 揭示深度网络中偏差主导决策的系统存在**：在点辨别任务中约 35-48% 的 trials 为偏差主导；在 ImageNet 模型中也存在一定比例。
3. **分层 BDI 展示偏差支持在网络深度上的分布**：早期卷积层和晚期线性层偏差主导比例高，ViT 中的 LayerNorm 是关键贡献者。
4. **偏差分量在读出权重退化时具有稳定作用**：当权重添加噪声时，保留偏置可显著提升准确率；对激活噪声影响不显著。
5. **无标签 BDI 可用于部署审计**：结合置信度阈值和 BDI 阈值的接受策略可以降低误匹配率，为机制感知的筛选提供工具。
6. **归因方法（DeepLIFT）无法替代 BDI**：高置信度-高 BDI 的样本中，归因可能模糊，而 BDI 明确显示偏差主导。

## 优点

- **创新性**：首次将决策边界分解为特征与偏移，提出 BDI，直接量化决策组成，填补了置信度与归因之间的空白。
- **通用性**：适用于多种架构（CNN、ViT、BERT），且支持无标签模式，实用性强。
- **可解释性**：分层 BDI 提供深度方向的分析，定位偏差来源。
- **严谨性**：通过噪声扰动、偏置归零等因果实验验证偏差分量的影响，而非仅相关性。
- **应用价值**：提出置信度+BDI 联合策略，可直接用于模型审计与分流，提升高价值场景的可靠性。

## 不足与局限

- **偏差类型局限**：仅考虑输入无关的模型内在偏移（如偏置项、归一化偏移），未覆盖数据集偏差、标签噪声、伪相关等输入依赖的偏差。
- **模型范围局限**：主要验证于 ImageNet 规模的 CNN 和 ViT，BERT 仅给出示例，缺乏对大型语言模型（如 GPT-4、LLaMA-2）的定量分析；未测试目标检测、强化学习等任务。
- **限于常见扰动**：仅使用高斯噪声，未测试对抗性攻击、覆盖其他分布偏移（如风格迁移、天气等）。
- **BDI 定义依赖梯度**：可能受梯度饱和影响，虽然作者讨论但未提出替代方案（如积分梯度加权）。
- **未探讨偏差的“好坏”**：指出偏差可稳定性能，但缺乏区分有益/有害偏差的标准；高 BDI 不直接等同于不可信，需要结合任务上下文。
- **算力信息缺失**：未提供完整训练代价，不利于他人复现。

（完）
