---
title: Interpretable compositional computation with recurrent neural networks
title_zh: 可解释的循环神经网络组合计算
authors: "Pezon, L., Van Meegen, A."
date: 2026-06-29
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.23.733979v1.full.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 神经网络可解释组合计算理论
tldr: 认知灵活性依赖可重用组件的组合性，但多任务神经网络中共享组件的本质不清。本文发展低秩循环神经网络潜空间共享动态度量结构的可解释组合计算理论，发现共享潜组件与任务依赖活动兼容，通过连接统计和神经表征识别其标志，并定位任务依赖的不同计算入口。这些结果为组合计算提供机制理解和可测试预测。
source: biorxiv
selection_source: fresh_fetch
motivation: 探索多任务神经网络中组合计算共享组件的本质和任务依赖使用方式。
method: 发展基于低秩RNN低维潜空间共享动态度量结构的可解释组合计算理论。
result: 发现共享潜组件与任务依赖活动兼容，识别了连接统计和神经表征中的标志，定位了任务依赖的不同计算入口。
conclusion: 理论提供了组合计算的机制理解和可测试标志，可解释不同组合任务解决方案。
---

## 摘要
灵活认知利用可复用组件实现对不同情境或任务的快速行为适应。对多任务训练的人工神经网络的分析表明，这种组合性由跨任务共享和复用的动力学结构支持。然而，这些共享组件的本质以及它们如何以任务依赖的方式被利用仍不清楚。在此，我们基于低秩循环神经网络低维潜空间中的共享动力学结构，发展了一种可解释的组合计算理论。我们证明这些共享潜组件在神经活动中并不直接可见，因此与任务依赖的活动兼容。我们在连接统计和神经表征中识别出共享潜组件的标志。这些标志为网络对特定扰动实验的响应提供了可检验的预测。最后，我们识别出任务依赖可以进入计算的不同位点，从而能够表征组合任务的定性不同解。总之，我们的理论通过低秩网络中的共享组件提供了对组合计算的机制性理解和可检验的标志。

## Abstract
Flexible cognition utilizes reusable components to enable rapid adaptation of behavior to different contexts or tasks. Analysis of artificial neural networks trained on multiple tasks suggested that this compositionality is supported by dynamical structures which are shared and re-used across tasks. However, the nature of these shared components, and how they can be used in a task-dependent manner, remained unclear. Here, we develop a theory of interpretable compositional computation based on shared dynamical structures in the low-dimensional latent space of low-rank recurrent neural networks. We show that these shared latent components are not immediately visible in the neural activity, and are thus compatible with task-dependent activity. We identify hallmarks of shared latent components both in the connectivity statistics and the neural representations. These hallmarks yield testable predictions for the networks response to specific perturbation experiments. Finally, we identify distinct loci where task-dependence can enter the computation, allowing us to characterize qualitatively different solutions to compositional tasks. In summary, our theory provides a mechanistic understanding and testable hallmarks of compositional computation via shared components in low-rank networks.