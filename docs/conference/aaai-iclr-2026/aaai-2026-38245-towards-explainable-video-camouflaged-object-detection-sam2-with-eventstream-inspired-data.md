---
title: "Towards Explainable Video Camouflaged Object Detection: SAM2 with Eventstream-Inspired Data"
title_zh: 迈向可解释的视频伪装目标检测：结合事件流启发数据的SAM2
authors: "Hong Zhang, Yixuan Lyu, Hanyang Liu, Jianbo Song, Ding Yuan, Yifan Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38245/42207"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的视频伪装目标检测，使用事件流启发数据
tldr: 本文针对视频伪装目标检测提出一种事件流启发的双分支框架，旨在提高可解释性。现有方法依赖光流或黑盒特征，计算成本高且可解释性差。所提方法通过模拟事件相机原理，提取像素级运动变化，区分目标运动与背景动态。实验表明该方法在多个VCOD基准上获得更好性能，同时提供直观的异常运动解释。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 620}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1396, \"height\": 384}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 253}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1458, \"height\": 391}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1158, \"height\": 479}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 870, \"height\": 332}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 788, \"height\": 421}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1443, \"height\": 246}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1776, \"height\": 533}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 847, \"height\": 136}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 833, \"height\": 245}]"
motivation: 现有视频伪装目标检测方法依赖黑盒特征，缺乏可解释性且计算成本高。
method: 设计事件流启发的双分支框架，通过像素级运动变化提取模块增强可解释性。
result: 在视频伪装目标检测基准上取得优异性能，同时提供可理解的运动解释。
conclusion: 事件流启发的运动建模能有效提升检测可解释性和性能。
---

## Abstract
Video Camouflaged Object Detection (VCOD) poses significant challenges due to the subtle appearance of camouflaged objects, especially under dynamic motion and occlusion. Existing methods predominantly rely on optical flow or black-box features for motion modeling, which often entail substantial computational costs and suffer from limited interpretability. Inspired by the human strategy of identifying abnormal movements between frames and the principle of event camera image formation, we propose an eventstream-inspired dual-branch framework for VCOD. Specifically, we design an eventstream-like data extraction module to capture pixel-level motion variations, effectively distinguishing object motion from background dynamics. This event-based representation is integrated into SAM2 through a dual-branch memory-augmented framework, consisting of Time Bridge Attention and Visual Bridge Attention, enabling joint modeling of motion and appearance cues. In addition, we introduce a Prompt Embedding Generator to eliminate the need for human-provided interactive prompts, facilitating fully automatic VCOD. Extensive experiments on MoCA-Mask and CAD2016 demonstrate that our approach significantly outperforms state-of-the-art methods, achieving both superior segmentation accuracy and interpretable motion modeling. To the best of our knowledge, this is the first work to incorporate eventstream-inspired representations into the VCOD task.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

视频伪装目标检测（VCOD）面临重大挑战：伪装物体外观与背景高度相似，且在动态运动和遮挡场景下难以检测。现有方法主要依赖光流或黑盒特征进行运动建模，计算成本高且可解释性差。受人类通过比较相邻帧识别异常运动的行为以及事件相机成像原理的启发，论文提出一种**事件流启发（eventstream-inspired）的双分支框架**，旨在实现**可解释**且**高性能**的VCOD。这是首次将事件流启发表示引入VCOD任务。

## 2. 论文提出的方法论

### 核心思想
通过模拟事件相机对像素级强度变化的敏感特性，从相邻RGB帧中提取类似事件的运动表示（事件流启发数据），并将其与SAM2结合，构建**双分支记忆增强框架**，同时建模运动与外观线索，实现无需人工提示的自动分割。

### 关键技术细节
- **事件流启发数据提取模块**：  
  1. 将相邻帧转换为灰度图，通过**ORB特征匹配+RANSAC**估计单应性矩阵进行全局运动补偿，消除相机运动干扰。  
  2. 计算补偿后帧的残差图 \( D_t = G_t - G'_t \)。  
  3. 使用基于局部高斯统计的**自适应阈值**生成正负运动图 \( P_t, N_t \)。  
  4. 将正负运动图投影到RGB通道形成事件流启发表示 \( E_t \)，并施加形态学操作去噪。  
  （对应公式1-3）

- **双分支记忆增强框架**：  
  - **事件流分支**（黄色箭头）：处理 \( E_t \) 得到运动特征 \( F^E_t \)，通过**Time Bridge Attention**与记忆库交互获取 \( M^E_t \)。  
  - **视觉分支**（绿色箭头）：处理当前帧 \( I_t \) 得到视觉特征 \( F^I_t \)，通过**Visual Bridge Attention**获取 \( M^I_t \)。  
  - 桥注意力（Bridge Attention）结构：自注意力 + 交叉注意力（以记忆为条件）+ MLP。

- **Prompt Embedding Generator (PEG)**：  
  融合事件流特征、视觉特征、记忆增强特征及高分辨率特征，通过通道&空间注意力、残差增强等生成特征级提示嵌入 \( P_t \)，替代人工交互提示，实现全自动VCOD。

- **损失函数**：联合损失 \( \mathcal{L} = \alpha \mathcal{L}_{\text{emb}} + \beta \mathcal{L}_{\text{mask}} + 20\mathcal{L}_{\text{focal}} + \mathcal{L}_{\text{Dice}} \)，其中 \( \alpha=1, \beta=0.5 \)。

### 算法流程（文字说明）
1. 对每对连续帧 \( I_{t-1}, I_t \) 提取事件流启发表示 \( E_t \)。  
2. 将 \( E_t \) 和 \( I_t \) 分别送入事件流分支和视觉分支。  
3. 两条分支分别通过Time/Visual Bridge Attention从记忆库 \( M_{t-1} \) 中检索相关特征，输出增强特征 \( M^E_t, M^I_t \)。  
4. PEG模块融合这些特征生成提示嵌入 \( P_t \)。  
5. Mask Decoder使用提示和增强特征预测当前帧掩码，并更新记忆库。

## 3. 实验设计

### 数据集
- **MoCA-Mask**：87个视频（22,939帧），71训练/16测试，伪装动物自然场景。  
- **CAD2016**：9个YouTube片段，每5帧标注像素掩码（较小数据集）。

### Benchmark
采用标准VCOD评估协议，在两个数据集上对比了9种SOTA方法：RCRNet, PNS-Net, MG, SLT-Net, IMEX, TSP-SAM, ZoomNeXt, EMIP, EMIP-L等。

### 评价指标
六项指标：\( S_\alpha \), \( F^\omega_\beta \), \( E_\phi \), 平均绝对误差（MAE）, 平均Dice (mDice), 平均IoU (mIoU)。

### 对比结果
- 在MoCA-Mask上：\( F^\omega_\beta \) 提升20.4%，mDice提升15.5%，mIoU提升17.5%。  
- 在CAD2016上：\( S_\alpha \)提升5.9%，\( F^\omega_\beta \)、mDice、mIoU提升超20%。  
- 所有方法中，本文方法在多数指标上最优（除MAE外，但结构指标更优）。

## 4. 资源与算力

- **GPU**：NVIDIA RTX 8000（单卡）。  
- **训练策略**：两阶段训练。  
  1. 第一阶段：在COD10K上微调SAM2（学习率：图像编码器3e-6，其他模块5e-6）。  
  2. 第二阶段：在MoCA-Mask上微调新增模块（PEG和桥注意力，学习率5e-4）。  
- **推理效率**：本文方法参数量98.10M（23.5M可训练+74.6M非可训练），FPS 2.56（表4），低于FSPNet、TSP-SAM等，内存占用3.78GB。  
- **未明确说明**：具体训练时长、GPU数量等未提及。

## 5. 实验数量与充分性

### 实验类型
- **主实验**：两个数据集上与9种方法对比（表1）。  
- **消融实验**（表2）：验证三个组件（Prompt Gen、Eventstream、Time Bridge）的有效性，逐步添加。  
- **事件流数据对比**（表3）：与ESIM合成事件数据对比性能和速度。  
- **计算效率对比**（表4）：参数量、FPS、内存。  
- **定性结果**：图5（MoCA-Mask两个场景）、图6（中间结果可视化）、图7（失败案例分析）。  
- **其他**：补充材料中还有更多可视化、训练步骤讨论等（提及但未在正文详述）。

### 充分性评价
实验设计较为全面：涵盖定量、定性、消融、效率、与真实事件数据对比。消融实验清晰展示了各模块贡献。但**对比方法范围有限**，主要聚焦于近三年VCOD方法，缺少更早期或跨领域方法。另外，仅使用两个公开数据集，且CAD2016规模较小，可能限制泛化性结论。

## 6. 论文的主要结论与发现

- 提出的事件流启发运动表示有效捕捉了像素级运动变化，与SAM2结合后显著提升了VCOD性能，同时提供了可解释的运动线索。  
- 通过自动提示生成（PEG）消除了对人工交互的依赖，实现了全自动在线VCOD。  
- 双分支记忆增强机制（Time/Visual Bridge Attention）联合建模运动与外观信息，尤其在遮挡和快速运动场景下表现出色。  
- 在MoCA-Mask和CAD2016上达到SOTA，并且计算效率优于同类方法。

## 7. 优点

- **创新性**：首次将事件流启发表示引入VCOD，摆脱光流/黑盒特征的局限，增强可解释性。  
- **实用性**：自动提示生成，无需人工标注；在线处理（仅用历史帧），适合实时场景。  
- **性能优异**：在多项指标上大幅领先现有最佳方法，尤其在结构度量上优势明显。  
- **效率较高**：参数量较少，推理速度快，内存占用低。  
- **实验充分**：包含了详尽的消融、对比、效率分析以及定性可视化，验证了各模块有效性。

## 8. 不足与局限

- **数据集有限**：仅使用MoCA-Mask和CAD2016两个数据集，后者规模小，且缺少真实事件流数据集（当前使用合成事件流启发数据，未使用真实事件相机数据）。  
- **初始帧敏感**：如失败案例（图7）所示，若初始帧中目标被严重遮挡或无法辨识，模型可能错误分割背景。作者尝试引入额外初始帧以缓解，但缺乏自适应性。  
- **MAE指标并非最优**：虽然结构指标领先，但平均绝对误差（MAE）不如某些方法，可能因为预测掩码边界较锐利，像素级误差略高。  
- **全局运动补偿假设**：使用单应性矩阵假设平面场景，在深度变化大的场景（如近景复杂背景）可能失效。  
- **未公开完整训练时长**：资源描述不够详细，无法完全复现训练成本。  
- **实验对比尚可完善**：缺少对更多长视频场景、不同遮挡程度的系统评估，也缺少与真实事件数据直接比较（仅有ESIM合成数据对比）。

（完）
