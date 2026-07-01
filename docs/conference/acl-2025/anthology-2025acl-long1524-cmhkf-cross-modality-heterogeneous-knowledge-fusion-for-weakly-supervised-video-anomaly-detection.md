---
title: "CMHKF: Cross-Modality Heterogeneous Knowledge Fusion for Weakly Supervised Video Anomaly Detection"
title_zh: CMHKF：面向弱监督视频异常检测的跨模态异构知识融合
authors: "Guohua Wang, Shengping Song, Wuchun He, Yongsen Zheng"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1524.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 弱监督视频异常检测但未涉及可解释性
tldr: 该论文针对弱监督视频异常检测任务，指出现有方法仅利用视觉模态的局限性，提出CMHKF框架，融合视频、音频和文本的跨模态异构知识。通过视频-文本知识对齐和音频特征自适应提取，在多个基准上提升了异常检测和定位精度。但由于缺乏对决策过程的解释，该工作与可解释异常检测需求有距离，但提供了可借鉴的多模态融合思路。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1524/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1643, \"height\": 838, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1524/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1524/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 693, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1524/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1663, \"height\": 666, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1524/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1593, \"height\": 884, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 741, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 170, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 137, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 798, \"height\": 168, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 113, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 796, \"height\": 687, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 795, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 798, \"height\": 198, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1524/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 796, \"height\": 227, \"label\": \"Table\"}]"
motivation: 现有弱监督视频异常检测方法仅利用视觉模态，忽略了音频和文本等丰富跨模态信息。
method: 提出CMHKF框架，通过视频-文本知识对齐与音频特征自适应提取，实现跨模态异构知识融合。
result: 在基准数据集上，该方法在异常检测和定位性能上超越了现有单模态方法。
conclusion: 该工作验证了跨模态信息对异常检测的有效性，但未来需增加可解释性分析以满足实际应用需求。
---

## Abstract
Weakly supervised video anomaly detection (WSVAD) presents a challenging task focused on detecting frame-level anomalies using only video-level labels. However, existing methods focus mainly on visual modalities, neglecting rich multi-modality information. This paper proposes a novel framework, Cross-Modality Heterogeneous Knowledge Fusion (CMHKF), that integrates cross-modality knowledge from video, audio, and text to improve anomaly detection and localization. To achieve adaptive cross-modality heterogeneous knowledge learning, we designed two components: Cross-Modality Video-Text Knowledge Alignment (CVKA) and Audio Modality Feature Adaptive Extraction (AFAE). They extract and aggregate features by exploring inter-modality correlations. By leveraging abundant cross-modality knowledge, our approach improves the discrimination between normal and anomalous segments. Extensive experiments on XD-Violence show our method significantly enhances accuracy and robustness in both coarse-grained and fine-grained anomaly detection.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **任务**：弱监督视频异常检测（WSVAD），仅用视频级标签定位帧级异常。
- **现有问题**：主流方法只利用视觉模态，在视觉模糊场景（如灰尘中区分爆炸 vs 大风）中区分能力不足；部分多模态工作仅做简单拼接融合，忽略了模态间潜在的关联和自适应调整。
- **核心动机**：融合视频、音频、文本三种异构知识，通过自适应跨模态知识学习提升异常检测与定位的精度和鲁棒性。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **整体框架 CMHKF**：
  - 输入：视频帧、音频片段、可学习的类别文本（如正常、暴力类）。
  - 特征提取：视频用 CLIP（ViT-B/16）图像编码器 + Local TE + Global GCN；文本用 CLIP 文本编码器；音频用 VGGish 网络。
  - 三个关键模块：
    1. **CVKA（跨模态视频-文本知识对齐）**：
       - 计算每一帧与每一类文本的余弦相似度，得到视觉-语义相似度矩阵。
       - 沿时间维度聚合得到视频级相似度向量，用 Top‑k 选出与视频语义最相关的 k 个类别文本。
       - 根据 Top‑k 相似度分数自适应聚合这些文本特征，得到与视频对齐的文本特征。
    2. **AFAE（音频模态特征自适应提取）**：
       - 将 CVKA 获得的 Top‑k 视觉-语义相似度投影到音频帧上，得到音频帧的时序显著性。
       - 引入 **Top‑k 窗口机制**：选取音频中显著帧，以帧为中心取宽度 2w+1 的局部窗口，将中心帧的显著性扩展到窗口内所有帧，缓解音视频细粒度不对齐问题。
       - 利用扩展后的显著性权重聚合音频特征，得到增强的音频特征。
    3. **MKAF（多模态知识自适应融合）**：
       - 使用扩展的 **Joint Cross-Attention**：对视频、文本、音频各特征与联合表示 J 做交叉注意力。
       - 将交互后的三个特征拼接并与 J 相加，经过线性投影得到融合特征 F<sub>fused</sub>。
- **目标函数**：
  - 粗粒度二分类：Binary Cross Entropy（L<sub>BCE</sub>）。
  - 细粒度多分类：MIL-Align 机制，并加入对比损失 L<sub>NA</sub>（拉大正常与异常文本）和 L<sub>AA</sub>（拉大不同异常类文本）。

### 3. 实验设计

- **主要数据集**：
  - **XD-Violence**：唯一同时包含视频和音频的大规模暴力检测数据集，含 4,757 个非修剪视频（217 小时），6 种暴力类别。
  - 评估指标：粗粒度用帧级 **AP**（Average Precision）；细粒度用 **mAP@IoU**（0.1 ~ 0.5 阈值下的平均 mAP）。
- **基准对比**：
  - 粗粒度：对比了 SVM baseline、Hasan et al.、GODS、CLAP（无监督）；Sultani et al.、HL-Net、RTFM、TEVAD、VadCLIP 等弱监督方法；并报告了不同输入模态（Video、Video+Audio、Video+Text、Video+Audio+Text）的结果。
  - 细粒度：对比了 Sultani et al.、3C-Net、W-TALC、Wu et al.、VadCLIP 等。
- **额外实验**：
  - 在 **UCF-Crime** 数据集（仅有视频）上做了补充实验（无音频），对比了更多方法，包括 STPrompt、UR-DMU 等。

### 4. 资源与算力

- 文中明确说明：
  - 使用 **PyTorch** 实现，**单张 NVIDIA RTX 3090 GPU**。
  - XD-Violence 主实验：**10 epochs**，学习率 1×10⁻⁵，优化器 AdamW。
  - UCF-Crime 补充实验：**20 epochs**，batch size 32，学习率 2×10⁻⁵。
- 未说明使用的 GPU 数量（推测为单卡）、显存大小或训练总时长。

### 5. 实验数量与充分性

- **实验组数**：
  - **粗粒度**与 **细粒度**主对比实验共 2 组（Table 1 & 2）。
  - **消融实验**丰富：CVKA（不同 k 值）、AFAE（有无 Top‑k 窗口、窗口大小 W）、多模态组合（Video/Video+Audio/Video+Text/Video+Audio+Text）、损失函数（L<sub>NA</sub>、L<sub>AA</sub>）、融合方法对比（Bilinear & Concat、Bilinear & Additive、Concat、MKAF）。
  - 额外在 **UCF-Crime** 上作了粗粒度与细粒度对比（Table 8 & 9）以及异常视频仅评估（Table 7）。
  - 定性分析：t-SNE 特征可视化、异常分数曲线可视化（Fig. 4 & 5）。
- **充分性与公平性**：
  - 对照方法涵盖近年 SOTA，并且对部分方法做了多模态重实现（标注*），保证了公平。
  - 全部实验均在同一框架下进行，消融实验设计合理、链式验证充分。
  - 唯一不足是 **XD-Violence 是唯一的音视频数据集**，泛化性验证仅靠 UCF-Crime（无音频），因此跨数据集、跨场景的结论可能有限。

### 6. 论文的主要结论与发现

- 提出的 **CMHKF** 在 XD-Violence 上粗粒度 AP 达到 **86.57%**，细粒度 AVG mAP 达到 **26.70%**，均大幅优于所有之前方法（包括单模态和双模态）。
- **CVKA** 通过 Top‑k 自适应选择语义相关文本显著提升了性能，k=2 最佳；**AFAE** 的窗口机制有效克服音视频时间不对齐，AP 提升 1.51%。
- **多模态融合**（Video+Audio+Text）比最佳双模态（Video+Text）分别提升 1.76% AP 和 2.38% 平均 mAP。
- 在 UCF-Crime 上也取得 SOTA（Video+Text 模态 AUC 88.24%，细粒度平均 mAP 9.54%），验证了框架的可迁移性。

### 7. 优点

- **创新性**：率先在 WSVAD 中实现视频、音频、文本三模态的自适应融合，而非简单拼接。
- **技术细节**：
  - CVKA 利用 CLIP 语义对齐动态筛选文本，减少无关噪声。
  - AFAE 中提出的 Top‑k 窗口机制有效解决多模态帧级不对齐问题。
  - MKAF 基于交叉注意力同时捕捉模态内和模态间关联，降低异构性。
- **实验严谨**：
  - 全面消融每个模块和超参数。
  - 在 UCF-Crime 上做补充验证，说明架构对缺少音频的场景仍有竞争力。
  - 分析了仅在异常视频上的性能，揭示了跨模态一致性的影响。

### 8. 不足与局限

- **数据集限制**：唯一同时包含音视频的 XD-Violence 数据集规模有限（217 小时），且类别集中于暴力事件；缺少更多样的多模态异常数据集进行泛化验证。
- **文本模态依赖**：目前使用固定可学习类标签，未能利用大语言模型生成丰富描述，可能限制细粒度语义表达能力。
- **弱监督固有缺陷**：伪标签精度不可靠对细粒度定位仍有影响（类似二阶段方法）。
- **可解释性不足**：文中未分析模型决策过程（如注意力权重可视化、异常原因推理），缺乏对“为何认为是异常”的解释。
- **资源细节缺失**：未报告完整训练时间、显存占用，难以复现或比较资源效率。

（完）
