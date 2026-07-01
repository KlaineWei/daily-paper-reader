---
title: Identity-Aware Vision-Language Model for Explainable Face Forgery Detection
title_zh: 身份感知视觉语言模型用于可解释人脸伪造检测
authors: "Junhao Xu, Jingjing Chen, Yang Jiao, Jiacheng Zhang, Zhiyu Tan, Hao Li, Yu-Gang Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38108/42070"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 基于身份感知VLM的可解释人脸伪造检测
tldr: 针对现有伪造检测方法依赖低级视觉线索且难以检测新手法的问题，提出身份感知VLM用于可解释人脸伪造检测，通过捕捉语义不一致实现可解释性。实验在多个基准上验证了其可解释性和泛化能力。该方法为图像伪造检测提供了身份层面的可解释分析。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38108/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 828, \"height\": 681, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38108/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1187, \"height\": 645, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38108/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 945, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 777, \"height\": 684, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 887, \"height\": 527, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 761, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 721, \"height\": 515, \"label\": \"Table\"}]"
motivation: 现有伪造检测方法难以检测语义不一致且依赖低级视觉线索，缺乏可解释性。
method: 设计个性化视觉语言模型，结合身份信息进行语义一致性分析以实现可解释伪造检测。
result: 在伪造检测基准上取得优异性能，并提供可解释的检测依据。
conclusion: 身份感知VLM增强了伪造检测的可解释性和对新手法的泛化能力。
---

## Abstract
Recent advances in generative artificial intelligence have enabled the creation of highly realistic image forgeries, raising significant concerns about digital media authenticity. While existing detection methods demonstrate promising results on benchmark datasets, they face critical limitations in real-world applications. First, existing detectors typically fail to detect semantic inconsistencies with the person’s identity, such as implausible behaviors or incompatible environmental contexts in given images. Second, these methods rely heavily on low-level visual cues, making them effective for known forgeries but less reliable against new or unseen manipulation techniques. To address these challenges, we present a novel personalized vision-language model (VLM) that integrates low-level visual artifact analysis and high-level semantic inconsistency detection. Unlike previous VLM-based methods, our approach avoids resource-intensive supervised fine-tuning that often struggles to preserve distinct identity characteristics. Instead, we employ a lightweight method that dynamically encodes identity-specific information into specialized identifier tokens. This design enables the model to learn distinct identity characteristics while maintaining robust generalization capabilities. We further enhance detection capabilities through a lightweight detection adapter that extracts fine-grained information from shallow features of the vision encoder, preserving critical low-level evidence. Comprehensive experiments demonstrate that our approach achieves 94.25% accuracy and 94.08% F1 score, outperforming both traditional forgery detectors and general VLMs while requiring only 10 extra tokens.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

近年来，生成式人工智能（尤其是GAN和扩散模型）能够生成高度逼真的伪造人脸图像，对数字媒体真实性构成严重威胁。现有检测方法存在三个关键局限：
- **缺乏身份级语义检测**：无法识别与个人身份相矛盾的高层语义不一致（如不合理的行为、不兼容的服装或环境）。
- **过度依赖低级视觉线索**：对已知伪造方法有效，但对未知新手法（如扩散模型生成的图像）泛化能力差。
- **可解释性不足**：传统检测器是黑盒系统，不提供检测理由。

因此，论文提出一个**身份感知的视觉语言模型（VLM）**，融合低级视觉伪影分析和高级语义不一致检测，同时提供可解释的伪造检测理由。

## 2. 论文提出的方法论

### 核心思想
通过轻量级方法将身份先验信息编码为专用的标识符令牌（identifier tokens），使VLM能够识别与身份不一致的元素（如外观、行为），而无需进行资源密集型的全模型微调。

### 关键技术细节
- **个性化身份先验注入**：
  - 定义两个专用令牌：`<id_a>`（外观先验）和`<id_b>`（行为先验），每个令牌对应N个可学习的软令牌（论文中N=4，总共10个令牌）。
  - 使用少量真实参考图像训练这些令牌，使模型学习目标的身份特征（外观识别和行为识别任务）。
- **检测适配器（Detection Adapter）**：
  - 从视觉编码器的浅层提取特征，通过投影层生成视觉令牌，保留低级伪影信息（如压缩痕迹、噪声模式）。
  - 与标准视觉令牌拼接后输入语言模型，实现多级特征融合。
- **训练策略**：
  - 第一阶段：训练检测适配器（无需身份信息），使用二元分类任务（Yes/No）学习通用伪造检测。
  - 第二阶段：个性化先验训练，使用真实图像和高质量伪造图像（含扩散模型和GAN生成）训练身份令牌，包括外观识别和行为识别两个目标。

### 公式说明
- 身份先验参数：`θprior = {<id_a>, <id_b>, {<token_a/b_i>}, W_new}`。
- 检测适配器：`Tadapter = Proj(F_shallow)`，`T_integrated = [T_standard; Tadapter]`。
- 训练损失：`L_adapter = CrossEntropy(VLM(T_standard; Tadapter), y)`；`L_personalization = L_appearance + L_behavior`。

## 3. 实验设计

### 数据集
- 论文自建数据集 **IDImage**：包含20位公众人物（政治、娱乐），每人约329张真实图像。伪造图像使用5种方法生成：
  - 训练集：SimSwap（GAN）、PhotoMaker（扩散模型）。
  - 测试集：Roop（GAN）、StoryMaker（扩散模型）、PuLID（扩散模型），与训练集方法完全不同，用于评估泛化能力。
  - 训练集每人约279张真实、780张伪造；测试集每人约50张真实、50张伪造。

### 基准方法
- **传统伪造检测器**：Meso4、Xception、Recce、UCF、RAIRNet、R-MFDN、NPR、ESSP。
- **通用VLM**：GPT-4o、Qwen2.5-VL、LLaVA-1.6-13B。
- **微调的VLM**：FFAA、Yo’LLaVA、LLaVA（SFT）。

### 评估指标
准确率（ACC）、精确率（Precision）、召回率（Recall）、F1分数。

## 4. 资源与算力

论文明确说明：
- 基座模型：LLaVA-1.6-13B。
- 训练硬件：2块NVIDIA A100 GPU。
- 训练时长：每个身份约20分钟，仅训练1个epoch。
- 额外参数量：仅10个令牌。
- 数据需求：每个身份约100张图像即可有效（0.5 GPU小时训练10个令牌）。

## 5. 实验数量与充分性

论文进行了多组实验，较为充分：
- **主对比实验**：在IDImage测试集上对比13种基线方法（见表1）。
- **个性化VLM对比**：与GPT-4o、Qwen2.5-VL、LLaVA在不同方式注入身份信息（文本描述、参考图像、两者结合）下对比（见表2）。
- **消融实验**：
  - 去除检测适配器。
  - 仅使用外观令牌或行为令牌。
  - 使用统一令牌而非解耦令牌。
  - 去掉思维链（CoT）训练。
- **训练数据规模影响**：从5%到100%逐步增加数据量（见表4）。
- **鲁棒性测试**：JPEG压缩（质量因子25）和Gaussian模糊（核21×21，sigma=8.0）下的性能（见表5）。

这些实验基本覆盖了方法各个模块的贡献，对比方法多样，且测试集与训练集伪造方法不同，评估公平且具有挑战性。

## 6. 论文的主要结论与发现

- 所提方法在IDImage测试集上达到**94.25%准确率、94.08% F1分数**，显著优于所有基线，包括传统检测器（最佳ESSP：89.08%准确率）和通用VLM（最佳GPT-4o：83.03%准确率）。
- 个性化身份先验注入显著提升召回率，但可能降低精确率；所提方法通过解耦外观/行为令牌和检测适配器平衡了性能。
- 仅需10个额外令牌即可实现高效身份感知，训练新身份仅需约0.5 GPU小时。
- 检测适配器对保留低级视觉线索至关重要，去除后精确率下降（96.56%→76.56%）。
- 解耦的表征（外观+行为）优于统一令牌。
- 链式推理训练有助于学习更有效的特征。

## 7. 优点

- **创新性**：首次将VLM个性化技术（如DreamBooth、Textual Inversion）引入人脸伪造检测，通过身份先验实现高层语义不一致检测。
- **可解释性**：生成自然语言解释，提供检测依据（如“发型与身份不符”），超越传统黑盒检测器。
- **轻量高效**：仅10个额外令牌，无需全模型微调，训练速度快（20分钟/身份），数据需求低（~100张真实图像）。
- **强泛化能力**：在训练与测试伪造方法不同的情况下仍保持高性能，对JPEG压缩和高斯模糊鲁棒。
- **实验设计严谨**：构建专用数据集，测试集伪造方法完全不同于训练集，公平评估泛化能力。

## 8. 不足与局限

- **数据集规模有限**：仅20个身份，且均为英语公众人物，可能存在文化/语言偏差；未能涵盖更广泛的身份类型。
- **伪造方法覆盖不全**：训练集只用了2种方法，测试集3种方法，现实中的伪造技术迭代迅速，需要持续扩展。
- **计算资源**：虽轻量，但依赖2张A100 GPU，普通研究者可能难以复现。
- **未探讨多身份交互**：论文假设每次检测针对单一已知身份，实际场景可能涉及未知身份或多人图像，方法需扩展。
- **可解释性质量未量化**：论文仅提供分类指标，未评估生成解释的准确性、完整性和人类可理解性。
- **消融实验仅针对一个测试集**：缺乏在多个公开基准（如FaceForensics++、DFDC等）上的验证，可能削弱结论的普适性。

（完）
