---
title: Decision-Driven Orthogonal Learning with Complementary Feature Mining for Robust Synthetic Image Detection
title_zh: 决策驱动正交学习与互补特征挖掘用于鲁棒合成图像检测
authors: "Kai Li, Wei Wang, Linchao Zhang, Siying Zhu, Wenqi Ren"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37553/41515"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 通过决策驱动正交学习与互补特征挖掘实现可解释伪造检测
tldr: 社交网络压缩严重干扰合成图像检测，且现有方法混淆压缩与伪造伪影。该论文提出决策驱动正交约束，定义从真实类中心指向伪造类中心的分类决策轴，强制特征沿该轴分离，从而保留伪造痕迹并抑制压缩干扰。同时引入互补特征挖掘增强高频细节。该方法不仅提升了检测鲁棒性，还通过正交特征提供了可解释性。实验表明在多个压缩数据集上性能显著提升。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 社交网络压缩导致伪造与压缩伪影混淆，且高频细节丢失。
method: 引入决策驱动正交约束和互补特征挖掘，分离伪造与压缩特征。
result: 在多个压缩数据集上，该方法在检测准确率和可解释性上均大幅领先。
conclusion: 该工作为可解释的鲁棒伪造检测奠定了方法基础。
---

## Abstract
The widespread and inconsistent compression applied by Online Social Networks severely degrades the performance of synthetic image detectors. We attribute this degradation to two main issues: 1) the model confuses forgery artifacts with compression artifacts, and 2) compression erodes crucial discriminative high-frequency details. Existing methods suppress compression features during training but overlook the overlap between compression features and forgery-related features, leading to the unintended removal of forgery traces. To address artifact confusion, we introduce a Decision-Driven Orthogonal Constraint, which defines a classification decision axis pointing from the real class centroid to the forged class centroid. This constraint enforces compression artifacts to be orthogonal to the decision axis, mitigating their interference with forgery detection without entirely removing them, thus preventing the suppression of forgery-related features. To mitigate the erosion of high-frequency details, we propose to mine complementary forgery cues from both low-frequency information and compressed high-frequency components. A bidirectional update strategy and an adaptive global-local modulator are proposed to facilitate the utilization of forgery cues. Extensive experiments demonstrate that our method achieves state-of-the-art generalization performance in challenging open-world detection scenarios.

---

## 论文详细总结（自动生成）

### 论文详细中文总结

#### 1. 核心问题与整体含义（研究动机和背景）
- **背景**：在线社交网络（OSNs）对图像进行广泛且不一致的压缩，严重降低了合成图像检测器的性能。
- **核心问题**：
  - **伪影混淆**：模型将伪造伪影与压缩伪影混淆，因为两者在特征空间中有重叠。
  - **高频细节侵蚀**：压缩算法丢弃了含有判别性伪造痕迹的高频信息。
- **现有方法局限**：
  - 部分方法使用配对数据学习压缩不变性，但配对数据在现实中难以获取。
  - 另一些方法使用梯度反转（Gradient Reversal）抑制压缩特征，但会无意中移除与伪造相关的特征，造成信息损失。
- **本文目标**：提出一种框架，能在不丢失伪造线索的情况下实现对压缩的鲁棒性，同时通过挖掘互补频率信息补偿高频细节的损失。

#### 2. 方法论：核心思想、关键技术细节
- **整体框架**：双分支架构，主分支使用预训练Vision Transformer（ViT）提取低频特征，辅助分支使用卷积网络提取高频特征。通过双向更新策略和自适应全局-局部调制器（AGLM）融合特征，最后施加决策驱动正交约束（DDOC）增强压缩鲁棒性。
- **关键技术细节**：
  - **双向更新策略**：
    - 第一阶段（高频注入）：ViT的低频特征作为Query，高频特征作为Key/Value进行交叉注意力，使低频特征吸收高频伪影。
    - 第二阶段（高频更新）：高频特征作为Query，注入后的低频特征作为Key/Value，使高频特征在全局上下文中聚焦判别性区域。
    - 交替进行多次交互，实现频率互补。
  - **自适应全局-局部调制器（AGLM）**：
    - 局部分支：对补丁标记（patch tokens）使用多尺度深度可分离卷积（kernel size 3/5/7）提取细粒度空间关系，不改变类标记（class token）。
    - 全局分支：对全特征序列使用标准适配器（adapter）进行低秩通道调整。
    - 两个分支输出相加作为残差，最终线性层初始化为零以保证训练稳定性。
  - **决策驱动正交约束（DDOC）**：
    - 定义分类决策轴 \( \mathbf{w}_f \)：从真实类中心指向伪造类中心的单位向量，由批量数据的特征均值计算。
    - 对于配对样本（原始图像 \( x_p \) 与压缩版本 \( x_c \)），定义压缩扰动向量 \( \mathbf{v}_c = \Phi(x_p) - \Phi(x_c) \)。
    - 正交损失 \( \mathcal{L}_{\text{ortho}} = \frac{1}{N}\sum_i \left( \frac{\mathbf{v}_{c,i}^\top \mathbf{w}_f}{\|\mathbf{v}_{c,i}\|_2 \|\mathbf{w}_f\|_2} \right)^2 \)：强制压缩扰动在决策轴上投影为零，从而不干扰分类。
    - 总损失：\( \mathcal{L}_{\text{total}} = \mathcal{L}_{\text{cls}} + \lambda \mathcal{L}_{\text{ortho}} \)，\( \lambda=0.1 \)。

#### 3. 实验设计
- **训练集**：使用ForenSynths数据集中ProGAN生成的图像，分为2类（chair, horse）和4类（car, cat, chair, horse）两个训练设置。20%数据经JPEG压缩（质量因子40）形成配对数据，80%保留原始未压缩。
- **测试集**：ForenSynths（包含8种GAN模型）和GANGen-Detection（更新生成模型）。两种评估场景：
  - **质量已知（Quality-Aware）**：测试集压缩质量与训练相同。
  - **质量未知（Quality-Agnostic）**：每个测试图像随机选择JPEG质量因子，模拟社交网络真实场景。
- **评估指标**：准确率（Acc）。
- **对比方法**：MesoNet, FF++, F3Net, MAT, SBIs, ADD, QAD, ODDN（最新梯度反转方法）等，共十多种基线。

#### 4. 资源与算力
- **论文明确说明**：所有实验使用PyTorch，在NVIDIA Tesla A100 GPU上进行训练和测试。
- **未明确说明**：GPU数量、训练总时长、单卡显存等具体细节未提供。仅提到超参数：学习率2e-5，batch size 32，训练15个epoch，优化器为SAM。

#### 5. 实验数量与充分性
- **主实验**：4组（Table 1-4），分别对应2类训练/质量已知、2类训练/质量未知、4类训练/质量已知、4类训练/质量未知。每组包含17个生成器子评估，并计算平均准确率。
- **消融实验**：1组（Table 5），逐步移除DDOC、AGLM、双向更新策略，验证各组件贡献。
- **可视化分析**：图4展示基线 vs 本文方法的logit分布，定性说明类间分离性。
- **充分性评价**：
  - **客观公平**：采用与基线完全相同的数据划分、设置（跟随ODDN协议），对比方法都是公开发表的SOTA，且结果直接引用或复现。
  - **覆盖全面**：涵盖多种生成模型、两种训练多样性、两种压缩场景，消融实验完整验证每个模块。
  - **可重复性**：除GPU细节外，代码基于PyTorch，超参数明确，其他研究者可复现。

#### 6. 主要结论与发现
- 决策驱动正交约束能有效分离压缩扰动与伪造特征，避免伪影混淆，在质量已知和未知场景下均显著优于基于梯度反转的方法（如ODDN）。
- 双向更新策略与AGLM能充分利用低频鲁棒结构和残存高频线索，补偿压缩导致的高频信息损失。
- 在2类训练下，本文方法在质量已知/未知场景的平均准确率分别为75.4%和74.5%，领先ODDN约4个百分点；在4类训练下达到76.5%和75.5%，同样大幅领先。
- 定性分析（logit分布）显示，本文方法使得真假样本特征形成清晰间隔，而基线类间重叠严重，证明模型学得更具判别性的表示。

#### 7. 优点
- **方法设计创新**：
  - 提出直接在决策层进行正交约束，而非粗暴抑制压缩特征，保留下游判别信息。
  - 构建低频（ViT全局建模）与高频（CNN局部细节）互补融合机制，并设计双向交互与自适应调制，针对压缩后高频退化问题有效。
- **实验充分且公平**：严格遵循最新基线ODDN的协议，多种生成模型、两种训练设置、两种压缩场景，对比方法全面，消融清晰。
- **实际应用价值**：质量未知场景的强鲁棒性贴近社交网络真实部署，解决核心痛点。
- **可解释性**：正交约束使模型学习到与分类决策正交的压缩特征，便于理解模型行为。

#### 8. 不足与局限
- **资源信息缺失**：未提供GPU数量、训练时间等，难以估算计算成本，也未与基线对比训练开销。
- **训练数据单一**：仅使用ProGAN生成图像作为训练集，虽然测试集涵盖更多生成器，但训练集本身多样性有限，可能限制泛化到更新的扩散模型（虽然提到GANGen-Detection包含扩散模型，但训练未包含）。
- **未考虑多轮迭代压缩**：仅模拟单次JPEG压缩，而社交网络可能叠加多种压缩、缩放、裁剪等操作。
- **正交损失的假设依赖**：DDOC要求配对数据（原始+压缩），虽然仅需20%配对，但若配对数据中存在噪声或不对齐，可能影响约束有效性。
- **高频分支设计**：卷积分支用于提取高频特征，但未详细说明如何保证提取到的确实是高频成分而非混杂的低频信息，可能存在冗余。
- **未与最先进的生成模型（如Stable Diffusion 3, Midjourney）直接对比**：测试集主要包含GAN生成图像，扩散模型的实验可能不够完整。

（完）
