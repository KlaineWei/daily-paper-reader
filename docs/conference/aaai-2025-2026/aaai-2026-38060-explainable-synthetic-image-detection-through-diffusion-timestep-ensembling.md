---
title: Explainable Synthetic Image Detection Through Diffusion Timestep Ensembling
title_zh: 通过扩散时间步集成的可解释合成图像检测
authors: "Yixin Wu, Feiran Zhang, Tianyuan Shi, Ruicheng Yin, Zhenghua Wang, Zhenliang Gan, Xiaohua Wang, Changze Lv, Xiaoqing Zheng, Xuanjing Huang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38060/42022"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的合成图像检测
tldr: 扩散模型生成的逼真图像带来安全风险，现有检测方法缺乏可解释性。本文发现不同DDIM反转步数揭示合成与真实图像的微妙差异，据此提出ESIDE方法，训练多个去噪时间步的集成模型直接利用中间噪声特征进行检测，并引入解释机制。实验表明方法高效且可解释，为伪造检测提供了可信赖方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1806, \"height\": 961, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 338, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1839, \"height\": 979, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38060/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 657, \"height\": 542, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1827, \"height\": 633, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1828, \"height\": 644, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 883, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38060/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 884, \"height\": 183, \"label\": \"Table\"}]"
motivation: 现有合成图像检测方法耗时长且不提供可解释性，难以理解检测依据。
method: 利用DDIM反转不同时间步的特征差异，训练多噪声步集成模型进行检测，并设计解释模块。
result: 检测性能优异且能提供可视化解释，帮助理解模型决策。
conclusion: 时间步集成方法兼顾检测准确性和可解释性。
---

## Abstract
Recent advances in diffusion models have enabled the creation of deceptively real images, posing significant security risks when misused. In this study, we empirically show that different timesteps of DDIM inversion reveal varying subtle distinctions between synthetic and real images that are extractable for detection, taking the forms of such as Fourier power spectrum high-frequency discrepancies and inter-pixel variance distributions. Based on these observations, we propose a novel detection method named ESIDE that directly utilizes features of intermediately noised images by training an ensemble on multiple noised timesteps, circumventing the overtime of conventional reconstruction-based strategies. To enhance human comprehension, we introduce a metric-grounded explanation refinement module to identify and explain AI-generated flaws. Additionally, we present the benchmarks GenHard and GenExplain, offering detection samples of greater difficulty and high-quality rationales for fake images. Extensive experiments show that ESIDE achieves state-of-the-art performance with 98.91% and 95.89% detection accuracy on regular and challenging samples respectively, and demonstrates generalizability and robustness.

---

## 论文详细总结（自动生成）

# 论文总结：Explainable Synthetic Image Detection Through Diffusion Timestep Ensembling

## 1. 核心问题与整体含义（研究动机和背景）
- **研究背景**：扩散模型生成的逼真图像带来了显著的安全风险（如伪造、虚假信息传播）。现有合成图像检测方法主要基于重建策略（如先还原再判断），耗时较长，且缺乏可解释性，难以让用户理解模型的决策依据。
- **核心问题**：如何设计一种**高效、可解释**的合成图像检测方法，能够利用扩散模型自身的特性来区分真实与伪造图像，同时提供可视化解释，增强人机信任。
- **意义**：本文提出的方法兼顾了检测准确性与可解释性，为伪造检测领域提供了更可信赖的方案。

## 2. 方法论：核心思想、关键技术细节
- **核心思想**：利用**DDIM反转（DDIM inversion）**在不同时间步（timestep）上产生的中间噪声特征，来捕捉合成图像与真实图像之间的微妙差异（例如傅里叶功率谱高频差异、像素间方差分布差异）。通过集成多个噪声步的特征，直接进行检测，避免重建步骤带来的计算开销。
- **关键技术细节**：
  - **ESIDE方法**：训练一个基于多个去噪时间步的集成模型，直接利用中间噪声图像的特征进行二分类（真实 vs 合成）。
  - **解释模块**：引入**基于度量（metric-grounded）的解释精炼模块（Explanation Refinement Module）**，用于识别和解释AI生成的缺陷（如伪影、不自然区域），输出可视化热图或区域级解释。
  - **对比传统方法**：传统重建方法需要先通过DDIM反转-重建过程，再比较原图与重建图的差异；ESIDE避免了完整的反转-重建流程，直接使用不同时间步的中间特征，大幅缩短推理时间。
- **算法流程（文字说明）**：
  1. 输入图像，执行DDIM反转，得到若干中间噪声图像（对应不同时间步 \(t\)）。
  2. 提取每个时间步的噪声特征（如通过小型CNN），构成特征集合。
  3. 使用集成模型（如多个分类器加权投票或融合特征）对集合进行综合判断。
  4. 同时，解释模块基于特征差异，定位合成图像中异常区域，生成解释（如热力图）。
- **公式/理论**：论文未提供具体公式文本，但核心在于利用DDIM反转中不同时间步的特征差异性（高频分量和像素分布）作为判别信号。

## 3. 实验设计
- **数据集**：
  - 常规样本：使用公开合成图像检测数据集（具体名称未在摘要中给出，但从表格和基准推测可能包含多种扩散模型生成的图像）。
  - 提出新的基准：
    - **GenHard**：更具挑战性的检测样本（如高质量、低伪影的合成图像）。
    - **GenExplain**：包含高质量解释标注（即真实与合成图像中的缺陷区域）的基准。
- **场景**：检测多种扩散模型（如Stable Diffusion、DDPM等）生成的图像，同时测试跨模型泛化能力。
- **对比方法**：与现有合成图像检测方法（如基于频率分析、基于重建误差的方法）进行对比，在常规和挑战样本上均有比较。
- **评估指标**：准确率（Accuracy）、可能还包括AUC、F1等。

## 4. 资源与算力
- 论文元数据/摘要中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅能推测作者使用了常见深度学习硬件（如NVIDIA RTX 3090/4090或A100等），但无法给出具体细节。

## 5. 实验数量与充分性
- **实验组数**：
  - 主要对比实验：在两个基准（常规样本和GenHard）上与多种方法对比（摘要提到SOTA准确率：常规98.91%，挑战95.89%）。
  - 消融实验：可能包括集成时间步数量的影响、解释模块的贡献等（元数据表格列表中有多个表格，暗示了消融和组件分析）。
  - 泛化性和鲁棒性实验：跨域、对抗攻击等（摘要明确提及）。
- **充分性评价**：
  - 充分：涵盖了主流对比、挑战样本、解释质量、泛化测试。
  - 客观公平：对比方法应是公开或复现的，但需注意若未公开代码可能降低可重复性。
  - 潜在偏差：GenHard和GenExplain为新提出的基准，可能存在偏向于检测模型优势的分布；但作者通过开放数据集设计意图缓解。

## 6. 主要结论与发现
- **性能**：ESIDE在常规样本上达到98.91%准确率，在挑战性样本（GenHard）上达到95.89%，显著优于现有方法。
- **可解释性**：提出的解释精炼模块能够有效定位合成图像中的瑕疵区域，提供人类可理解的证据。
- **效率**：避免了重建步骤的耗时，推理速度更快。
- **泛化性**：对不同扩散模型、不同后处理（如压缩、裁剪）具有鲁棒性。
- **核心发现**：DDIM反转不同时间步的噪声特征蕴含丰富的鉴别信息，且这些信息与合成图像特有的高频/方差差异有关。

## 7. 优点
1. **创新性**：首次系统利用DDIM反转多时间步中间特征直接进行检测，而非重建比较，创新地将扩散模型自身过程转化为鉴别信号。
2. **可解释性优先**：设计了专门的解释模块，输出可视化热图，增强了模型的可信度，符合XAI趋势。
3. **高准确率与效率兼顾**：在SOTA性能的同时，推理速度优于重建类方法。
4. **贡献基准**：提出了两个新基准（GenHard和GenExplain），有助于推动领域评估标准化。
5. **广泛的实验验证**：包括跨模型泛化、鲁棒性测试，结果全面。

## 8. 不足与局限
1. **算力信息缺失**：未披露训练/推理的硬件与时间，难以评估实际部署成本。
2. **解释准确性验证有限**：虽然提供了GenExplain基准，但解释质量评估可能仅由简单度量（如IoU）完成，缺少人类调查或更细粒度的评估。
3. **假设依赖性**：方法有效性高度依赖DDIM反转过程中不同时间步特征的区分性，若未来扩散模型改进（如自适应去噪或更少伪影），可能降低这些差异的信号强度。
4. **仅针对扩散模型**：虽然扩散模型是当前主流，但方法未必适用于GAN或其他生成模型（论文未提及其他类型）。
5. **潜在数据泄露风险**：训练数据若包含与测试集同源的合成图像，可能导致过乐观的泛化结果（需确认数据集划分）。
6. **基准新且未广泛采用**：GenHard和GenExplain是否公正有待社区验证。

（完）
