---
title: "IMOL: Incomplete-Modality-Tolerant Learning for Multi-Domain Fake News Video Detection"
title_zh: IMOL：面向多领域假新闻视频检测的不完整模态容忍学习
authors: "Zhi Zeng, Jiaying Wu, Minnan Luo (罗敏楠), Herun Wan, Xiangzheng Kong, Zihan Ma, Guang Dai, Qinghua Zheng (郑庆华)"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1494.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 多领域假新闻检测但缺乏可解释性
tldr: 该论文针对现有假新闻视频检测方法仅针对单一领域且假设模态完整的问题，提出了IMOL（不完全模态容忍学习）框架，用于多领域假新闻视频检测。IMOL通过跨模态知识融合和模态缺失下的鲁棒学习，在构建的两个真实世界多领域基准上取得了优于现有方法的检测结果。然而，该方法并未在检测过程中提供可解释性分析，因此仅与可解释假检测需求存在间接关联，可作为可解释性研究的底层方法参考。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 769, \"height\": 1004, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 711, \"height\": 976, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 672, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 748, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 789, \"height\": 858, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 728, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1627, \"height\": 891, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 788, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 786, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1494/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 761, \"height\": 346, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1494/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 512, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1494/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 756, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1494/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 622, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1494/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 650, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1494/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 740, \"height\": 207, \"label\": \"Table\"}]"
motivation: 现有假新闻视频检测方法多针对单一领域且假设模态完整，无法应对真实场景中的多领域和不完整模态问题。
method: 提出IMOL框架，通过不完全模态容忍学习，融合跨模态知识实现多领域假新闻视频检测。
result: 在两个真实世界多领域基准上取得了优于现有方法的检测性能。
conclusion: 该工作为多领域假新闻检测提供了新思路，但未来需结合可解释性分析以提升可信度。
---

## Abstract
While recent advances in fake news video detection have shown promising potential, existing approaches typically (1) focus on a specific domain (e.g., politics) and (2) assume the availability of multiple modalities, including video, audio, description texts, and related images. However, these methods struggle to generalize to real-world scenarios, where questionable information spans diverse domains and is often modality-incomplete due to factors such as upload degradation or missing metadata. To address these challenges, we introduce two real-world multi-domain news video benchmarks that reflect modality incompleteness and propose IMOL, an incomplete-modality-tolerant learning framework for multi-domain fake news video detection. Inspired by cognitive theories suggesting that humans infer missing modalities through cross-modal guidance and retrieve relevant knowledge from memory for reference, IMOL employs a hierarchical transferable information integration strategy. This consists of two key phases: (1) leveraging cross-modal consistency to reconstruct missing modalities and (2) refining sample-level transferable knowledge through cross-sample associative reasoning. Extensive experiments demonstrate that IMOL significantly enhances the performance and robustness of multi-domain fake news video detection while effectively generalizing to unseen domains under incomplete modality conditions.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有假新闻视频检测方法存在两个主要局限：① 通常只针对特定领域（如政治），忽略了现实世界中新闻跨越多个领域（如灾害、金融、健康等）的复杂性；② 假设所有视频模态（视频、音频、文本、图像）均完整可用，但真实场景中常因上传退化、元数据丢失、设备故障等导致模态缺失。
- **研究意义**：亟需一种能够同时处理**多领域**和**不完整模态**的鲁棒检测方法，以提升模型在真实复杂环境中的泛化能力和实用性。

## 2. 论文提出的方法论

### 核心思想
受人类认知理论启发：人类可以通过已有模态推断缺失模态（跨模态引导），并通过检索记忆中相似经验进行关联推理。IMOL 模拟这一过程，实现不完整模态下的鲁棒检测。

### 关键技术细节
- **模态特征编码**：使用 BERT（文本）、VGG19（图像）、C3D（视频）、VGGish（音频）分别提取特征，缺失模态用零向量填充。
- **域信息编码**：设计域单元（Domain Units）和域移表示（Domain-shift Representation），捕捉域相关性和跨域信息。
- **跨模态一致性学习（MCL）**：通过残差自编码器（Residual Autoencoder）将完整模态特征映射到共享语义空间，重建缺失模态的特征，最小化原始与重建特征的均方根误差。
- **检索增强对比学习（RACL）**：从批次中选取**正样本**（同标签语义最相似）和**硬负样本**（异标签语义最相似），通过对比损失增强跨样本一致性，提升对不完整模态的判别能力。
- **最终分类**：使用混合专家（MoE）策略整合样本特征、域特定特征和域移特征，通过 Transformer 和 MLP 输出真假预测。

### 损失函数
整体优化目标：\( L_f = \alpha L_{MCL} + \beta L_{RACL} + L_C \)，其中 \( L_{MCL} \) 为模态一致性损失，\( L_{RACL} \) 为对比损失，\( L_C \) 为交叉熵分类损失。

## 3. 实验设计

### 数据集与场景
- **FakeSV_IM**：基于中文 FakeSV 构建，包含 9 个领域（灾害、社会、健康、娱乐、政治、科学、军事、教育、金融），样本总数为 3624（1810 假 + 1814 真），引入 15 种缺失模态模式，缺失率从 0 到 0.7 测试。
- **FakeTT_IM**：基于英文 FakeTT 构建，样本总数为 1991（1172 假 + 819 真），同样包含 9 个领域和多种缺失模式。
- **Domain Generalization**：从上述数据集中抽取出常见域（Ch-6/En-6）作为训练集，稀有域（Ch-3/En-3）作为测试集，评估跨域泛化能力。
- **Temporal Analysis**：按视频发布时间 8:2 划分训练/测试，评估时间泛化性。

### Benchmark & 对比方法
- 对比方法：TikTec、FANVM、SV-FEND、MMVD、MoMKE（均为多模态假新闻检测基线）。
- 额外对比：GPT-3.5-turbo 和 GPT-4V（零样本设置）。
- 所有基线采用相同特征和随机种子，确保公平。

## 4. 资源与算力

- **GPU 型号**：NVIDIA 3090Ti（论文仅提及“experiments were conducted on NVIDIA 3090Ti GPUs”）。
- **未明确说明**：GPU 数量、训练时长、总计算量（FLOPS 和参数量在表2中给出，但仅作复杂度对比，未提及实际训练开销）。
- 总体而言，论文**未提供完整的算力资源细节**。

## 5. 实验数量与充分性

### 实验数量
- **主实验**（表1）：在两大数据集上，对比 5 种基线，缺失率从 0 到 0.7 共 8 种设置，报告 ACC 和 F1。
- **计算复杂度**（表2）：参数量、FLOPs 对比。
- **消融实验**（表3）：移除 Domain、MCL、RACL 三种组件。
- **领域泛化**（图8）：两组跨域测试（Ch-3/En-3）。
- **时间分析**（图9）：时间顺序划分下的性能对比。
- **LLM 对比**（表4）：GPT-3.5、GPT-4V 零样本测试。
- **参数分析**（图10）：硬负样本数量 n 的影响。

### 充分性评价
- **充分**：覆盖了不同缺失率、消融、跨域泛化、时间泛化、大模型对比、超参数敏感性，实验维度全面。
- **公平性**：明确声明对基线使用相同特征和随机种子，采用五折交叉验证。
- **潜在不足**：未在更多真实噪声模态（如自然缺失而非随机丢弃）上测试；领域标注可能存在主观性；未见基于人类标注的验证。

## 6. 论文的主要结论与发现

1. IMOL 在所有缺失率设置下均显著优于现有方法，尤其在 0.7 高缺失率下仍保持较高准确率（FakeSV_IM 上 ACC 77.19%，FakeTT_IM 上 ACC 79.23%）。
2. 消融实验表明域信息、跨模态一致性学习和检索增强对比学习均不可或缺，其中域信息最敏感。
3. 领域泛化实验中，IMOL 在稀有域上的 ACC 和 F1 比次优方法约高 2-5 个百分点，证明其跨域迁移能力。
4. 时间泛化分析显示 IMOL 比基线提升约 2-4 个百分点，具有更好的时序鲁棒性。
5. 与 GPT-3.5/4V 对比，IMOL 在零样本设置下仍大幅领先（En-3 上 ACC 高出 13%），说明专用小型模型在特定任务上性能更强。

## 7. 优点

- **任务创新**：首次系统研究**多领域 + 不完整模态**的假新闻视频检测，构建两个真实基准。
- **方法新颖**：灵感来自认知理论，将跨模态重建与跨样本推理有机结合，框架可解释性强。
- **实验全面**：覆盖多种缺失率、消融、域泛化、时间泛化、LLM 对比，验证充分。
- **实用性强**：模型参数量与主流方法相当（约 760M），计算复杂度可接受。
- **代码开源**：提供了 GitHub 仓库链接，有利于后续研究。

## 8. 不足与局限

- **检索质量依赖**：检索增强对比学习依赖批次内样本相似度，不同批次或小批次下可能引入噪声，影响稳定性。
- **极端预测风险**：极小预测分数可能导致大量零值，增加过拟合或梯度消失风险（论文在局限性中提到）。
- **缺失模式模拟简单**：仅采用随机丢弃模拟缺失，未覆盖视频质量退化、传感器噪声等真实复杂缺失情况。
- **域标注粒度**：领域标签为人工标注，可能存在模糊或重叠（如社会与政治），未来可考虑自动域发现。
- **未涉及可解释性**：模型作为黑盒，未提供检测理由，不适合需要解释的高风险场景（如新闻事实核查）。
- **大模型对比限制**：GPT-3.5/4V 使用零样本提示，未进行微调或有监督适配，对比不够直接。

（完）
