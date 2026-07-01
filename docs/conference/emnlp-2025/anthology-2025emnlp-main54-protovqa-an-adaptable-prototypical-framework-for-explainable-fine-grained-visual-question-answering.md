---
title: "ProtoVQA: An Adaptable Prototypical Framework for Explainable Fine-Grained Visual Question Answering"
title_zh: ProtoVQA：面向可解释细粒度视觉问答的自适应原型框架
authors: "Xingjian Diao, Weiyi Wu, Keyi Kong, Peijun Qing, Xinwen Xu, Ming Cheng, Soroush Vosoughi, Jiang Gui"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.54.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 基于原型的可解释VQA框架
tldr: 现有VQA模型缺乏可解释性。ProtoVQA提出统一的原型框架，学习问题感知的原型作为推理锚点，将答案连接到可判别的图像区域，并通过空间约束增强可解释性，同时保持高准确率。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1649, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 402, \"height\": 303, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 400, \"height\": 302, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 1646, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1489, \"height\": 2231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1654, \"height\": 1245, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1489, \"height\": 1984, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1652, \"height\": 1106, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1653, \"height\": 1114, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1328, \"height\": 1993, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1653, \"height\": 1242, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1653, \"height\": 1112, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.54/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1653, \"height\": 1243, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.54/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1556, \"height\": 569, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.54/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 634, \"height\": 219, \"label\": \"Table\"}]"
motivation: VQA在安全关键领域需要可解释性，但现有方法缺乏。
method: 学习问题感知的原型作为推理锚点，连接答案与判别性图像区域，并应用空间约束。
result: 在VQA任务上实现高准确率且提供可解释性。
conclusion: 原型基方法能有效提升VQA的可解释性。
---

## Abstract
Visual Question Answering (VQA) is increasingly used in diverse applications ranging from general visual reasoning to safety-critical domains such as medical imaging and autonomous systems, where models must provide not only accurate answers but also explanations that humans can easily understand and verify. Prototype-based modeling has shown promise for interpretability by grounding predictions in semantically meaningful regions for purely visual reasoning tasks, yet remains underexplored in the context of VQA. We present ProtoVQA, a unified prototypical framework that (i) learns question-aware prototypes that serve as reasoning anchors, connecting answers to discriminative image regions, (ii) applies spatially constrained matching to ensure that the selected evidence is coherent and semantically relevant, and (iii) supports both answering and grounding tasks through a shared prototype backbone. To assess explanation quality, we propose the Visual–Linguistic Alignment Score (VLAS), which measures how well the model’s attended regions align with ground-truth evidence. Experiments on Visual7W show that ProtoVQA yields faithful, fine-grained explanations while maintaining competitive accuracy, advancing the development of transparent and trustworthy VQA systems.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：视觉问答（VQA）在安全关键领域（如医疗影像、自动驾驶、刑事司法）对模型透明度要求极高，但当前最先进的VQA模型多为黑盒，难以解释其推理过程或验证其可靠性。
- **现有方法不足**：传统VQA可解释性方法主要依赖注意力可视化或事后解释，往往不能忠实反映模型内部决策过程。原型学习在纯视觉任务中已展现可解释性优势，但在多模态VQA中尚未得到充分探索。
- **本文目标**：提出一个统一的无原型框架ProtoVQA，通过**问题感知的原型**和**空间约束的贪婪匹配**，为VQA提供忠实、细粒度的可解释性，同时保持有竞争力的准确性。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：
  - 学习**问题感知的原型**作为推理锚点，将图像中判别性区域与答案链接起来。
  - 使用**空间约束的贪婪匹配**确保所选视觉证据在空间上连续且语义相关。
  - 通过共享原型骨干支持**答案预测**和**视觉定位**两种下游任务。

- **关键技术细节**：
  1. **特征提取**：
     - 视觉：预训练 DeiT 作为骨干，提取补丁特征 \(F = [f_{CLS}, f_1, \dots, f_N]\)，并中心化得到 \(F_{visual} = [f_1 - f_{CLS}, \dots, f_N - f_{CLS}]\)。
     - 文本：预训练 DeBERTa 编码问题，经可学习特征投影器映射到共享视觉-语言空间。
     - 答案处理：对多选题（Type 2）使用与问题分支共享权重的冻结投影器；对坐标型答案（Type 1）使用专用投影器。
  2. **可解释原型部分选择模块**：
     - 将前 \(m \times k\) 个问题token重塑为 3D 张量 \(P \in \mathbb{R}^{m \times k \times D}\)，形成 \(m\) 个原型，每个原型含 \(k\) 个子补丁。
     - **贪婪匹配**：对每个原型 \(P_i\)，迭代 \(k\) 次选择最优补丁-子补丁对：
       - 计算相似度矩阵 \(S^n_{n,j}\)。
       - 引入可用性掩码 \(M^t\) 和邻接掩码 \(A^t\)（空间约束半径 \(r\)），选出最优对 \((n^*, j^*)\)。
       - 更新掩码，防止重复选择并保证空间连续性。
       - 最终匹配得分：\(score(P_i) = \sum_{t=1}^k w_t \cdot S^{n^*_t, j^*_t}_t\)，其中 \(w_t\) 可学习。
  3. **答案预测**：将匹配的补丁特征与处理后的答案特征拼接，通过分类层输出。
  4. **解释对齐评估**：提出**Visual-Linguistic Alignment Score (VLAS)**，计算模型关注区域与真实标注框的IoU阈值（\(\theta=0.5\)）之上的问答对比例。

## 3. 实验设计

- **数据集**：Visual7W（Zhu et al., 2016）——包含327,939个QA对，覆盖47,300张COCO图像，每个问题有4个候选项，共561,459个对象级定位标注。用于评估答案预测和视觉定位。
- **基准方法**：对比了8种代表性方法：SUPER、QOI_Attention、SDF of VLT、STL、CFR、BriVL、CTI、Bi-CMA。这些方法涵盖CNN-RNN和Transformer架构。
- **评估指标**：
  - 准确率（Accuracy）——答案预测性能。
  - VLAS@1和VLAS@3——解释对齐质量。
- **实验场景**：多选视觉问答（Type 2）和视觉定位（Type 1）。

## 4. 资源与算力

- **硬件**：单张NVIDIA A800 GPU（80GB显存）。
- **训练轮次**：200个epoch。
- **优化器**：Adam，学习率 \(1 \times 10^{-4}\)，批次大小64。
- **图像尺寸**：224×224，补丁大小16×16。
- **原型配置**：每类 \(m=10\) 个原型，每个原型 \(k=3\) 个子补丁；空间约束半径 \(r=3\)。
- **其他**：未提及总训练时长或是否多卡并行。

## 5. 实验数量与充分性

- **实验覆盖**：
  - 主试验：表1（准确率对比）和表2（VLAS对比）。
  - 定性可视化：图2展示了4个样例，附录D额外提供10个样例（共14个），涵盖人/动物解剖、物体识别、交互关系、空间关系等。
- **充分性**：
  - 对比基线较全面（8种），包括传统方法和Transformer基准。
  - 提供了准确率和解释对齐的两方面评估，但缺少消融实验（例如：不同原型数量 \(m\)、子补丁数量 \(k\)、空间约束半径 \(r\) 的影响；未与不适用原型或不同匹配策略的变体对比）。
  - 未与同类型可解释VQA方法（如其他原型或注意力基方法）直接比较VLAS。
- **公平性**：使用标准Visual7W测试集，对比方法均来自已发表文献，结果报告明确。但作者指出Bi-CMA微调后准确率更高，ProtoVQA以牺牲少量准确率换取解释性。

## 6. 主要结论与发现

- ProtoVQA在Visual7W测试集上达到70.23%准确率，与使用ViT骨干的Bi-CMA（70.53%无微调）持平，略低于微调后的Bi-CMA（73.07%），但**显著优于其他Transformer基线**。
- 在解释对齐方面：ProtoVQA的VLAS@1=0.4103，VLAS@3=0.2466，分别比Bi-CMA提升66.4%和119.6%，证明其关注区域与真实证据高度一致。
- 定性可视化显示：模型能准确定位细粒度部位（如耳朵、手臂）、物体、交互关系及空间关系，提供人类可验证的解释。

## 7. 优点

- **统一框架**：通过共享原型骨干同时支持答案预测和视觉定位，任务适配灵活。
- **问题感知原型**：原型直接从问题token生成，动态捕捉视觉与语义关联，克服单模态原型局限性。
- **空间约束贪婪匹配**：保证所选补丁空间连续，增强解释的语义连贯性，计算简单（作者自述低复杂度、可扩展）。
- **新评估指标VLAS**：克服传统IoU对解释质量评估的不足（如惩罚部分有效重叠、对标注尺度敏感），以二值阈值衡量解释是否可接受，更符合人类判断。
- **可视化充分**：提供多个样例，覆盖不同问题类型，直观展示细粒度解释能力。

## 8. 不足与局限（作者自述 + 本文分析）

1. **解释忠实性与性能的平衡**：作者指出在保持准确率的同时提升原型解释的忠实性仍有改进空间，未来可探索联合优化、自适应原型初始化等。
2. **领域泛化有限**：仅在通用VQA基准上评估，未在医疗、自动驾驶等安全关键领域验证，需要领域特定原型词汇和微调。
3. **不支持自由生成式VQA**：当前架构限于多项选择和定位任务，未扩展至大语言模型指导的开放生成式VQA。
4. **缺少消融实验**：论文未系统分析原型数量、子补丁数量、空间约束半径等超参数的影响，也未对比变体（如无空间约束、不同匹配策略）。
5. **VLAS阈值单一**：仅使用IoU>0.5，未探讨不同阈值下的鲁棒性；且该指标可能对边界框标注质量敏感。
6. **对比基线解释性**：未与专门的可解释VQA方法（如注意力掩码、概念瓶颈模型）直接比较解释质量，仅与无解释能力的黑盒模型对比。
7. **计算资源细节省略**：未报告每轮训练耗时、推理速度，难以评估实际部署成本。
8. **潜在偏差**：Visual7W数据集基于COCO，可能包含常见物体的偏斜分布，模型解释质量可能受数据集偏差影响。

（完）
