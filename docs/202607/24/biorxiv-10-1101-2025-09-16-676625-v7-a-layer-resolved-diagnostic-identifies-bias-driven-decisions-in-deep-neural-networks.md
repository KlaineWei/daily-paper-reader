---
title: A layer-resolved diagnostic identifies bias-driven decisions in deep neural networks
title_zh: 一种层级解析的诊断方法识别深度神经网络中的偏差驱动决策
authors: "Nakuci, J."
date: 2026-07-16
pdf: "https://www.biorxiv.org/content/10.1101/2025.09.16.676625v7.full.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 层分辨的偏差诊断方法可应用于目标检测和异常检测的可解释性
tldr: 深度神经网络的高置信度不一定源于输入特征，也可能由偏置项驱动，这引发信任问题。本文提出偏置主导指数（BDI），通过层间分解将置信度拆分为输入依赖的特征支持和输入无关的偏置支持。实验表明，在CNN、ViT和Transformer语言模型中，高置信度常与偏置驱动决策共存。BDI还能在读出权重受损时稳定性能，并可用于机制感知的接受规则，实现决策审计与分类。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1714, \"height\": 911}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1715, \"height\": 1346}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1723, \"height\": 748}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1705, \"height\": 412}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1723, \"height\": 1168}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1724, \"height\": 729}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1720, \"height\": 810}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1723, \"height\": 1626}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1783, \"height\": 481}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1624, \"height\": 897}]"
motivation: 现有置信度无法区分决策是否由输入特征支持，导致信任缺失。需要一种诊断指标来揭示决策组成。
method: 提出偏置主导指数（BDI），逐层量化输入无关偏置对决策边界的相对贡献，分解置信度为特征支持和偏置支持。
result: 跨模型系列（CNN、ViT、Transformer）实验显示高置信度常与偏置驱动决策共存；偏置成分在读出权重退化时稳定性能。
conclusion: BDI作为通用诊断指标，可区分特征支持与偏置驱动决策，支持机制感知的审计与分类决策。
---

## 摘要
现代人工智能系统可能既准确又自信，但这本身并不能揭示决策是否得到了输入的充分支持。这造成了信任问题，因为置信度反映的是模型的决断程度，而非支撑这种决断的依据。在此，我们证明神经网络的置信度可以分解为依赖于输入的特征支持和与输入无关的偏移支持。我们通过偏差主导指数（Bias Dominance Index, BDI）形式化这种分解，BDI是一种层级解析的度量，量化了与输入无关的偏移对决策边界的相对贡献，从而揭示置信度究竟主要由特征支持还是偏差驱动。在卷积神经网络、视觉Transformer和Transformer语言模型中，BDI表明高置信度可以与偏差驱动的决策共存。层级解析分析映射了网络深度中偏差驱动支持的分布。扰动分析进一步表明，当读出权重退化时，偏差分量可以稳定性能。最后，我们将决策组成操作化为一个结合置信度和BDI的接受规则，用于机制感知的审计和分诊。综上所述，这些结果将BDI定位为一种通用的决策组成诊断工具，能够区分跨模型家族的特征支持决策和偏差驱动决策。

## Abstract
Modern AI systems can be accurate and confident, but this alone does not reveal whether a decision is well supported by the input. This creates a trust problem because confidence reports how decisive a model is, but not what supports that decisiveness. Here we show that neural-network confidence can be decomposed into input-dependent feature support and input-independent offset support. We formalize this decomposition through the Bias Dominance Index (BDI), a layer-resolved measure quantifying the relative contribution of input-independent offsets to the decision margin, revealing whether confidence is primarily feature-supported or bias-driven. Across convolutional neural networks, a vision transformer and a transformer language model, BDI shows that high confidence can coexist with bias-driven decisions. Layer-resolved analyses map where bias-driven support across network depth. Perturbation analyses further show that the bias component can stabilize performance when readout weights are degraded. Finally, we operationalize decision composition into an acceptance rule that combines confidence and BDI for mechanism-aware auditing and triage. Together, these results position BDI as a general diagnostic of decision composition that distinguishes feature-supported from bias-driven decisions across model families.

---

## 论文详细总结（自动生成）

# 中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：深度神经网络（DNN）在输入不完整、模糊或退化时，常产生高置信度预测，但这种自信可能并非源于输入特征的有力支持，而可能来自与输入无关的偏置项（如偏置参数、归一化偏移等）。传统上仅靠置信度或准确率无法区分决策是“特征支撑”还是“偏置驱动”，这导致了信任问题——模型看似自信，但支撑其决断的机制可能是脆弱的、非证据导向的。
- **整体含义**：本文旨在提出一种机制感知的诊断工具，量化决策边界中偏置相对于特征的贡献，从而揭示模型置信度的真正来源，并帮助用户判断何时可以信任一个预测。该工作对模型可解释性、可靠性审计和安全性具有重要实用价值。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：将神经网络的决策边界（logit margin）分解为输入依赖的特征分量和输入无关的偏置分量，通过“偏置主导指数”（Bias Dominance Index, BDI）量化偏置的相对主导程度。
- **关键技术细节**：
  1. **决策边界分解**：对于输入 \(x\)，最终层logit为 \(z_k(x) = w_k^\top a + b_k\)，目标类 \(t\)与非目标类 \(r\)的边界 \(\Delta z = z_t - z_r = (w_t - w_r)^\top a + (b_t - b_r)\)，其中特征分量 \(C_{\text{feat}} = (w_t - w_r)^\top a\)，偏置分量 \(C_{\text{bias}} = b_t - b_r\)。
  2. **BDI定义**：\[ BDI = \frac{|C_{\text{bias}}|}{|C_{\text{bias}}| + |C_{\text{feat}}| + \epsilon} \]，取值范围[0,1]；0表示完全特征主导，1表示完全偏置主导；阈值0.5作为偏置主导判据。
  3. **层级解析BDI（layer-resolved BDI）**：对每层线性变换 \(u^{(\ell)} = W^{(\ell)} a^{(\ell-1)} + b^{(\ell)}\)，分别计算特征部分和偏置部分，然后利用梯度加权内积得到该层对决策边界的贡献 \(C_{\text{feat}}^{(\ell)} = \langle g^{(\ell)}, u_{\text{feat}}^{(\ell)} \rangle\)，\(C_{\text{bias}}^{(\ell)} = \langle g^{(\ell)}, u_{\text{bias}}^{(\ell)} \rangle\)，进而得到层级BDI。还可汇总为全局BDI_all。
  4. **标签无关形式**：在多分类设置中，使用top-1与top-2 logit之差作为决策边界，无需真实标签，适合无标签部署场景。
  5. **适用范围**：可扩展到各种含偏置项（如线性层偏置、LayerNorm偏移、注意力投影偏置）的模型架构（CNN、ViT、BERT）。
- **公式/算法流程文字说明**：对每个输入，提取最终层激活向量；计算logit边界；分别提取特征和偏置分量；计算BDI。层级版本则逐层计算梯度加权贡献，再求BDI。

## 3. 实验设计：数据集/场景、Benchmark、对比方法
- **数据集与场景**：
  - **点判别任务（dot-discrimination task）**：自制二分类任务（红/蓝点数量判断），训练5个CNN（基于ImageNet预训练卷积层，微调全连接层），测试集1000样本。
  - **Tiny ImageNet**：200类子集，10000张验证图像，用于评估AlexNet、VGG-16、ViT-b/16（ImageNet预训练）的标签无关BDI。
  - **Tiny ImageNet-C**：添加高斯噪声的5个严重等级，每等级1000张，共5000张，用于测试分布偏移下BDI特性。
  - **BERT掩码补全任务**：使用几个人工设计的提示，展示语言模型中BDI的应用。
- **Benchmark**：主要与softmax置信度对比，验证BDI提供了置信度无法揭示的决策机制信息。未与现有其他可解释性方法（如Grad-CAM、DeepLIFT）进行定量比较，仅用DeepLIFT作为定性说明。
- **对比方法**：主要对比“含有偏置”和“去除偏置”时的性能（在扰动分析中），以及在不同置信度水平下高低BDI子集的错误率差异。无直接与其他解释性指标对比。

## 4. 资源与算力
- **明确说明**：论文中提到训练和测试在Google Colab上的NVIDIA A100 GPU上进行（用于点判别任务）。但未详细说明训练时长、总GPU数量或能耗。
- **结论**：算力信息较为简略，仅提及硬件类型，未提供具体训练时间或计算量数据。

## 5. 实验数量与充分性
- **实验数量**：
  - 点判别任务：训练了5个独立模型，每个模型测试1000个样本；还进行了噪声扰动实验（激活噪声 vs 权重噪声，10个噪声水平，1000次模拟）。
  - Tiny ImageNet：AlexNet、VGG-16、ViT-b/16各在clean和corrupted条件下评估；层钳制分析（逐层置零偏置）验证层级BDI。
  - BERT：仅示例性提示，未系统量化。
- **充分性评估**：
  - **优点**：覆盖多种架构（CNN、ViT、Transformer），验证了小任务和大规模数据集上的泛化能力；引入了层级分析和扰动验证，增强了结论可靠性。
  - **不足**：主要在ImageNet-corners的视觉模型上测试，语言模型仅展示少数示例；缺少与其他可解释性指标（如集成梯度、Grad-CAM）的定量对比；消融实验较为简单（仅去除偏置），未系统探讨超参数敏感性。

## 6. 论文的主要结论与发现
- **BDI揭示了置信度无法区分的决策异质性**：相同的软max置信度下，不同样本的BDI差异巨大，存在高置信度但偏置主导的决策。
- **偏置主导在多种架构中普遍存在**：在CNN、ViT和BERT中均存在高置信度偏置主导的决策，层级BDI显示偏置主导在早期卷积层和深层线性层尤其显著。
- **偏置在噪声下具有稳定作用**：当读出权重受到高斯噪声扰动时，保留偏置项可显著提升准确率；而激活噪声下偏置影响不显著。
- **BDI可用于无标签审计**：采用top-1/top-2边界，与置信度结合形成两参数接受规则（Confidence≥τ且BDI≤γ），能够降低错误率，且相比纯置信度阈值可识别机制差异。
- **BDI并非偏置幅度的简单反映**：层级分析显示相同偏置幅度下BDI值存在巨大离散性，说明BDI衡量的是相对支撑而非绝对偏置大小。

## 7. 优点：方法或实验设计上的亮点
- **创新性**：提出“决策组成”（decision composition）概念，量化特征支撑与偏置支撑的相对作用，填补了仅依赖置信度或归因方法的空白。
- **理论清晰**：基于仿射层逻辑的精确分解，形式化简洁，易于理解和实现。
- **实用性强**：标签无关形式使得方法可直接在无真实标签的部署环境中使用；结合置信度与BDI的接受规则可作为可审计的筛选策略。
- **跨架构通用性**：统一处理CNN中的偏置、ViT的LayerNorm偏移、BERT的注意力投影偏置，展示广泛适用性。
- **层级解析能力**：提供深度方向上的偏置主导演化图，有助于定位问题层。

## 8. 不足与局限
- **实验覆盖有限**：语言模型部分仅提供了几个示例，缺乏系统评估；视觉模型主要基于ImageNet系列，未针对更多样化的数据集（如医学图像、自动驾驶场景）验证。
- **对比缺乏**：未与现有归因方法（如Integrated Gradients、Grad-CAM、SHAP）进行定量对比，无法说明BDI在解释性或审计效果上的相对优势。
- **偏置定义局限**：仅考虑“输入无关的显式偏移”，未涵盖权重中隐含的、但与输入相关的虚假关联（如纹理偏置）。作者承认这是局限，但未提供解决方案。
- **梯度饱和问题**：层级BDI依赖局部梯度，可能受饱和区域影响（作者提及，但未提供缓解措施如使用平滑梯度）。
- **扰动实验简单**：仅测试了高斯噪声，未考虑对抗性扰动或其他真实世界退化（如遮挡、模糊、亮度变化）。
- **信任规则的实际验证不足**：虽然提出置信度+BDI的接受规则，但未与现有不确定性拒绝方法（如基于预测熵、模型集成不确定性）进行性能比较，也缺乏在真实高风险场景中的部署案例。

（完）
