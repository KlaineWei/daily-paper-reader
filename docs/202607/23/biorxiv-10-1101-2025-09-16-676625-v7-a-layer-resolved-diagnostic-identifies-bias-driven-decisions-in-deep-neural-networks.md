---
title: A layer-resolved diagnostic identifies bias-driven decisions in deep neural networks
title_zh: 一种分层诊断方法识别深度神经网络中的偏差驱动决策
authors: "Nakuci, J."
date: 2026-07-16
pdf: "https://www.biorxiv.org/content/10.1101/2025.09.16.676625v7.full.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 用于深度神经网络可解释性的层解析诊断方法
tldr: 现代AI系统的高置信度可能来自输入无关的偏移而非特征支持，导致信任问题。本文提出偏置优势指数（BDI），通过层解析度量量化偏移对决策边界的贡献。实验表明，在CNN、视觉Transformer和Transformer语言模型中，高置信度可与偏移驱动决策共存，且偏移成分在读出权重退化时稳定性能。BDI实现了机制感知的决策审核与分流。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1714, \"height\": 911}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1715, \"height\": 1346}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1723, \"height\": 748}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1705, \"height\": 412}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1723, \"height\": 1168}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1724, \"height\": 729}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1720, \"height\": 810}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1723, \"height\": 1626}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1783, \"height\": 481}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-09-16-676625-v7/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1624, \"height\": 897}]"
motivation: 高置信度不能区分决策是基于输入特征还是输入无关的偏移，需要诊断决策组成。
method: 提出偏置优势指数（BDI），层解析地量化输入无关偏移对决策边界的相对贡献。
result: 在多种模型上高置信度可共存于偏移驱动决策；偏移成分在读出权重退化时稳定性能。
conclusion: BDI作为通用诊断工具，能区分特征支持和偏移驱动决策，支持机制感知的审计。
---

## 摘要
现代人工智能系统可以做到准确且自信，但这本身并不能揭示决策是否得到了输入的良好支持。这造成了信任问题，因为置信度反映的是模型的决定性程度，而非支撑这种决定性的依据。在这里，我们表明神经网络置信度可以分解为依赖于输入的特征支持和独立于输入的偏移支持。通过偏差主导指数（BDI），一种分层度量指标，量化独立于输入的偏移对决策边际的相对贡献，我们正式化这种分解，从而揭示置信度是主要依赖特征支持还是由偏差驱动。在卷积神经网络、视觉Transformer和Transformer语言模型中，BDI表明高置信度可以与偏差驱动决策共存。分层分析映射了网络深度中偏差驱动支持的位置。扰动分析进一步表明，当读出权重退化时，偏差分量可以稳定性能。最后，我们将决策构成操作化为一个接受规则，结合置信度和BDI进行机制感知的审计与分流。总之，这些结果将BDI定位为一种通用的决策构成诊断工具，能够区分不同模型家族中特征支持与偏差驱动的决策。

## Abstract
Modern AI systems can be accurate and confident, but this alone does not reveal whether a decision is well supported by the input. This creates a trust problem because confidence reports how decisive a model is, but not what supports that decisiveness. Here we show that neural-network confidence can be decomposed into input-dependent feature support and input-independent offset support. We formalize this decomposition through the Bias Dominance Index (BDI), a layer-resolved measure quantifying the relative contribution of input-independent offsets to the decision margin, revealing whether confidence is primarily feature-supported or bias-driven. Across convolutional neural networks, a vision transformer and a transformer language model, BDI shows that high confidence can coexist with bias-driven decisions. Layer-resolved analyses map where bias-driven support across network depth. Perturbation analyses further show that the bias component can stabilize performance when readout weights are degraded. Finally, we operationalize decision composition into an acceptance rule that combines confidence and BDI for mechanism-aware auditing and triage. Together, these results position BDI as a general diagnostic of decision composition that distinguishes feature-supported from bias-driven decisions across model families.