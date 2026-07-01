---
title: Breaking Latent Prior Bias in Detectors for Generalizable AIGC Image Detection
title_zh: 打破检测器中潜在先验偏差以实现可泛化的AIGC图像检测
authors: "Yue Zhou, Xinan He, Kaiqing Lin, Bing Fan, Feng Ding, Bin Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=sVSVgWIkb0"
tags: ["query:xai-objdet"]
score: 4.0
evidence: AIGC图像检测，分析潜在先验偏差，与伪造检测相关
tldr: 针对AIGC图像检测器对未见生成器泛化差的问题，发现潜在先验偏差是重要原因。提出流形对抗训练，通过在扩散模型的初始潜在噪声上优化生成流形上的对抗样本，迫使检测器学习鲁棒的人工痕迹特征。实验证明该方法显著提升了对未知生成器的检测泛化能力，为伪造检测可解释性提供了新视角。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有AIGC检测器对未见生成器的图像泛化能力差，根源在于潜在先验偏差。
method: 提出流形对抗训练，优化扩散模型初始噪声生成流形上对抗样本，迫使检测器关注鲁棒特征。
result: 在多个生成器上验证，该方法有效提升了检测泛化性能。
conclusion: 揭示了潜在先验偏差对伪造检测的影响，为解决泛化问题提供了有效方案。
---

## Abstract
Current AIGC detectors often achieve near-perfect accuracy on images produced by the same generator used for training but struggle to generalize to outputs from unseen generators. We trace this failure in part to latent prior bias: detectors learn shortcuts tied to patterns stemming from the initial noise vector rather than learning robust generative artifacts. To address this, we propose \textbf{On-Manifold Adversarial Training (OMAT)}: by optimizing the initial latent noise of diffusion models under fixed conditioning, we generate \emph{on-manifold} adversarial examples that remain on the generator’s output manifold—unlike pixel-space attacks, which introduce off-manifold perturbations that the generator itself cannot reproduce and that can obscure the true discriminative artifacts. To test against state-of-the-art generative models, we introduce GenImage++, a test-only benchmark of outputs from advanced generators (Flux.1, SD3) with extended prompts and diverse styles. We apply our adversarial-training paradigm to ResNet50 and CLIP baselines and evaluate across existing AIGC forensic benchmarks and recent challenge datasets. Extensive experiments show that adversarially trained detectors significantly improve cross-generator performance without any network redesign. Our findings on latent-prior bias offer valuable insights for future dataset construction and detector evaluation, guiding the development of more robust and generalizable AIGC forensic methodologies.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：当前AIGC图像检测器在训练集生成器上表现近乎完美，但对未见过的生成器（如新型扩散模型）输出的图像泛化能力很差。
- **归因**：论文发现这一失败部分源于“潜在先验偏差”（latent prior bias）——检测器学习到与初始噪声向量模式相关的捷径（shortcut），而非鲁棒的人工痕迹特征。
- **研究动机**：揭示泛化失败的根本原因，并设计一种不改变网络结构就能提升跨生成器泛化能力的方法，为AIGC取证的可解释性和鲁棒性提供新视角。

## 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：通过在生成器的**输出流形（on-manifold）** 上构造对抗样本进行训练，迫使检测器关注真正与生成过程相关的鲁棒特征，而不是易受潜在先验偏差影响的伪特征。
- **关键技术细节**：
  - **On-Manifold Adversarial Training (OMAT)**：固定扩散模型的条件输入，**优化初始潜在噪声向量**，使得生成的图像在保持生成流形不变的前提下，对检测器产生最大攻击效果。
  - 与传统的像素空间对抗攻击不同：像素空间扰动会导致生成器无法再现的“off-manifold”失真，反而可能掩盖真正的判别性痕迹；而OMAT通过调整潜在噪声，使对抗样本仍位于生成流形上。
  - 使用对抗训练范式（adversarial training）将OMAT产生的样本加入训练数据，提升检测器的鲁棒性。
- **公式/算法流程**（文字说明）：
  1. 输入：预训练的扩散生成器G（固定条件c），初始潜在噪声z，检测器D。
  2. 构造对抗目标：最大化检测器对G(z,c)的错误分类损失，同时约束z在允许范围内（通常用小幅度扰动）。
  3. 通过梯度反向传播更新z，得到优化的z*。
  4. 用G生成图像x* = G(z*, c)，作为对抗样本。
  5. 将x*加入训练集，重新训练检测器（或微调）。

## 3. 实验设计
- **数据集/场景**：
  - 提出**GenImage++** 测试专用基准，包含先进生成器（Flux.1, SD3）的输出，使用扩展提示和多样风格。
  - 采用已有的AIGC取证benchmark（原文未明确列出具体名称，但提及“existing AIGC forensic benchmarks”和“recent challenge datasets”）。
- **基准模型**：ResNet50和CLIP作为基线检测器。
- **对比方法**：主要为标准训练（无对抗训练）的检测器 vs. 经过OMAT对抗训练的检测器。未提及与其他对抗训练方法的对比（如PGD对抗训练），但强调了与像素空间攻击的对比（概念性）。
- **评估指标**：跨生成器泛化性能（准确率等），但具体数字未在摘要中给出。

## 4. 资源与算力
- **文中未明确说明**：未提及使用的GPU型号、数量、训练时长等算力信息。仅描述方法本身，不涉及资源开销。

## 5. 实验数量与充分性
- **实验组数**：摘要提到“extensive experiments”，包含多个生成器、两个基线模型、多个benchmark。但没有具体列出消融实验或变体数量。
- **充分性评价**：
  - 优点：覆盖了从经典到最新的生成器（包括Flux.1, SD3），并设计了专门测试集GenImage++，增强了泛化评估的难度。
  - 不足：未提供详细的消融实验（如对抗强度、潜在噪声扰动范围的影响）、未与现有的其他泛化增强方法（如数据增强、域适应）对比。实验统计显著性未说明。

## 6. 主要结论与发现
- OMAT对抗训练显著提高了检测器对未见生成器的泛化性能，且无需改变网络架构。
- 潜在先验偏差是导致泛化失败的重要原因，解释了为什么检测器在训练生成器上“过拟合”。
- 在流形上生成对抗样本比在像素空间更有效，能避免引入不可靠的虚假特征。
- 该发现对未来的数据集构建和检测器评估具有指导意义。

## 7. 优点
- **思想创新**：首次从潜在先验偏差角度解释AIGC检测泛化问题，并引入流形对抗训练解决。
- **方法简洁有效**：无需重新设计网络，仅通过训练数据增强就实现跨生成器泛化提升。
- **实验基准新颖**：推出GenImage++测试集，覆盖当前最先进生成器，对社区有贡献。
- **可解释性贡献**：揭示了检测器学习捷径的现象，为伪造检测的鲁棒性提供了新的分析视角。

## 8. 不足与局限
- **实验覆盖不足**：
  - 仅验证了ResNet50和CLIP两种基线，未测试更多检测架构（如ViT、基于频率的检测器）。
  - 生成的对抗样本依赖于扩散模型的潜在空间，对于其他生成模型（如GAN）是否适用未讨论。
- **偏差风险**：
  - 潜在先验偏差主要存在于基于噪声初始化的生成模型（扩散模型），对于无噪声输入的生成器（如某些GAN）可能不显著。
  - 对抗训练可能降低检测器在训练生成器上的精度（未报告）。
- **应用限制**：
  - OMAT需要访问生成器的反向传播梯度，在实际黑盒场景下不可行；也假设了训练时能获取生成器模型，可能不适用于未知、闭源生成器。
  - 未考虑对抗样本的多样性和视觉质量，可能产生不易察觉但语义改变的图像。
- **资源与复现**：未提供代码、超参数、训练细节，可复现性需验证。

（完）
