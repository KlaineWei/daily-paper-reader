---
title: Data Descriptions from Large Language Models with Influence Estimation
title_zh: 基于影响估计的LLM数据描述生成
authors: "Chaeri Kim, Jaeyeon Bae, Taehwan Kim"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1717.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 利用影响估计的XAI方法识别有益数据描述
tldr: 深度学习模型行为理解是挑战，现有可解释AI多关注预测解释。本文提出一种新方法，利用大语言模型生成文本描述，并通过影响估计和CLIP评分识别对训练最有帮助的描述。该方法可提供模型如何优先利用信息的洞察，具有通用性，可迁移至目标检测等任务的可解释性分析。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1575, \"height\": 497, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1615, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1472, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 751, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 260, \"height\": 208, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 811, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1621, \"height\": 280, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 285, \"height\": 209, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 287, \"height\": 215, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1519, \"height\": 948, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1528, \"height\": 947, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1527, \"height\": 956, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1521, \"height\": 949, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1519, \"height\": 941, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 330, \"height\": 253, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1717/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 302, \"height\": 297, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1487, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1329, \"height\": 502, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 813, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 734, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 809, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 739, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1503, \"height\": 458, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1717/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 792, \"height\": 367, \"label\": \"Table\"}]"
motivation: 现有可解释AI多解释预测，缺乏识别对训练有益的数据描述的方法。
method: 提出流水线：使用LLM生成描述，结合外部知识库，通过影响估计和CLIP分数优化。
result: 该方法能有效识别对模型训练贡献最大的描述，提供模型决策偏好洞察。
conclusion: 为模型训练数据选择提供可解释性视角，具有广泛应用潜力。
---

## Abstract
Deep learning models have been successful in many areas, but understanding their behavior remains a challenge. Most prior explainable AI (XAI) approaches have focused on interpreting how models make predictions. In contrast, we introduce a novel approach that identifies textual descriptions most beneficial for model training. By analyzing which descriptions contribute most effectively to the model training, our method has the potential to provide insights into how the model prioritizes and utilizes information for decision-making. To achieve this, we propose a pipeline that generates textual descriptions using large language models, incorporates external knowledge bases, and refines them through influence estimation and CLIP score. Furthermore, leveraging the phenomenon of cross-modal transferability, we propose a novel benchmark task named cross-modal transfer classification to examine the effectiveness of our textual descriptions. In zero-shot experiments, we demonstrate that our textual descriptions improve classification accuracy compared to baselines, leading to consistent performance gains across nine image classification datasets. Additionally, understanding which descriptions contribute most to model performance can shed light on how the model utilizes textual information in its decision-making.

---

## 论文详细总结（自动生成）

# 论文总结：基于影响估计的LLM数据描述生成

## 1. 核心问题与研究动机

- **问题背景**：深度学习模型在许多领域取得了成功，但其行为理解仍然是“黑箱”。现有的可解释AI（XAI）研究大多聚焦于如何解释模型的预测结果，很少关注如何从数据层面进行解释。
- **核心目标**：提出一种新方法，利用大语言模型生成能够解释图像类别的文本描述，并通过影响估计和CLIP评分识别对训练最有帮助的描述，从而提升模型的可解释性和性能。
- **核心假设**：通过识别哪些文本描述对模型训练贡献最大，可以提供模型如何优先利用信息的洞察，揭示黑箱模型的决策机制。

## 2. 方法论：核心思想与技术细节

### 2.1 整体框架（三阶段流程）

1. **生成文本描述**：利用GPT-3.5和Wikipedia外部知识库，通过两阶段提示生成每个图像类别的详细文本描述。
2. **选择最有帮助的描述（Proponent Texts）**：通过提出的**IFT（Influence scores For Texts）** 指标，筛选出对模型训练最有益的文本描述。
3. **交叉模态迁移分类**：利用CLIP模型对齐图像和文本嵌入，先训练图像模型，再用筛选出的文本描述进行微调训练。

### 2.2 关键技术创新

- **两阶段提示策略**：
  - 第一阶段：从类别名称中提取外观相关组件（如身体结构、毛色、眼睛等）。
  - 第二阶段：结合Wikipedia URL，生成每个组件的详细信息，以弥补LLM知识不足并减少幻觉。
- **IFT（影响分数For Texts）**：综合了**影响分数**（来自TracIn方法，衡量训练图像对验证样本的影响）和**CLIP分数**（图像-文本相似度），用于评估文本描述的重要性。
- **交叉模态迁移分类**：利用CLIP的对齐能力，先用图像训练线性分类器，再使用经过IFT加权的文本描述进行二次训练，提升分类性能。

### 2.3 核心公式（文字描述）

- **影响分数**：通过TracIn方法，使用多个检查点计算训练图像对验证样本损失的影响，即损失减小的总幅度。
- **IFT**：对所有训练图像和验证图像组合，计算每个文本描述的影响分数与CLIP分数之和的平均值。
- **加权训练**：在交叉模态迁移训练中，每个文本描述的损失贡献按其IFT分数（归一化后）进行加权。

## 3. 实验设计与对比

### 3.1 使用的数据集（9个）

| 数据集 | 类别数 | 特点 |
|--------|--------|------|
| CUB 200 2011 | 200 | 细粒度鸟类识别 |
| Miniimagenet | 100 | 小样本学习基准 |
| CIFAR-10 | 10 | 通用图像分类 |
| CIFAR-100 | 100 | 通用图像分类（更多类别） |
| OxfordPets | 37 | 猫狗品种分类 |
| EuroSAT | 10 | 卫星图像土地分类 |
| Food101 | 101 | 食物图像分类 |
| 102flowers | 102 | 花卉分类 |
| DTD | 47 | 纹理图案分类 |

### 3.2 对比方法（基线）

- **CLIP Zero-shot**：直接使用CLIP进行零样本分类
- **Menon**（2023）：通过描述进行分类
- **LaBo**（Yang et al., 2023）：语言引导瓶颈模型
- **CuPL**（Pratt et al., 2023）：定制化提示生成
- **VDT-Adapter**（Maniparambil et al., 2023）：视觉描述提示
- **Only Images**：仅使用图像训练

### 3.3 实验场景

1. **零样本分类**：测试文本描述本身作为分类依据的效果
2. **交叉模态迁移分类**：测试文本描述对图像模型的提升效果
3. **消融实验**：评估IFT各成分（单独使用影响分数、CLIP分数）的效果
4. **Wiki URL消融**：评估是否使用Wikipedia外部知识的差异
5. **GPT-4o评估**：第三方评估文本描述的质量（Helpful、Informative、Relevant）
6. **新VLM验证**：使用更新的CLIP模型验证鲁棒性

## 4. 资源与算力

- **硬件**：使用NVIDIA 3090 GPU
- **训练时间**：
  - 仅图像训练：约2小时（对全部9个数据集）
  - 交叉模态迁移训练（使用文本描述）：少于30分钟
- **影响分数计算**：使用预训练ResNet34，在200个epoch中每10个epoch保存检查点
- **注意**：论文未明确说明使用的LLM（GPT-3.5/4）推理成本，也未提供详细的超参数优化计算量

## 5. 实验数量与充分性

### 实验数量
- **主要实验结果**（表1、表2）：9个数据集 × 6种方法，共54组主要对比
- **消融实验**（表3、表4）：9个数据集 × 4种配置
- **零样本+新模型实验**（表7）：8个数据集 × 6种方法
- **GPT-4o评估**（表5、表6）：100个随机类别 × 3个实例，共300个评估案例
- **可视化分析**（图3-7）：多种定性对比和t-SNE可视化

### 充分性评估
- **高度充分**：实验覆盖了多个维度——不同数据集类型（细粒度、通用、纹理、卫星等）、不同任务设置（零样本、迁移学习）、不同消融（IFT成分、外部知识）、不同模型（CLIP版本）
- **公平性**：对基线方法，使用了其原始代码生成描述，并统一使用GPT-3.5以保证对比公平
- **客观性**：GPT-4o评估使用盲评（描述随机排序），减少主观偏差

## 6. 主要结论与发现

1. **IFT有效筛选有益文本**：综合影响分数和CLIP分数，能够有效识别对模型训练最有帮助的文本描述，去除不相关或误导性信息。
2. **文本描述提升图像分类**：在零样本和交叉模态迁移场景下，本方法的文本描述优于所有基线，在9个数据集上均实现性能提升。
3. **外部知识关键作用**：使用Wikipedia URL的两阶段提示，能生成更具体、更准确、更少幻觉的描述。
4. **交叉模态迁移分类可行有效**：利用CLIP的对齐能力，使用文本描述训练分类器能提升模型性能，揭示了模型对文本信息的利用机制。
5. **可解释性增强**：通过筛选出的Proponent Texts，可以了解模型关注哪些特征，提供黑箱模型的固有可解释性。

## 7. 方法设计的优点

### 方法创新点
1. **数据层面的可解释性**：区别于传统XAI（解释预测结果），本文从数据出发，解释哪些数据对训练最有帮助。
2. **IFT指标的新颖性**：首次将影响估计（原本用于图像）扩展到文本领域，结合CLIP分数衡量文本的有用性。
3. **两阶段提示**：结合外部知识库，弥补LLM知识不足，减少幻觉。
4. **交叉模态迁移分类基准**：提出新的评估标准，验证文本描述对视觉模型的帮助。

### 实验设计的优点
- **跨数据集验证**：覆盖9个不同类型数据集，确保方法通用性
- **多种评估维度**：定量（准确率）、定性（图例）、GPT-4o第三方评估
- **消融全面**：验证每个组件（影响分数、CLIP分数、外部知识）的必要性
- **跨模型验证**：使用不同CLIP版本验证鲁棒性
- **成本低廉**：仅需微调线性层，计算效率高

## 8. 不足与局限

### 实验设计局限
1. **LLM依赖性**：生成的描述质量高度依赖预定义提示和LLM本身（GPT-3.5/4），可能导致性能波动。
2. **计算成本随规模增长**：影响分数计算需要多个检查点和大量图像-图像对，当数据集规模很大时，计算负担显著增加。
3. **模型局限**：仅使用CLIP对齐图像和文本，未探索其他多模态模型。

### 方法局限性
1. **文本描述差异**：不同LLM或提示设置下，生成的描述质量不一致，影响性能。
2. **继承LLM偏见**：方法依赖GPT系列，可能继承其训练数据中的偏见。
3. **仅限分类任务**：方法暂未扩展到目标检测、分割等其他任务。

### 潜在风险
- **外部知识可靠性**：Wikipedia虽然权威，但某些小众类别可能缺乏足够信息。
- **幻觉残留**：尽管使用Wikipedia，当Wikipedia缺乏相关信息时，LLM仍然可能生成幻觉内容。

### 其他局限
- 未详细说明超参数优化过程
- 未比较其他提示策略（如少样本提示、思维链）
- 未在更大规模数据集（如ImageNet）上验证

（完）
