---
title: "DySy-Det: A Synergistic Framework with Dynamic Reconstruction-Path Consistency for AI-Generated Image Detection"
title_zh: DySy-Det：基于动态重建路径一致性的协同AI生成图像检测框架
authors: "Fanli Jin, Feng Lin, Gaojian Wang, Tong Wu, Zhisheng Yan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40868/44829"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 利用注意力图增强AI生成图像检测的可解释性
tldr: 针对AI生成图像检测过拟合域内伪造模式，提出DySy-Det框架。微调CLIP提取语义并生成注意力图定位关键判别区域，指导多域伪造线索融合。在跨生成器测试中表现优异，注意力图提供可视化解释。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 510}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1821, \"height\": 564}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 602}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40868/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1808, \"height\": 557}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1726, \"height\": 567}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1720, \"height\": 317}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1742, \"height\": 819}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40868/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 728, \"height\": 297}]"
motivation: 现有方法忽略不同域间的互补伪造线索。
method: 微调CLIP提取高层语义，利用注意力图掩码驱动多域伪造特征挖掘。
result: 在多个跨生成器数据集上达到SOTA。
conclusion: 协同多域特征和注意力图提升检测泛化与可解释性。
---

## Abstract
Advanced image generative models have led to concerns about malicious use, underscoring the necessity for generalizable detection methods. However, existing approaches tend to overfit to domain-specific forgery patterns, while overlooking complementary cues from different domains. Therefore, we introduce DySy-Det (Dynamic Synergy Detector), a novel framework that mines collaborative and robust forgery artifacts from multiple evidence domains. First, DySy-Det fine-tunes a CLIP vision transformer to extract high-level semantics for identifying conceptual inconsistencies, while generating attention maps that pinpoint key discriminative regions. Then, this semantic guidance, in the form of a mask, directs a targeted reconstruction process. By focusing on these salient areas, our approach effectively extracts localized reconstruction errors, thereby filtering out irrelevant background noise. Furthermore, inspired by the intrinsic generative mechanics of diffusion models, we introduce the concept of Reconstruction-Path Consistency (RPC), which quantifies the temporal stability of the denoising trajectory to expose dynamic generative artifacts. We capture this by computing noise alignment scores across multiple timesteps and encode them via a lightweight network. Extensive evaluations on GenImage and UniversalFakeDetect benchmarks demonstrate that DySy-Det outperforms the state-of-the-art detector by 6.14% and 1.57% in mean accuracy, respectively.

---

## 论文详细总结（自动生成）

# DySy-Det 论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有AI生成图像检测方法过度拟合特定生成器带来的伪造模式，忽略了不同域（如语义、重建误差、动态轨迹）之间的互补线索，导致在未见过的生成器上泛化能力差。
- **整体含义**：为应对生成技术快速演进带来的伪造图像滥用威胁（虚假信息、版权侵权、隐私泄露），急需开发能够跨生成器泛化的检测框架。DySy-Det 通过协同多种证据源（高层语义不一致、局部重建误差、动态生成伪影）来挖掘鲁棒的伪造痕迹。

## 2. 方法论

### 核心思想
设计一个三模块协同框架，将不同域的特征有机融合，并引入动态生成伪影特征“重建路径一致性”（RPC），以克服静态分析的局限。

### 关键技术细节
- **语义驱动的异常提取器（SDAE）**：使用LoRA高效微调CLIP视觉编码器（ViT-L/14），获取语义嵌入并生成注意力图。通过指数移动平均（EMA）跨层聚合注意力，选出Top-k高响应位置形成二元掩码，用于定位判别区域。
- **注意力引导的残差增强器（AGRE）**：在稳定扩散模型中，对输入图像进行单步前向加噪和反向去噪，计算预测噪声与真实噪声之间的逐元素平方误差（公式7）。利用SDAE生成的掩码对上采样后的误差图进行逐元素相乘（公式8），从而聚焦关键区域，抑制背景噪声。
- **重建路径一致性分析器（RPCA）**：在多个稀疏采样时间步（t∈{200,250,300}）上计算预测噪声与真实噪声的余弦相似度（公式9），形成时序向量（公式10）。进一步通过轻量级1D卷积网络（Conv1D）建模局部时间演化，增强对动态生成伪影的敏感性（公式11）。
- **分类器**：将三个模块的输出（语义嵌入x_clip、局部重建误差x_error、动态特征x_rpc）拼接（公式12），送入MLP进行二分类，采用交叉熵损失优化（公式13）。

## 3. 实验设计

- **数据集**：
  - **GenImage**：训练仅使用Stable Diffusion V1.4生成图像，测试包括8个生成器（Midjourney、SD V1.4、SD V1.5、ADM、GLIDE、Wukong、VQDM、BigGAN）。
  - **UniversalFakeDetect**：训练仅使用ProGAN图像（四个类别：马、椅子、猫、汽车），测试包括19个子集（ProGAN、CycleGAN、BigGAN、StyleGAN、GauGAN、StarGAN、SITD、CRN、DeepFake、IMLE、SAN、Guided Diffusion、DALLE、LDM、Glide等）。
- **基准（Benchmark）**：报告平均准确率（mAcc）和平均平均精度（mAP）。
- **对比方法**：包括ResNet-50、Spec、F3Net、CNNSpot、GramNet、DeiT-S、Swin-T、UnivFD、FreqNet、NPR、LaRE²、AIDE、LGrad、FatFormer等，使用其官方预训练模型或重实现结果。

## 4. 资源与算力

- 文中明确说明：所有实验在**两块NVIDIA A6000 GPU**上进行，使用**固定随机种子32**，单epoch训练，batch size为48，Adam优化器学习率1e-4。未提及训练总时间，但指出模型在单个epoch即可收敛（由于采用预训练骨干和参数高效微调）。

## 5. 实验数量与充分性

- **主要实验**：
  - 在GenImage上对比11种方法（表1、表2），包括准确率和平均精度。
  - 在UniversalFakeDetect上对比10种方法（表3），包括19个子集的准确率。
  - 鲁棒性测试：对JPEG压缩、WebP压缩、高斯模糊、高斯噪声四种扰动进行不同强度评估（图3）。
  - 可视化分析：t-SNE特征分布可视化（图4）及logit分布（附录）。
  - 消融实验：在GenImage上设置5种配置（表4），分别移除CLIP、误差、掩码、RPC等组件，验证各模块贡献。
  - 补充实验：在附录中提供了AP结果等。
- **充分性与公平性**：实验覆盖两个主流基准、多个生成器类型（GANs、扩散模型等），且与多个SOTA方法在同一协议下比较（单源训练、跨域测试）。鲁棒性测试和消融实验全面。作者开源代码，结果可复现。因此实验较为充分且公平。

## 6. 主要结论与发现

- DySy-Det在GenImage上达到**mAcc 93.02%**（超过SOTA方法AIDE 6.14%）、**mAP 99.65%**；在UniversalFakeDetect上达到**mAcc 91.56%**（超过之前最好方法FatFormer 1.57%）。
- 所有三个模块（CLIP语义、引导重建误差、RPC）均对性能有正向贡献，分别移除导致准确率下降1.5%~2.5%。**掩码引导**能有效滤除背景噪声，提升重建误差的判别质量。
- RPC特征作为**动态生成伪影**，能暴露静态分析无法捕获的时间轨迹不一致，显著提升跨域泛化。
- 在常见图像扰动下（JPEG压缩、模糊、噪声），DySy-Det整体上优于对比方法，表现出较强的鲁棒性。
- t-SNE可视化显示：本方法能较好分离真实图像与来自不同生成器的伪造图像，形成紧凑聚类，说明学到的特征更通用。

## 7. 优点

- **协同创新**：将高层语义、局部重建误差、动态轨迹三种互补线索有机结合，而非简单拼接。利用注意力图实现语义指导重建，增强信号相关性。
- **动态特征引入**：首次提出“重建路径一致性”（RPC），量化去噪轨迹的时间稳定性，弥补静态分析对生成过程内部结构的忽视。
- **参数高效**：采用LoRA微调CLIP，仅需极少量可训练参数；RPCA使用轻量1D卷积，整体训练效率高（单epoch）。
- **强泛化性**：在仅依赖单一源生成器训练的情况下，对20+种未见生成器均保持高准确率，显著领先现有方法。
- **鲁棒性**：对常见图像处理操作表现出抗性，实用性较强。
- **可解释性**：注意力掩码可定位关键判别区域；RPC得分序列可解释去噪一致性。

## 8. 不足与局限

- **实验覆盖范围有限**：仅测试了两个基准数据集，未包含更多样化的伪造类型（如DeepFake人脸、GAN生成的内容等），也未评估对低分辨率或高噪声图像的极端情况。
- **依赖固定生成器做重建**：AGRE模块使用Stable Diffusion v1.5作为重建模型，当待检测图像来源于完全不同的生成范式（如非扩散模型）时，重建误差可能不够稳定。尽管实验显示仍然有效，但可能存在偏向。
- **计算成本**：尽管训练仅需单epoch，但每个测试图像需要执行多次去噪步骤（三个时间步）以及CLIP前向，推理速度可能不如纯CNN方法。
- **超参数敏感性**：掩码Top-k值（k=100）、时间步选择、EMA动量β等均通过实验选定，未进行详尽的超参数扫描，最佳配置可能随数据分布变化。
- **仅评估准确率和平均精度**：未报告F1分数、ROC-AUC等其他指标，也未分析假阳性/假阴性率，可能隐藏类别不平衡下的性能。
- **未讨论真实世界应用场景**：如在线检测延迟、对抗攻击鲁棒性（除常见扰动外）、模型篡改防御等。

（完）
