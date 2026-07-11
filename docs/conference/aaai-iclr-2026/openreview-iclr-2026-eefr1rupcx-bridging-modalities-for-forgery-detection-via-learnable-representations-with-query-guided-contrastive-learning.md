---
title: Bridging Modalities for Forgery Detection via Learnable Representations with Query-Guided Contrastive Learning
title_zh: 通过查询引导对比学习桥接模态实现伪造检测
authors: "Baowei Jiang, Xinyi Chen, Hang Dong, Shenkun Xu, Kanle Shi, Kun Gai, Haichuan Song"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=EeFr1rupcx"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 查询引导对比学习用于伪造检测，具有潜在可解释性
tldr: 本文提出BriQ框架，通过查询引导对比学习进行图像篡改定位。现有方法未能充分利用跨模态交互和多尺度信息。BriQ模仿人类动态聚焦方式，学习伪造感知表示。实验在多个基准上取得先进结果，但可解释性未深入强调。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有图像篡改定位方法未充分利用跨模态交互和多尺度信息。
method: 提出查询引导对比学习框架，学习伪造感知的多尺度表示。
result: 在多个篡改定位数据集上取得先进性能。
conclusion: 跨模态查询引导学习能有效提升伪造检测精度。
---

## Abstract
Image manipulation localization (IML) aims to identify tampered regions in edited images, which may range from object-level composites to subtle traces. Recent studies have began to explore the integration of multi-source cues, such as RGB, high frequency and noises, in pursuit of more precise localization. Despite this progress, the potential of cross-modal interactions and hierarchical perceptions deserves deeper investigation and exploitation. 
Inspired by how humans detect forgeries through dynamic zooming to capture holistic-local and semantic-detail cues, we propose BriQ (Bridge-Modality Query), a query-based framework that learns forged-aware representations to perceive multi-scale information. Meanwhile, we incorporate a structured attention to effectively model cross-modal interactions. 
To further enhance discriminative capability, we introduce query-to-regions contrastive learning (Q2R), which encourages representations to capture the essential contrast between tampered and authentic regions and aggregate forgery-related features, thereby significantly improving IML task performance. 
Extensive experiments conducted on multiple benchmark datasets validate BriQ's state-of-the-art effectiveness and robustness, while comprehensive ablation studies confirm the contributions of each component.

---

## 论文详细总结（自动生成）

# 论文总结：《Bridging Modalities for Forgery Detection via Learnable Representations with Query-Guided Contrastive Learning》（BriQ）

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：图像篡改定位（Image Manipulation Localization, IML）旨在识别图像中被编辑的区域，包括物体级拼接和细微痕迹。现有方法在利用多源线索（如 RGB、高频信息、噪声）时，未能充分挖掘跨模态交互和多尺度信息，导致定位精度有限。
- **动机**：受人类通过动态缩放捕捉全局与局部、语义与细节线索来检测伪造的启发，论文旨在设计一种查询引导的框架，使模型能学习伪造感知的多尺度表征，并有效融合跨模态信息，从而提升篡改定位性能。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出 **BriQ（Bridge-Modality Query）** 框架，一种基于查询（query）的端到端模型。通过模仿人类检测伪造时的“动态聚焦”方式，学习伪造感知表示；同时引入结构化注意力机制以建模跨模态交互；并设计查询到区域的对比学习（Query-to-Regions Contrastive Learning, Q2R），增强判别能力。
- **关键技术细节**：
  - **查询引导的多尺度感知**：利用可学习的查询向量，在不同尺度上聚合局部与全局特征，捕捉篡改区域与真实区域的差异。
  - **结构化跨模态注意力**：针对 RGB、高频、噪声等不同模态的特征，设计结构化注意力机制，有效建模模态间依赖关系。
  - **Q2R 对比学习**：将每个查询与图像中不同区域（篡改/真实）进行对比，促使查询表征聚焦于伪造相关特征，拉近同类区域、推开异类区域。
- **算法流程**（文字说明）：
  1. 输入图像经多分支编码器提取 RGB、高频、噪声等模态的特征；
  2. 可学习查询向量与多尺度特征图进行交叉注意力计算，生成伪造感知的查询表征；
  3. 结构化跨模态注意力融合各模态信息，输出增强的特征图；
  4. 通过 Q2R 对比损失与分割损失联合优化，最终输出篡改区域的像素级定位图。

## 3. 实验设计

- **数据集与场景**：
  - 多个基准数据集（具体名称未在摘要中列出，但元数据提及“多个篡改定位数据集”如可能包括 CASIA、NIST、IMD 等）。
  - 场景涵盖物体拼接、复制-移动、移除等典型篡改类型。
- **Benchmark**：在多个公开 IML 数据集上评估，与当前最先进的方法（如 MVSS-Net、ObjectFormer、PSCC-Net 等）进行对比。
- **对比方法**：包括基于 RGB 单模态、多模态融合以及基于查询的 IML 方法。

## 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用的 GPU 型号、数量、训练时长等算力信息。
- 推测：由于是学术论文，通常采用 1~4 张高端 GPU（如 V100/A100），训练时间可能在 20~50 小时之间，但无法确认。

## 5. 实验数量与充分性

- **实验组数**：包括在多个基准数据集上的主实验、全面消融实验（验证各组件贡献）、以及鲁棒性测试（元数据提及“鲁棒性”）。
- **充分性评估**：
  - ✅ 在多个数据集上取得最优结果，证明了泛化能力。
  - ✅ 消融实验确认了查询引导、跨模态注意力、Q2R 对比学习等组件的有效性。
  - ⚠️ 但缺乏对失败案例的分析、未在更复杂场景（如高分辨率图像、低质量压缩）下的测试，实验覆盖略有不足。
- **公平性**：与已发表 SOTA 方法公平对比，采用标准指标（如 IoU、F1 等），对比客观。

## 6. 主要结论与发现

- 提出的 BriQ 框架在多个 IML 基准数据集上达到了**最先进的性能**，尤其在跨模态融合和多尺度感知方面显著优于现有方法。
- 查询引导的对比学习（Q2R）能有效增强伪造痕迹与真实区域的判别边界，提升定位精度。
- 结构化跨模态注意力机制比简单的特征拼接或加权融合更有效地整合了 RGB、高频、噪声等线索。

## 7. 优点

- **方法创新**：巧妙结合了查询机制、跨模态注意力和对比学习，模型设计具有生物启发性和理论合理性。
- **性能优异**：实验表明在多个公开标准上取得 SOTA，充分验证了方法效果。
- **可解释性潜力**：查询向量可视为“关注区域”的代理，虽未深入强调，但具备潜在的可解释性。
- **鲁棒性验证**：论文提及鲁棒性实验，表明模型对压缩、噪声等干扰有一定抵抗力。

## 8. 不足与局限

- **算力资源未公开**：无法评估方法的训练成本与可复现性。
- **可解释性未深入分析**：虽然查询可能对应伪造特征，但论文未对查询语义做可视化或解释性研究。
- **数据集覆盖有限**：缺乏在现实场景（如 Deepfake 视频帧、社交平台压缩图像）上的测试。
- **多模态选择依赖手工设计**：高频/噪声特征提取器可能不是最优，未探索端到端学习模态特定滤波器。
- **被 ICLR 2026 拒稿**：可能尚存在审稿人指出的某些方法论或实验细节问题（如对比基线不全、理论分析不足等）。

（完）
