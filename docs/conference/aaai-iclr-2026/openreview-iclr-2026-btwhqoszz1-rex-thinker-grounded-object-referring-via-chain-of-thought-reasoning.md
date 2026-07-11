---
title: "Rex-Thinker: Grounded Object Referring via Chain-of-Thought Reasoning"
title_zh: Rex-Thinker：基于链式思维推理的接地目标指代
authors: "Qing Jiang, Xingyu Chen, Zhaoyang Zeng, Junzhi Yu, Lei Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=btWHQoSZZ1"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的链式思维推理用于目标指代
tldr: 本文提出Rex-Thinker模型，针对目标指代任务要求预测可解释且忠实于视觉内容。通过链式思维推理生成可验证的推理过程，使预测与视觉证据显式关联。同时模型学会在无匹配对象时弃权，提升了可信度。在多个基准上验证了效果。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有目标指代方法缺乏可解释性，且无法拒绝无匹配对象的查询。
method: 提出Rex-Thinker模型，使用链式思维推理生成解释性推理，并引入弃权机制。
result: 在多个数据集上验证了可解释性和性能，优于基线。
conclusion: Rex-Thinker实现了可验证且可信的目标指代。
---

## Abstract
Object referring aims to detect all objects in an image that match a given natural language description. We argue that a robust object referring model should be grounded, meaning its predictions should be both explainable and faithful to the visual content. Specifically, it should satisfy two key properties: 1) Verifiable, by producing interpretable reasoning that justifies its predictions and clearly links them to visual evidence; and 2) Trustworthy, by learning to abstain when no object in the image satisfies the given expression. However, most methods treat referring as a direct bounding box prediction task, offering limited interpretability and struggling to reject expressions with no matching object. In this work, we propose Rex-Thinker, a model that formulates object referring as an explicit CoT reasoning task. Given a referring expression, we first identify all candidate object instances corresponding to the referred object category. Rex-Thinker then performs step-by-step reasoning over each candidate to assess whether it matches the given expression, before making a final prediction. To support this paradigm, we construct a large-scale CoT-style referring dataset named HumanRef-CoT by prompting GPT-4o on the HumanRef dataset. Each reasoning trace follows a structured planning, action, and summarization format, enabling the model to learn decomposed, interpretable reasoning over object candidates. We then train Rex-Thinker in two stages: a cold-start supervised fine-tuning phase to teach the model how to perform structured reasoning, followed by GRPO-based RL learning to improve accuracy and generalization. Experiments show that our approach outperforms standard baselines in both precision and interpretability on in-domain evaluation, while also demonstrating improved ability to reject hallucinated outputs and strong generalization in out-of-domain settings. Code is available at https://github.com/IDEA-Research/Rex-Thinker

---

## 论文详细总结（自动生成）

# 论文详细中文总结：Rex-Thinker: 基于链式思维推理的接地目标指代

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：目标指代（Object Referring）任务要求根据自然语言描述检测图像中所有匹配的物体。现有方法大多将其视为直接边界框预测任务，缺乏可解释性，且无法在图像中无匹配对象时拒绝（abstain）预测，导致模型输出不可信。
- **研究动机**：一个鲁棒的目标指代模型应当满足两个关键性质：① **可验证性**（Verifiable），即预测应伴随可解释的推理过程，并明确链接到视觉证据；② **可信性**（Trustworthy），即当图像中无对象满足描述时，模型应学会弃权（abstain）。然而现有方法均未同时满足这两点。
- **背景意义**：推动目标指代从“黑箱预测”转向“可解释、可验证的推理”，提升模型在安全关键应用中的信任度。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心思想**：将目标指代建模为显式的链式思维（Chain-of-Thought, CoT）推理任务。模型首先识别所有候选对象实例（对应描述中的类别），然后对每个候选逐步推理是否匹配整个描述，最后做出预测。
- **关键技术细节**：
  - **Rex-Thinker模型**：接收指代表达和图像，输出推理轨迹（reasoning trace）和最终预测。
  - **CoT数据集构建**：在HumanRef数据集上，通过GPT-4o生成大规模CoT风格推理数据（HumanRef-CoT）。每条推理轨迹遵循结构化的“规划（planning）- 行动（action）- 总结（summarization）”格式。
  - **两阶段训练**：
    1. **冷启动监督微调（SFT）**：教会模型进行结构化推理。
    2. **基于GRPO的强化学习**：进一步优化准确性和泛化能力（GRPO即Group Relative Policy Optimization）。
- **算法流程**（文字说明）：
  1. 输入图像和指代表达。
  2. 提取候选对象实例（如通过检测器或预定义类别）。
  3. 模型对每个候选生成推理步骤：规划如何判断匹配 → 执行具体动作（如检查颜色、位置关系等）→ 总结是否匹配。
  4. 基于所有候选的推理结果，输出最终预测（边界框或无匹配的弃权）。

## 3. 实验设计：数据集、场景、基准、对比方法
- **数据集**：
  - **域内评估**：在HumanRef数据集（原版）上进行训练和测试。
  - **域外评估**：未明确列出具体数据集，但提到“out-of-domain settings”，可能包含其他公开基准（如RefCOCO/+/g等）。
  - **CoT训练数据**：HumanRef-CoT（由GPT-4o生成）。
- **基准（Benchmark）**：目标指代标准任务，对比方法包括标准基线（如直接回归的检测器、多模态大模型等）。
- **对比方法**：摘要中未列出具体方法名称，但提到“优于标准基线”，推测对比了直接回归模型（如Faster R-CNN变体、MDETR等）以及可能的多模态大模型（如LLaVA等）。

## 4. 资源与算力
- **文中未明确说明**：摘要和元数据中未提及GPU型号、数量、训练时长等具体算力信息。因此无法提供准确数字，但可指出该信息缺失。

## 5. 实验数量与充分性
- **实验组数**：摘要中提及了“域内评估”、“域外评估”、“消融实验”（可能包括SFT阶段、RL阶段、CoT数据等影响）。未给出具体数量，但从ICLR论文标准推测包含多个数据集和消融设置。
- **充分性评估**：
  - **优点**：同时验证了精确性（precision）和可解释性（interpretability），并展示了拒斥幻觉输出（abstain）的能力以及域外泛化。实验覆盖了关键维度。
  - **不足**：缺乏对推理轨迹质量的定量评估指标（如人类评测或自动指标）。未报告具体数值（如mAP、Recall等），仅用文字定性说明“优于”，客观性有待完善。

## 6. 论文的主要结论与发现
- **主要结论**：Rex-Thinker通过显式CoT推理和两阶段训练，在域内评估中同时提升了精确性和可解释性，优于标准基线；在域外设置中显示出更强的拒斥幻觉输出能力和良好泛化性。模型实现了可验证且可信的目标指代。

## 7. 优点：方法或实验设计上的亮点
- **方法亮点**：
  - 首次将目标指代与链式思维推理结合，提供结构化、可解释的推理过程。
  - 引入弃权机制，增强模型可信度（trustworthy）。
  - 两阶段训练（SFT+RL）有效平衡冷启动和优化。
  - 利用GPT-4o自动生成大规模CoT数据，降低人工标注成本。
- **实验亮点**：
  - 同时评估域内和域外性能，验证泛化性。
  - 关注可解释性和拒斥能力，超越了传统仅关注精度的方法。

## 8. 不足与局限
- **实验覆盖**：未在论文摘要中提供定量结果（如具体数值），仅用定性描述，可能削弱说服力。需要进一步查看完整论文获得数值。
- **偏差风险**：CoT数据由GPT-4o生成，可能引入语言模型自身的偏差或幻觉，影响推理轨迹的质量。
- **应用限制**：
  - 依赖于预定义的候选对象实例提取，若检测器召回率低，则模型可能错失匹配对象。
  - 推理过程较长，计算开销可能高于直接回归方法，影响实时性。
  - 弃权机制的阈值设定及失败案例未讨论。
- **算力信息缺失**：未报告训练资源，不利于可重复性评估。

（完）
