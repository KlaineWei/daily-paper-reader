---
title: AI-Generated Video Detection via Perceptual Straightening
title_zh: 通过感知直线化检测AI生成视频
authors: "Christian Internò, Robert Geirhos, Markus Olhofer, Sunny Liu, Barbara Hammer, David Klindt"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=LsmUgStXby"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 通过感知直线化检测AI生成视频，提供可解释的时间分析
tldr: 论文针对AI生成视频检测的泛化性问题，提出基于感知直线化假设的ReStraV方法。利用预训练DINOv2模型，量化视频时间轨迹的曲率和步长距离，通过偏离自然视频几何属性的程度来检测生成视频。实验表明该方法具有良好泛化性和可解释性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有检测方法泛化性差且难以捕捉时间不一致性。
method: 基于感知直线化假设，量化DINOv2表示中的时间曲率进行检测。
result: 在多种生成视频检测任务中取得优异性能。
conclusion: 感知直线化提供了可解释且通用的视频伪造检测途径。
---

## Abstract
The rapid advancement of generative AI enables highly realistic synthetic video, posing significant challenges for content authentication and raising urgent concerns about misuse. Existing detection methods often struggle with generalization and capturing subtle temporal inconsistencies. We propose $ReStraV$ ($Re$presentation $Stra$ightening for $V$ideo), a novel approach to distinguish natural from AI-generated videos. Inspired by the ``perceptual straightening'' hypothesis—which suggests real-world video trajectories become more straight in neural representation domain—we analyze deviations from this expected geometric property. Using a pre-trained self-supervised vision transformer (DINOv2), we quantify the temporal curvature and stepwise distance in the model's representation domain. We aggregate statistical and signals descriptors of these measures for each video and train a classifier. Our analysis shows that AI-generated videos exhibit significantly different curvature and distance patterns compared to real videos. A lightweight classifier achieves state-of-the-art detection performance (e.g., $97.17$ % accuracy and $98.63$ % AUROC on the VidProM benchmark, substantially outperforming existing image- and video-based methods. ReStraV  is computationally efficient, it is offering a low-cost and effective detection solution. This work provides new insights into using neural representation geometry for AI-generated video detection.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：生成式AI技术飞速发展，能够生成高度逼真的合成视频，给内容真实性验证带来巨大挑战，现有检测方法泛化能力差，且难以捕捉细粒度的时序不一致性。
- **整体含义**：提出一种基于“感知直线化”（perceptual straightening）假设的新方法，通过分析神经网络表示中视频时间轨迹的几何属性（曲率和步长距离）来区分自然视频与AI生成视频，旨在提升检测的泛化性和可解释性。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：借鉴认知科学中的“感知直线化”假设——真实世界的视频在神经表示空间中时间轨迹趋于直线化，而AI生成视频会偏离这一几何属性。
- **关键技术细节**：
  - 使用预训练的自监督视觉Transformer（DINOv2）提取视频帧的嵌入表示。
  - 对每个视频，在DINOv2表示空间中量化时间轨迹的**曲率**（temporal curvature）和**步长距离**（stepwise distance）。
  - 汇总这些度量的统计特征和信号描述符（如均值、方差等），形成一个视频级特征向量。
  - 训练一个轻量级分类器（如逻辑回归或小MLP）区分真实与生成视频。
- **算法流程（文字说明）**：
  1. 输入视频 → 均匀采样帧序列。
  2. 每帧通过DINOv2提取特征向量 → 得到时间特征轨迹。
  3. 计算轨迹上每连续三点的曲率，以及相邻帧的欧氏距离。
  4. 对曲率和距离序列提取统计量（均值、标准差、偏度、峰度等）和信号处理特征（如频谱熵）。
  5. 将上述特征拼接，输入分类器进行二分类。

## 3. 实验设计
- **数据集/场景**：主要基准为 **VidProM** 数据集（包含真实和多种AI生成视频），此外还可能涉及其他生成方法（如扩散模型、GAN等）构建的检测场景。
- **基准（Benchmark）**：VidProM上的准确率（Accuracy）和AUROC作为主要指标。
- **对比方法**：与现有的**基于图像的方法**和**基于视频的方法**进行比较（未列出具体方法名，但声称显著优于两者）。
- **实验结果**：在VidProM上达到 **97.17% 准确率** 和 **98.63% AUROC**，为当前最优（state-of-the-art）。

## 4. 资源与算力
- **未明确说明**：论文摘要未提及训练所用的GPU型号、数量、训练时长等具体算力信息。仅声称方法计算高效（computationally efficient），但缺乏量化细节。

## 5. 实验数量与充分性
- **实验数量**：主要报告了VidProM一个基准上的性能，未提及在其他数据集（如FaceForensics、DFDC等）上的跨域泛化测试。也未明确描述消融实验（如不同特征组合、不同曲率定义的影响）。
- **充分性**：实验覆盖有限，缺少对多种生成方法、不同分辨率、不同内容类型的广泛验证。未与最新检测方法（如基于视频Transformer的检测器）进行公平比较（未列出基线细节）。因此，实验充分性存在不足。

## 6. 论文的主要结论与发现
- AI生成视频在DINOv2表示空间中表现出显著不同的曲率和步长距离模式，偏离了自然视频的“直线化”几何属性。
- 基于这一几何偏差，即使使用轻量级分类器也能达到高检测性能，表明感知直线化是一种可解释且通用的视频伪造检测线索。

## 7. 优点：方法或实验设计上的亮点
- **创新性强**：将认知科学假设（感知直线化）引入视频伪造检测，提供了全新的可解释视角。
- **泛化潜力**：基于通用几何属性，理论上对不同生成方法具有更好的泛化能力（实验结果支持）。
- **计算高效**：使用预训练模型+简单统计特征+轻量分类器，推理成本低。
- **可解释性**：曲率和距离模式可直接可视化，解释为何判定为生成视频。

## 8. 不足与局限
- **实验验证不足**：仅在单一基准VidProM上报道结果，缺少跨数据集、跨生成器、跨实时域（如摄像头拍摄 vs 高质生成）的泛化测试。
- **未与最强基线全面比较**：未列出对比方法的具体名称和来源，无法判断比较是否公平。
- **消融分析缺失**：未系统地评估各特征成分（曲率 vs 距离 vs 统计量 vs 信号特征）的贡献。
- **资源消耗不透明**：未提供训练和推理的硬件、时间信息，难以评估实际部署成本。
- **依赖固定预训练模型**：DINOv2的特征质量可能影响方法在极端数据或未来新型生成器上的鲁棒性。
- **对短时或单帧视频的适用性未讨论**：时间曲率计算需要足够帧数，可能不适用于极短视频。

（完）
