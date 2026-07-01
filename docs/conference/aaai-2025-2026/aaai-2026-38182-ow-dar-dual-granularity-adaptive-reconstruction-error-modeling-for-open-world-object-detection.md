---
title: "OW-DAR: Dual-Granularity Adaptive Reconstruction-Error Modeling for Open-World Object Detection"
title_zh: OW-DAR：双粒度自适应重构误差建模用于开放世界目标检测
authors: "Linhua Ye, Xing Xi, Ronghua Luo"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38182/42144"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 开放世界目标检测方法，无可解释性
tldr: 该论文针对开放世界目标检测中已知类别先验偏差导致未知物体检测困难的问题，提出OW-DAR方法，通过细粒度和粗粒度协同建模增强前景-背景可分离性。实验表明有效提升未知物体检测性能。方法未涉及可解释性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38182/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 890, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38182/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1830, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38182/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 886, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38182/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1827, \"height\": 681, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38182/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1843, \"height\": 719, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38182/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1844, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38182/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1841, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38182/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38182/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 246, \"label\": \"Table\"}]"
motivation: 现有方法受已知类别先验偏差限制，难以检测未知物体。
method: 通过细粒度掩码重构和粗粒度建模协同，增强前景-背景可分离性。
result: 在开放世界检测基准上提升未知物体检测性能。
conclusion: 双粒度建模减少已知类别偏差，但未提供可解释性。
---

## Abstract
Open-world object detection (OWOD) aims to detect known and unknown objects in dynamic environments. However, only known classes are labeled during training, making it challenging for detectors to recognize unknown objects during inference. Existing methods typically rely on supervision from known categories, leading models to overconfidently misclassify visually similar unknowns as known, and dissimilar ones as background. This known-class prior bias limits the model’s ability to detect unknown objects. In this paper, we propose a novel method, OW-DAR, which enhances foreground-background separability through collaborative fine-grained and coarse-grained modeling. At the fine-grained level, we propose Fine-grained Masked Reconstruction (FMR), which randomly masks regions of the feature map to guide the reconstruction toward semantic structures, rather than memorizing low-level patterns. At the coarse-grained level, we propose Adaptive Region-based Error Aggregation (AREA), which operates on object proposals to aggregate reconstruction errors. This enables the model to attend to semantically ambiguous foreground-background boundaries while suppressing the influence of local outliers during optimization. Finally, we leverage robust reconstruction errors to perform unsupervised foreground-background modeling, enabling probabilistic estimation for potential unknown objects. We validate the effectiveness of OW-DAR on standard OWOD benchmark. Experimental results demonstrate that OW-DAR consistently outperforms existing state-of-the-art methods, achieving a +18.8 improvement in unknown object recall (U-Recall).

---

## 论文详细总结（自动生成）

# OW-DAR: 双粒度自适应重构误差建模用于开放世界目标检测——论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究问题**：开放世界目标检测（OWOD）要求模型在训练阶段仅用已知类别的标注，推理时检测出已知和未知类别对象。现有方法因依赖已知类别的监督信号，导致模型产生“已知类别先验偏差”：对视觉上相似于已知类别的未知对象会过度自信地误分类为已知类别；对差异较大的未知对象则误判为背景。
- **研究背景**：现有OWOD方法（如ORE、OW-DETR、CAT等）普遍使用基于已知类别学习到的“对象性”（objectness）知识来生成伪标签，这加剧了先验偏差，限制了未知对象的召回率。
- **论文目标**：通过消除已知类别先验偏差，提升未知对象的检测能力，同时保持对已知类别的检测精度。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：受人类感知理论（预测编码和全局-局部处理）启发，通过**双粒度（细粒度+粗粒度）重构误差建模**来增强前景-背景可分离性，从而无偏地估计未知对象的概率。
- **整体架构**：基于Faster R-CNN + FPN（特征金字塔网络）的检测器，并附设一个双粒度自编码器。细粒度分支采用**细粒度掩码重构（FMR）**，粗粒度分支采用**自适应区域误差聚合（AREA）**。最终利用稳健的重构误差进行无监督前景-背景建模，获得未知对象的概率估计。
- **关键技术细节**：
  - **细粒度掩码重构（FMR）**：
    - 在FPN输出的特征图（如某一尺度的特征图 \(X \in \mathbb{R}^{H_F \times W_F \times C}\)）上，对每个元素以概率 \(r\) 随机掩码（置0），得到掩码特征图 \(X_{\text{mask}} = X \odot M\)，其中 \(M\) 为二进制掩码。
    - 通过编码器-解码器（自编码器）重构原始特征，计算元素级重构误差 \(E = \|\hat{X} - X\|\)。
    - 目标：引导模型关注局部语义结构而非低层模式，使得背景（结构规律）重构误差低，前景（结构复杂/遮挡频繁）重构误差高。
  - **自适应区域误差聚合（AREA）**：
    - 针对候选对象提议（默认使用Selective Search生成，但可替换为其他无监督提议方法），通过ROIAlign提取每个提议对应的重构误差区域 \(E_{b_i}\)，计算其均值 \(\bar{e}_i = \frac{1}{|b_i|}\sum_{j \in b_i} e_j\)。
    - 损失函数：\(L_{\text{AREA}} = \frac{1}{N} \sum_{i=1}^{N} \exp(-\alpha \bar{e}_i) \cdot \bar{e}_i^2\)，其中 \(\alpha\) 控制动态调整，抑制极端重构误差噪声，使模型聚焦于语义模糊的前景-背景边界。
  - **未知概率估计**：
    - 观察到前景和背景的重构误差呈偏态分布，采用非对称Weibull分布分别拟合前景（\(WB_{fg}\)）和背景（\(WB_{bg}\)）。
    - 对候选未知对象的重构误差图 \(E_{uk}\)，计算其属于前景的概率软标签：\(s(E_{uk}) = \left( \frac{WB_{fg}(E_{uk})}{WB_{bg}(E_{uk}) + WB_{fg}(E_{uk})} \right)^\gamma\)，其中 \(\gamma\) 控制软标签尖锐度。
    - 该软标签用作无监督训练信号，指导模型对未知区域的识别。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：标准OWOD基准数据集（S-OWODB），基于MS COCO数据集划分，包括4个任务增量学习场景（Task 1-4）。Task 1包含部分已知类别，后续任务逐步引入新类别，且所有任务中均存在未知类别。
- **评价指标**：
  - U-Recall：未知类别的召回率（主要指标）
  - mAP：已知类别的平均精度（包括当前已知、先前已知、两者平均）
  - WI（Wandering Instances）：被误分类为未知的已知实例数量
  - A-OSE（Average Open Set Error）：平均开放集错误数
- **对比方法**：
  - 无基础模型的方法：ORE-EBUI、OW-DETR、CAT、PROB、Hyp-OW、ORTH、MEPU-SS
  - 结合基础模型的方法：MEPU-FS、PROB+SAM、SGROD
  - 本方法：OW-DAR（默认无基础模型）、OW-DAR+SAM（增加SAM监督）
- **实验设置**：比较了各个任务（Task 1-4）下的U-Recall和mAP。额外评估了混淆指标（WI、A-OSE）。

## 4. 资源与算力

- 论文中未明确报告训练所使用的GPU型号、数量、训练总时长等详细算力信息。
- 仅在可视化分析中提到了在单张RTX 3090 GPU上测量推理速度，OW-DAR达到35.42 FPS，高于对比方法（SGROD: 24.51 FPS, MEPU-SS: 32.25 FPS, ORTH: 31.84 FPS）。
- **结论**：训练资源未公开，推理速度数据表明模型具有轻量化优势。

## 5. 实验数量与充分性

- **主实验**：在4个任务（T1-T4）上与现有SOTA方法进行全面对比，覆盖无基础模型和有基础模型两类设置。
- **消融实验**：
  - 组件消融（Tab.3）：分别移除FMR、移除AREA，验证双模块有效性。
  - 提议方法对比（Tab.4）：比较Selective Search、FreeSOLO、SAM、RandBox四种无监督区域提议方法，证明OW-DAR对提议质量不敏感。
  - 重构损失函数对比（Tab.5）：比较ℓ1、ℓ2、Huber损失与本文自适应损失，验证AREA中损失设计的优越性。
  - 掩码比率敏感性分析（Fig.4）：评估FMR中掩码比率r对性能的影响，确定最优值0.6。
- **可视化分析**（Fig.3）：定性展示检测结果，与其他方法进行直观对比。
- **实验充分性评价**：实验数量充足，涵盖了主要对比、部件消融、超参数分析、鲁棒性验证（不同提议方法）等维度。结果呈现清晰，消融实验证明了每个模块的贡献。对比方法涵盖了近年的主要工作，且考虑了基础模型版本的数据泄漏问题（排除了CLIP等）。整体实验设计公平、客观。

## 6. 论文的主要结论与发现

- OW-DAR在标准OWOD基准上显著超越现有方法，在Task 1上U-Recall达到52.1%，比最强无基础模型MEPU-SS提升+18.8%，比有基础模型SGROD提升+6.0%。已知类别检测性能（mAP）也达到75.1%，优于对比方法。
- 双粒度协同建模有效缓解了已知类别先验偏差，使模型能清晰分离前景（包括未知对象）和背景。
- 本方法不依赖任何视觉基础模型（如SAM、FreeSOLO），而能通过重构误差无偏估计未知对象概率。结合SAM后性能略有提升（+~2.0%），但核心能力源于自身双粒度设计。
- 方法的强度不在于提议生成质量，而在于从大量混合前景-背景候选精准区分未知对象的能力。

## 7. 优点

- **创新性**：首次将双粒度重构误差建模引入开放世界目标检测，从细粒度（元素级掩码）和粗粒度（区域级聚合）两个层次协同增强可分离性，方法新颖且有理论支撑（人类感知机制）。
- **有效性**：在多个任务和指标上实现大幅提升，消融实验充分验证各模块贡献。
- **轻量化**：采用纯卷积架构，不引入额外参数，推理速度快（35.42 FPS），易于部署。
- **泛化能力**：对不同无监督区域提议方法（Selective Search、RandBox、FreeSOLO、SAM）均表现稳健，表明方法对提议质量不敏感，具有较强的通用性。
- **实验严谨**：考虑了基础模型的数据泄漏问题，排除了CLIP等不合适的对比方法，并提供了多种设置下的对比，保证了结论的可靠性。

## 8. 不足与局限

- **实验覆盖**：
  - 仅在一个基准数据集（S-OWODB）上评估，缺乏更多样化的开放世界场景（如自动驾驶、工业检测等）验证。
  - 未报告模型在不同已知类别数量、不同类型未知对象（如小目标、遮挡严重）下的性能分析。
- **资源与可重复性**：未公开训练所需算力（如GPU型号、训练时长），可能影响复现成本评估。
- **局限性**：
  - 方法依赖于无监督区域提议（如Selective Search），虽经测试鲁棒，但在极端复杂背景或边缘场景下可能仍有偏差。
  - 未知概率估计采用固定的Weibull分布假设，是否始终最优缺乏更深入的理论或实验验证。
  - 在面对与已知类别高度相似的未知对象时，重构误差差异可能缩小，存在漏检风险（论文未专门分析这种边界情况）。
- **缺失可解释性**：元数据中标注了“方法未涉及可解释性”，即黑箱性质，难以解释为何某个区域被判定为未知。

（完）
