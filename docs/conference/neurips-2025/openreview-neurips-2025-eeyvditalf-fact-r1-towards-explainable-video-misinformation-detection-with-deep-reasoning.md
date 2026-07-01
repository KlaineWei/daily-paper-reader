---
title: "Fact-R1: Towards Explainable Video Misinformation Detection with Deep Reasoning"
title_zh: Fact-R1：面向可解释视频错误信息检测的深度推理方法
authors: "Fanrui Zhang, Dian Li, Qiang Zhang, Chenjun, sinbadliu, Junxiong Lin, Jiahong Yan, Jiawei Liu, Zheng-Jun Zha"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EeyvDitalf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的视频错误信息检测
tldr: 现有视频错误信息检测方法过拟合模板且缺乏深度推理。本文引入FakeVV大规模基准和Fact-R1框架，通过长链思考指令微调和规则强化学习实现可解释的深度推理，显著提升虚假视频检测的可解释性和泛化能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 缺乏大规模视频错误信息数据集，现有方法过拟合且可解释性不足。
method: 提出Fact-R1框架，结合长链思考指令微调、偏好对齐和协同规则强化学习。
result: 在FakeVV基准上实现了可解释的深度推理检测。
conclusion: Fact-R1增强了视频错误信息检测的可解释性和准确率。
---

## Abstract
The rapid spread of multimodal misinformation on social media has raised growing concerns, while research on video misinformation detection remains limited due to the lack of large-scale, diverse datasets. Existing methods often overfit to rigid templates and lack deep reasoning over deceptive content. To address these challenges, we introduce FakeVV, a large-scale benchmark comprising over 100,000 video-text pairs with fine-grained, interpretable annotations. In addition, we further propose Fact-R1, a novel framework that integrates deep reasoning with collaborative rule-based reinforcement learning. Fact-R1 is trained through a three-stage process: (1) misinformation long-Chain-of-Thought (CoT) instruction tuning, (2) preference alignment via Direct Preference Optimization (DPO), and (3) Group Relative Policy Optimization (GRPO) using a novel verifiable reward function. This enables Fact-R1 to exhibit emergent reasoning behaviors comparable to those observed in advanced text-based reinforcement learning systems, but in the more complex multimodal misinformation setting. Our work establishes a new paradigm for misinformation detection, bridging large-scale video understanding, reasoning-guided alignment, and interpretable verification.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文摘要内容生成的结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：社交媒体上多模态错误信息的快速传播日益引发担忧，但针对视频错误信息检测的研究由于缺乏大规模、多样化的数据集而进展有限。
- **核心问题**：现有方法过度拟合于固定模板，缺乏对欺骗性内容的深度推理能力，导致可解释性和泛化能力不足。需要一种既能准确检测视频虚假信息又能提供可解释推理的解决方案。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：构建大规模、细粒度标注的视频错误信息基准（FakeVV），并设计一个集成深度推理与规则强化学习的新型框架（Fact-R1），通过三阶段训练实现可解释的检测。
- **关键技术细节**：
    1. **FakeVV基准**：包含超过10万个视频-文本对，并带有细粒度、可解释的标注。
    2. **Fact-R1框架**：通过三阶段训练流程：
        - **阶段1：长链思维（CoT）指令微调**：使模型能够生成逐步推理链条来解释错误信息。
        - **阶段2：偏好对齐**：使用直接偏好优化（DPO），对齐模型输出与人类对合理推理的偏好。
        - **阶段3：协同规则强化学习**：使用一种新颖的可验证奖励函数进行组相对策略优化（GRPO），促使模型展现出与高级文本强化学习系统类似的突现推理行为（emergent reasoning behaviors），但在更复杂的多模态错误信息场景中。
- **公式或算法流程**：摘要未给出具体数学公式，但流程可概括为：输入视频-文本对 → CoT推理生成 → DPO偏好微调 → GRPO强化学习（基于可验证奖励） → 输出可解释的检测结果。

### 3. 实验设计：数据集、基准与对比方法

- **数据集**：论文创建了FakeVV基准，包含超过10万个视频-文本对，覆盖多样化的错误信息类型，并提供细粒度、可解释的标注。未提及使用的其他外部数据集。
- **基准**：FakeVV本身即作为主要基准（benchmark）用于评估。
- **对比方法**：摘要未明确列出具体对比方法，但从动机推断，应会对比现有过度依赖模板的方法和缺乏深度推理的基线模型。

### 4. 资源与算力

- **说明**：论文摘要中**没有明确提及**使用的GPU型号、数量、训练时长等算力信息。该信息可能存在于论文正文但未被摘要覆盖。

### 5. 实验数量与充分性

- **实验数量**：摘要仅从整体角度描述结果，未给出具体实验组数（如消融实验、不同数据集测试、跨领域泛化实验等）。
- **充分性与客观性**：摘要声称Fact-R1实现了可解释的深度推理检测，并建立了新的范式。但由于缺乏具体实验细节（如对比表格、消融数据、统计显著性测试等），仅凭摘要难以判断实验的充分性和客观公平性。需要阅读全文获取详细实验设计。

### 6. 论文的主要结论与发现

- **主要发现**：Fact-R1框架成功地将深度推理和可解释性引入视频错误信息检测，在FakeVV基准上显著提升了检测的可解释性和准确率。
- **关键结论**：通过长链思维指令微调、偏好对齐和规则强化学习的组合，模型能够展现出类似于高级文本推理系统的突现推理行为，但针对的是更复杂的多模态虚假信息场景。这项工作为错误信息检测建立了新的范式，连接了大规模视频理解、推理引导对齐和可解释验证。

### 7. 优点：方法或实验设计上的亮点

- **方法亮点**：
    - **首创性**：提出了首个大规模、细粒度可解释的视频错误信息基准FakeVV（10万+视频-文本对）。
    - **三阶段训练框架**：巧妙结合了CoT指令微调、DPO偏好对齐和基于规则强化学习的GRPO，将深度推理能力成功迁移到多模态虚假检测中。
    - **可验证奖励函数**：为强化学习提供了可靠的信号，促进了模型推理行为的涌现。
    - **提升可解释性**：通过长链思维推理，不仅检测结果，还能给出逐步解释，增强了模型的可信度和透明度。

### 8. 不足与局限

- **实验覆盖不足**（基于摘要推断）：未展示在不同类型虚假视频（如深度伪造、语境操纵、虚假字幕）上的分解性能，也未说明在跨领域或少样本场景下的泛化能力。
- **偏差风险**：FakeVV数据集本身的覆盖范围、标注一致性、潜在的标注偏见（如语言、文化、主题偏差）未在摘要中讨论，可能影响方法的公平性和泛化性。
- **计算代价**：三阶段训练（指令微调+DPO+GRPO）通常需要大量计算资源，但摘要未透露，对于实际部署可能存在效率瓶颈。
- **应用限制**：方法依赖高质量的视频-文本对和可验证的奖励函数设计，在真实开放环境（噪声、缺失模态、对抗样本）下的鲁棒性尚未说明。
- **对比不充分**：未提及与现有其他可解释错误检测方法（如基于注意力、因果推理等方法）的直接定量对比，难以评判其相对优势。

（完）
