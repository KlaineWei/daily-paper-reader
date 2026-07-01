---
title: "Towards Explainable Video Camouflaged Object Detection: SAM2 with Eventstream-Inspired Data"
title_zh: 迈向可解释视频伪装目标检测：基于SAM2与事件流启发数据
authors: "Hong Zhang, Yixuan Lyu, Hanyang Liu, Jianbo Song, Ding Yuan, Yifan Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38245/42207"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 基于事件流启发数据的可解释视频伪装目标检测
tldr: 针对现有视频伪装目标检测方法依赖光流或黑盒特征导致可解释性差的问题，提出事件流启发双分支框架，通过模拟事件相机原理提取像素级运动变化，实现可解释的伪装物体检测。实验表明该方法在解释性和性能上均优于现有方法。为视频目标检测提供了新的可解释性视角。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1396, \"height\": 384, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 253, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1458, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1158, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 870, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38245/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 788, \"height\": 421, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1443, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1776, \"height\": 533, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 847, \"height\": 136, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38245/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 833, \"height\": 245, \"label\": \"Table\"}]"
motivation: 现有方法使用光流或黑盒特征，计算成本高且可解释性有限。
method: 提出事件流启发数据提取模块，捕获像素级运动变化，结合SAM2进行可解释的双分支检测。
result: 在VCOD基准上取得先进结果，并提升了可解释性。
conclusion: 事件流启发框架有效区分物体运动与背景动态，增强了可解释性。
---

## Abstract
Video Camouflaged Object Detection (VCOD) poses significant challenges due to the subtle appearance of camouflaged objects, especially under dynamic motion and occlusion. Existing methods predominantly rely on optical flow or black-box features for motion modeling, which often entail substantial computational costs and suffer from limited interpretability. Inspired by the human strategy of identifying abnormal movements between frames and the principle of event camera image formation, we propose an eventstream-inspired dual-branch framework for VCOD. Specifically, we design an eventstream-like data extraction module to capture pixel-level motion variations, effectively distinguishing object motion from background dynamics. This event-based representation is integrated into SAM2 through a dual-branch memory-augmented framework, consisting of Time Bridge Attention and Visual Bridge Attention, enabling joint modeling of motion and appearance cues. In addition, we introduce a Prompt Embedding Generator to eliminate the need for human-provided interactive prompts, facilitating fully automatic VCOD. Extensive experiments on MoCA-Mask and CAD2016 demonstrate that our approach significantly outperforms state-of-the-art methods, achieving both superior segmentation accuracy and interpretable motion modeling. To the best of our knowledge, this is the first work to incorporate eventstream-inspired representations into the VCOD task.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

视频伪装目标检测（VCOD）旨在从动态场景中检测与背景高度融合的物体。由于伪装物体外观模糊、运动微妙且常伴随遮挡，现有方法大多依赖光流或黑盒特征进行运动建模，不仅计算成本高，而且可解释性差。受人类通过比较相邻帧识别异常运动的视觉策略以及事件相机成像原理的启发，作者提出一种事件流启发的双分支框架，旨在实现可解释、高性能的VCOD。

## 2. 方法论

**核心思想**：模拟事件相机记录像素级亮度变化的方式，从相邻RGB帧中提取事件流启发的运动表征，并利用SAM2的强视觉先验，通过双分支记忆增强框架联合建模运动与外观线索，同时设计自动提示生成器消除人为交互。

**关键技术细节**：
- **事件流启发数据提取模块**：对相邻灰度帧进行基于ORB特征匹配和RANSAC的单应性全局运动补偿，计算运动残差图 D_t；通过自适应高斯阈值生成正/负运动图 P_t 和 N_t；将二者投影到RGB通道形成事件流表征 E_t；最后进行形态学操作去噪。
- **双分支记忆增强框架**：事件流分支（黄色箭头）提取运动特征 F_E_t，通过时间桥注意力（Time Bridge Attention）从记忆库中检索运动相关信息；视觉分支（绿色箭头）处理当前帧 I_t，通过视觉桥注意力（Visual Bridge Attention）获取外观一致性信息。两者独立参数共享架构，包含自注意力、交叉注意力和MLP。
- **提示嵌入生成器（PEG）**：融合事件流特征、视觉特征、记忆增强特征和高分辨率特征，通过残差增强、通道/空间注意力、自注意力和卷积投影生成稠密提示嵌入 P_t，无需人工标注即可引导SAM2的掩码解码器。
- **损失函数**：组合结构感知损失（加权BCE+IoU）、分割损失、SAM2的Focal Loss（权重20）和Dice Loss（权重1），超参数α=1, β=0.5。

## 3. 实验设计

**数据集与基准**：
- **MoCA-Mask**：87个视频（22,939帧），伪装动物自然场景。71个序列训练，16个测试。
- **CAD2016**：9个YouTube视频，每5帧标注像素级掩码。

**对比方法**：9种SOTA方法，包括RCRNet、PNS-Net、MG、SLT-Net、IMEX、TSP-SAM (M+P/M+B)、ZoomNeXt (T=1/T=5)、EMIP、EMIP-L。涵盖基于光流、记忆、Transformer等多种范式。

**评估指标**：6个标准指标——结构度量Sα、加权F-measure Fωβ、增强对齐度量Eϕ、平均绝对误差MAE、平均Dice、平均IoU。

## 4. 资源与算力

论文明确说明：所有实验在 **PyTorch** 框架下、**NVIDIA RTX 8000 GPU** 上运行。输入帧缩放到1024×1024。**未具体说明GPU数量、训练总时长或总计算开销**。仅提及使用余弦学习率调度，第一阶段SAM2微调学习率3×10⁻⁶/5×10⁻⁶，第二阶段视频微调5×10⁻⁴。

## 5. 实验数量与充分性

**实验组数**：包括主实验（2个数据集×9种SOTA对比）、消融实验（4种模块组合逐步添加）、与ESIM事件相机合成数据对比、计算效率对比（参数量、FPS、显存）、失败案例分析。总计至少5大类实验。消融实验验证了提示生成器、事件流数据、时间桥注意力的各自贡献，且每个组件均带来显著提升。实验设计相对充分，对比方法涵盖主流benchmark，指标全面。但消融实验仅在MoCA-Mask上报告，未在CAD2016上重复；对超参数（α,β）仅简单说明见补充材料，正文中未展示详细灵敏度分析。总体公平性良好，但部分SOTA方法代码未公开（如ZoomNeXt），导致无法完全复现所有对比。

## 6. 主要结论与发现

1. 提出的方法在**MoCA-Mask**上相比第二名ZoomNeXt在Fωβ上提升约20.4%（0.573 vs 0.476），mDice提升15.5%，mIoU提升17.5%；在**CAD2016**上Sα提升5.9%，Fωβ、mDice、mIoU提升均超过20%。
2. 事件流启发运动建模相比传统ESIM合成事件数据，**速度提升6倍以上**（35.65 vs 5.73 FPS），且所有指标均更优。
3. 双分支记忆增强显著提升性能，尤其是时间桥注意力使Fωβ相对提升超过50%。
4. 提示嵌入生成器成功替代人工提示，实现全自动分割。
5. 推理时参数量98.10M，FPS 2.56，显存3.78GB，优于多数对比方法。

## 7. 优点

- **可解释性**：事件流表征直接对应像素级运动残差，物理含义清晰，克服了光流或黑盒特征的不透明性。
- **自动化**：通过PEG模块消除对人工交互提示的依赖，更适合大规模视频处理。
- **在线处理**：仅使用历史帧（因果设置），无需未来帧，符合实际视频流场景。
- **运动-外观联合建模**：双分支记忆桥注意力有效融合两类信息，对遮挡和小目标检测效果好。
- **计算效率**：参数量、推理速度和显存占用均优于同类别方法。

## 8. 不足与局限

- **初始化敏感性**：模型高度依赖第一帧的提示质量（如第4.6节失败案例所示），当初始帧中目标严重遮挡时会导致误分割。作者虽提出可改用第100帧作为条件，但未给出自适应选择机制。
- **数据集有限**：仅使用两个公开VCOD数据集（MoCA-Mask和CAD2016），其中CAD2016规模较小（9个视频）。作者也承认缺少大规模专有VCOD数据集。
- **消融实验覆盖不足**：仅在MoCA-Mask上进行消融，未在CAD2016上验证各模块的泛化性；超参数敏感性分析仅提及见补充材料，正文未展示。
- **全局运动补偿假设**：单应性变换假设场景近似平面，对于深度剧烈变化的场景（如剧烈视角变换）可能失效。
- **未使用真实事件流数据**：当前仅从RGB帧合成事件流启发表征，未直接利用真实事件相机数据，可能损失部分时间分辨率优势。
- **对比公平性**：部分SOTA方法（如ZoomNeXt）由于代码未提供，作者采用其论文报告数值，无法保证完全相同的测试设置；在线/离线设置的区分虽已说明，但MAE指标并非最优（主要优化对象级结构度量）。

（完）
