---
title: "DySy-Det: A Synergistic Framework with Dynamic Reconstruction-Path Consistency for AI-Generated Image Detection"
title_zh: DySy-Det：具有动态重建路径一致性的协同框架用于AI生成图像检测
authors: "Fanli Jin, Feng Lin, Gaojian Wang, Tong Wu, Zhisheng Yan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40868/44829"
tags: ["query:xai-objdet"]
score: 8.0
evidence: AI生成图像检测，利用注意力图定位判别区域提供可解释性
tldr: 针对现有伪造检测方法过拟合特定域模式的问题，提出动态协同检测框架DySy-Det。微调CLIP提取高层语义并生成注意力图定位关键判别区域，引导多域伪造痕迹挖掘。该方法不仅提升了泛化性，还通过注意力图提供了可解释的检测依据。实验表明在跨生成模型检测中表现优异。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1821, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1808, \"height\": 557, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1726, \"height\": 567, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1720, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1742, \"height\": 819, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 728, \"height\": 297, \"label\": \"Table\"}]"
motivation: 现有AI生成图像检测方法过拟合特定域伪造模式，且缺乏可解释性。
method: 微调CLIP提取语义并生成注意力图，利用语义引导动态挖掘多域协同伪造伪影。
result: 跨多种生成模型检测中达到最优性能，并输出可解释的判别区域。
conclusion: 语义引导的多域协同检测与注意力可视化增强了泛化性和可解释性。
---

## Abstract
Advanced image generative models have led to concerns about malicious use, underscoring the necessity for generalizable detection methods. However, existing approaches tend to overfit to domain-specific forgery patterns, while overlooking complementary cues from different domains. Therefore, we introduce DySy-Det (Dynamic Synergy Detector), a novel framework that mines collaborative and robust forgery artifacts from multiple evidence domains. First, DySy-Det fine-tunes a CLIP vision transformer to extract high-level semantics for identifying conceptual inconsistencies, while generating attention maps that pinpoint key discriminative regions. Then, this semantic guidance, in the form of a mask, directs a targeted reconstruction process. By focusing on these salient areas, our approach effectively extracts localized reconstruction errors, thereby filtering out irrelevant background noise. Furthermore, inspired by the intrinsic generative mechanics of diffusion models, we introduce the concept of Reconstruction-Path Consistency (RPC), which quantifies the temporal stability of the denoising trajectory to expose dynamic generative artifacts. We capture this by computing noise alignment scores across multiple timesteps and encode them via a lightweight network. Extensive evaluations on GenImage and UniversalFakeDetect benchmarks demonstrate that DySy-Det outperforms the state-of-the-art detector by 6.14% and 1.57% in mean accuracy, respectively.

---

## 论文详细总结（自动生成）

# 论文中文总结：DySy-Det：具有动态重建路径一致性的协同框架用于AI生成图像检测

## 1. 论文的核心问题与整体含义
- **研究动机**：先进图像生成模型（GAN、扩散模型）的恶意使用日益严重，需要通用且可推广的检测方法。
- **核心问题**：现有检测方法过度拟合特定域伪造模式（如像素级不一致、频率异常、重建误差），在未见过的生成模型上性能大幅下降；同时，不同证据域（语义、结构、动态）之间的互补信息未被有效利用。
- **整体含义**：本文旨在构建一个协同多源线索的框架，通过提取高层语义不一致、局部重建误差和动态生成伪影，实现跨生成模型的鲁棒检测，并为检测提供可解释性。

## 2. 论文提出的方法论
- **核心思想**：整合三种互补的伪造证据：
    1. **高层语义不一致**：利用CLIP视觉编码器（LoRA微调）提取语义嵌入，并生成注意力图定位判别区域。
    2. **局部重建误差**：利用注意力图作为掩码，引导扩散模型对图像进行单步加噪-去噪，仅计算关键区域的重建残差，抑制背景噪声。
    3. **动态生成伪影（RPC）**：沿去噪轨迹采样多个时间步，计算预测噪声与真实噪声的余弦相似度序列，再通过轻量级Conv1D网络捕捉时间稳定性差异。
- **关键技术细节**：
    - **SDAE模块**：对CLIP ViT-L/14的QKV投影矩阵添加低秩适应（LoRA, r=8, α=16），通过EMA累加各层注意力得到累积图，取Top-100位置生成二值掩码。
    - **AGRE模块**：使用Stable Diffusion v1.5，在时间步t∈{200,250,300}对图像潜变量加噪，计算重建误差，并用上采样后的掩码加权，得到局部残差特征。
    - **RPCA模块**：在稀疏采样的时间步上计算`cos(ϵ_true, ϵ_pred)`，串联为向量s，输入一维卷积网络（Conv1D）提取时序模式。
    - **融合与分类**：将语义嵌入x_clip、局部误差x_error、动态特征x_rpc拼接，经MLP输出预测概率，使用交叉熵损失训练。
- **公式流程**：
    - 注意力累积：`˜A_i = β·˜A_{i-1} + (1-β)·A_i`
    - 重建误差：`LRL[i,j] = (ϵ_{i,j} - ϵ_θ(z_t, t)_{i,j})^2`
    - RPC相似度：`s^{(i)} = (ϵ_true·ϵ_pred)/(||ϵ_true||·||ϵ_pred||)`
    - 最终预测：`ŷ = f(Concat(x_clip, x_error, x_rpc))`

## 3. 实验设计
- **数据集**：
    - **GenImage**：训练集为Stable Diffusion V1.4生成图像，测试集包括8个生成器（Midjourney, SD V1.4/V1.5, ADM, GLIDE, Wukong, VQDM, BigGAN）。
    - **UniversalFakeDetect**：训练集为ProGAN生成的4类图像（马、椅子、猫、车），测试集包括19个子集（ProGAN, CycleGAN, BigGAN, StyleGAN, GauGAN, StarGAN, SITD, CRN, DeepFake, IMLE, SAN, Guided Diffusion, DALLE, LDM, GLIDE等）。
- **基准方法**：对比了ResNet-50, Spec, F3Net, CNNSpot, GramNet, DeiT-S, Swin-T, UnivFD, FreqNet, NPR, LaRE^2, AIDE, FatFormer等10余种方法。所有对比均使用官方预训练模型或重现实现在相同设置下评估。
- **评价指标**：平均准确率（mAcc）和平均精度（mAP）。
- **额外实验**：鲁棒性测试（JPEG压缩、WebP压缩、高斯模糊、高斯噪声），t-SNE特征可视化，消融实验。

## 4. 资源与算力
- 文中明确说明：实验使用**两块NVIDIA A6000 GPU**，训练仅**1个epoch**，batch size为48，学习率1e-4，Adam优化器，固定随机种子32。
- 未明确报告单次训练时长，但1个epoch在GenImage（百万级图像）上估计为数小时。推理开销因涉及多步扩散采样（3个时间步）和CLIP前向，相对较高。

## 5. 实验数量与充分性
- **主要对比**：在GenImage上报告了8个生成器的Acc和AP，UniversalFakeDetect上报告了19个子集的Acc。结果覆盖了主流GAN和扩散模型。
- **消融实验**：表4系统地验证了CLIP、重建误差、注意力掩码、RPC四个组件的贡献，包含5个设置，清晰展示了每部分的增益。
- **鲁棒性实验**：在4种扰动下（图3）与UnivFD、FreqNet、NPR、AIDE等对比，证明了方法的鲁棒性。
- **可视化**：t-SNE图展示了特征可分性，额外附录提供了logit分布。
- **公平性**：所有对比方法使用官方代码或重现在相同数据划分下评估，确保公平。训练仅使用单个生成器数据，测试覆盖未见模型，设置符合通用检测挑战。
- **充分性评价**：实验设计较全面，覆盖了多种生成器类型、扰动条件、消融验证，足以支撑主要结论。但未涉及对抗攻击下的鲁棒性，也缺少真实世界场景（如社交媒体压缩、截屏）的测试。

## 6. 论文的主要结论与发现
- DySy-Det在**GenImage**上达到**mAcc 93.02%**、**mAP 99.65%**，分别比先前最佳方法AIDE高出6.14%和1.89%。
- 在**UniversalFakeDetect**上达到**mAcc 91.56%**，超过FatFormer 1.57%，比UnivFD提升10.30%。
- 在常见图像扰动下（JPEG、WebP、模糊、噪声），DySy-Det保持最高或接近最高的准确率，仅极端JPEG（质量=50）略低于UnivFD。
- 消融实验表明各组件均不可或缺，其中RPC贡献最大（+2.57%），注意力掩码贡献+1.5%，重建误差贡献+1.1%。
- t-SNE可视化证明统一特征空间能清晰分离真实图像与多种生成图像，泛化性强。

## 7. 优点
- **方法创新**：首次提出动态重建路径一致性（RPC）作为检测特征，捕获扩散过程的时序不一致；利用CLIP注意力图指导重建，实现语义与低层残差的协同。
- **通用性强**：仅在单个生成器上训练，即可泛化到20余种未见生成器，远超现有方法。
- **可解释性**：通过注意力图突出判别区域，为检测提供直观的可视化依据。
- **鲁棒性好**：对常见图像降质（压缩、模糊、噪声）具有较好的抵抗力。
- **代码开源**：提供GitHub仓库，方便复现和拓展。

## 8. 不足与局限
- **计算成本**：依赖CLIP ViT-L/14和Stable Diffusion v1.5两个大模型，推理需多次扩散前向（3个时间步），资源要求较高，可能不适合实时或边缘端部署。
- **训练数据集限制**：仅在单一生成器训练，尽管泛化出色，但假设真实图像分布仅来自训练集（如ProGAN的4类），可能对未见过的真实场景或低质量真实图像存在偏差。
- **动态特征依赖性**：RPC基于扩散模型内禀机制，对于非扩散生成器（如纯GAN生成的图像）可能不够敏感，尽管实验显示仍有效，但未深入分析。
- **未覆盖对抗样本**：未测试攻击者故意添加对抗扰动或后处理以规避检测的情况，实际应用安全性存疑。
- **评估范围**：主要使用标准基准数据集，缺乏真实社交媒体或视频帧检测等更复杂场景的评估。
- **消融实验完整度**：虽然验证了组件，但未探索不同注意力层选择、Top-k值、时间步采样策略等超参数的影响，可能未达到最优配置。

（完）
