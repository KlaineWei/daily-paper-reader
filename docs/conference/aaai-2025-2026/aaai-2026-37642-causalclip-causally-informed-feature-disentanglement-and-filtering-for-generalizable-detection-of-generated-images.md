---
title: "CausalCLIP: Causally-Informed Feature Disentanglement and Filtering for Generalizable Detection of Generated Images"
title_zh: CausalCLIP：因果引导的特征解耦与过滤用于生成图像的泛化检测
authors: "Bo Liu, Qiao Qin, Qinghui He"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37642/41604"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 因果特征解耦用于生成图像检测，提供可解释的线索
tldr: 该论文针对生成图像检测中特征混杂导致泛化性差的问题，提出CausalCLIP框架。通过因果推断原则显式解耦因果特征与伪相关特征，并采用目标过滤保留可迁移的鉴别性线索。方法在多个生成技术数据集上展现出强泛化能力，且因果特征提供了可解释的取证依据。这直接支持了可解释伪造检测的需求。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37642/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 843, \"height\": 642, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37642/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1750, \"height\": 778, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37642/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37642/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 828, \"height\": 718, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37642/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1809, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37642/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1810, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37642/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1818, \"height\": 591, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37642/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1800, \"height\": 593, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37642/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 366, \"label\": \"Table\"}]"
motivation: 现有方法特征纠缠，混杂伪相关模式限制泛化。
method: 利用因果推断解耦因果与非因果特征，并过滤保留可迁移线索。
result: 在多种生成技术下检测泛化性显著提升。
conclusion: 提供可解释的伪造检测方案。
---

## Abstract
The rapid advancement of generative models has increased the demand for generated image detectors capable of generalizing across diverse and evolving generation techniques. However, existing methods, including those leveraging pre-trained vision-language models, often produce highly entangled representations, mixing task-relevant forensic cues (causal features) with spurious or irrelevant patterns (non-causal features), thus limiting generalization. To address this issue, we propose CausalCLIP, a framework that explicitly disentangles causal from non-causal features and employs targeted filtering guided by causal inference principles to retain only the most transferable and discriminative forensic cues. By modeling the generation process with a structural causal model and enforcing statistical independence through Gumbel-Softmax-based feature masking and Hilbert-Schmidt Independence Criterion (HSIC) constraints, CausalCLIP isolates stable causal features robust to distribution shifts. When tested on unseen generative models from different series, CausalCLIP demonstrates strong generalization ability, achieving improvements of 6.83% in accuracy and 4.06% in average precision over state-of-the-art methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究问题**：生成图像检测器在面对未见过的生成模型（GAN、扩散模型等）时泛化能力差。现有方法（包括基于预训练视觉-语言模型如CLIP的方法）提取的特征高度纠缠，将任务相关的因果取证线索（如生成痕迹）与伪相关或无关模式（如数据集风格、压缩伪影）混合在一起，导致模型过拟合于训练分布下的非因果特征，在分布偏移时性能严重下降。
- **研究动机**：作者认为，要实现跨生成模型的强泛化，必须显式地将稳定的因果特征与虚假的非因果特征分离开来，而不是仅在纠缠空间中粗粒度地抑制无关特征。
- **整体含义**：提出CausalCLIP框架，通过因果推理原则指导特征解耦与过滤，仅保留可迁移、可判别的取证线索，从而提升检测器对多种生成技术的泛化能力。

## 2. 方法论

### 核心思想
- **“解耦-过滤”范式**：首先将CLIP提取的语义特征通过因式分解模块（Factorization Module）解耦为因果特征（causal features）和非因果特征（non-causal features），然后通过对抗掩蔽模块（Adversarial Masking Module）进一步压制非因果特征，迫使分类器仅依赖稳定的因果子空间进行决策。
- **理论基础**：利用结构因果模型（SCM）假设生成过程，其中因果特征源自与生成无关的内容因子，非因果特征源自生成器特定的风格/伪影因子，两者独立。目标是从纠缠特征中恢复因果特征。

### 关键技术细节
1. **因式分解模块**：
   - 输入CLIP嵌入 \(E\)，通过Gumbel-Softmax参数化的特征掩码 \(M\) 将特征分为：
     \[ \tilde{Z}_c = M \odot E, \quad \tilde{Z}_{nc} = (1-M) \odot E \]
   - 掩码由MLP + Gumbel噪声 + softmax生成，温度参数控制稀疏性，实现可微特征选择。
2. **对抗掩蔽模块**：
   - 设置一个最小-最大博弈：分类器 \(h\) 从\(\tilde{Z}_c\)预测真/假，对手 \(d\) 从\(\tilde{Z}_{nc}\)预测真/假。
   - 优化目标：最小化分类损失的同时最大化对手的预测损失，使\(\tilde{Z}_{nc}\)变得对任务无信息。
   - 额外引入掩码正则项：\(\ell_1\)稀疏项 + Hilbert-Schmidt独立性准则（HSIC）惩罚，强制因果与非因果特征统计独立。
3. **反事实干预**：
   - 对因果特征进行随机掩码（Bernoulli采样）得到\(\tilde{Z}^{CF}_c\)，要求分类器保持预测一致性（KL散度约束），增强对分布扰动的鲁棒性。
4. **总体损失函数**：
   \[ L_{total} = L_{cls} - \alpha L_{adv} + L_{mask} + \beta L_{inv} \]
   其中\(L_{cls}\)为交叉熵分类损失，\(L_{adv}\)为对抗损失，\(L_{mask}\)包含\(\ell_1\)和HSIC，\(L_{inv}\)为反事实一致性损失，\(\alpha,\beta\)为平衡系数。训练时交替优化分类器、对手和掩码。

## 3. 实验设计

### 数据集与场景
- **训练集**：
  - ProGAN（来自CNNDet，36万张真实+36万张生成）
  - Stable Diffusion v1.4（来自GenImage，3.2万对真实-生成）
- **测试集**：15个生成模型，涵盖GAN系列（ProGAN, CycleGAN, StarGAN, StyleGAN, BigGAN, GauGAN, Deepfake, SAN）和扩散系列（SD1.4, SD1.5, ADM, GLIDE, Midjourney, Wukong, VQDM）。真实图像来自ImageNet, LSUN, FaceForensics++, CelebA-HQ, CelebA, COCO。
- **评价指标**：平均精度（AP）和准确率（ACC）。
- **baselines**：CNNSpot, FreDect, Fusing, LGrad, DIRE, UnivFD, NPR, CLIPping, VIB-Net等9种SOTA方法。
- **实验设置**：
  1. **扩散源训练**：在SDv1.4上训练，测试全部15个模型。
  2. **GAN源训练**：在ProGAN上训练，测试全部15个模型。
- **额外分析**：特征可视化（UMAP）、鲁棒性测试（JPEG压缩、高斯模糊）、消融实验。

## 4. 资源与算力

- 文中明确说明：所有实验在 **NVIDIA Tesla V100 GPU** 上使用PyTorch实现。
- **未提及**：GPU数量、训练时长、显存消耗。因此无法给出具体算力统计，但可以推测为单卡或有限数量GPU。

## 5. 实验数量与充分性

- **实验组数**：
  - 2个主要训练-测试迁移场景（扩散源、GAN源），每个场景报告了15个测试模型的AP和ACC，共30张表（表1-4）。
  - 1组消融实验（表5）：分别测试因式分解模块和掩蔽模块的贡献，共4种组合。
  - 1组特征可视化（图3）：3种方法（CLIP、VIB、Ours）在seen/unseen下的UMAP。
  - 1组鲁棒性实验（图4）：在JPEG压缩（不同质量因子）和高斯模糊（不同sigma）下对比4种方法。
- **充分性与公平性**：
  - 对比方法涵盖了从早期CNN到最新CLIP适配方法的9种SOTA，且均使用相同的训练集和测试协议。
  - 两个训练源（GAN和扩散）提供了双向迁移挑战，测试集覆盖主流生成模型。
  - 消融实验设计合理，验证了各组件的必要性。
  - 鲁棒性分析覆盖常见图像退化，具有实际意义。
- **结论**：实验设计较全面，数量充足，公平性较好。但缺少跨数据集（如不同分辨率、跨语言文本）或更复杂扰动（如对抗攻击）的评估。

## 6. 主要结论与发现

- CausalCLIP在**跨模型泛化**方面显著优于所有baselines：
  - 扩散源训练：AP提升2.32%，ACC提升4.62%；在未见过的GAN模型上提升6.83%（ACC）和4.06%（AP）。
  - GAN源训练：AP提升1.23%，ACC提升3.26%；在未见过的扩散模型上提升8.57%（ACC）和2.64%（AP）。
- 特征可视化表明：CausalCLIP在seen和unseen域均能实现清晰的真实-假特征分离，而CLIP和VIB存在严重重叠。
- 鲁棒性实验中，CausalCLIP在JPEG压缩和高斯模糊下性能最稳定。
- 消融实验证实：联合使用因式分解和对抗掩蔽模块达到最佳效果，单独使用也各有提升，两者互补。

## 7. 优点

- **创新性**：首次将因果特征解耦引入生成图像检测领域，提出“解耦-过滤”新范式，超越简单的信息瓶颈（如VIB）。
- **方法论完备**：结合结构因果模型、Gumbel-Softmax可微掩码、HSIC独立性约束、对抗学习、反事实干预，技术链条完整且可复现。
- **实验验证充分**：涵盖两大主流生成家族（GAN和扩散），双向迁移测试具有很强的说服力；消融和鲁棒性分析增强了方法的可信度。
- **代码开源可能性**：论文虽未明确提供代码链接，但实现细节清晰，便于复现。
- **泛化性突出**：在多个未见过的生成器上性能大幅领先，证明因果特征的有效性。

## 8. 不足与局限

- **实验覆盖不足**：
  - 未测试真实世界复杂场景：如低分辨率、屏幕翻拍、后处理（裁剪、缩放、水印嵌入）等。
  - 未评估对最新大型生成模型（如DALL·E 3、Sora视频生成）的泛化能力。
  - 仅关注图像级别，未扩展至视频生成检测。
- **算力信息缺失**：未给出训练时间、GPU数量、显存消耗，不利于计算资源评估。
- **潜在偏差风险**：训练数据仅使用了ProGAN和SDv1.4两种源，可能存在对这两种生成器偏好的隐式因果特征；HSIC和反事实干预的超参数（\(\alpha,\beta,\tau\)）在不同场景下是否稳定未探讨。
- **应用限制**：CLIP-ViT-L/14作为固定骨干，推理成本较高；因果掩码和对抗模块增加了模型复杂度，不适合轻量级或实时部署场景。
- **可解释性**：虽然声称因果特征可提供解释，但未展示具体哪些特征维度对应何种取证线索，缺乏定性分析。

（完）
