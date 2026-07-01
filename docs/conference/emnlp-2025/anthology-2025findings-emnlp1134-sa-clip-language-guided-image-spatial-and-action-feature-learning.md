---
title: "SA-CLIP: Language Guided Image Spatial and Action Feature Learning"
title_zh: SA-CLIP：语言引导的图像空间与动作特征学习
authors: "Guanlin Li, Wenhao Shao, Praboda Rajapaksha, Noel Crespi"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1134.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 使用CLIP进行交通异常检测，但未涉及可解释性
tldr: 针对CLIP模型在交通异常检测中难以捕捉空间和动作关系的问题，提出了SA-CLIP模型，通过构建包含1M样本的空间和动作关系标注数据集来训练模型。在VSR和DoTA数据集上的实验表明，该方法有效提升了异常检测性能，但论文未探讨检测结果的可解释性，因此与可解释性异常检测需求仅有间接关联。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 781, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1621, \"height\": 844, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 431, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 816, \"height\": 420, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 813, \"height\": 528, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1134/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 813, \"height\": 393, \"label\": \"Table\"}]"
motivation: 解决CLIP在交通异常检测中无法有效捕捉物体间空间和动作关系的局限性。
method: 构建包含1M样本的空间和动作关系标注数据集，训练SA-CLIP模型以增强语言引导的图像特征。
result: 在VSR和DoTA数据集上取得性能提升，验证了空间和动作特征对异常检测的有效性。
conclusion: SA-CLIP改进了CLIP的异常检测能力，但缺乏可解释性分析。
---

## Abstract
We observed that Contrastive Language-Image Pretraining (CLIP) models struggle with real-world downstream tasks such as road traffic anomaly detection, due to their inability to effectively capture spatial and action relationships between objects within images. To address this, we compile and curate a dataset with 1M samples of images using language supervision provided by the common image caption dataset, in which each image is paired with subject-relationship-object descriptions emphasizing spatial and action interactions, and train a S patial and A ction relationship aware CLIP ( SA-CLIP ) model. We evaluated the proposed model on the Visual Spatial Reasoning (VSR) dataset and further verified its effectiveness on the Detection-of-Traffic-Anomaly (DoTA) dataset. Experiment results show that the proposed SA-CLIP demonstrates strong abilities in understanding spatial relationships while achieving good zero-shot performance on the traffic anomaly detection task.

---

## 论文详细总结（自动生成）

# SA-CLIP: 语言引导的图像空间与动作特征学习 —— 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：标准的 CLIP 模型在真实世界下游任务（如道路交通异常检测）中表现不佳，主要原因是无法有效捕捉图像中物体之间的空间关系（如“在左边”、“在后面”）和动作交互（如“碰撞”、“撞击”）。
- **整体含义**：许多关键任务（如交通事故检测）依赖于对物体相对位置和动作的准确理解。CLIP 的对比学习目标主要对齐整体图像-文本对，缺乏对局部空间关系和动作语义的精细建模，导致其在区分正常/异常场景时能力不足。
- **研究动机**：作者观察到，对于同一场景，CLIP 无法通过文本描述区分异常（如“保险杠抵住保险杠”）和正常（如“保险杠并排”），从而提出改进 CLIP 以提升空间和动作感知能力。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
- 利用语言监督（图像描述）中的主语-关系-宾语（SVO）结构，显式建模物体间的空间（通过介词短语）和动作（通过动词）关系，训练一个空间与动作感知的 CLIP 模型（SA-CLIP）。

### 关键技术细节

#### 2.1 数据集构建
- 从 MSCOCO、SBUCaption、CC3M、CC12M、Visual Genome 等大规模图像-描述数据集中提取约 97 万样本。
- **两步流程**：
  1. **规则解析**：使用依存句法分析器从描述中提取 SVO 三元组（主语、关系、宾语），并扩展包含介词短语（表示空间关系）。
  2. **噪声过滤**：利用 GPT-4o 对种子数据标注三元组的正确性，训练一个轻量级二分类器（基于 bert-base-uncased）来自动过滤低质量三元组。

#### 2.2 模型架构
- 采用双编码器架构（文本编码器 + 视觉编码器），均初始化为 CLIP-ViT-B-32。
- **文本特征**：输入句子和提取的 SVO 三元组。通过索引位置分别获取主语、关系、宾语的表示，经平均池化和线性投影得到聚合的 SVO 表示 \( r_{svo} \)。最终文本表示为句子特征与 SVO 特征的拼接：\( u = \text{Concat}(\text{Pool}(r_{sent}), r_{svo}) \)。
- **视觉特征**：基于 SVO 三元组中的主语和对象，使用现成目标检测器提取感兴趣区域（ROI），将 ROI 特征与位置嵌入相加，得到 ROI 表示 \( r_{roi} \)。最终图像表示为全局图像特征与 ROI 特征的拼接：\( v = \text{Concat}(f_v(\text{image}), r_{roi}) \)。

#### 2.3 训练目标
- **样本间对比学习**（Inter-sample Contrastive Learning）：拉近不同样本中相似 SVO 结构的文本和视觉表示。正样本通过文本 SVO 相似度检索得到，负样本为批内其他样本。
- **样本内对比学习**（Intra-sample Contrastive Learning）：采用三元组损失（Triplet Loss），以图像特征为锚点，对应文本描述为正样本，LLM 生成的反义描述（相同主语和对象但关系相反）为负样本。
- 总损失为样本间对比损失（文本侧和视觉侧）与三元组损失的线性叠加。

## 3. 实验设计

### 数据集与场景

| 数据集 | 用途 | 规模 | 任务 |
|--------|------|------|------|
| CLEVR 生成场景 | 验证空间关系表征能力 | 受控场景（两个物体、八种空间配置：前/后/左/右等） | t-SNE 可视化 |
| VSR (Visual Spatial Reasoning) | 定量评估空间理解 | 6,940 图像，66 种空间关系，零样本测试集 1,222 样本 | 二元分类（描述是否正确描述空间关系） |
| DoTA (Detection-of-Traffic-Anomaly) | 真实世界异常检测 | 测试集中 597 个相关样本，分三类：车辆-车辆(VV)、车辆-人(VP)、车辆-障碍物(VO) | 异常检测（ROC-AUC） |

### Benchmark 与对比方法
- **VSR**：对比完全微调方法（VisualBERT、ViLT、LXMERT）和零样本方法（CLIP-ViT-H-14 带提示）。
- **DoTA**：对比微调方法（AnoPred、FOL-STD、FOL-Ensemble、TTHF）和零样本 CLIP-ViT-B-32。

## 4. 资源与算力

- 文中明确说明：使用 **1 块 NVIDIA A100 GPU（80GB 内存）**，训练 **30,000 步**，批次大小 512（即每步 1,024 个图像-文本对），采用 **AdamW 优化器**，学习率 5e-4，并冻结视觉模型（locked tuning）。
- 未提及训练总耗时（小时数），但给出了计算资源配置。

## 5. 实验数量与充分性

- **实验组数**：主要实验有 3 大块：
  1. CLEVR 可视化定性实验。
  2. VSR 零样本性能（表1）及消融实验（表3）。
  3. DoTA 异常检测（表2）。
- **消融实验**（表3）：在 VSR 上逐一去除 SVO、ROI、三元组损失以及是否在构建的关系数据集上预训练，共 7 种配置。
- **充分性评价**：
  - 定性 + 定量结合，覆盖受控场景和真实场景，设计合理。
  - 对比方法包括经典微调模型和 SOTA，公平性较好（零样本 vs 微调明确区分）。
  - 消融实验完整，验证了每个组件的贡献。
  - 但在 DoTA 上仅 AUC，缺少精确率/召回率等其他指标；且只对比了 CLIP-ViT-B-32 作为零样本基线（未对比更大 CLIP 模型如 ViT-L/14 的零样本），有一定局限性。

## 6. 论文的主要结论与发现

- SA-CLIP 在 CLEVR 可视化中形成了清晰的按空间关系聚类的表征，而 CLIP 无法区分，证明其空间感知能力显著提升。
- 在 VSR 零样本测试中，SA-CLIP（57.8%）优于 CLIP-ViT-H-14（54.5%），且参数量仅为 151M 对比 1B，并接近完全微调的 ViLT（63.0%）。
- 在 DoTA 异常检测中，SA-CLIP 零样本 AUC 全面优于 CLIP（VV: 56.8 vs 49.7, VP: 58.2 vs 49.8, VO: 52.1 vs 50.0），尤其 VP 类表现突出（72.1%，甚至超过部分微调方法）。
- VO（车辆-障碍物）类表现最差，作者分析是因为依赖于目标检测器的质量（障碍物检测难度大）。

## 7. 优点

- **方法创新**：将 SVO 结构引入 CLIP 训练，显式建模空间和动作关系，无需额外人工标注。
- **数据集构建**：利用依存解析+LLM 过滤的思路，从现有大规模数据中自动提取高质量关系数据，实用性强。
- **训练策略**：样本间对比 + 样本内三元组损失的设计，既增强 SVO 表征的判别性，又保持跨模态对齐，且通过 LLM 生成反义描述作为难负例。
- **实验全面**：从可视化到定量基准再到真实任务，验证链条完整。
- **参数效率**：仅 151M 参数即达到甚至超过 1B 参数模型的零样本性能。

## 8. 不足与局限

- **缺乏生成能力**：依赖预定义文本知识，无法自适应生成新描述，灵活性受限（但作者指出推理高效）。
- **对检测器依赖**：性能高度依赖现成目标检测器对主语和对象的定位质量，尤其障碍物（VO）类准确率低，表明检测器是其瓶颈。
- **未见实例泛化**：模型可能只是在学习映射已见过的实例，而非真正理解语义关系，作者计划未来做定性分析。
- **实验覆盖不足**：
  - 未在更多空间关系数据集（如 GQA、NLVR2）上评估。
  - DoTA 实验仅 AUC，缺乏多指标对比（如 F1、PR-AUC）。
  - 零样本基线只用了 CLIP-ViT-B-32，未与更大 CLIP 模型或改进版本（如 CLIP 结合目标检测器）对比。
- **可解释性未分析**：论文未探讨检测结果的可解释性与可解释性异常检测需求仅有间接关联（题目提及但正文未展开）。

（完）
