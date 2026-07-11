---
title: "ResProto-FD: Visual-Language Residual Prototype Sets for Generalized Face Forgery Detection"
title_zh: ResProto-FD：面向通用面部伪造检测的视觉语言残差原型集
authors: "Jiuyao Jing, Yu Zheng, Chunlei Peng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37473/41435"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 基于残差原型集的面部伪造检测，提供可解释的伪造线索
tldr: 针对伪造检测泛化性不足，提出ResProto-FD框架。通过构建残差原型集捕获多样伪造痕迹，结合视觉语言残差学习区分真假。方法在多个跨域数据集上表现优异，原型可视化增强可解释性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有伪造检测方法对未知伪造泛化差。
method: 利用残差原型集从训练中学习最有信息的伪造特征，结合视觉语言对齐。
result: 在多个伪造检测基准上取得领先的泛化性能。
conclusion: 残差原型集有效捕获伪造线索，提升泛化与可解释性。
---

## Abstract
With the rapid development of generative models, such as generative adversarial networks and diffusion models, the task of face forgery detection has emerged, aiming to identify forged faces in real-world scenarios. A key challenge for current face forgery detection models is improving generalization to unknown forgeries. To address this, we propose ResProto-FD, a framework that constructs residual prototype sets to capture diverse forgery cues and discriminative differences from real faces. Our novel perspective collects prototypes from the most informative residual features generated during training, enabling better representation of various forgery traces and real-vs-fake distinctions. First, we introduce a Visual-Language Residual Learning (VLRL) module based on the CLIP model. This module constructs residual features between image and text embeddings to capture inconsistencies between visual features and associated textual semantics. In doing so, it guides the model to attend to subtle visual forgery clues and enhances the discriminative power of image representations. Furthermore, we design a Gradient-aware Residual Prototypes (GRP) mechanism— a dynamic collection strategy that selectively stores uncertain residual features based on gradient signals to build the prototype sets. This enhances the model’s ability to generalize to unknown forgery types. Extensive experiments across various datasets and forgery methods demonstrate that ResProto-FD significantly improves generalization performance and consistently outperforms state-of-the-art methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：随着生成对抗网络（GAN）和扩散模型等生成技术的快速发展，面部伪造技术日益逼真，对隐私、身份安全和公众信任构成严重威胁。现有面部伪造检测方法在特定数据集上表现良好，但面对未知伪造类型时泛化能力严重不足。
- **核心问题**：如何提升检测模型对未见过的伪造类型（out-of-distribution）的泛化性能，尤其是在多模态视觉-语言模型（如CLIP）框架下进一步挖掘图像特征中的伪造线索。
- **整体含义**：提出一种基于“残差原型集”的新视角，通过捕捉训练过程中最具信息量的残差特征来表征真假差异，从而增强模型对未知伪造的泛化能力。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：构建残差原型集（Residual Prototype Sets），利用视觉语言残差学习（VLRL）增强图像表示对伪造线索的判别力，并在训练过程中通过梯度感知动态选择原型，推理时通过原型关联分类。
- **关键技术细节**：
  - **Visual-Language Residual Learning (VLRL)**：
    - 基于预训练CLIP模型，冻结文本编码器，微调图像编码器。
    - 计算视觉-语言残差特征：`f_res = f_train - λ * f_text`，其中λ控制语义覆盖范围。
    - 使用残差特征与类特定文本特征的相似度作为logits：`z_res = sim(f_res, f_text) * τ`。
    - 加入类先验校正的交叉熵损失和基于互信息（MI）的正则化项，构成VLRL总损失 `L_RL`。
  - **Gradient-aware Residual Prototypes (GRP)**：
    - 动态维护每个类别（真实/伪造）的固定大小原型集。
    - 对每个batch中的残差特征，计算其对类特定损失梯度的L2范数作为原型分数 `g`。
    - 真实类：取batch中所有真实残差特征的均值作为候选原型；伪造类：因多样性大，用K-means聚类为4个子簇中心作为候选原型。
    - 原型更新采用分数衰减策略：若新候选分数大于等于存储原型分数乘以衰减因子γ的dwell time次方，则替换。
    - 推理时：混合所有类别原型，对测试图像提取的特征计算余弦相似度，取前K个，softmax归一化后按类别加和得到伪造置信度。
- **公式/算法流程**：参见论文式(1)-(12)及图2、图3。核心是残差特征构建、梯度计算、聚类与更新、相似度分类。

### 3. 实验设计
- **数据集**：训练集为FaceForensics++ (FF++) 的c23压缩版本；测试集包括Celeb-DF (CDF)、DeepfakeDetection (DFD)、Deepfake Detection Challenge (DFDC) 以及包含40种伪造方法的DF40数据集（选取e4s、fsgan、inswap、simswap等）。
- **Benchmark**：帧级AUC和视频级AUC，并报告AP和EER。
- **对比方法**：
  - 传统方法：Xception, EfficientB4, Face X-ray, F3Net, FFD, SPSL, SRM, CORE, RECCE, UCF等。
  - CLIP-based方法：RepDFD, C2P-CLIP, VLFFD等。
  - 其他SOTA：FoCus, PFGDD, LSDA, DiffusionFake, Freqdebias, PCL+I2G, LipForensics, FTCN, UIA-ViT, SBI, SLADD, DCL, SeeABLE, NACO, IID, CDFA, ProDet, X2-DFD等。

### 4. 资源与算力
- **文中明确说明**：
  - GPU：2张 NVIDIA RTX 3090。
  - 软件环境：CUDA 12.4.1, PyTorch 2.5.1。
  - 学习率：5×10⁻⁷，权重衰减：1×10⁻⁶，优化器：Adam。
- **未说明**：具体训练时长（epoch数或小时数）未在文中给出。

### 5. 实验数量与充分性
- **实验数量**：三组主要实验：跨数据集帧级（表2）、视频级（表3）、DF40帧级（表4）；消融实验：模块分析（表5）、VLRL组件（表6）、GRP衰减率（表7）、K参数（图4）。
- **充分性与公平性**：
  - 对照组充分，覆盖了多种主流方法和数据集。
  - 所有方法均统一训练于FF++(c23)并测试于其他数据集，保证公平。
  - 消融实验验证了每个模块的贡献，参数敏感性分析全面。
- **客观性**：结果显著优于几乎所有对比方法（多个数据集上AUC领先），统计指标清晰。

### 6. 论文的主要结论与发现
- ResProto-FD在多个跨数据集和跨伪造类型的泛化测试中均取得最优或接近最优的AUC，大幅超过现有SOTA（如表2平均AUC 84.9% vs 第二名81.5%）。
- VLRL模块通过残差特征引导模型关注图像中未覆盖于文本语义的伪造痕迹，显著提升判别力。
- GRP模块利用梯度感知动态构建原型集，进一步提升了泛化性能，且联合使用效果最佳。
- 衰减策略γ=0.99时效果最优，验证了淘汰过时原型的必要性。
- 推理时K=64（即总原型数）得到最稳定结果。

### 7. 优点
- **方法创新**：首次将残差原型集引入面部伪造检测，结合视觉-语言对齐与动态梯度选择。
- **泛化能力强**：在多个真实世界数据集上均表现优异，尤其对未见过的伪造方法（如DF40中的e4s等）提升显著。
- **可解释性**：原型集可视为可解释的典型伪造/真实特征，有助于分析模型关注点。
- **实验设计全面**：涵盖了帧级、视频级、多种伪造类型，并与大量SOTA进行公平对比。

### 8. 不足与局限
- **训练开销大**：文中明确承认训练时需额外的反向传播计算梯度、以及batch内K-means聚类/特征平均，导致显著增加训练成本。
- **通用性局限**：仅使用CLIP ViT-B/16，未探索更大模型或其他视觉主干；文本提示固定（表1），可能无法覆盖所有伪造语义。
- **测试集覆盖**：测试集中于常见的公开数据集，未在真实动态场景或低质量/对抗样本下评估。
- **消融实验局限**：未分析文本提示数量或λ参数的影响；GRP中聚类数固定为4，未优化。
- **偏差风险**：训练仅用FF++，可能对基于GAN的伪造有偏好；对扩散模型伪造的泛化虽好，但样本有限。

（完）
