---
title: "Decompose and Attribute: Boosting Generalizable Open-Set Object Detection via Objectness Score"
title_zh: 分解与归因：通过物体性分数提升可泛化开放集目标检测
authors: "Yuxuan Yuan, Lichen Wei, Luyao Tang, Chaoqi Chen, Zheyuan Cai, Yue Huang, Xinghao Ding"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38220/42182"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 通过分解与归因实现可解释的开放集目标检测
tldr: 针对开放集目标检测中域偏移和未知类别的问题，提出DOAT框架。通过小波分解分离域风格与语义结构，并利用物体性分数归因，提升泛化能力。实验证明在跨域设置下优于现有方法，归因机制增强可解释性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 845, \"height\": 515}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1828, \"height\": 574}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 473}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1732, \"height\": 452}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38220/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 863, \"height\": 297}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1842, \"height\": 1030}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 356}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 391}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 731, \"height\": 241}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38220/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1831, \"height\": 365}]"
motivation: 现有开放集检测方法忽略域偏移，难以泛化。
method: 小波分解分离域风格与语义，结合物体性分数归因。
result: 在多个开放集检测基准上取得最佳泛化性能。
conclusion: 分解与归因有效提升开放集目标检测的泛化和可解释性。
---

## Abstract
Open-set object detection (OSOD) aims to recognize known object categories while localizing previously unseen instances. However, real-world scenarios often involve co-occurring domain shifts and novel object categories. Existing OSOD methods typically overlook domain shifts, relying on source-trained representations that entangle domain-specific style with semantic content, thereby hindering generalization to both unseen domains and novel categories. To address this challenge, we propose a unified framework, termed DecOmpose and ATtribute (DOAT), which disentangles domain-specific style from semantic structure, thereby facilitating generalizable object detection. DOAT employs wavelet-based feature decomposition to separate style information from high-frequency structural details, thus enabling an explicit separation of domain and category shifts. To account for domain shift, the low-frequency components are perturbed within a style subspace to simulate diverse domain appearances. For unknown object discovery, the high-frequency components are utilized to estimate objectness scores via an attribution mechanism that fuses wavelet energy with semantic distance to known-category prototypes. Extensive experiments on standard open-set benchmarks have demonstrated the superior generalization performance of DOAT.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

**研究动机**：开放集目标检测（OSOD）旨在检测已知类别并定位未知实例。真实场景中常同时出现**域偏移**（如光照、天气变化）和**未知对象类别**。现有OSOD方法大多忽略域偏移，依赖源域训练的特征表示，这些表示将域特定风格与语义内容纠缠在一起，导致在未见过的域和未见过的类别上泛化能力差。

**核心问题**：如何在域偏移下有效地发现未知对象？作者认为关键在于**显式解耦域特定变化与语义内容**。

**贡献**：提出统一框架DOAT（DecOmpose and ATtribute），通过小波分解将域敏感的低频风格信息与域不变的高频结构信息分离；同时设计物体性归因机制，利用高频线索和语义偏差估计类别无关的物体性分数，从而在域偏移下鲁棒检测未知对象。

## 2. 方法论

### 2.1 核心思想
- **频率分解**：利用离散小波变换（DWT）将特征图分解为低频分量（含域风格）和高频分量（含对象边界/结构）。低频分量在风格子空间内扰动以模拟域变化；高频分量用于估计物体性分数。
- **物体性归因**：由两部分组成：
  - **能量引导归因（EGA）**：计算高频小波能量作为结构丰富度度量；
  - **语义引导归因（SGA）**：测量查询与已知类别原型在语义空间中的距离。
  两者融合得到软物体性分数，监督物体性头的训练。

### 2.2 关键技术细节
- **小波分解**：使用Haar小波四个核（LL, LH, HL, HH），分别提取低频和高频特征。公式(2)(3)。
- **低频风格多样化（LFSD）**：
  - 对低频特征进行AdaIN风格重归一化（公式(4)）；
  - 通过最远点采样（FPS）从源域风格池中选择K个风格基，用Dirichlet分布采样插值权重生成新风格（公式(5)）。
- **物体性归因**：
  - EGA：对每个查询的预测框在各尺度上提取高频子带能量（公式(6)），拼接后输入物体性头。
  - SGA：维护已知对象嵌入的指数移动平均原型（公式(7)），计算查询与原型余弦距离（公式(8)），与归一化能量乘积得到软分数（公式(9)）。
  - 损失函数：二分类交叉熵（公式(10)）。

### 2.3 算法流程
1. 输入图像经过backbone提取多尺度特征。
2. 对各层特征应用小波分解，分离低频(LL)和高频(LH,HL,HH)。
3. 低频特征通过LFSD模块进行风格扰动，增强域泛化能力。
4. 解码器查询结合高频能量引导和语义引导的物体性分数，联合优化物体性头和分类头。
5. 最终分类概率 = 物体性概率 × 条件类别概率（公式(1)）。

## 3. 实验设计

### 3.1 数据集与场景
| 源域 → 目标域 | 设置 |
|--------------|------|
| Cityscapes → Foggy Cityscapes | 12种设置（4种语义/频率子任务×3种未知类别数） |
| Cityscapes → BDD100K | het-sem设置（3种未知类别数） |
| Pascal VOC → Clipart1K | 3种未知类别数（6,8,10） |

### 3.2 Benchmark及评价指标
- **已知类性能**：mAP_k（基类平均精度）
- **未知类性能**：AR_u（未知类平均召回率）、WI（荒野影响）、AOSE（绝对开放集误差）

### 3.3 对比方法
D-DETR（基线）、OpenDet、OW-DETR、PROB、CAT、SOMA、SS-OWFormer。所有方法在统一设置下复现评估。

## 4. 资源与算力
文中明确说明：**单卡NVIDIA A40 GPU**，训练80个epoch，批次大小4，初始学习率2×10⁻⁴，优化器AdamW。未提及使用多卡或训练总时长。仅提到采用ResNet-50 backbone（DINO预训练），未探索更大backbone。

## 5. 实验数量与充分性

### 5.1 主要实验结果
- **表1**：Cityscapes→Foggy Cityscapes：12组设置，DOAT在几乎所有设置中AR_u最高，mAP_k与SOTA相当或更好，WI/AOSE通常最低。
- **表2**：Pascal VOC→Clipart：3组设置，DOAT全面领先，AR_u提升显著（如6未知类时34.92 vs SOMA的26.64）。
- **表3**：Cityscapes→BDD100K（het-sem）：3组设置，DOAT在AR_u和AOSE上最优，但提升幅度较小（由于低光照、运动模糊等挑战）。

### 5.2 消融实验（表4、表5、图5）
- **表4**：逐步去除分解/归因模块，证实每个模块均对AR_u有显著贡献；去掉SGA后性能下降。
- **表5**：比较不同风格扰动策略（随机插值、随机扰动、FPS低频、FPS全特征），FPS低频最佳，验证扰动低频的有效性。
- **图5**：物体性分数分布呈可区分的高斯状；损失权重在0.5~2.0之间性能稳定，说明鲁棒性。

### 5.3 客观性与公平性
- 对比方法均为近期代表性工作，且在同一基础检测器（D-DETR）上复现。
- 覆盖多种域偏移（天气、风格、域迁移）和类别偏移（异构/同构语义、频率变化）。
- 消融实验充分验证各组件必要性，超参数分析表明模型不敏感。

## 6. 主要结论与发现
- DOAT在跨域开放集检测中显著优于现有方法，尤其在未知类召回率上提升明显。
- 小波分解能有效分离域风格与语义结构，低频扰动增强域泛化，高频线索辅助未知发现。
- 物体性归因机制无需显式建模未知类，通过融合结构能量和语义偏差实现类别无关的物体性估计。
- 风格多样化采用FPS+低频扰动带来最佳增益。

## 7. 优点
- **创新性**：首次将小波变换用于开放集检测中的风格-语义解耦，并集成到端到端检测器中。
- **方法简洁有效**：物体性分数设计无需伪标签或额外未知类合成，训练稳定。
- **实验全面**：覆盖12种域-类别偏移组合，消融实验严谨，超参数鲁棒性分析到位。
- **可解释性**：物体性分数分布可区分，归因机制直观（高频能量对应结构，语义距离对应类别相似性）。

## 8. 不足与局限
- **场景局限性**：仅在自动驾驶（Cityscapes/BDD/Foggy）和剪贴画（Clipart）数据集上验证，缺乏自然图像（如COCO、OpenImages）等更通用场景的评估。
- **BDD100K提升有限**：由于低光照、运动模糊和小目标，高频线索受限，DOAT优势不够突出。说明方法对视觉质量敏感的局限性。
- **对比方法时效性**：对比工作截至2024年，未与2025年更新的开放集检测方法比较（如可能的新工作）。
- **计算开销未量化**：未报告小波分解和归因模块的额外FLOPs或推理速度，实际部署成本未知。
- **假设局限**：假设域偏移主要由低频风格变化主导（雾、亮度等），但某些域偏移（如视角、材质变化）可能同时影响高低频，此时方法效果可能受限。
- **Backbone单一**：仅使用ResNet-50，未探索更强backbone（如Swin Transformer）或更大的输入尺寸对泛化能力的影响。

（完）
