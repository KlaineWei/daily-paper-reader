---
title: Structure-adaptive Adversarial Contrastive Learning for Multi-Domain Fake News Detection
title_zh: 结构自适应对抗对比学习用于多领域假新闻检测
authors: "Lingwei Wei, Dou Hu, Wei Zhou, Philip S. Yu, Songlin Hu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.505.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 多领域假新闻检测方法，与伪造检测主题相关
tldr: 针对多领域假新闻检测中领域适应性不足的问题，提出结构自适应对抗对比学习框架StruACL，通过对比表示和对抗训练实现跨域结构知识迁移。实验表明该方法在多个领域上显著提升检测性能，尤其在数据稀缺条件下表现突出。该工作为多源伪造检测提供了有效范式。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.505/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1395, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.505/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1301, \"height\": 774, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.505/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 697, \"height\": 890, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.505/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1541, \"height\": 478, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1646, \"height\": 338, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1363, \"height\": 499, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1556, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1641, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 796, \"height\": 307, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 799, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1374, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.505/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1631, \"height\": 312, \"label\": \"Table\"}]"
motivation: 现有模型跨域泛化能力差，数据受限时尤甚。
method: 构建对比表示和对抗训练实现结构知识迁移。
result: 在多个假新闻数据集上取得最优结果，尤其小样本场景。
conclusion: 结构自适应对抗对比学习有效提升跨域检测鲁棒性。
---

## Abstract
The rapid proliferation of fake news across multiple domains poses significant threats to society. Existing multi-domain detection models typically capture domain-shared semantic features to achieve generalized detection. However, they often fail to generalize well due to poor adaptability, which limits their ability to provide complementary features for detection, especially in data-constrained conditions. To address these challenges, we investigate the propagation-adaptive multi-domain fake news detection paradigm. We propose a novel framework, Structure-adaptive Adversarial Contrastive Learning (StruACL), to adaptively enable structure knowledge transfer between multiple domains. Specifically, we first contrast representations between content-only and propagation-rich data to preserve structural patterns in the shared representation space. Additionally, we design a propagation-guided adversarial training strategy to enhance the diversity of representations. Under the StruACL objective, we leverage a unified Transformer-based and graph-based model to jointly learn transferable semantic and structural features for detection across multiple domains. Experiments on seven fake news datasets demonstrate that StruACL-TGN achieves better multi-domain detection performance on general and data-constrained scenarios, showing the effectiveness and better generalization of StruACL.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义
- **研究动机**：假新闻在多领域快速传播对社会构成严重威胁。现有多领域检测模型通常只捕获领域共享的语义特征，但泛化能力差，尤其在数据受限（低资源）条件下，模型难以提供互补的检测特征。
- **整体含义**：论文研究了一种新的“传播自适应多领域假新闻检测范式”，旨在同时利用含有传播结构的域和仅有文本内容的域，提升跨域检测的泛化能力。

## 2. 方法论：核心思想、关键技术、算法流程
- **核心思想**：通过结构自适应对抗对比学习（StruACL），在共享表示空间中保留并迁移传播结构知识，同时增强表示的多样性。
- **关键技术**：
  - **结构感知对比学习（StruCL）**：对含有传播结构的样本和仅有内容样本的表示进行对比，强制拉大不同结构类型样本的距离，同时保持同类型样本的紧凑性，从而在共享空间中保留结构模式。
  - **传播引导对抗训练（PAT）**：采用快速梯度法（FGM）在嵌入层添加对抗扰动，生成最坏情况样本。对原始样本和对抗样本同时施加分类与对比损失，增强表示鲁棒性。
  - **模型架构（TGN）**：共享的Transformer（多语言BERT）编码语义，图神经网络（GNN）编码传播图结构；混合分类器由域特定和域共享分类器组成，最终预测为两者输出的平均。
- **算法流程**：
  1. 对每条新闻，若存在传播图G，则通过GNN提取结构特征；否则仅用Transformer提取语义表示。
  2. 计算分类损失L_CLS（跨域交叉熵）和结构对比损失L_StruCL。
  3. 对原始样本生成对抗扰动，计算对抗样本的分类损失L_r-adv_CLS和对比损失L_r-adv_StruCL。
  4. 总损失 L_total = L_CLS + L_StruCL + L_r-adv_CLS + L_r-adv_StruCL。

## 3. 实验设计：数据集、Benchmark、对比方法
- **数据集**：7个公开假新闻数据集，覆盖中、英、阿拉伯、粤语，包含纯文本和带传播结构的样本。
  - 纯文本：Weibo21（中文）、Covid19（英文）
  - 含传播结构：Twitter（英文）、TwitterCovid19、WeiboCovid19、Arabic、Cantonese
- **Benchmark**：
  - **CrossEval**：3个域（Weibo21、Twitter、WeiboCovid19），跨平台跨事件。
  - **CovidEval**：5个域（Covid19、WeiboCovid19、TwitterCovid19、Arabic、Cantonese），同事件COVID-19。
- **对比方法**：共9种。
  - 纯内容方法：XLM-RoBERTa、EANN、MDFEND、M3FEND、FADED
  - 传播方法：GCNFN、BiGCN、SAT-TGN、UCLR-TGN
- **评估指标**：Accuracy（Acc）、Macro-F1，并报告相对XLM-RoBERTa的F1平均改进Δp。
- **统计显著性**：对最优结果进行t检验（p<0.05）。

## 4. 资源与算力
- 明确说明：所有实验在单张NVIDIA Tesla A100 80GB显卡上运行。
- **未提及**训练时长、模型参数量（除表6提到约265MB）、总实验耗时等细节。

## 5. 实验数量与充分性
- **实验组数**：
  - 总体性能 × 2个Benchmark（表2）
  - 细粒度跨域结果（表3、4）
  - 成对域迁移实验（表5：4种组合，每种含4个对比方法）
  - 低资源数据集单任务对比（表6：3个低资源域 vs 4个基线）
  - 消融实验（表7：7种变体，分别在2个Benchmark上）
  - 数据受限泛化实验（图4：5种训练比例）
  - 传播结构影响分析（图3：移除特定域传播结构后的效果）
- **充分性评价**：实验覆盖全面，同时包含同构/异构域、全量/低资源、结构有无等场景；消融组设计合理；使用统计显著性检验，结果客观公平。

## 6. 主要结论与发现
- StruACL-TGN在CrossEval上平均F1达89.25%（Δp = +2.42%），在CovidEval上达81.38%（Δp = +10.12%），显著优于所有基线。
- 结构知识对多领域检测至关重要：移除传播结构后所有域性能下降；特别是来自WeiboCovid19的传播特征对Twitter检测提升最大。
- 在数据受限条件下（训练集比例20%~80%），StruACL始终优于对比方法，展示了强的泛化能力。
- 消融实验证实结构对比学习（StruCL）和对抗训练（PAT）均不可或缺，联合使用效果最佳。

## 7. 优点
- **方法创新**：首次明确提出“传播自适应”多领域假新闻检测范式，系统设计了结构对比与对抗训练相结合的目标，有效弥合语义与结构表示之间的鸿沟。
- **实验严谨**：涵盖7个数据集、9种对比方法、多个消融变体、数据稀缺模拟、结构重要性分析，验证充分。
- **跨语言泛化**：采用多语言BERT，在英语、中文、阿拉伯语、粤语上均取得提升。
- **低资源友好**：在仅数百样本的低资源域上，StruACL依然优于单任务模型，展示出良好的迁移能力。

## 8. 不足与局限
- **模态局限**：仅考虑文本和传播图结构，未涉及图像、视频等多模态信息（作者在Limitations中明确提及）。
- **数据集差异**：不同域样本量极不均衡（如WeiboCovid19仅411条），可能导致训练不稳定或过拟合风险。
- **计算资源报告不完整**：未提供训练时间、参数搜索成本等，影响可复现性。
- **语言覆盖有限**：虽涉及四语，但低资源语言（阿拉伯语、粤语）样本量极小，结果可能受偶然性影响。
- **未分析偏差**：未探讨模型对特定平台或事件的偏见，实际部署可能存在公平性问题。

（完）
