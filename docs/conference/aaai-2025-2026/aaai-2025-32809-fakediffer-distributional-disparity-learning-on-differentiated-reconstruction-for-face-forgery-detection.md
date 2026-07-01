---
title: "FakeDiffer: Distributional Disparity Learning on Differentiated Reconstruction for Face Forgery Detection"
title_zh: FakeDiffer：基于差异化重构的分布差异学习用于人脸伪造检测
authors: "Bo Wang, Zhao Zhang, Suiyi Zhao, Xianming Ye, Haijun Zhang, Meng Wang"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/32809/34964"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 人脸伪造检测方法，未显式提供可解释性
tldr: 该论文针对现有伪造检测方法泛化性差的问题，提出FakeDiffer框架，通过学习真实与伪造图像的分布差异来提升泛化能力。但方法专注于分布差异学习，未提供可解释性机制。实验在多个伪造类型上验证了泛化性能。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32809/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 880, \"height\": 882, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32809/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1845, \"height\": 921, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32809/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1852, \"height\": 964, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32809/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 881, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32809/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 869, \"height\": 785, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32809/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1844, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32809/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1845, \"height\": 587, \"label\": \"Table\"}]"
motivation: 现有方法过拟合已知伪造模式，泛化到未知样本能力弱。
method: 提出真实-伪造分布差异学习框架，通过差异化重构学习图像内在信息。
result: 在跨伪造类型泛化实验中取得良好性能。
conclusion: 分布差异学习提升了泛化性，但未涉及可解释性。
---

## Abstract
Existing face forgery detection methods achieve promising performance when training and testing forgery data are from identical manipulation types, while they fail to generalize well to unseen samples. In this paper, we experimentally investigate and find that the poor generalization of the methods mainly arises from their overfitting on the known fake patterns. Excessively focused on seen fakes, those detectors fail to effectively learn image-intrinsic information and the distributional disparity between real and fake images. Then, to address this issue, we redefine fake learning as real-fake distributional disparity learning. We propose a novel deepfake detection framework learning distributional disparity based on the differentiated reconstruction on real and fake images for improved generalization. Specifically, distributional disparity learning on differentiated reconstruction of the real and fake images, enforces the model to learn image-invariant intrinsic representations. The reconstruction on real and fake images forces the decoders to learn the distribution of real and fake images, respectively. Moreover, to avoid the influence from the specificalization of the known fake patterns, we further propose the information interaction learning on the encoded intrinsic information and the pixel disparity between the input image and its reconstruction to distinguish face forgeries that are even unknown. Extensive experiments on large-scale benchmark datasets demonstrated the effectiveness of addressing the overfitting issue of the classification network, and verified the superior performance of our method.

---

## 论文详细总结（自动生成）

# FakeDiffer: 基于差异化重构的分布差异学习用于人脸伪造检测 —— 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有的人脸伪造检测方法在训练和测试数据来自相同伪造类型时表现良好，但在面对**未知伪造样本时泛化能力很差**。作者通过实验发现，这一问题的根源在于**模型过度拟合已知的伪造模式**，而忽略了图像内在信息以及真实与伪造图像之间的分布差异。这些检测器过分关注已见过的伪造痕迹，导致无法有效学习图像不变性内在表示和真实-伪造分布差异。
- **核心问题**：如何设计方法使模型不仅识别已知伪造模式，还能捕捉**真实与伪造图像之间的分布差异**，从而提升对未见伪造类型的泛化能力。
- **整体含义**：作者重新定义伪造检测任务为“真实-伪造分布差异学习”，并提出FakeDiffer框架，通过**差异化重构**（对真实和伪造图像分别使用不同解码器重构）来强制模型学习图像内在不变信息，并融合重构误差信息以区分未知伪造。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
- 利用**统一编码器 + 双解码器（真实重构器、伪造重构器）** 进行差异化重构，使编码器学习**图像不变性内在表示**，而两个解码器分别学习真实和伪造图像的分布。
- 进一步提出**信息交互学习**，将编码得到的内在表示、真实重构误差、伪造重构误差三者融合，利用通道注意力机制为不同来源信息赋予权重，最终用于分类。

### 关键技术细节
#### 2.1 分布差异学习模块
- **输入**：添加白噪声后的图像 $\tilde{X}$，分为真实图像 $\tilde{X}_r$ 和伪造图像 $\tilde{X}_f$。
- **编码**：统一编码器 $F_e$（基于XceptionNet）提取中间表示 $M = F_e(\tilde{X})$。由于受双解码器约束，$M$ 被认为是**图像不变性内在表示**。
- **重构**：
  - 真实重构分支：$\hat{X}_r = F_r(M_r)$，仅对真实样本计算重构损失 $L_{rr}$（L1 loss）。
  - 伪造重构分支：$\hat{X}_f = F_f(M_f)$，仅对伪造样本计算重构损失 $L_{fr}$（L1 loss）。
- **误差图编码**：通过共享权重的卷积网络 $f$ 计算重构误差图：
  $$E_r = f(|F_r(M) - X|)$$
  $$E_f = f(|F_f(M) - X|)$$
  得到真实重构误差信息和伪造重构误差信息。

#### 2.2 信息交互学习模块
- 将三种特征（$M$, $E_r$, $E_f$）通过**像素级相加**得到融合特征图 $K$。
- 对 $K$ 进行全局平均池化得到全局特征 $G$，然后通过MLP和softmax生成三个权重，分别作用于 $M$, $E_r$, $E_f$，得到加权后的 $\hat{M}, \hat{E}_r, \hat{E}_f$。
- 最终融合特征 $T = \hat{M} + \hat{E}_r + \hat{E}_f$ 送入分类头进行二元分类。

#### 2.3 损失函数
- 总损失：$L = \lambda_r L_{rr} + \lambda_f L_{fr} + L_{cls}$，其中 $L_{cls}$ 为二分类交叉熵损失。经验设置 $\lambda_r = \lambda_f = 0.1$。

## 3. 实验设计

### 数据集与场景
- **训练/测试数据集**：
  - **FaceForensics++ (FF++)**：包含Deepfakes (DF)、Face2Face (F2F)、FaceSwap (FS)、NeuralTextures (NT)四种类型，有C23（高质量）和C40（低质量）两个版本。
  - **Celeb-DF (CDF)**：590个真实视频+5639个高质量伪造视频。
  - **WildDeepfake (WDF)**：3805个真实序列+3509个伪造序列，来自互联网，场景多样。
- **实验场景**：
  1. **Intra-testing**：在FF++（C23和C40）、Celeb-DF、WDF上训练并测试（同分布）。
  2. **Cross-testing（跨数据集）**：在FF++ C40上训练，在Celeb-DF和WDF上测试。
  3. **跨伪造类型交叉测试**：在FF++ C40上，用四种伪造类型之一训练，在其他类型和全集上测试。
- **评估指标**：Accuracy (Acc), Area Under the Curve (AUC), Equal Error Rate (EER)。

### 基准方法对比
- 对比方法包括：MesoNet, Multi-task, Xception, Face X-ray, Two-branch, RFM, Freq-SCL, MultiAtt, LiSiam, RECCE, SIA, F2Trans-B, CFM, DisGRL, ATSC, UniAttack等。

## 4. 资源与算力

- **文中明确说明**：所有实验在**单个 NVIDIA GeForce RTX 4090 GPU** 上完成，使用 PyTorch 1.11。
- **训练配置**：30个epoch，batch size=32，学习率2e-4（含warmup 10000步），权重衰减1e-5。
- **未提及**：具体训练时长（如每epoch耗时等）未报告。

## 5. 实验数量与充分性

### 实验数量
- **表1**：Intra-testing（4个数据集，两个质量版本，共约6组对比）。
- **表2**：Cross-testing（跨数据集2组：FF++→Celeb-DF，FF++→WDF）。
- **表3**：跨伪造类型交叉测试（4种训练类型分别测试其他3种及平均，共4×4=16组子实验）。
- **表4**：消融实验（不同信息源，包括real-inf, fake-inf, Xception, dual recons, FakeDiffer，在4个跨类型验证和2个跨数据集验证上）。
- **表5**：消融实验（不同融合方式：相加 vs 交互，同样在6个验证任务上）。
- 总计约 **30+组实验**。

### 充分性、客观性、公平性
- **充分性**：覆盖了同分布、跨数据集、跨伪造类型三大场景，消融实验验证了各模块贡献，实验设计较为全面。
- **客观性**：所有指标采用标准AUC/Acc/EER，与已发表论文结果直接比较（部分引用原文数据，部分复现）。
- **公平性**：与多种SOTA方法对比，在相同实验设置下进行（统一使用FF++官方划分），但部分对比方法的结果可能引用自原始论文而非完全复现，存在微小偏差风险。

## 6. 论文的主要结论与发现

- **核心发现**：现有方法泛化差的主要原因是对已知伪造模式的**过拟合**，而非对真实图像的过拟合。
- **方法有效性**：FakeDiffer通过差异化重构学习分布差异，显著提升跨域泛化性能。例如在FF++ C40的跨伪造类型平均AUC上，FakeDiffer达到76.66%（NT训练）和72.52%（F2F训练），超过RECCE等。
- **信息交互学习优于简单相加**：消融实验表明，交互融合方式（加权注意力）比直接像素相加更有效。
- **图像不变性内在表示**是鲁棒的关键：单独使用编码器表示（Xception）效果弱于结合重构误差信息，而交互融合三者最佳。

## 7. 优点（方法或实验设计上的亮点）

1. **创新性**：首次提出**差异化重构**学习真实与伪造的分布差异，而非简单共享重构器，更符合两类数据本质差异。
2. **模块设计合理**：通过双解码器约束编码器学习图像不变性，同时保留重构误差作为强判别线索。
3. **信息交互机制**：利用通道注意力自适应融合三种特征，提升特征表达能力。
4. **实验全面**：不仅做了标准跨数据集测试，还做了**细粒度跨伪造类型交叉测试**，更有力证明泛化能力。
5. **可复现性**：使用常见骨架（Xception）和标准数据集，超参数明确，易于复现。

## 8. 不足与局限

1. **可解释性欠缺**：论文未提供任何可解释性分析（如注意力可视化、误差图可视化），难以理解模型具体关注哪些区域。
2. **算力报告不完整**：仅提及GPU型号，未给出训练时长、参数量、推理速度等，不利于资源评估。
3. **对比方法覆盖有限**：缺少与最新的基于Transformer或视觉语言模型（如ViT、CLIP-based）的对比，时效性略逊。
4. **单一骨架依赖**：仅使用Xception作为编码器，未尝试其他更强骨干（如ResNet、EfficientNet）验证通用性。
5. **应用限制**：方法假设训练数据中同时有真实和伪造样本，且伪造样本需标注类型从而分别送入对应解码器。在只有真实数据或伪造类型未知的场景下可能不适用。
6. **未讨论失败案例**：没有分析哪些伪造类型或场景下性能仍然较差，缺乏误差分析。

（完）
