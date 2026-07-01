---
title: Enhancing Interpretable Image Classification Through LLM Agents and Conditional Concept Bottleneck Models
title_zh: 通过LLM智能体和条件概念瓶颈模型增强可解释图像分类
authors: "Yiwen Jiang, Deval Mehta, Wei Feng, Zongyuan Ge"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.600.pdf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 通过概念瓶颈模型增强可解释图像分类，与可解释目标检测强相关
tldr: 针对概念瓶颈模型概念冗余或覆盖不足的问题，提出基于LLM智能体的动态概念库调整方法，并设计条件概念瓶颈模型改进概念评分机制，在保持可解释性的同时提升图像分类性能。实验证明该方法有效平衡了概念充分性与简洁性，为可解释深度学习提供了新思路。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.600/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.600/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1491, \"height\": 695, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.600/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1317, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.600/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 763, \"height\": 577, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.600/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 951, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.600/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 776, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.600/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 186, \"label\": \"Table\"}]"
motivation: 概念瓶颈模型的概念库存在冗余或覆盖不足问题。
method: 引入动态智能体调整概念库，提出条件概念瓶颈模型优化评分。
result: 概念库更紧凑且覆盖更全，分类性能与可解释性均提升。
conclusion: 动态概念调整和条件评分能显著增强可解释分类。
---

## Abstract
Concept Bottleneck Models (CBMs) decompose image classification into a process governed by interpretable, human-readable concepts. Recent advances in CBMs have used Large Language Models (LLMs) to generate candidate concepts. However, a critical question remains: What is the optimal number of concepts to use? Current concept banks suffer from redundancy or insufficient coverage. To address this issue, we introduce a dynamic, agent-based approach that adjusts the concept bank in response to environmental feedback, optimizing the number of concepts for sufficiency yet concise coverage. Moreover, we propose Conditional Concept Bottleneck Models (CoCoBMs) to overcome the limitations in traditional CBMs’ concept scoring mechanisms. It enhances the accuracy of assessing each concept’s contribution to classification tasks and feature an editable matrix that allows LLMs to correct concept scores that conflict with their internal knowledge. Our evaluations across 6 datasets show that our method not only improves classification accuracy by 6% but also enhances interpretability assessments by 30%.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：概念瓶颈模型（CBM）通过可解释的人可读概念实现图像分类，但现有概念库存在两个关键问题：概念数量难以确定（过多导致冗余，过少导致覆盖不足）；传统CBM对所有类别共享同一概念评分机制，忽视了同一概念对不同类别的贡献差异。
- **整体含义**：本文旨在动态优化概念库的规模与内容，同时改进概念评分机制，以在保持可解释性的前提下提升分类准确率，并利用LLM的内在事实知识自动纠正错误激活，增强模型的可信度。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：提出**条件概念瓶颈模型（CoCoBMs）**，引入类别特定的评分和权重；设计**LLM智能体（Concept Agent）**，通过环境反馈动态调整概念库，自动确定最优概念数量。
- **关键技术细节**：
  - **CoCoBMs**：  
    - 类别特定评分：对每个类别单独计算概念得分（公式2），替代传统CBM的共享评分（公式1）。  
    - 条件学习：使用可学习提示向量与类别名、概念名拼接（公式3），通过CLIP计算图像与文本的相似度。  
    - 可编辑矩阵E（公式4）：LLM判断概念-类别对的客观事实相关性，若概念与类别事实不符，则将该概念对该类别的得分置零（公式5）。  
    - 训练目标：加权二分类交叉熵损失（公式6）。
  - **Concept Agent**：  
    - 记忆模块：维护生成、删除、事实验证的概念列表及版本历史。  
    - 行动模块：包含概念生成（LLM提示）、概念选择（学习搜索）、事实验证（多选题）、实例选择（K-means聚类）、环境感知（在少量样本上训练CoCoBMs获取反馈）。  
    - 规划模块：分析概念得分激活模式（公式7-9），识别冗余概念（零贡献或模式相同且距离小于阈值）和不足概念（某类别无激活或与其他类别无法区分），驱动下一轮迭代。  
    - 迭代直到所有类别可识别且无冗余。
- **算法流程**：初始化概念库 → 智能体感知环境 → 分析激活模式 → 删除冗余、补充缺失 → 更新概念库 → 重复直至收敛。

## 3. 实验设计
- **数据集**：CUB（鸟类200类）、CIFAR-10、CIFAR-100、Food-101、Flower、Oxford-Pets，共6个不同规模和挑战的数据集。
- **基准方法**：
  - CBM基线：Label-free CBM (LF-CBM)、LaBo（每类1/2/3个概念）、LM4CV（概念数为标签数的0.6/1/2倍）。
  - 随机词概念库（512个随机词）作为非可解释基线。
  - 黑盒模型：图像特征线性探针、CLIP提示学习（8个可学习token）。
- **对比指标**：分类准确率（Acc）+ 可解释性（Inte，由LLM评估的真实性和区分度构成）。
- **公平性**：所有方法使用同一CLIP ViT-B/32骨干；概念数量对比时控制倍数；可解释性评估采用固定多选题集。

## 4. 资源与算力
- **明确说明**：论文未提供具体GPU型号、数量或训练时长细节。
- **已知信息**：使用CLIP ViT-B/32，batch size 2048，Adam优化器，学习率0.01；概念生成与事实验证调用GPT-4o API，可解释性评估调用GPT-4-turbo；训练在少数样本（每类16个）上进行反馈，最终在完整数据集上训练。

## 5. 实验数量与充分性
- **实验数量**：
  - 主实验：6个数据集上对比多种CBM变体和黑盒模型（图3，约30个点）。
  - 消融实验：动态vs静态接地（表1，3个数据集）、可编辑矩阵有无（表2，3个数据集）。
  - 样本量影响（图4，3个规模）。
  - 案例研究（CIFAR-10迭代过程、Oxford-Pets概念排名，图5）。
- **充分性与公平性**：
  - 覆盖了从细粒度到通用分类的多个场景，概念数量范围从几十到上万。
  - 对比了不同规模的概念库（LaBo-n vs LaBo-3n等），确保比较公平。
  - 可解释性评估采用固定多选题集并多次投票，减少随机性。
  - 缺点：未在更大规模数据集（如ImageNet）或更多模态上验证；未与Res-CBM等最新方法对比。

## 6. 主要结论与发现
- **分类性能**：动态Agent确定的概念数量约为标签数，相比同规模方法（LaBo-n, LM4CV-n）准确率平均提升6%；甚至优于使用三倍概念的LaBo-3n（平均提升0.51%），并优于使用更多概念的LF-CBM（提升1.36%）。与黑盒模型差距缩小至2-3%。
- **可解释性**：达到77.46%平均可解释性分数，较LM4CV-2n提升约30%；真实性和区分度均显著提高。
- **动态接地**显著提升可解释性（平均+10.76%），且在小样本下保持稳定。
- **可编辑矩阵**在轻微牺牲准确率（约1-2%）的前提下大幅提升可解释性（+30~40%），表明事实约束对可解释性至关重要。

## 7. 优点
- **方法创新**：首次将LLM智能体引入概念库动态构建，解决了概念数量最优化的难题；条件概念瓶颈模型针对性地改进了传统CBM的评分缺陷。
- **可解释性评估**：设计基于LLM的定量评估（真实性与区分度），更具实用性和可重复性。
- **实验全面**：6个数据集、多种基线、消融和案例研究，结果有说服力。
- **实用性强**：概念库简洁（约等于标签数），且智能体可自动发现难以区分的类别对，辅助人类分析。

## 8. 不足与局限
- **计算开销**：事实验证阶段需枚举所有概念-类别对（共M×N次LLM调用），扩展性受限于概念数；论文尝试过滤策略但增加了迭代次数。
- **LLM不稳定性**：概念生成和事实验证依赖LLM内部知识，存在随机性和偏差风险，可能导致结果波动。
- **实验局限**：未在更大规模数据集（如ImageNet）或更复杂任务（多标签、分割）上验证；未与如Res-CBM、Post-hoc CBM等更近的工作比较。
- **资源细节缺失**：未报告训练所需GPU型号、数量及时间，不利于复现和成本估算。
- **应用限制**：依赖于CLIP等预训练视觉-语言模型，对于CLIP未见过的领域或高度专业化的图像，概念对齐可能失效。

（完）
