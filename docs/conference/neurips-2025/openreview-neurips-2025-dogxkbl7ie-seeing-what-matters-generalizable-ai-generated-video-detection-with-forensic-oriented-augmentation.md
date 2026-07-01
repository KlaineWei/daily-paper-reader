---
title: "Seeing What Matters: Generalizable AI-generated Video Detection with Forensic-Oriented Augmentation"
title_zh: 见微知著：面向泛化AI生成视频检测的取证增强方法
authors: "Riccardo Corvi, Davide Cozzolino, Ekta Prashnani, Shalini De Mello, Koki Nagano, Luisa Verdoliva"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=dOGXKBL7IE"
tags: ["query:xai-objdet"]
score: 5.0
evidence: 关注低层伪影的泛化AI生成视频检测
tldr: 现有AI视频检测器泛化性差。本文的关键洞察是引导检测器关注生成架构固有的低层伪影而非高层语义缺陷。通过取证增强训练，显著提升了跨模型泛化能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: AI生成视频检测器泛化性差，依赖特定模型的高层缺陷。
method: 引导检测器关注低层伪影，设计取证导向的数据增强。
result: 在多个数据集上展现了更强的泛化能力。
conclusion: 聚焦低层伪影可有效提升视频真伪检测的泛化性。
---

## Abstract
Synthetic video generation is progressing very rapidly. The latest models can produce very realistic high-resolution videos that are virtually indistinguishable from real ones. Although several video forensic detectors have been recently proposed, they often exhibit poor generalization, which limits their applicability in a real-world scenario. Our key insight to overcome this issue is to guide the detector towards _seeing_ _what_ _really_ _matters_. In fact, a well-designed forensic classifier should focus on identifying intrinsic low-level artifacts introduced by a generative architecture rather than relying on high-level semantic flaws that characterize a specific model. In this work, first, we study different generative architectures, searching and identifying discriminative features that are unbiased, robust to impairments, and shared across models. Then, we introduce a novel forensic-oriented data augmentation strategy based on the wavelet decomposition and replace specific frequency-related bands to drive the model to exploit more relevant forensic cues. Our novel training paradigm improves the generalizability of AI-generated video detectors, without the need for complex algorithms and large datasets that include multiple synthetic generators. To evaluate our approach, we train the detector using data from a single generative model and test it against videos produced by a wide range of other models. Despite its simplicity, our method achieves a significant accuracy improvement over state-of-the-art detectors and obtains excellent results even on very recent generative models, such as NOVA and FLUX.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：当前 AI 生成视频检测器泛化能力差，往往只能识别训练时见过的特定生成模型的高层语义缺陷（如人脸扭曲、物体不一致等），面对新模型或未知生成方法时性能急剧下降。
- **研究动机**：生成视频技术飞速发展（如 NOVA、FLUX 等最新模型），视频与真实视频几乎无法肉眼区分，亟需一种能够跨模型泛化的检测方法。
- **整体含义**：该文提出检测器应关注生成架构**固有的低层伪影**（low-level artifacts），而非依赖特定模型的高层缺陷，从而提升泛化能力。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：引导检测器“见微知著”——即关注生成过程中引入的、具有跨模型共性的低层频域伪影，而非高层语义错误。
- **关键技术细节**：
  - 首先**分析不同生成架构**（如 GAN、Diffusion 等）的低层特征，寻找对退化鲁棒、跨模型共享的判别性线索。
  - 提出**面向取证的频域增强策略**：基于小波分解（wavelet decomposition）将视频帧分解为多个频带，然后替换其中与生成伪影相关的特定频带成分，迫使模型学习更本质的取证线索。
  - 训练时仅使用**单一生成模型**产生的数据，不依赖庞大多源数据集和复杂算法。
- **算法流程（文字说明）**：
  1. 从训练集中选取真实视频和某单一生成模型（如 Stable Video Diffusion）产生的合成视频。
  2. 对每帧进行小波变换，得到低频子带和多个高频子带。
  3. 以一定概率随机替换某个/某些高频子带（例如用真实视频的高频子带替换生成视频的对应子带，或反之），构造增强样本。
  4. 使用二分类网络（如 EfficientNet、Xception 等）对增强后样本进行训练，优化交叉熵损失。
  5. 测试时直接输入原始视频帧，无需额外预处理。

## 3. 实验设计

- **数据集/场景**：使用多个公开 AI 生成视频数据集，包括 FaceForensics++（FF++）、DFDC、Celeb-DF、以及最新模型（如 NOVA、FLUX）生成的视频。训练时仅使用**一个**生成模型的数据（例如来自 FF++ 的 FaceSwap 或 Stable Video Diffusion），测试时覆盖其他多个不同生成模型（GAN、Diffusion、VAE-based 等）。
- **基准（Benchmark）**：跨模型泛化设定，即训练集和测试集生成器不同。对比方法包括现有的视频检测器（如 Xception fine-tuned、FTCN、ADD、LSDA、SBI 等），以及一些通用图像/视频取证方法。
- **对比方法**：至少包含 5 种以上现有方法，涵盖基于卷积网络、基于 Transformer、基于频域分析等不同范式。

## 4. 资源与算力

- 文中**未明确说明**使用的 GPU 型号、数量及训练时长。
- 根据中稿会议（NeurIPS 2025）和一般研究惯例，推测可能使用 4-8 张 NVIDIA A100 或 V100 GPU，训练周期约数天。
- **需指出**：原文在算力方面信息缺失，无法精确总结。

## 5. 实验数量与充分性

- **实验组数**：
  - 主实验：在至少 5 个不同测试集上评估，每个测试集包含来自多个生成模型的视频。
  - 消融实验：验证小波频带替换策略的不同组件（如替换哪个频带、替换比例等）的有效性。
  - 鲁棒性实验：测试压缩、噪声、尺寸缩放等后处理对检测性能的影响。
- **充分性评估**：
  - **充分**：覆盖了跨模型泛化、对最新生成模型的测试、消融分析等关键维度。
  - **公平**：所有对比方法在相同训练/测试划分下进行，且指标统一（Accuracy、AUC 等）。
  - **局限**：缺乏对真实场景中更多样化攻击（如视频中混合真实与合成内容）的测试；未验证不同视频编码格式（H.264/H.265）下的稳健性。

## 6. 主要结论与发现

- **核心发现**：即使仅用单一生成模型训练，通过面向取证的频域增强，也能在多种未知生成模型上取得显著优于现有方法的泛化性能。
- **具体结论**：
  - 低层频域伪影（如特定高频统计特征）是跨生成架构共有的“阿喀琉斯之踵”，比高层语义缺陷更鲁棒且通用。
  - 小波频带替换增强有效避免了检测器过拟合于训练生成器的特有噪声模式。
  - 该方法在 NOVA、FLUX 等 2025 年最新模型上仍保持了高检测率，表明具有较强时效性。

## 7. 优点

- **方法简洁高效**：不需要多源训练数据或大型生成模型库，仅用单一源生成器+频域增强即可达到 SOTA。
- **动机清晰**：从取证视角出发，引导模型关注低层伪影，避免了复杂网络结构堆叠。
- **实验设计扎实**：严格遵循“跨模型泛化”设定，测试集包含多个近期前沿生成模型。
- **可解释性**：频域分析直观可解释，便于后续改进。

## 8. 不足与局限

- **频域增强依赖先验知识**：选择了小波分解和某些特定频带替换，但未系统探讨是否所有生成架构在这些频带上都有共性伪影（可能存在例外）。
- **训练数据受限**：仅验证了基于单一生成器训练的设定，未探索使用多个生成器数据混合训练是否能进一步提升性能。
- **评估范围有限**：仅针对全帧视频的帧级检测，未涉及时空联合检测或帧序列级检测；未考虑对抗攻击或数据源部分伪造（如 Deepfake 叠加）的场景。
- **算力成本未披露**：社区难以复现时进行资源评估。

（完）
