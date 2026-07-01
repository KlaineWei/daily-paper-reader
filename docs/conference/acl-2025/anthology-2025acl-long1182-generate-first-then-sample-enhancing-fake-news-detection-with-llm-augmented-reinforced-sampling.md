---
title: "Generate First, Then Sample: Enhancing Fake News Detection with LLM-Augmented Reinforced Sampling"
title_zh: 先生成后采样：利用LLM增强强化采样提升假新闻检测
authors: "Zhao Tong, Yimeng Gu, Huidong Liu, Qiang Liu, Shu Wu, Haichao Shi, Xiao-Yu Zhang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1182.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 使用LLM和强化采样进行假新闻检测
tldr: 针对假新闻检测性能低且数据不平衡问题，利用LLM生成多种风格假新闻样本，结合强化采样增强训练集，有效提升检测准确率，尤其改善了假新闻的识别能力。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 760, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 700, \"height\": 766, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1628, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 382, \"height\": 287, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 378, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 381, \"height\": 284, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 378, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 382, \"height\": 286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1182/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 379, \"height\": 286, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1182/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1607, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1182/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 780, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1182/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 818, \"height\": 444, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1182/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 833, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1182/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 829, \"height\": 307, \"label\": \"Table\"}]"
motivation: "假新闻检测器对假新闻识别性能落后20%以上。"
method: LLM生成多风格假新闻并结合强化采样。
result: 显著提升假新闻检测准确率。
conclusion: 为数据增强提供新思路。
---

## Abstract
The spread of fake news on online platforms has long been a pressing concern. Considering this, extensive efforts have been made to develop fake news detectors. However, a major drawback of these models is their relatively low performance—lagging by more than 20%—in identifying fake news compared to real news, making them less suitable for practical deployment. This gap is likely due to an imbalance in the dataset and the model’s inadequate understanding of data distribution on the targeted platform. In this work, we focus on improving the model’s effectiveness in detecting fake news. To achieve this, we first adopt an LLM to generate fake news in three different styles, which are later incorporated into the training set to augment the representation of fake news. Then , we apply Reinforcement Learning to dynamically sample fake news, allowing the model to learn the optimal real-to-fake news ratio for training an effective fake news detector on the targeted platform. This approach allows our model to perform effectively even with a limited amount of annotated news data and consistently improve detection accuracy across different platforms. Experimental results demonstrate that our approach achieves state-of-the-art performance on two benchmark datasets, improving fake news detection performance by 24.02% and 11.06% respectively.

---

## 论文详细总结（自动生成）

# 论文总结：Generate First, Then Sample: Enhancing Fake News Detection with LLM-Augmented Reinforced Sampling

## 1. 论文的核心问题与整体含义
- **研究动机**：假新闻检测器在实际部署中面临严重性能不平衡——识别假新闻的F1分数比识别真新闻低20%以上，导致大量假新闻被漏检。
- **问题根源**：现有数据集存在严重样本不平衡（假新闻数量远少于真新闻），且模型缺乏对目标平台数据分布的自适应能力。
- **整体目标**：提出一种既能缓解假新闻样本不足，又能自动学习最优真假新闻比例的方法，从而显著提升假新闻检测的准确性。

## 2. 论文提出的方法论
- **核心思想**：先生成后采样（Generate First, Then Sample）。先利用大语言模型（LLM）生成多种风格的假新闻以扩充训练集，再通过强化学习动态调整假新闻的采样比例，使模型适应特定平台的数据分布。
- **关键技术细节**：
  - **多视角假新闻生成**：使用ChatGLM-6B作为LLM，对每条原始假新闻以三种风格（重写、扩展、伪装）生成变体，使假新闻数量变为原来的4倍（原始+3种生成）。
  - **强化采样**：将最优采样比例的学习建模为马尔可夫决策过程（MDP），并使用深度Q网络（DQN）求解。
    - **状态**：由四部分组成：全局真假比（R）、主题级真假比（Φ）、预训练模型的置信度分数（P）、新闻主题标签（D）。
    - **动作空间**：四个离散动作，对应假新闻采样比例分别为50%、100%、150%、200%。
    - **奖励函数**：结合验证集上的准确率（Acc）和宏平均F1（Macro-F1），通过权重α和β平衡。
    - **训练流程**：在每个时间步t，智能体观察当前状态st，选择动作at调整采样比例，训练假新闻检测器一个epoch，计算奖励rt并更新至下一状态st+1，通过最小化时间差分误差来更新DQN网络。

## 3. 实验设计
- **数据集**：
  - Weibo21（中文社交平台）
  - GossipCop（英文娱乐新闻）
  - 额外在Twitter数据集上进行泛化性验证。
- **基准方法**：
  - 深度学习方法：BERT、EANN、Publisher-Emo、ENDEF。
  - 基于LLM的方法：GPT-3.5-turbo（直接提示）、SuperICL、ARG、LLM-GAN。
- **评估指标**：宏F1、准确率、真新闻F1、假新闻F1。
- **实验组数**：主实验（2个数据集×9个baseline）、消融实验（去除3个组件）、敏感性分析（动作空间大小、α/β权重）、附加LLM泛化实验（Llama3-8B）和额外数据集实验。

## 4. 资源与算力
- 论文明确说明：实验在4块NVIDIA GeForce RTX 4090 GPU（每块24GB显存）上进行。
- 训练细节：使用Adam优化器，batch size=16，学习率1e-4，训练10个epoch。
- 未提供总训练时长，但基于硬件配置可推测在合理范围内。

## 5. 实验数量与充分性
- **充分性**：实验设计较为全面，包括：
  - 主实验在两个标准数据集上对比9种代表性方法；
  - 消融实验验证了LLM生成（G）、强化采样（RS）、主题分类（TC）三个组件的必要性；
  - 敏感性分析考察了动作空间大小、奖励函数权重对性能的影响；
  - 附加实验使用Llama3-8B作为LLM生成器、在Twitter数据集上测试，验证了方法的泛化性。
- **客观性与公平性**：使用了公开数据集和标准评估指标，baseline涵盖经典和新近方法，消融实验设计合理。但缺乏对生成假新闻质量可能导致偏差的讨论。

## 6. 论文的主要结论与发现
- 提出GSFND框架在Weibo21和GossipCop上均达到SOTA，假新闻检测F1分别提升11.06%和24.02%，同时真新闻检测F1也有提升。
- LLM生成的多风格假新闻能有效缓解样本不平衡；强化学习动态采样能自适应目标平台，找到最优真假比（Weibo21最优比为1:1.5，GossipCop为1:0.5）。
- 消融实验表明，去除LLM生成导致最大性能下降，去除强化采样次之，去除主题分类也有显著影响，证实各组件均不可或缺。

## 7. 优点
- **创新性**：首次将LLM数据增强与强化学习采样结合用于假新闻检测，针对“假新闻检测性能差”这一核心问题提出系统解决方案。
- **状态设计全面**：将全局比值、主题比值、置信度、主题标签融入状态，使RL智能体能多维感知数据分布。
- **实验扎实**：不仅包含主实验和消融，还进行了超参数敏感性和跨模型/跨数据集泛化验证，体现了方法的鲁棒性。
- **可部署性**：使用ChatGLM-6B等轻量级LLM，支持消费级GPU运行，有利于实际落地。

## 8. 不足与局限
- **生成质量与伦理风险**：论文未深入分析LLM生成假新闻的质量是否可能引入偏见或破坏检测器鲁棒性；生成假新闻本身可能被滥用于制造虚假内容。
- **动作空间离散**：仅支持4个离散采样比例，论文自承未来可扩展到连续值。
- **LLM选择有限**：主实验仅使用ChatGLM-6B，虽然在附录补充了Llama3-8B实验，但未系统对比多种LLM（如GPT-4、Llama2等）的影响。
- **泛化性验证不足**：虽然增加了Twitter数据集，但主要实验仅覆盖两个语种（中文、英文），对其他语言、多模态场景未涉及。
- **计算资源**：虽然使用了4块4090，但对于资源受限的场景仍可能过高；论文未披露训练总耗时，无法评估实际效率。

（完）
