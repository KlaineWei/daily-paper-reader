---
title: A layer-resolved diagnostic identifies bias-driven decisions in deep neural networks
title_zh: 一种层级解析的诊断方法识别深度神经网络中的偏差驱动决策
authors: "Nakuci, J."
date: 2026-07-16
pdf: "https://www.biorxiv.org/content/10.1101/2025.09.16.676625v7.full.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 层级偏置主导指数用于神经网络决策可解释性，可转移至目标检测场景
tldr: 深度神经网络的置信度无法揭示决策是否基于输入特征还是内在偏置，这引发信任问题。提出偏置主导指数（BDI），通过层分解将置信度拆分为特征支持与偏置偏移，量化偏置对决策边界的贡献。实验表明，高置信度可与偏置驱动决策共存，BDI在CNN、ViT及Transformer语言模型中均有效，且偏置组件在权重退化时稳定性能。BDI结合置信度形成接受规则，实现机制感知的决策审计与分类。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1714, \"height\": 911}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1715, \"height\": 1346}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1723, \"height\": 748}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1705, \"height\": 412}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1723, \"height\": 1168}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1724, \"height\": 729}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1720, \"height\": 810}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1723, \"height\": 1626}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1783, \"height\": 481}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1624, \"height\": 897}]"
motivation: 现有置信度指标无法区分决策依赖输入特征还是内在偏置，导致对模型判断的信任缺乏依据。
method: 提出偏置主导指数（BDI），通过层分辨度量输入无关偏置对决策边界的相对贡献，分解置信度为特征支持与偏置偏移。
result: BDI揭示高置信度可共存于偏置驱动决策，层分析映射偏置支持深度，扰动实验显示偏置组件在读出权重退化时稳定性能。
conclusion: BDI作为通用诊断工具，结合置信度可实现机制感知的决策审计与分类，提升模型可解释性。
---

## 摘要
现代人工智能系统可以既准确又自信，但这本身并不能揭示决策是否得到了输入的良好支持。这造成了信任问题，因为置信度报告的是模型的决断程度，而不是支持这种决断的依据。在此，我们展示了神经网络的置信度可以分解为依赖于输入的特征支持和独立于输入的偏移支持。我们通过偏差主导指数（BDI）形式化了这种分解，这是一种层级解析的度量，量化了独立于输入的偏移对决策边界的相对贡献，揭示了置信度主要是由特征支持还是由偏差驱动。在卷积神经网络、视觉Transformer和Transformer语言模型中，BDI表明高置信度可以与偏差驱动的决策共存。层级解析分析映射了网络深度上偏差驱动支持的分布。扰动分析进一步表明，当读出权重退化时，偏差成分可以稳定性能。最后，我们将决策构成操作化为一个接受规则，该规则结合了置信度和BDI，用于机制感知的审计和分类。这些结果共同将BDI定位为一种通用的决策构成诊断方法，能够在不同模型家族中区分特征支持的决策和偏差驱动的决策。

## Abstract
Modern AI systems can be accurate and confident, but this alone does not reveal whether a decision is well supported by the input. This creates a trust problem because confidence reports how decisive a model is, but not what supports that decisiveness. Here we show that neural-network confidence can be decomposed into input-dependent feature support and input-independent offset support. We formalize this decomposition through the Bias Dominance Index (BDI), a layer-resolved measure quantifying the relative contribution of input-independent offsets to the decision margin, revealing whether confidence is primarily feature-supported or bias-driven. Across convolutional neural networks, a vision transformer and a transformer language model, BDI shows that high confidence can coexist with bias-driven decisions. Layer-resolved analyses map where bias-driven support across network depth. Perturbation analyses further show that the bias component can stabilize performance when readout weights are degraded. Finally, we operationalize decision composition into an acceptance rule that combines confidence and BDI for mechanism-aware auditing and triage. Together, these results position BDI as a general diagnostic of decision composition that distinguishes feature-supported from bias-driven decisions across model families.