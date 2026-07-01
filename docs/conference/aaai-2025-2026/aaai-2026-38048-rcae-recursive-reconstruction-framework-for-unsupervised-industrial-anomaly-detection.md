---
title: "RcAE: Recursive Reconstruction Framework for Unsupervised Industrial Anomaly Detection"
title_zh: RcAE：无监督工业异常检测的递归重构框架
authors: "Rongcheng Wu, Hao Zhu, Shiying Zhang, Mingzhe Wang, Zhidong Li, Hui Li, Jianlong Zhou, Jiangtao Cui, Fang Chen, Pingyang Sun, Qiyu Liao, Ye Lin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38048/42010"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 异常检测递归重构方法
tldr: 无监督工业异常检测任务中，传统自编码器单次解码难以处理多尺度异常。本文提出递归自编码器RcAE，通过迭代重建逐步抑制异常并恢复正常结构，并设计跨递归检测模块利用重建动态信息。实验表明该方法在多个工业数据集上显著优于现有方法，为异常检测提供了更精细的递归机制。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38048/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 767, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38048/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1831, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38048/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1482, \"height\": 752, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38048/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 870, \"height\": 649, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38048/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1841, \"height\": 1176, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38048/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 714, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38048/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 885, \"height\": 183, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38048/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 855, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38048/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 892, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38048/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 691, \"height\": 186, \"label\": \"Table\"}]"
motivation: 传统自编码器单次解码无法有效处理不同严重程度和尺度的异常，导致异常抑制不完整和细节丢失。
method: 提出递归自编码器结构，迭代进行重建，逐步抑制异常并精炼正常结构，同时引入跨递归检测模块利用重建序列。
result: 在多个工业异常检测基准数据集上取得了领先的检测和定位性能。
conclusion: 递归机制能够有效提升异常检测的精度和鲁棒性，为无监督异常检测提供了新范式。
---

## Abstract
Unsupervised industrial anomaly detection requires accurately identifying defects without labeled data. Traditional autoencoder-based methods often struggle with incomplete anomaly suppression and loss of fine details, as their single-pass decoding fails to effectively handle anomalies with varying severity and scale. We propose a recursive architecture for autoencoder (RcAE), which performs reconstruction iteratively to progressively suppress anomalies while refining normal structures. Unlike traditional single-pass models, this recursive design naturally produces a sequence of reconstructions, progressively exposing suppressed abnormal patterns. To leverage this reconstruction dynamics, we introduce a Cross Recursion Detection (CRD) module that tracks inconsistencies across recursion steps, enhancing detection of both subtle and large-scale anomalies. Additionally, we incorporate a Detail Preservation Network (DPN) to recover high-frequency textures typically lost during reconstruction. Extensive experiments demonstrate that our method significantly outperforms existing non-diffusion methods, and achieves performance on par with recent diffusion models with only 10% of their parameters and offering substantially faster inference. These results highlight the practicality and efficiency of our approach for real-world applications.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **任务**：无监督工业异常检测，需要在无标签数据下精确识别产品缺陷。
- **现有方法痛点**：传统自编码器（AE）存在四大局限：
  1. 过拟合于有限且同质的正常数据，导致泛化差、漏检高。
  2. 表达力强的潜在空间可能重建异常区域，降低检测对比度。
  3. 单次解码会过度平滑高频细节，在正常区域产生误报。
  4. 固定尺度架构难以处理不同大小和严重程度的异常。
- **对比最新方法**：GAN、Transformer、扩散模型虽然提升重建质量，但计算成本高、推理慢、参数多，不适合工业部署。
- **本文目标**：在不引入复杂或资源密集设计的前提下，实现高质量异常重建与检测，兼顾性能与效率。

## 2. 方法论：核心思想、关键技术细节、算法流程

### 2.1 整体框架
本文提出**RcAE（Recursive Convolutional Autoencoder）**，由三个模块组成：
- **递归自编码器（RcAE）**：将重建过程变为多步迭代，逐步抑制异常并稳定正常结构。
- **细节保留网络（DPN）**：恢复高频纹理细节，减少正常区域的误报。
- **跨递归检测模块（CRD）**：利用多步重建的动态差异，定位异常。

### 2.2 递归自编码器（RcAE）

- **结构**：使用共享参数的编码器 \(E\) 和解码器 \(D\)，分别进行递归压缩和递归重建。
- **压缩阶段**：输入图像 \(x\) 经 \(N\) 次递归压缩，每次通过 \(E\) 降低空间分辨率（下采样卷积层，kernel=2, stride=2）。
- **重建阶段**：从压缩表示开始，经 \(N\) 次递归重建，每次通过 \(D\) 恢复分辨率（反卷积上采样）。
- **渐进优势**：早期递归保留细节但可能残留异常，后期递归更好抑制异常但可能过平滑。这种渐进行为暴露异常模式。
- **损失函数**：\(L_{\text{rec}} = \|I - I_N^R\|_1 + \|I' - (I_N^R)'\|_1\)，包括像素级 L1 损失和梯度边缘损失。

### 2.3 细节保留网络（DPN）

- **目标**：选择性地恢复正常区域的高频细节，避免引入异常。
- **结构**：轻量4层卷积自编码器，含跳跃连接。输入为递归重建图像 \(I_n^R\) 与输入梯度 \(I'\) 的拼接，输出残差图 \(\text{Res}_n^D\)。
- **输出**：\(I_n^D = I_n^R + \text{Res}_n^D\)。
- **损失**：\(L_{\text{DPN}} = \|(I_n^D) - I\|_1 + \|(I_n^D)' - I'\|_1\)，只对正常样本训练，冻结 RcAE。
- **推理**：异常产生分布外残差，DPN 无法恢复，从而保持抑制。

### 2.4 跨递归检测模块（CRD）

- **目标**：利用多步重建间的动态不一致性，生成像素级异常图。
- **结构**：4 层 3D 卷积自编码器（含跳跃连接），输入为原始图像 \(I\) 与所有细节增强重建 \(\{I_n^D\}\) 的拼接。
- **输出**：异常图 \(M_A\)。
- **训练**：冻结 RcAE 和 DPN，仅用正常样本，通过简单数据增强（随机色块、复制粘贴、随机线条）生成伪异常掩码 \(M_P\)，优化 \(L_{\text{CRD}} = \|M_A - M_P\|_2 + \|M_A' - M_P'\|_2\)。

### 2.5 训练策略

- **三阶段独立训练**（均从零开始）：
  - Stage 1: 训练 RcAE，递归深度随机采样自 \([1,N]\)。
  - Stage 2: 冻结 RcAE，训练 DPN。
  - Stage 3: 冻结 RcAE 和 DPN，训练 CRD。
- **优化器**：Adam（\(\eta=10^{-4}, \beta_1=0.9, \beta_2=0.999, \epsilon=10^{-8}\)）。
- **设置**：递归深度 \(N=5\)，输入分辨率 \(1024\times1024\)。

## 3. 实验设计

### 3.1 数据集
- **MVTec AD**：15 个类别（5 纹理 + 10 物体），包含多种缺陷。
- **VisA**：12 个类别，结构更复杂，异常类型更多样。

### 3.2 评价指标
- 图像级 AUROC（I-AUROC）
- 像素级 AUROC（P-AUROC）

### 3.3 对比方法
- **非扩散方法**：DRAEM、PatchCore、RD4AD、EfficientAD。
- **流方法**：MSFlow。
- **扩散方法**：D3AD、DiAD、DiffAD、GLAD（使用 DINO+潜扩散）。

### 3.4 基准设置
- 所有基线采用官方设置。
- 本文方法从头训练，不使用任何预训练模型。

## 4. 资源与算力

- **GPU**：NVIDIA RTX 4090。
- **软件**：Python 3.10。
- **训练时长**：
  - Stage 1: 1500 epochs
  - Stage 2: 400 epochs
  - Stage 3: 300 epochs
- **参数效率**：本文方法仅用扩散模型 10% 的参数，推理速度显著更快。
- **未明确说明**：具体训练总时间（小时）、模型参数量精确值（仅在图4中显示圈大小相对比较）。

## 5. 实验数量与充分性

- **主实验**：在两个数据集上对比 9 种方法，报告每个类别和平均结果（表1），共 27 组数据（15+12 类别 × 2 指标）。
- **消融实验**：
  - 核心组件消融（表2）：RcAE、DPN、CRD 逐步添加，共 4 组。
  - 递归深度 \(N\) 影响（表3）：N=1~6，两组数据集，共 12 组。
  - 跳跃连接与参数共享消融（表4）：4 组配置，两个数据集，共 8 组。
  - 数据效率实验（表5）：5 种训练数据比例（10%~100%），对比 ConvAE，共 10 组。
  - CRD 输入递归步数消融（表6）：NR=1,3,5，共 3 组。
  - 重建质量定量（SSIM/PSNR）在文中文字提及，未列表。
- **计算效率对比**（图4）：参数量 vs. 精度 vs. 推理时间。
- **结论**：实验覆盖全面，消融充分，对比方法多样（含强基线如扩散模型），数据客观公平（使用标准指标和公开代码设置）。

## 6. 主要结论与发现

- **性能优势**：
  - MVTec AD：I-AUROC 98.9%，P-AUROC 98.7%，优于所有非扩散方法，与最先进扩散方法 GLAD 持平，但参数少 90%。
  - VisA：I-AUROC 99.2%，P-AUROC 98.6%，排名前二。
- **递归机制有效**：逐步重建可抑制异常并保持正常结构，跨步态差异提供有效检测线索。
- **细节保留网络**：降低误报，提升重建的 SSIM 和 PSNR。
- **数据高效**：仅用 10% 训练数据即超越全数据 ConvAE 的性能。
- **效率平衡**：在精度-效率 trade-off 上达到最优，适合工业部署。

## 7. 优点

1. **创新框架**：递归重建思想简单但有效，参数共享使模型轻量。
2. **模块化设计**：RcAE、DPN、CRD 各司其职，可独立训练，易于扩展。
3. **检测能力强**：能同时捕捉细微和大尺度异常，利用时序动态信息。
4. **训练友好的损失函数**：结合梯度损失，保留边缘信息。
5. **无需预训练**：从零开始训练，避免外部知识依赖，适用于稀疏数据场景。
6. **实验充分**：多维度消融、数据效率测试、跨数据集验证，结果可靠。

## 8. 不足与局限

1. **逻辑异常处理弱**：对需要语义推理的高级逻辑异常（如正确位置但错误数量）效果较差（论文自述）。
2. **递归深度选择**：N=5 为最优，但未讨论对不同异常类型的最佳深度自适应策略。
3. **伪异常生成**：简单增强（色块、线条）可能不覆盖所有真实缺陷模式，存在偏差风险。
4. **计算资源**：虽然参数少，但递归过程仍需多次前向，推理时间略长于单次模型。
5. **数据集覆盖**：仅限于 MVTec AD 和 VisA，未在更复杂场景（如医疗、卫星图像）验证泛化性。
6. **未报道**：模型参数量精确数值、训练总耗时、推理 FPS 等具体工程数据，不利于严格复现比对。

（完）
