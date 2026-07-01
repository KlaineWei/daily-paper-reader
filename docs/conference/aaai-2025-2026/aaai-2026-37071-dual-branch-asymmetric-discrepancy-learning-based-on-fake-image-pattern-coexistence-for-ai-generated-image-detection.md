---
title: Dual-Branch Asymmetric Discrepancy Learning Based on Fake Image Pattern-Coexistence for AI-Generated Image Detection
title_zh: 基于伪造图像模式共存的双分支非对称差异学习用于AI生成图像检测
authors: "Chunli Song, Jie Liu, Peiyang Wang, Ying Huang, Guixuan Zhang, Zhi Zeng, Shuwu Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37071/41033"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 使用基于SHAP的定量分析实现伪造检测可解释性
tldr: 本文针对高保真AI生成图像与真实图像难以区分的问题，提出双分支非对称差异学习框架，基于模式共存假设，通过SHAP定量分析验证合成图像同时包含真实与合成模式。该方法不仅提升了检测准确率，还提供了模型决策的可解释性，是面向伪造检测的可解释方法。实验表明该方法在多个基准上表现优异。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1833, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 773, \"height\": 464, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 878, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 353, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37071/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1838, \"height\": 784, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37071/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1844, \"height\": 664, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37071/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1845, \"height\": 223, \"label\": \"Table\"}]"
motivation: AI生成图像与真实图像难以区分，传统检测方法依赖显式伪影或统一特征学习效果不佳。
method: 提出双分支非对称差异学习，利用模式共存假设，并通过SHAP进行可解释性分析。
result: 在多个数据集上验证了检测性能提升，SHAP分析揭示了决策依据。
conclusion: 方法兼顾性能与可解释性，为AI生成图像检测提供了新的解释方向。
---

## Abstract
With the rapid advancement of generative models, high-fidelity AI-generated images have become increasingly indistinguishable from real images, posing significant challenges to traditional detection methods that rely on explicit artifacts or uniform feature learning. We hypothesize that detection ambiguity originates from pattern coexistence: synthetic images simultaneously embed (a) authentic patterns inherited from real-image distributions and (b) synthetic patterns induced by generative architectures, whereas real images maintain consistent patterns. We validate this hypothesis through SHAP-based quantitative analysis, demonstrating that synthetic images inherently exhibit a dual distribution—simultaneously containing authentic patterns and synthetic traces—while real images show a unimodal distribution. Building on this insight, this paper proposes a Dual-Branch Asymmetric Discrepancy Learning (DADL) framework. The DADL leverages multi-scale feature extraction and Asymmetric Feature Discrepancy Loss to capture and amplify such pattern differences across multiple scales. Extensive experiments on three benchmarks (AIGCDetectBenchmark, GenImage, and Chameleon) show that DADL achieves state-of-the-art performance, with particular strengths in detecting high-fidelity synthetic images from diffusion models (e.g., Midjourney, SDv1.4, SDv1.5) and enhancing generalization across diverse generative paradigms. This study not only offers an effective approach for AIGI detection but also sheds light on the intrinsic properties of synthetic images, providing a new perspective for advancing AIGI forensics.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：随着生成模型（GANs、扩散模型等）的快速发展，高保真AI生成图像（AIGI）与真实图像越来越难以区分。传统检测方法依赖显式伪影或统一特征学习，当生成图像逼真度极高时，这些方法表现不佳。
- **整体含义**：作者提出“模式共存假说”（Pattern-Coexistence Hypothesis），认为合成图像同时包含继承自真实图像分布的“真实模式”和生成架构引入的“合成模式”，而真实图像则保持一致的单峰分布。这一内在双重性导致传统检测器将合成图像视为同质实体而失效。基于此，论文旨在通过放大虚假图像内部的模式不一致性来提升检测性能与泛化能力。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：利用合成图像中真实模式与合成模式共存的固有双重性，设计双分支非对称差异学习（DADL）框架，使模型对真实图像强化特征一致性，对虚假图像放大特征差异。
- **关键技术细节**：
  - **双分支特征提取器**：两个结构相同但权重独立的轻量级ResNet分支（Branch-A和Branch-B），分别从输入图像提取互补特征。
  - **非对称特征差异损失（AD Loss）**：核心公式：
    \[
    L_{AD}(z_1, z_2) = 
    \begin{cases}
    \text{dist}(z_1, z_2), & \text{若}x\text{为真实图像} \\
    \max(0, m_t - \text{dist}(z_1, z_2)), & \text{若}x\text{为虚假图像}
    \end{cases}
    \]
    其中 \(\text{dist}(z_1, z_2) = \| \frac{z_1}{\|z_1\|_2} - \frac{z_2}{\|z_2\|_2} \|_2^2\)，\(m_t\) 通过EMA动态更新（\(\beta=0.99\)，初始值0.5）。该损失使真实图像的双分支特征距离减小，虚假图像的特征距离被推大到至少与真实图像平均距离相当。
  - **多尺度差异挖掘**：在浅层纹理特征（Stage1）和深层语义特征（Stage2）上分别计算AD Loss，并引入可学习权重 \(\alpha_1, \alpha_2\)（\(\alpha_1+\alpha_2=1\)），构建总AD损失 \(L_{AD} = \alpha_1 L_{AD}(z_{1,s},z_{2,s}) + \alpha_2 L_{AD}(z_{1,d},z_{2,d})\)。
  - **联合优化**：最终损失 \(L = L_{CE} + \lambda L_{AD}\)（\(\lambda=0.5\)）。特征表示采用双分支深层特征的差向量 \(z_{diff} = z_{1,d} - z_{2,d}\)，送入分类器进行二分类（真实/虚假）。
- **测试阶段**：根据输入图像的双分支特征距离大小判定：距离小（一致性）→真实，距离大（不一致性）→虚假。

### 3. 实验设计
- **数据集与基准**：
  1. **AIGCDetectBenchmark**：含ProGAN、StyleGAN、BigGAN、CycleGAN、StarGAN、GauGAN、StyleGAN2、WFIR、ADM、Glide、Midjourney、SDv1.4、SDv1.5、VQDM、Wukong、DALL-E2等16种生成模型图像。
  2. **GenImage**：训练于SDv1.4（ImageNet真实+SDv1.4虚假），测试Midjourney、SDv1.4、SDv1.5、ADM、GLIDE、Wukong、VQDM、BigGAN。
  3. **Chameleon**：三个训练场景（ProGAN、SDv1.4、All GenImage），测试跨生成器泛化。
- **对比方法**：包括CNNSpot、FreDect、Fusing、GramNet、LNP、LGrad、DIRE、UnivFD、PatchCraft、NPR、AIDE、SAFE、Effort、AIGI-Holmes等14种以上SOTA方法。
- **评价指标**：分类准确率（Acc）和平均精度（AP），并报告每个测试集的平均指标ACC_M和AP_M。

### 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量及训练时长。仅提及训练参数：使用AdamW优化器，训练100个epoch，batch size为32，学习率5×10⁻³，权重衰减0.01。模型基于轻量级ResNet（类似SAFE）构建，计算资源需求相对较低。

### 5. 实验数量与充分性
- **实验组数**：共计三大基准实验（每基准含多个子场景），以及一项消融研究（多尺度AD Loss、超参数λ敏感性分析）。
- **充分性**：实验覆盖了多种生成模型（GAN、扩散模型、商业模型）、多个性能指标（Acc、AP、平均指标）、多个训练/测试设置（单生成器训练 vs 多生成器训练）。对比方法全面（含最新SOTA）。消融实验验证了各模块的必要性，超参分析检验了鲁棒性。整体设计客观、公平，结果充分支持结论。

### 6. 论文的主要结论与发现
- **模式共存假说得到验证**：通过SHAP分析，虚假图像呈现双峰分布（同时包含真实与虚假证据），真实图像为单峰分布。
- **DADL框架实现SOTA**：在AIGCDetectBenchmark上ACC_M达94.71%（超第二名1.55%），在GenImage上ACC_M达92.52%（超第二名1.42%），在Chameleon（All GenImage训练）上达67.77%（超第二名2.0%）。
- **优势场景**：对扩散模型（Midjourney、SDv1.4、SDv1.5、VQDM等）高保真图像检测效果显著提升。
- **多尺度策略必要**：融合浅层和深层AD Loss优于单一尺度。
- **泛化能力强**：在未见过生成器上仍保持高准确率。

### 7. 优点
- **新颖的假说驱动**：基于“模式共存”假说设计方法，而非简单堆砌特征。
- **可解释性**：利用SHAP进行定量分析，提供了模型决策依据，增强可信度。
- **轻量高效**：采用轻量级ResNet双分支，计算开销低。
- **多尺度协同**：浅层纹理+深层语义的差异挖掘，能捕捉高保真图像中的细微合成痕迹。
- **自适应阈值**：EMA动态调整AD Loss边界，使训练稳定且适应性好。
- **实验全面且结果领先**：在多个主流基准上均取得SOTA，尤其在高品质扩散模型上优势明显。

### 8. 不足与局限
- **特定数据集表现较弱**：如WFIR数据集上准确率偏低（52.82%），可能与WFIR的独特伪影模式未被充分捕捉有关。
- **未揭示计算资源细节**：缺乏GPU型号、训练时间等关键实验环境信息，影响可复现性。
- **训练数据单一**：主要实验仅用ProGAN或SDv1.4训练，虽然泛化到其他生成器，但在真实世界复杂场景（如混合来源、后处理）下性能未知。
- **超参数依赖**：λ=0.5通过实验确定，但可能需要在更广泛场景下调优。
- **仅二分类**：未考虑多类别（如不同生成模型类型）区分能力。
- **可解释性工具局限**：SHAP分析仅用于验证假说，未融入模型架构本身使决策过程透明化。

（完）
