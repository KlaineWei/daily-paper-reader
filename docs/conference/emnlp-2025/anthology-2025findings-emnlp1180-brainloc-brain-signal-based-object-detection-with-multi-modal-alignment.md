---
title: "BrainLoc: Brain Signal-Based Object Detection with Multi-modal Alignment"
title_zh: BrainLoc：基于多模态对齐的脑信号目标检测
authors: "Jiaqi Duan, Xiaoda Yang, Kaixuan Luan, Hongshun Qiu, Weicai Yan, Xueyi Zhang, Youliang Zhang, Zhaoyang Li, Donglin Huang, JunYu Lu, Ziyue Jiang, Xifeng Yang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.1180.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 基于脑信号的目标检测
tldr: 现有关注用户意图的方法依赖中间模态导致效率低。BrainLoc直接利用fMRI信号进行目标检测，通过多模态对齐策略增强特征提取，在保持轻量化的同时提升检测精度。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1180/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1539, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1180/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1637, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1180/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 773, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.1180/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1631, \"height\": 524, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1180/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.1180/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 493, \"label\": \"Table\"}]"
motivation: 传统方法通过中间模态表达用户意图存在效率低下和失真问题。
method: 提出fMRI引导的轻量目标检测模型，采用多模态对齐增强特征。
result: 在脑信号数据集上取得高检测精度。
conclusion: 脑信号作为直接意图表达模态在目标检测中具有潜力。
---

## Abstract
Object detection is a core challenge in computer vision. Traditional methods primarily rely on intermediate modalities such as text, speech, or visual cues to interpret user intent, leading to inefficient and potentially distorted expressions of intent. Brain signals, particularly fMRI signals, emerge as a novel modality that can directly reflect user intent, eliminating ambiguities introduced during modality conversion. However, brain signal-based object detection still faces challenges in accuracy and robustness. To address these challenges, we present BrainLoc, a lightweight object detection model guided by fMRI signals. First, we employ a multi-modal alignment strategy that enhances fMRI signal feature extraction by incorporating various modalities including images and text. Second, we propose a cross-domain fusion module that promotes interaction between fMRI features and category features, improving the representation of category information in fMRI signals. Extensive experiments demonstrate that BrainLoc achieves state-of-the-art performance in brain signal-based object detection tasks, showing significant advantages in both accuracy and convenience.

---

## 论文详细总结（自动生成）

### 论文总结：BrainLoc：基于多模态对齐的脑信号目标检测

#### 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：传统目标检测依赖中间模态（如文本、语音、图像）来表达用户意图，这导致效率低下且意图可能失真（例如用户需费力描述纹理、空间信息）。脑信号（尤其是fMRI）能直接反映用户意图，避免模态转换的歧义。
- **背景**：fMRI具有高信息熵，可捕捉丰富的语义和视觉细节，优于EEG。然而，现有基于脑信号的目标检测方法在准确性和鲁棒性上仍有挑战。论文旨在构建一个轻量级、高精度的fMRI引导目标检测模型，实现更自然的人机交互（如智能眼镜实时定位用户关注的物体）。

#### 2. 方法论：核心思想、关键技术细节
- **核心思想**：提出 BrainLoc，一个轻量级fMRI目标检测框架，包含三大模块：特征提取、跨域融合、定位。
- **关键技术细节**：
  - **特征提取**：设计轻量级提取器（ConvBlock + ResidualBlock + TransformerBlock + Qformer），将fMRI信号映射到CLIP特征空间。采用多模态对齐策略，同时对齐fMRI与图像（L1损失）、文本类别（余弦损失）、文本描述（对比损失）三种模态，损失函数组合为 \( L_{total} = 0.5 L_{fMRI-cat} + 0.25 L_{fMRI-img} + 0.25 L_{fMRI-cap} \)。
  - **跨域融合**：利用视觉域（fMRI特征）和语义域（类别特征）在共享CLIP空间中的互补优势。通过相似度计算获取精确类别，再采用交叉注意力机制（以fMRI特征为Query，类别特征为Key/Value）融合得到融合特征。
  - **定位模块**：将融合特征和背景图像输入Grounding DINO，使用匈牙利算法优化分类损失（交叉熵）和IoU损失，生成最终边界框。

#### 3. 实验设计
- **数据集**：
  - **NSD**（Natural Scenes Dataset）：8名被试，10,000张自然场景图像（基于COCO），包含多目标，噪声较高。
  - **GOD**（Generic Object Decoding）：5名被试，200个类别的单目标图像（基于ImageNet），信号更纯净。
- **训练策略**：两阶段。第一阶段用NSD训练特征提取器；第二阶段冻结提取器，用GOD的fMRI信号与NSD中对应物体的图像配对，训练融合和定位模块。
- **基准对比**：
  - **脑信号方法**：UMBRAE、Shikra-w/ Brain-Diffuser、Shikra-w/ MindEye、Shikra-w/ DREAM、UMBRAE-S 等（通过先重建图像再用Shikra检测的方式）。
  - **文本方法**：Grounding DINO、Shikra（纯文本输入）。
- **评价指标**：acc@0.5（IoU > 0.5的准确率）和IoU。将COCO 80类分为“显著”（含生物/物体）和“不显著”子集进行评估。

#### 4. 资源与算力
- **算力**：明确提及使用 **4张A800 GPU**，训练 **1000 epochs**。模型总可训练参数为130M，约为MindEye的1/10。

#### 5. 实验数量与充分性
- **实验数量**：
  - 主要性能对比（表1）：对比了6种脑信号方法、2种文本方法，覆盖全部、显著、不显著等细分类别。
  - 消融实验（表2）：5组消融，分别移除多模态对齐、主类别优化、对比学习、融合模块，以及替换定位模块为Shikra。
  - 额外讨论：分析了损失函数选择原因及模型区分颜色细节的能力。
- **充分性**：实验设计全面，覆盖主流基线，消融验证了各模块必要性。但仅用了两个数据集（NSD/GOD），且均为实验室环境采集，未在真实场景或更多被试上验证。

#### 6. 主要结论与发现
- **BrainLoc 在脑信号目标检测上达到SOTA**：acc@0.5为64.13%，IoU为67.08%，显著优于其他脑信号方法（如UMBRAE acc@0.5仅18.93%）。
- **与文本方法比较**：BrainsLoc的IoU高于Grounding DINO（67.08 vs 48.66），但acc@0.5略低（64.13 vs 80.16），说明其定位更精确但存在某些边界框偏离阈值的情况。
- **关键发现**：避免图像重建步骤、多模态对齐和跨域融合是性能提升的核心；模型能捕获颜色等细粒度信息，从而区分“红苹果”与“绿苹果”，而文本方法仅能识别“苹果”。

#### 7. 优点
- **方法亮点**：
  - **轻量化**：参数仅为MindEye的1/10，无需图像生成，推理效率高。
  - **多模态对齐创新**：同时对齐fMRI与图像、文本类别、文本描述三种模态，损失函数设计合理（融合余弦、L1、对比损失）。
  - **跨域融合模块**：利用视觉和语义域的互补优势，通过交叉注意力提升类别与空间信息的融合。
- **实验亮点**：
  - 两阶段训练策略有效利用NSD和GOD的特点。
  - 消融实验充分，清晰展示了各组件的贡献。
  - 对比基线覆盖全面（包括重建+检测的级联方法）。

#### 8. 不足与局限
- **数据依赖**：fMRI采集成本高，难以获取大规模、高质量数据；个体脑活动差异可能影响泛化。
- **生态效度**：仅使用实验室采集的NSD和GOD数据集，未在真实场景（如动态视频、多模态干扰）下验证。
- **模型上限**：性能仍落后于文本方法（如Grounding DINO的acc@0.5），且依赖预训练CLIP和Grounding DINO的固定能力。
- **未来方向**：论文指出将转向EEG以实现实时应用，但未在EEG上实验。
- **局限性**：未公开代码或模型，结果可复现性未知；仅报告了平均指标，未提供统计显著性检验。

（完）
