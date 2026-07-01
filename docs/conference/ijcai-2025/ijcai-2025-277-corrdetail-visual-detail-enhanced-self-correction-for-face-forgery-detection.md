---
title: "CorrDetail: Visual Detail Enhanced Self-Correction for Face Forgery Detection"
title_zh: CorrDetail：面向人脸伪造检测的视觉细节增强自校正方法
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0277.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 人脸伪造检测与视觉细节增强
tldr: 该论文针对人脸伪造检测问题，提出了一种视觉细节增强的自校正方法（CorrDetail）。方法通过提取并利用高分辨率细节特征，结合自校正网络逐步修正误判，从而提升伪造区域定位能力。实验在FaceForensics++等数据集上验证了其有效性，获得了更高的检测精度。该工作为虚假人脸检测提供了可解释的细节辅助手段。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-277/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 875, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-277/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 948, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-277/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 867, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-277/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 872, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-277/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1637, \"height\": 693, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-277/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 875, \"height\": 371, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-277/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1831, \"height\": 697, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-277/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 839, \"height\": 616, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-277/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 887, \"height\": 487, \"label\": \"Table\"}]"
motivation: 人脸伪造检测中，现有方法对细节信息利用不足，导致检测不准。
method: 提出CorrDetail框架，包含视觉细节增强模块和自校正机制。
result: 在多个基准数据集上取得了更高的检测准确率和鲁棒性。
conclusion: 视觉细节增强和自校正相结合能有效提升伪造检测性能。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

# 中文详细总结：CorrDetail: Visual Detail Enhanced Self-Correction for Face Forgery Detection

## 1. 核心问题与整体含义（研究动机和背景）

人脸伪造检测面临两大挑战：
- **基于纯视觉的方法**虽能获取伪造痕迹，但往往缺乏可解释性，只能输出二分类结果，无法给出具体伪造线索。
- **多模态方法**（结合视觉与语言）虽然能提供语义解释，但大视觉语言模型（VLM）容易产生“幻觉”，输出不准确的伪造描述，降低可靠性和准确性。

本文旨在解决上述问题，提出一种**视觉细节增强的自校正框架（CorrDetail）**，通过引入错误引导的问题、视觉细粒度细节增强以及融合决策策略，提升人脸伪造检测的**性能**和**可解释性**，同时有效抑制VLM的幻觉现象。

---

## 2. 方法论：核心思想、关键技术细节

### 2.1 整体框架
CorrDetail包括三个核心模块：
1. **自校正视觉问答（Self-Correction VQA, SCVQA）**：训练策略
2. **跨模型伪造细节增强（Cross-model Forgery Detail Enhancement, CFDE）**：视觉特征增强
3. **决策融合（Decision Fusion）**：包含提示增强机制和双专家模型决策

### 2.2 自校正视觉问答（SCVQA）
- 在训练时，对原始问题以特定概率引入**错误**或**正确**的伪造细节描述：
  - 70% 概率加入错误细节（作为错误引导问题）
  - 15% 概率加入正确细节的同义替换
  - 15% 保持原问题
- 使模型学会忽略误导信息，聚焦于图像中的真实伪造特征，而不是依赖提示获取答案，从而减少幻觉。

### 2.3 跨模型伪造细节增强（CFDE）
- 针对VLM在视觉-文本对齐过程中丢失细粒度伪造细节的问题，引入额外的**视觉Transformer分支（ViT）**，提取图像的内在视觉特征。
- 将额外文本提示（`P_extra`）作为查询`Q`，图像令牌`I_token`作为值`V`，视觉特征`I_vit`作为键`K`，通过交叉注意力机制生成增强的图像令牌`Ĩ_token`：
  ```
  P_token = Tokenizer(P_extra)
  I_vit = ViT(I)
  I_token = Projector(CLIP(I))
  Ĩ_token = A(P_token, I_vit, A(P_token, I_vit, I_token))
  ```
  其中`A(Q,K,V) = softmax(QK^T/√d_k)V + V`。
- 最终`Ĩ_token`作为新的图像令牌输入VLM，增强对伪造细节的感知。

### 2.4 决策融合（Decision Fusion）
#### 2.4.1 提示增强机制（Prompt Enhancement Mechanism）
- 针对面部占比小、背景干扰等困难样本，加入引导提示（如“请更关注脸部/背景”），获得第二轮预测概率。
- 根据两轮预测的置信度变化，使用**比例融合**公式调整最终输出，纠正因注意力偏移导致的误判。
- 超参数λ=0.1用于排除极端置信度样本。

#### 2.4.2 双专家模型决策（Dual-Expert Model Decision）
- 独立训练一个纯视觉分支（包含CLIP、ViT、多尺度模块），使用交叉熵损失，获得独立预测概率`P_vis`。
- 将VLM分支输出`P_fus`与视觉分支输出相乘并归一化，得到最终概率`P_final`，实现信息互补与偏差减少。

---

## 3. 实验设计

### 3.1 数据集
- **训练集**：基于FF++数据集构建了自校正VQA数据集（SCVQA），包含19,797个[图像, 问题, 答案]三元组。
- **评估集**：
  - **内测试**：FF++（低质量LQ和高质量HQ）
  - **跨测试**：Celeb-DF、WildDeepfake (WDF)、DeepForensics-1.0 (DFR)、DeepFaceGen（包含27种实时AIGC方法）

### 3.2 基准与对比方法
- 对比了XceptionNet、EfficientNet-B4、Local-relation、RFM、RECCE、CD-Net、UIA-VIT、GS、HiFi-Net、PFG-DD、RECCE（DD-VQA）等11种主流方法。
- 注：RECCE (DD-VQA) 也是基于VLM的方法。

### 3.3 评价指标
- 准确率（ACC）、AUC、等错误率（EER）

---

## 4. 资源与算力

论文明确提到：
- **GPU**：3块 Nvidia A100 GPU
- **训练**：微调LLaVA-1.5-7B，学习率5e-5，训练3个epoch，batch size 64
- **优化器**：AdamW，余弦退火学习率衰减
- 其他硬件细节未提及。

---

## 5. 实验数量与充分性

论文做了以下实验：
1. **内测试（Intra-testing）**：在FF++（LQ和HQ）上与SOTA对比（表1），包含ACC、AUC、EER共7个指标。
2. **跨测试（Cross-testing）**：在Celeb-DF、WDF、DFR、DeepFaceGen上进行跨数据集的泛化测试（表1、表2、图5）。
3. **消融实验**：对SCVQA、CFDE、决策融合三个模块进行逐步消融（表3），共3×2×2=8种组合（含全无）。
4. **可视化分析**：GPT-4o mini对比示例（图4）、CFDE热力图对比（图6）、困难样本提示增强案例（图3）。

**充分性评价**：实验设计较为全面，涵盖内测、跨测、泛化测试，并提供了可视化解释。但消融实验仅在FF++ LQ和HQ上进行，未在跨数据集上做完整的消融，略有不足。对比方法均为公开SOTA，评价指标标准，公平性较好。

---

## 6. 主要结论与发现

- CorrDetail在**内测试**中在FF++ LQ和HQ上均取得最佳ACC和AUC（如LQ上ACC达94.41%，AUC 96.93%；HQ上ACC 99.28%，AUC 99.92%）。
- **跨测试**中，在Celeb-DF上ACC和AUC均超过72%，EER降至33.87%，显著优于所有对比方法。
- 在更困难的DeepFaceGen基准上（仅跨测试），CorrDetail甚至优于在该数据集上内测的RECCE等方法，展现了强大的**泛化能力**和**鲁棒性**。
- 消融实验证实：三个模块均有效，其中CFDE和决策融合贡献最大，SCVQA对降低幻觉和提升细节提取有重要作用。
- 定性示例表明CorrDetail能给出正确且详细的伪造线索，而GPT-4o mini会出现错误或幻觉。

---

## 7. 优点

1. **创新性**：将自校正机制引入人脸伪造检测，通过错误引导训练抑制VLM幻觉，是一个新颖的设计。
2. **模块化设计**：CFDE模块通过交叉注意力跨模态增强视觉细节，决策融合有效处理困难样本和补偿信息损失，各模块可解释性强。
3. **性能领先**：在多个基准上达到SOTA，尤其跨数据集泛化能力突出。
4. **可解释性**：能输出文本形式的伪造细节，帮助理解检测依据。
5. **实验翔实**：涵盖内测、跨测、泛化测试，并进行了消融和可视化分析。

---

## 8. 不足与局限

1. **消融实验范围有限**：仅在内测试FF++（LQ/HQ）上做了消融，未在跨数据集（如Celeb-DF、DeepFaceGen）上验证各模块的贡献，可能低估了模块在不同场景下的重要性。
2. **依赖大规模预训练模型**：基座为LLaVA-1.5-7B，对计算资源要求较高（3×A100），可能限制了在资源受限场景的部署。
3. **数据集规模**：SCVQA数据集仅基于FF++构建，未包含更广泛的AIGC伪造类型（如Midjourney、Stable Diffusion等），在真实世界复杂场景下的泛化性有待进一步验证（虽然作者在DeepFaceGen上做了跨测，但SCVQA本身来自FF++）。
4. **超参数敏感性**：提示增强机制中的λ=0.1为固定值，不同数据集可能需要调整，但未进行敏感性分析。
5. **未对比最新VLM方法**：对比方法中仅包含RECCE (DD-VQA)一种VLM方法，未与近期更强大的多模态大模型（如GPT-4V、LLaVA-NeXT等）进行全面比较（尽管作者与GPT-4o mini做了定性对比）。
6. **实践限制**：框架需要同时运行VLM和独立视觉分支，推理速度可能较慢，论文未提供效率对比。

（完）
