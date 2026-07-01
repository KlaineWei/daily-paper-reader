---
title: Learnable Frequency Decomposition for Image Forgery Detection and Localization
title_zh: 图像伪造检测与定位的可学习频率分解
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0152.pdf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 图像伪造检测与定位，使用可学习频率分解，具可解释性
tldr: 该论文针对图像伪造检测与定位问题，提出了可学习的频率分解方法。通过自动学习鉴别性频率特征，该方法不仅能检测伪造区域，还能通过频率分布提供可解释的检测依据。实验表明，该方法在多个伪造检测数据集上达到了领先性能，且定位精度高，为可解释伪造检测提供了新思路。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 757, \"height\": 680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1710, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 695, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 632, \"height\": 362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1280, \"height\": 985, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 607, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 812, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-152/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 853, \"height\": 549, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-152/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1833, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-152/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 871, \"height\": 465, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-152/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 694, \"height\": 326, \"label\": \"Table\"}]"
motivation: 现有伪造检测方法缺乏可解释性和频率域针对性。
method: 设计可学习的频率分解模块，从输入图像中提取多频带特征并融合用于检测和定位。
result: 在标准数据集上取得了最优的检测和定位精度。
conclusion: 该方法验证了频率分解在可解释伪造检测中的有效性。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

# 图像伪造检测与定位的可学习频率分解（F2D-Net）论文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：现有基于深度学习的图像伪造检测与定位方法大多聚焦于空间域建模，未充分探索频域策略。然而，图像编辑留下的痕迹在RGB域不可见，但在频域中往往明显。
- **关键观察**：作者通过傅里叶变换分析真实图像与伪造图像的频域差异，发现：
  - 操纵痕迹在**相位分量**中比幅度分量更突出，因为相位对应语义内容，而伪造常改变物体语义；
  - 操纵引起的频率变化**同时分布在低频和高频**，并非仅集中于高频。
- **核心目标**：利用频域相位信息和自适应高低频分解，提升伪造检测与定位的精度和鲁棒性。

## 2. 方法论：核心思想、关键技术细节
- **总体框架**：提出 **F2D-Net**（Forensic Frequency Decomposition Network），包含两个子网络：
  1. **频谱分解子网络（SDSN）**：将图像分解为幅度和相位，重点学习相位谱中的伪造痕迹；
  2. **频率分离子网络（FSSN）**：自适应将特征分解为低频和高频，采用分治策略分别处理，缓解频率间耦合。

### 关键技术细节
- **SDSN 核心组件**：
  - 使用 **ResNet-50** 作为骨干。
  - 插入 **相位强调交互块（PEI）**：包含空间分支和频率分支，通过 **空间-频率双交叉注意力（SFDCA）** 实现双域信息交互，增强相位特征提取。
  - 通过傅里叶变换将特征映射到频域，对相位进行卷积操作后与幅度重组，再逆变换回空间。
- **FSSN 核心组件**：
  - 利用全局平均池化和全连接层预测一个二维掩码（mask），定义低通/高通边界（α, β 缩放值，范围0~1）。
  - 基于该掩码从特征中分离出低频分量 $G_L$ 和高频分量 $G_H$（对幅度分量进行掩码乘，相位分量卷积处理）。
  - 分别对 $G_L$ 和 $G_H$ 进行空间域卷积处理后再融合，并与空间分支通过 **双注意力模块（DA）** 融合得到最终定位图。
- **检测分支**：通过 ConvGeM 将定位图转换为检测预测。
- **损失函数**：组合 Dice 损失（定位和边缘）与 BCE 损失（检测），设置 α=0.6, β=0.2。

## 3. 实验设计
- **预训练数据**：自制大规模合成篡改数据集，包含拼接、复制-移动、移除三种类型。
- **测试数据集**：
  - **定位评估**：CASIA、Coverage、Columbia、NIST16、IMD20（真实网络图像）。
  - **检测评估**：CASIA-D（由原 CASIA 分割）。
- **对比方法**：ManTraNet、SPAN、PSCCNet、ObjectFormer、TANet、HiFi IFDL 等 SOTA 方法。
- **评估指标**：像素级 AUC、F1 分数；检测 AUC、F1。
- **两种实验设置**：
  1. **预训练模型直接评估**：在合成数据上训练后，直接测试全部数据集。
  2. **微调模型评估**：在测试数据的训练集上微调，再在其测试集上评估。
- **鲁棒性评估**：对 NIST16 图像施加缩放、高斯模糊、高斯噪声、JPEG 压缩等失真，比较 AUC。
- **消融实验**：分别去除 ALP（额外相位学习）、SFDCA、FSSN 组件，以及在 CASIA 和 NIST16 上评估。
- **可视化分析**：展示预测掩码、PEI 块特征、GradCAM 等。

## 4. 资源与算力
- **文中未明确说明使用的 GPU 型号、数量及训练时长**。
- 仅在致谢中提及国家自然科学基金资助，未提供具体训练硬件信息。

## 5. 实验数量与充分性
- **实验组数**：
  - 定位预训练模型在5个数据集（表1a）上的评估。
  - 定位微调模型在3个数据集（表1b）上的 AUC 和 F1 对比。
  - 检测性能在 CASIA-D 上的对比（表1c）。
  - 鲁棒性测试8种失真条件（表2）。
  - 消融实验5种变体（表3）。
  - PEI 块数量影响实验（图6）。
  - 多组可视化分析（图5、7、8）。
- **充分性评价**：实验覆盖多个常见数据集和多种伪造类型，设置了预训练和微调两种场景，并进行了鲁棒性和消融分析，对比了多个 SOTA 方法，实验设计较为全面。
- **公平性**：使用了与对比方法相同的训练/测试划分，指标一致，结果客观可信。

## 6. 主要结论与发现
- F2D-Net 在绝大多数数据集上取得了最优或次优的定位和检测性能，尤其对复制-移动等难以察觉的伪造效果显著。
- 相位学习（ALP）对性能贡献最大（消融实验中 AUC 下降最多），验证了相位成分作为伪造痕迹的主要载体。
- 自适应频率分离（FSSN）能有效细化定位，减少假阳性。
- 相比其他方法，F2D-Net 在 JPEG 压缩、噪声等失真下表现出更强的鲁棒性。
- 可视化证明 PEI 和 FSSN 能增强对伪造区域的关注。

## 7. 优点
- **方法创新**：首次系统地将傅里叶域相位学习和自适应高低频分离结合起来用于 IFDL，填补了频域策略在图像伪造检测中的空白。
- **设计合理**：基于频率分析观察设计组件，PEI 块有效促进空间-频率交互；FSSN 采用分治策略处理耦合痕迹。
- **性能领先**：在多个基准数据集上超越 SOTA，尤其是 Copy-Move 数据集上 AUC 达 94.2%。
- **鲁棒性强**：面对多种常见图像后处理操作（压缩、缩放、噪声）仍保持较高 AUC。
- **可解释性**：通过频域分解和相位强调，模型能提供与伪造区域更相关的特征，具有一定的可解释性。

## 8. 不足与局限
- **计算开销未报告**：未给出模型的参数量、FLOPs 或推理时间，难以评估实际部署成本。
- **预训练数据合成局限**：自建合成数据集可能与真实世界伪造存在分布差异，泛化性可能受限（如 Columbia 数据集上预训练非最优）。
- **对未知伪造类型泛化性未验证**：仅测试了拼接、复制-移动、移除三类，未涉及如深度伪造、GAN 生成图像等更复杂类型。
- **实验细节缺失**：未说明训练超参数（学习率、batch size、epoch）、数据增强策略等，影响实验可复现性。
- **未提供失败案例**：没有分析模型在哪些情况下会失败或误判，缺乏对模型边界的讨论。
- **硬件资源未说明**：无法评估训练耗时和计算资源需求。

（完）
