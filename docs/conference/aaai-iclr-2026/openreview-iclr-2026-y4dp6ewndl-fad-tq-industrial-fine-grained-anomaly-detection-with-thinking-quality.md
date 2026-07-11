---
title: "FAD-TQ: Industrial Fine-grained Anomaly Detection with Thinking Quality"
title_zh: FAD-TQ：具备思维质量的工业细粒度异常检测
authors: "Weijia Li, Xin Liu, Guo-Sen Xie, Hongsong Wang, Caifeng Shan, Fang Zhao"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=Y4DP6eWndl"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 细粒度异常检测的可解释推理
tldr: 本文提出FAD-TQ，一个轻量级强化学习框架用于工业细粒度异常检测。基于分组策略梯度范式的训练无需参考模型和监督微调数据，使模型能够生成关于异常类型和原因的可解释推理。实验表明其在多个工业数据集上优于现有方法，同时具备思维质量。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有异常检测方法缺乏过程级可解释推理，且奖励函数能力有限。
method: 提出FAD-TQ，基于分组策略梯度范式的轻量级强化学习框架。
result: 在工业异常检测数据集上实现了高精度和可解释推理。
conclusion: FAD-TQ为异常检测提供了轻量级可解释方案。
---

## Abstract
Recent research in industrial anomaly detection (IAD) has shifted beyond binary classification and segmentation, increasingly focusing on process-level, interpretable reasoning about the type and cause of anomalies. While multimodal
large language models (MLLMs) have enabled this reformulation through visual
question answering, current anomaly detection methods still suffer from two major limitations: the limited capacity of reward functions to capture intricate complexities and the reliance on generating supervised fine-tuning (SFT) data. Hence,
we propose FAD-TQ, a lightweight reinforcement learning framework for finegrained anomaly detection with thinking quality. Built upon the Group Policy
Gradient paradigm, it eliminates the reference model and KL regularization to reduce rollout overhead and directly optimize the original reinforcement learning
objective. To enable fine-grained guidance over the reasoning process, we design a thinking quality reward composed of two components: an efficiency reward
that penalizes redundant reasoning, and a relevance reward that encourages taskaligned, coherent thought trajectories. Furthermore, we introduce MVTec-LOCOAD-Pair3C, a principled evaluation protocol built on the existing dataset. By
defining three decision types—normal, structural anomaly, and logical anomaly,
rather than binary classification. Extensive experiments demonstrate that FAD-TQ
improves interpretability, accuracy, streamlined reasoning and training efficiency
with reduced computational costs. It demonstrates the potential of using smallscale benchmarks to evaluate MLLM capabilities in IAD. We hope this framework
and evaluation protocol can serve as an example for future research on processlevel reasoning in anomaly detection.

---

## 论文详细总结（自动生成）

# 论文总结：FAD-TQ：具备思维质量的工业细粒度异常检测

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：工业异常检测（IAD）正从简单的二分类/分割任务转向过程级、可解释的推理，即不仅要判断是否有异常，还要解释异常的类型和原因。
- **现有方法局限**：当前基于多模态大语言模型（MLLMs）的方法存在两大瓶颈：
  - 奖励函数的容量有限，难以捕捉复杂的异常特征。
  - 生成监督微调（SFT）数据成本高、依赖性强。
- **整体目标**：提出一个轻量级强化学习框架，实现对异常种类和原因的细粒度、可解释推理，同时降低训练开销。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：利用分组策略梯度（Group Policy Gradient, GPP）范式，无需参考模型和KL正则化，直接优化原始强化学习目标，从而减少 rollout 开销。
- **关键技术**：
  - **奖励设计**：提出“思维质量（Thinking Quality）”奖励，由两部分组成：
    - 效率奖励：惩罚冗余推理，鼓励简洁的思维链。
    - 相关性奖励：鼓励推理轨迹与任务目标一致、逻辑连贯。
  - **框架特点**：轻量级，不依赖SFT数据，无需参考模型，训练效率高。
- **算法流程说明**（文字描述）：
  1. 基于分组策略梯度，模型通过多次采样生成推理轨迹。
  2. 对每个轨迹计算思维质量奖励（效率+相关性）。
  3. 直接利用该奖励更新策略网络，无需KL散度项或参考模型。

## 3. 实验设计

- **数据集**：基于现有数据集构建了 **MVTec-LOCOAD-Pair3C** 评估协议，该协议定义了三种决策类型：正常、结构异常、逻辑异常（而非二分类）。底层数据来源于 MVTec LOCO AD 等工业异常检测数据集。
- **Benchmark**：提出的评估协议本身作为基准，用于衡量模型在三种决策类型上的细粒度推理能力。
- **对比方法**：论文宣称“优于现有方法”，但摘要中未列出具体对比方法的名称，仅笼统提及“existing anomaly detection methods”和“current anomaly detection methods”。因此具体对比方法需查阅全文。

## 4. 资源与算力

- 文中**未明确说明**使用的 GPU 型号、数量、训练时长等算力细节。仅提及“reduced computational costs”和“lightweight”，但无具体硬件配置。

## 5. 实验数量与充分性

- **实验数量**：摘要仅用了“Extensive experiments”概括，未列出具体实验组数（如不同数据集、消融实验等）。
- **充分性判断**：基于摘要信息，无法判断实验是否充分、客观、公平。需要查看完整论文的：
  - 是否在多个数据集上验证？
  - 是否进行了消融研究（例如奖励组件的贡献、策略梯度变体对比等）？
  - 是否与强基线（如其他MLLM-based方法）公平对比？
- 目前仅能评价：提出了新的评估协议，但实验报告细节缺失。

## 6. 主要结论与发现

- **主要发现**：FAD-TQ 在可解释性、准确性、推理简洁性和训练效率上均有提升，同时降低了计算成本。
- **潜力发现**：展示了利用小规模基准（MVTec-LOCOAD-Pair3C）评估 MLLM 在工业异常检测中推理能力的可行性。
- **贡献总结**：为工业异常检测的过程级推理提供了一个轻量级、可解释的解决方案和标准化评估协议。

## 7. 优点（方法或实验设计的亮点）

- **方法层面**：
  - 无需参考模型和SFT数据，大幅降低训练成本。
  - 奖励函数设计新颖：将推理效率与相关性解耦，引导模型生成既准确又简洁的推理链。
  - 基于分组策略梯度，直接优化原始RL目标，减少计算开销。
- **实验设计层面**：
  - 提出了 MVTec-LOCOAD-Pair3C 评估协议，将异常检测从二分类升级为三分类（正常、结构异常、逻辑异常），更贴合工业实际需求。
  - 协议设计具有原则性，有望成为未来细粒度异常检测推理的标准基准。

## 8. 不足与局限

- **实验覆盖不足**：摘要未提供详细的实验设置、对比结果和消融研究，无法验证方法的具体优势和鲁棒性。
- **偏差风险**：仅依赖单一数据集（MVTec LOCO AD 衍生集）可能无法代表工业异常检测的全部场景（如纹理、物体等）。
- **应用限制**：
  - 方法基于强化学习，可能对奖励函数的设计敏感，泛化到新异常类型时需重新设计奖励。
  - 轻量级设计可能牺牲了部分表达力，与大型MLLM相比在复杂场景下的推理准确性有待验证。
- **资源与复现**：未提供算力信息，复现门槛不明确。

（完）
