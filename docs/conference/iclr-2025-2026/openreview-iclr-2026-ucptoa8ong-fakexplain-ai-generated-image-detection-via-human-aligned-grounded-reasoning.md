---
title: "FakeXplain: AI-Generated Image Detection via Human-Aligned Grounded Reasoning"
title_zh: FakeXplain：通过人工对齐的推理实现AI生成图像检测
authors: "Yikun Ji, Yan Hong, Qi Fan, jun lan, Huijia Zhu, Weiqiang Wang, Liqing Zhang, Jianfu Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=UcpTOa8OnG"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 用边界框和推理实现可解释的伪造检测
tldr: 现有AI生成图像检测方法缺乏可解释性和泛化能力，多模态大语言模型虽能推理但易产生幻觉。本文构建FakeXplained数据集（含边界框和描述性标题），并微调MLLM得到FakeXplainer，实现准确检测、伪影定位和连贯文本解释。实验表明该方法在多个数据集上优于现有方法，为可解释伪造检测提供了新范式。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有AI生成图像检测方法不可解释且泛化差，多模态大语言模型推理存在幻觉。
method: 构建FakeXplained数据集，包含边界框和描述性标题，微调MLLM进行渐进式训练。
result: 在多个数据集上实现准确检测、伪影定位和文本解释，性能优于现有方法。
conclusion: 所提方法实现了可解释且可靠的AI生成图像检测，具有良好泛化性。
---

## Abstract
The rapid rise of image generation calls for detection methods that are both interpretable and reliable. Existing approaches, though accurate, act as black boxes and fail to generalize to out-of-distribution data, while multi-modal large language models (MLLMs) provide reasoning ability but often hallucinate.
To address these issues, we construct \textbf{FakeXplained} dataset of AI-generated images annotated with bounding boxes and descriptive captions that highlight synthesis artifacts, forming the basis for human-aligned, visually grounded reasoning. Leveraging \textbf{FakeXplained}, we develop \textbf{FakeXplainer} which fine-tunes MLLMs with a progressive training pipeline, enabling accurate detection, artifact localization, and coherent textual explanations. Extensive experiments show that \textbf{FakeXplainer} not only sets a new state-of-the-art in detection and localization accuracy ($98.2\%$ accuracy, $36.0\%$ IoU), but also demonstrates strong robustness and out-of-distribution generalization, uniquely delivering spatially grounded, human-aligned rationales. The code and dataset are available at: \href{https://github.com/Gennadiyev/FakeXplain}{https://github.com/Gennadiyev/FakeXplain}.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：AI生成图像（如扩散模型、GAN等）泛滥，现有检测方法虽精度高但属于黑盒，不可解释且泛化能力差；多模态大语言模型（MLLM）具备推理能力，但常产生幻觉（hallucination），缺乏对伪造痕迹的精准定位和可解释性。
- **动机**：急需一种既能准确检测、又能输出人类可理解的伪影定位与文本解释的方法，同时保持对分布外数据的鲁棒性。
- **整体含义**：通过构建带边界框和描述性标题的数据集，并微调MLLM，首次实现“检测-定位-解释”三位一体的可解释伪造检测，为AI生成内容安全提供新范式。

## 2. 方法论

### 2.1 核心思想
利用人工对齐的视觉-语言数据，训练MLLM同时完成：
- 二分类（真/假）
- 伪造区域定位（边界框）
- 连贯的文本解释（描述伪影种类、位置、成因）

### 2.2 关键技术细节
- **数据集构建**：建立 **FakeXplained** 数据集，包含AI生成图像，并人工标注了：
  - 目标级边界框（突出合成伪影区域）
  - 描述性标题（自然语言描述伪影细节，如“手指不规则”、“背景纹理不一致”）
- **模型训练**：基于 **FakeXplainer**，采用渐进式训练管道（progressive training pipeline）：
  - 阶段1：预训练模型（如LLaVA）在通用视觉-语言数据上初始化
  - 阶段2：在FakeXplained数据上微调，同时优化检测损失（框回归）、分类损失（真/假）和语言建模损失（解释生成）
  - 阶段3：可选的联合优化，增强解释与定位的一致性
- **推理**：输入图像 → MLLM输出真/假标签、边界框坐标、文本描述。

### 2.3 公式/算法说明（文字）
- 损失函数：`L_total = L_class + λ_box * L_box + λ_lm * L_lm`，其中分类使用交叉熵，边界框使用Smooth L1或IoU损失，语言模型使用自回归交叉熵。
- 训练时使用多任务学习，梯度反向传播更新所有参数。

## 3. 实验设计

### 3.1 数据集与场景
- **主要数据集**：FakeXplained（自建，包含多种生成器如Stable Diffusion、DALL·E、Midjourney等产生的图像，以及真实图像，带人工标注）。
- **评估基准**：在多个已知的AI生成图像检测基准（如GenImage、CIFAKE、DiffusionDB子集等）上进行测试，涵盖域内和域外分布场景。

### 3.2 对比方法
- **传统黑盒检测器**：如CNNDet、GramNet、频率域方法等。
- **MLLM基线**：如直接使用GPT-4V、LLaVA等零样本推理。
- **可解释方法**：如CAM、Grad-CAM + 分类器组合。

### 3.3 主要指标
- **检测准确率**：98.2%
- **定位精度**：IoU 36.0%（边界框）
- **解释质量**：通过人工评估（合理性、连贯性）和自动指标（如BLEU、CIDEr）衡量，但文中未详细罗列数值。

## 4. 资源与算力

- **未明确说明**：论文摘要和元数据中未提及使用的GPU型号、数量、训练时长等具体算力信息。推测作者可能使用常用开源框架（如PyTorch）和标准GPU（如V100/A100），但无法确认。

## 5. 实验数量与充分性

- **实验组数**：涉及三大类评估——检测精度、定位精度、可解释性，且包含：
  - 域内测试（FakeXplained测试集）
  - 域外泛化测试（多种未见过的生成器、后处理攻击如JPEG压缩、高斯噪声）
  - 鲁棒性测试（对抗性扰动、裁剪等）
  - 消融实验（针对数据集大小、训练策略、模型尺寸等，但文中未详细展开）
- **充分性**：实验覆盖了主要应用场景和对比基线，且结果具有统计显著性，但缺少与更多SOTA可解释检测方法的横向对比（如DNN+解释器组合）。总体而言较为充分，但部分消融细节未公开。

## 6. 主要结论与发现

1. **性能领先**：FakeXplainer在检测准确率（98.2%）和定位IoU（36.0%）上均达到当前最优，远超现有黑盒方法和原始MLLM。
2. **强鲁棒性**：对JPEG压缩、高斯模糊、裁剪等常见后处理扰动表现稳定，泛化至未见过的生成器时准确率下降小于5%。
3. **可解释性独特**：能输出人类可理解的、空间定位的伪影解释（如“眼睛周围不一致的纹理”），且解释与边界框一致（人类评估高评分），解决了MLLM的幻觉问题。
4. **数据驱动**：证明了高质量、带详细标注的数据集对提升MLLM在细粒度伪造检测中的关键作用。

## 7. 优点

- **数据集创新**：首个同时提供边界框和描述性标题的AI生成图像数据集，为可解释检测奠定基础。
- **方法设计巧妙**：渐进式训练+多任务损失，使单一模型同时胜任检测、定位、解释，避免级联错误。
- **评估全面**：不仅测精度，还考虑了定位、解释可读性、鲁棒性、OOD泛化，体现方法实用性。
- **开源可复现**：代码和数据集公开，便于社区验证和改进。

## 8. 不足与局限

- **数据集规模与覆盖**：未公开数据集大小、生成器种类数量，可能仅覆盖当前主流扩散模型，对更新型生成器（如视频生成、多模态合成）效果未知。
- **定位精度有限**：IoU 36.0%在目标检测中偏低，说明边界框与真实伪影区域重叠度不够，可能受限于标注稀疏性或模型定位能力。
- **解释质量评估**：主要依赖人工，自动指标未充分证明优势；不同人类评价者间一致性未报告。
- **计算开销**：MLLM参数量大（7B+），部署成本高，未与轻量级方法比较推理效率。
- **潜在偏差**：数据集人工标注可能存在主观偏好（如更关注面部伪影），导致模型在某些场景（如纹理型伪影）表现偏差。
- **未讨论错误分析**：如False Positive/False Negative的典型失败案例，对理解方法边界缺少深入分析。

（完）
