---
title: Dual-Branch Asymmetric Discrepancy Learning Based on Fake Image Pattern-Coexistence for AI-Generated Image Detection
title_zh: 基于假图模式共存的双支非对称差异学习用于AI生成图像检测
authors: "Chunli Song, Jie Liu, Peiyang Wang, Ying Huang, Guixuan Zhang, Zhi Zeng, Shuwu Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37071/41033"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 基于SHAP的可解释性用于AI生成图像检测
tldr: 本文提出基于双支非对称差异学习的AI生成图像检测方法。通过SHAP分析验证了合成图像中真实模式与合成模式共存的假设，并利用这一发现设计检测网络。模型在多个生成模型数据集上取得高检测率，同时提供了特征重要性解释。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 490}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1833, \"height\": 501}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 773, \"height\": 464}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 878, \"height\": 389}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37071/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 353}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37071/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1838, \"height\": 784}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37071/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1844, \"height\": 664}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37071/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1845, \"height\": 223}]"
motivation: AI生成图像检测面临模式共存导致的模糊性问题。
method: 提出双支非对称差异学习网络，利用SHAP分析指导特征学习。
result: 在多个生成器数据集上检测性能优异，并提供了可解释分析。
conclusion: 模式共存假设有效提升了检测和可解释性。
---

## Abstract
With the rapid advancement of generative models, high-fidelity AI-generated images have become increasingly indistinguishable from real images, posing significant challenges to traditional detection methods that rely on explicit artifacts or uniform feature learning. We hypothesize that detection ambiguity originates from pattern coexistence: synthetic images simultaneously embed (a) authentic patterns inherited from real-image distributions and (b) synthetic patterns induced by generative architectures, whereas real images maintain consistent patterns. We validate this hypothesis through SHAP-based quantitative analysis, demonstrating that synthetic images inherently exhibit a dual distribution—simultaneously containing authentic patterns and synthetic traces—while real images show a unimodal distribution. Building on this insight, this paper proposes a Dual-Branch Asymmetric Discrepancy Learning (DADL) framework. The DADL leverages multi-scale feature extraction and Asymmetric Feature Discrepancy Loss to capture and amplify such pattern differences across multiple scales. Extensive experiments on three benchmarks (AIGCDetectBenchmark, GenImage, and Chameleon) show that DADL achieves state-of-the-art performance, with particular strengths in detecting high-fidelity synthetic images from diffusion models (e.g., Midjourney, SDv1.4, SDv1.5) and enhancing generalization across diverse generative paradigms. This study not only offers an effective approach for AIGI detection but also sheds light on the intrinsic properties of synthetic images, providing a new perspective for advancing AIGI forensics.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：生成模型（GAN、扩散模型等）的快速发展使得AI生成图像高度逼真，传统检测方法依赖显式伪影或统一特征学习，难以区分高保真伪造图像。
- **核心问题**：现有方法将合成图像视为“纯伪影”，忽略了其内在的**模式共存**现象——合成图像同时包含从真实图像分布继承的“真实模式”和生成架构引入的“合成痕迹”，而真实图像模式一致。
- **研究动机**：作者通过SHAP（Shapley Additive Explanations）定量分析验证了**模式共存假设**：合成图像的SHAP值呈现双峰分布（同时存在正/负贡献），真实图像呈现单峰分布。基于此，提出利用这种内在不一致性进行检测。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **检测原则**：放大伪造图像的内部不一致性，同时强化真实图像的一致性。
- **DADL框架**（Dual-Branch Asymmetric Discrepancy Learning）：双分支非对称差异学习网络，利用**非对称特征差异损失（AD Loss）**，促使两个分支对真实图像输出相似特征，对伪造图像输出差异大的特征。

### 关键技术细节
1. **双分支特征提取器**：两个结构相同但权重独立的轻量ResNet（类似SAFE架构）并行提取特征，从头独立训练，自然形成互补的归纳偏置。
2. **AD Loss（公式1-4）**：
   - 对真实图像：最小化两个分支特征之间的归一化L2距离 → 强制一致性。
   - 对伪造图像：最大化该距离（超过动态边界 \(m_t\)） → 放大内在差异。
   - 动态边界 \(m_t\) 通过指数移动平均（EMA）基于当前批次真实样本的平均距离更新（\(\beta=0.99\)），初始值0.5。
3. **多尺度差异挖掘**：在浅层（阶段1，高频伪影敏感）和深层（阶段2，结构畸变敏感）分别计算AD Loss，通过可学习权重 \(\alpha_1, \alpha_2\)（满足 \(\alpha_1+\alpha_2=1\)）融合。
4. **双损失联合优化**：
   - 最终分类使用两个分支深层特征的差值 \(z_{\text{diff}} = z_{1,d} - z_{2,d}\) 送入分类器，计算交叉熵损失 \(L_{\text{CE}}\)。
   - 总损失 \(L = L_{\text{CE}} + \lambda L_{\text{AD}}\)，\(\lambda=0.5\)。
5. **输入预处理**：先对图像进行离散小波变换（DWT）转换到频率域，再应用标准数据增强（RandomCrop、RandomHorizontalFlip、RandomRotation、RandomMask）。

### 算法流程（文字描述）
- 训练阶段：输入图像 → 双分支提取特征 → 在浅层/深层分别计算AD Loss → 合并为多尺度AD Loss → 深层特征差分作为最终表示 → 分类器预测 → 联合优化L_CE+L_AD。
- 测试阶段：输入图像 → 双分支特征计算距离 → 若距离小则判为真实，距离大则判为伪造。

## 3. 实验设计

### 数据集
- **AIGCDetectBenchmark**（Zhong et al., 2023）：训练使用ProGAN的4个类别（car/cat/chair/horse），测试覆盖16种生成器（含GAN、扩散模型如Midjourney、SDv1.4/1.5、VQDM、Wukong等）。
- **GenImage**（Zhu et al., 2023）：训练使用ImageNet真实图 + SDv1.4伪造图，测试8种生成器。
- **Chameleon**（Yan et al., 2024）：三种训练场景——ProGAN、SDv1.4、All GenImage（混合多种生成器）。

### 评估指标
- **ACC**（分类准确率）和**AP**（平均精度），并报告测试集平均指标**ACC_M**和**AP_M**。

### 对比方法
共13种：CNNSpot、FreDect、Fusing、GramNet、LNP、LGrad、UnivFD、DIRE、PatchCraft、NPR、AIDE、SAFE、Effort、AIGI-Holmes（部分表涉及）。涵盖基于伪影、频域、重建、预训练、可解释性等多种范式。

### 实现细节
- 轻量ResNet（2阶段），AdamW优化器，100 epochs，batch size 32，学习率5e-3，weight decay 0.01。
- 数据增强：DWT + RandomCrop等。

## 4. 资源与算力

**论文中未明确说明使用的GPU型号、数量及训练时长**。仅提及使用AdamW优化器训练100个epochs，batch size 32，未提供具体硬件配置或训练时间。这是本文在可重复性方面的一个小缺失。

## 5. 实验数量与充分性

- **实验数量**：在三大benchmark上进行了**全量对比**（表1-表3），每个数据集均覆盖多种生成器；额外进行了**消融实验**（图4：多尺度AD Loss的消融）和**超参数λ敏感性分析**（图5，λ从0.25到1.5）。
- **充分性**：
  - 对比方法涵盖最新SOTA（2023-2025年），包括AIGI-Holmes、Effort等。
  - 在GenImage上针对Midjourney等高质量商业模型有显著提升（99.15%，次优91.50%）。
  - 消融实验验证了浅层和深层AD Loss各自及融合的有效性。
  - 超参数λ在很大范围内性能稳定，表明鲁棒性。
- **公平性**：实验设置严格遵循各benchmark官方协议（如训练/测试划分），对比方法结果多数来自原文或官方报告。但未提供跨数据集训练的泛化实验（如仅用ProGAN训练，直接测试其他数据集），不过Chameleon部分已涵盖单一生成器训练的评估。

综合来看，实验充分、设计客观，覆盖了主要检测范式和多种生成模型，消融和敏感性分析增强了结论可信度。

## 6. 主要结论与发现

1. **模式共存假设成立**：SHAP分析实证了合成图像的双峰分布vs真实图像的单峰分布，这是传统检测失败的根本原因。
2. **DADL实现SOTA**：在AIGCDetectBenchmark上ACC_M达94.71%（优于次优AIGI-Holmes的93.16%）；GenImage上ACC_M 92.52%（优于次优Effort 91.10%）；Chameleon上All GenImage训练场景67.77%（优于次优AIDE 65.77%）。
3. **对扩散模型检测优势突出**：尤其在Midjourney、SDv1.4/1.5、VQDM等高保真模型上表现优异，验证了方法对细微伪造痕迹的捕获能力。
4. **多尺度策略必要**：仅用浅层或深层AD Loss均不如两者融合，表明伪造痕迹在不同尺度上的互补性。

## 7. 优点

- **理论创新**：首次提出并验证“模式共存”假设，为检测提供了可解释的物理基础。
- **方法设计巧妙**：利用双分支+不对称损失，简单高效（轻量ResNet），无需复杂预训练或外部模型。
- **多尺度差异挖掘**：双阶段特征层同时捕捉高频伪影和结构畸变，覆盖面广。
- **动态边界机制**：EMA更新边界适应训练进程，避免硬阈值。
- **实验扎实**：覆盖三大主流benchmark，与13种SOTA方法全面对比，消融和敏感性分析完整。
- **可解释性强**：SHAP可视化直接展示模型决策依据，便于理解检测原理。

## 8. 不足与局限

- **资源信息缺失**：未报告GPU型号、数量及训练时间，不利于复现和效率对比。
- **个别数据集表现弱**：在AIGCDetectBenchmark的WFIR数据集上仅52.82%准确率，作者承认可能因WFIR的独特伪影模式与多尺度机制不完全匹配。
- **训练数据依赖性**：虽在单一生成器训练时表现良好，但Chameleon上ProGAN训练场景仅59.24%（略高于次优），提升幅度有限；可能仍存在对特定生成模型偏置的风险。
- **未讨论对高分辨率或视频场景的扩展**：图像尺寸和动态场景未涉及，实际应用（如深度伪造视频帧）有待验证。
- **超参λ固定**：仅验证了λ在0.5时最优，但未探索自适应学习权重，可能在不同数据集上需重新调节（尽管结果表明鲁棒）。
- **方法复杂度**：双分支虽轻量，但相比单流网络仍需2倍参数，且需同时训练两个独立分支，训练内存开销略高。

（完）
