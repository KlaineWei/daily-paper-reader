---
title: Explainable Synthetic Image Detection Through Diffusion Timestep Ensembling
title_zh: 通过扩散时间步集成进行可解释合成图像检测
authors: "Yixin Wu, Feiran Zhang, Tianyuan Shi, Ruicheng Yin, Zhenghua Wang, Zhenliang Gan, Xiaohua Wang, Changze Lv, Xiaoqing Zheng, Xuanjing Huang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38060/42022"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 通过扩散时间步集成进行可解释合成图像检测
tldr: 针对合成图像检测缺乏可解释性的问题，本文提出ESIDE方法，利用DDIM逆过程不同时间步的噪声特征，训练集成分类器，并通过频谱差异等可视化线索增强人类理解。实验证明该方法在多个检测基准上性能优异且提供可解释证据。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 685}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1806, \"height\": 961}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 338}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1839, \"height\": 979}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 657, \"height\": 542}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1827, \"height\": 633}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1828, \"height\": 644}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 177}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 883, \"height\": 259}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 299}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 884, \"height\": 183}]"
motivation: 合成图像检测需要可解释性以增强信任，但现有方法多为黑箱。
method: 利用DDIM逆过程不同时间步的中间噪声特征，训练集成模型，并生成频谱等可视化解释。
result: 在多个合成图像检测数据集上取得领先性能，同时提供人类可理解的解释。
conclusion: ESIDE实现了检测精度与可解释性的有效平衡，为安全领域提供了可靠方案。
---

## Abstract
Recent advances in diffusion models have enabled the creation of deceptively real images, posing significant security risks when misused. In this study, we empirically show that different timesteps of DDIM inversion reveal varying subtle distinctions between synthetic and real images that are extractable for detection, taking the forms of such as Fourier power spectrum high-frequency discrepancies and inter-pixel variance distributions. Based on these observations, we propose a novel detection method named ESIDE that directly utilizes features of intermediately noised images by training an ensemble on multiple noised timesteps, circumventing the overtime of conventional reconstruction-based strategies. To enhance human comprehension, we introduce a metric-grounded explanation refinement module to identify and explain AI-generated flaws. Additionally, we present the benchmarks GenHard and GenExplain, offering detection samples of greater difficulty and high-quality rationales for fake images. Extensive experiments show that ESIDE achieves state-of-the-art performance with 98.91% and 95.89% detection accuracy on regular and challenging samples respectively, and demonstrates generalizability and robustness.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 扩散模型（如 Stable Diffusion、DALL-E 3、Midjourney）生成的图像越来越逼真，给安全领域带来严重威胁，需要有效的合成图像检测方法。
- 现有检测方法主要分为三类：深度学习检测器（如 CNN、ViT）、频域分析（利用合成图像在高频上的缺陷）、空域分析（像素级关系）。基于扩散模型的重建方法（如 DIRE、SeDID、LaRE、DRCT）需要同时进行噪声添加和去噪重建，耗时较长。
- 现有检测方法在困难样本上表现不足，且缺乏可解释性：人类无法理解“是/否”判定背后的原因。因此，需要在提升检测精度的同时，提供高质量的解释。

## 2. 论文提出的方法论

### 核心思想
- 观察到 DDIM 逆过程的不同时间步会揭示真/假图像间不同的细微差异（如傅里叶功率谱高频差异、像素间方差分布），这些特征可以直接提取，无需重建。
- 基于此，提出 ESIDE 管道：仅需一次噪声添加（DDIM 逆过程），对多个中间噪声时间步的图像分别训练分类器，再通过 AdaBoost 集成，从而避免传统重建策略的高耗时。

### 关键技术细节
1. **DDIM 逆过程**：对输入图像 x₀ 进行 T 步 DDIM 逆过程，得到序列 {x₀, x₁, ..., x_T}。
2. **集成学习**：每个时间步（步长 stride s）对应一个基分类器 m_k，训练在相应噪声图像上。采用 AdaBoost 框架：
   - 初始化样本权重 w_{k,i} = 1/N。
   - 加权二元交叉熵损失 L_WB。
   - 计算加权误差 e_k，进而得到模型权重 α_k = 0.5 * ln((1-e_k)/e_k)。
   - 更新样本权重，并归一化。
   - 最终预测：H(x_i) = sign( Σ α_k * h_k(x_i) )。
3. **解释细化模块**：当图像被鉴定为合成时，首先用多标签分类器识别缺陷类型（14 类）。然后利用 MLLM (gpt-4o) 生成初步解释。通过 Faster R-CNN 检测子区域，用 CLIP ViT 提取视觉嵌入，计算每个短语与各区域的相似度，加权得到聚合表示，再计算短语评分。通过 Top-K 采样保留高相关短语，并提示模型发现遗漏的缺陷，迭代 3 次获得最终解释。
4. **数据集构建**：
   - GenHard：从 GenImage 训练子集中提取被 CBSID 错误分类的样本（108,704 张合成 + 112,682 张自然图像），构成更难的检测样本。
   - GenExplain：涵盖 14 类常见缺陷，共 54,210 组（图像-缺陷-解释），经人工校验和细化生成。

## 3. 实验设计

- **数据集**：GenImage（百万级，包含 8 个生成器子集：Midjourney、SD V1.4、SD V1.5、ADM、GLIDE、Wukong、VQDM、BigGAN）。划分验证集 9:1 用于训练和评估。
- **Benchmark**：原始 GenImage 测试集 + 自己构建的 GenHard（困难样本测试集）。
- **对比方法**：ResNet-50、DeiT-S、Swin-T、CNNSpot、CBSID、DIRE、LGrad、UnivFD、FreqNet、NPR、DRCT。对比场景包括：
  1. **同源检测**：训练集和测试集来自同一生成器。
  2. **跨域泛化**：训练集来自 SD V1.4，测试集来自其他生成器。
- **鲁棒性实验**：引入三种扰动：高斯模糊（σ∈[0.5,2.5]）、任意旋转（θ∈[-45°,45°]）、亮度变化（α∈[0.3,1.8]）。
- **消融实验**：移除 DDIM 中间噪声、移除集成权重、仅用无噪声图像、抑制高频傅里叶峰值等。

## 4. 资源与算力

- 论文中明确提到：
  - DDIM 预处理时间：每张图像 2.66 秒（L20 GPU），而 DRCT 为 5.71s、DIRE 为 5.24s。
  - 训练时间：在 GLIDE 子集上每个 epoch 44.2 秒，基线平均为 32.6±19.1 秒。
  - 使用 low GPU memory consumption，模型可分布式部署。
  - 未说明 GPU 型号、数量及总训练时长等详细算力资源，仅提及使用了 L20 GPU 进行时间测试。

## 5. 实验数量与充分性

- **实验数量**：
  - 主检测实验（表1）：8个生成器×2个测试集（原始+困难），共16组结果。
  - 跨域泛化（表2）：训练于 SD V1.4，测试于其他7个子集的原始+困难，共14组。
  - 鲁棒性（表4）：8个子集×3种扰动，但表4只给出了平均结果。
  - 缺陷分类（表3）：8个子集上的 Exact Match 和 mAP。
  - 消融（表5、表6）：分别4组和2组。
  - 解释细化（图6）：4次迭代的5个指标。
- **充分性**：
  - 实验覆盖了同源、跨域、鲁棒性、消融等多种场景，比较全面。
  - 对比了多个 SOTA 基线，公平性较好（基于公开数据集和方法）。
  - 但跨域泛化实验仅训练了一个源域（SD V1.4），未进行多源训练或更广泛的交叉验证，可能存在偏差。
  - 缺陷分类仅提供一个简单基线，未与其他方法对比，略显单薄。

## 6. 论文的主要结论与发现

- ESIDE 在原始和困难样本上均达到 SOTA：平均准确率 98.91%（原始）、95.89%（困难），分别比基线平均提高 7.28% 和 15.10%。
- 跨域泛化表现良好，尤其在困难样本上具有竞争力。
- 鲁棒性优于最强基线（FreqNet、NPR、DRCT），平均准确率 80.63%。
- 消融表明：利用中间噪声时间步进行集成是关键，去除集成或使用全噪声/无噪声都会显著降低性能；高频峰值抑制会减少集成效果。
- 解释细化模块通过评分引导迭代，提高了解释的语义相似度、词汇多样性和信息密度（尽管困惑度略有上升）。

## 7. 优点

- **性能领先**：在多个设置下超越所有基线，尤其在困难样本上提升显著。
- **效率高**：仅需一次 DDIM 逆过程，无需重建，预处理时间减半。
- **可解释性强**：首次将合成图像检测与高质量解释结合，通过多标签缺陷分类、MLLM 生成、评分引导细化实现。
- **数据集贡献**：构建了 GenHard（更具挑战性）和 GenExplain（含缺陷类型与解释），促进后续研究。
- **鲁棒性好**：对常见扰动（模糊、旋转、亮度）具有良好抗性。

## 8. 不足与局限

- **实验覆盖**：跨域泛化仅训练了一个源域（SD V1.4），未测试其他源域作为训练集的情况；未在更广泛的数据集（如 DiffusionDB、CIFAKE 等）上评估，泛化能力结论有限。
- **偏差风险**：GenHard 基于 CBSID 的错误分类，可能引入选择偏差；GenExplain 的人工筛选可能遗漏某些缺陷类型或引入主观性。
- **缺陷分类基线弱**：仅提供一个简单 MLP 基线，未与现有方法（如直接使用 MLLM 进行分类）对比，且 mAP 和 EM 偏低（平均 37.55% 和 48.67%），说明任务本身具有挑战性，但论文未深入讨论。
- **解释细化依赖 MLLM**：使用 gpt-4o，但该模型可能产生幻觉，且需要多次 API 调用，成本高；细化的迭代次数固定为 3，未探索自适应停止条件。
- **算力细节缺失**：未完整报告 GPU 型号、总训练时长、分布式设置等，可复现性受限。
- **仅针对视觉检测**：未考虑其他模态（如文本、音频）或更深层的语义线索，应用范围有限。

（完）
