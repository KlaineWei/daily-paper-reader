---
title: Few-Shot Learner Generalizes Across AI-Generated Image Detection
title_zh: 小样本学习器泛化于AI生成图像检测
authors: "Shiyu Wu, Jing Liu, Jing Li, Yequan Wang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=uvU29AfoNT"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 利用小样本学习进行伪造图像检测，与伪造检测相关但无可解释性
tldr: "该论文针对AI生成图像检测中对未见模型泛化差且标注数据稀缺的问题，提出小样本检测器（FSD）。通过学习专门度量空间，仅需10个额外样本即可在GenImage数据集上平均准确率提升11.6%。但论文未涉及可解释性。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有伪造图像检测器对未见模型泛化差且数据收集困难。
method: 提出FSD，学习专门度量空间以区分未见伪造图像。
result: "仅需10个样本即在GenImage上提升11.6%平均准确率。"
conclusion: 实现了高效的少样本伪造检测，但无可解释性。
---

## Abstract
Current fake image detectors trained on large synthetic image datasets perform satisfactorily on limited studied generative models. However, these detectors suffer a notable performance decline over unseen models. Besides, collecting adequate training data from online generative models is often expensive or infeasible. To overcome these issues, we propose Few-Shot Detector (FSD), a novel AI-generated image detector which learns a specialized metric space for effectively distinguishing unseen fake images using very few samples. Experiments show that FSD achieves state-of-the-art performance by $+11.6\%$ average accuracy on the GenImage dataset with only $10$ additional samples. More importantly, our method is better capable of capturing the intra-category commonality in unseen images without further training. Our code is available at https://github.com/teheperinko541/Few-Shot-AIGI-Detector.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：当前AI生成图像（AIGI）检测器在已知生成模型上表现良好，但面对未见过的生成模型时性能显著下降。此外，为训练检测器而收集来自在线生成模型的充足标注数据往往昂贵或不可行。
- **核心问题**：如何让伪造图像检测器能够在仅使用极少样本的情况下，泛化到未见过的AI生成模型上，从而解决数据稀缺和模型泛化性差的双重挑战。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出小样本检测器（Few-Shot Detector, FSD），通过学习一个专门的度量空间（specialized metric space），利用极少量样本（文中为10个额外样本）来有效区分未见过的伪造图像。
- **关键技术细节**：
  - 该方法属于小样本学习（few-shot learning）范式，通过构建一个能够捕捉图像间“距离”的度量空间，使得真实图像与伪造图像在该空间中形成可分聚类。
  - 在推理时，仅需提供少数新类别（新生成模型）的样本作为支撑集（support set），即可通过最近邻或距离度量方式对未见过的伪造图像进行分类。
  - 无需对模型进行重新训练或微调，即可泛化到未见过的生成模型。
- **公式/算法流程（文字描述）**：文中未给出具体公式，但从摘要推断其流程为：训练阶段学习一个特征嵌入网络，通过对比学习或度量学习方法优化真实/伪造图像的特征表示；测试阶段，对每个新生成模型类别，给定少量标注样本（如10张伪造+真实），计算查询图像与支撑集样本的距离，根据最近邻原则判断真假。

## 3. 实验设计

- **数据集**：使用GenImage数据集（大规模AI生成图像基准，包含多个生成模型）。
- **Benchmark**：以GenImage上的平均准确率作为主要性能指标。
- **对比方法**：摘要称FSD达到“state-of-the-art performance”，但未列出具体对比的基线方法（如传统CNN检测器、基于频域的方法等）。由于信息不足，无法得知对比方法的完整列表。
- **场景**：评估在仅有10个额外样本（即few-shot设置）下的泛化能力，与基于大量训练数据的传统检测器对比。

## 4. 资源与算力

- **文中未明确说明**：未提及使用的GPU型号、数量、训练时长、显存消耗等具体算力信息。仅有开放代码链接（GitHub），可能代码库中包含运行环境说明，但基于给定文本无法获知。

## 5. 实验数量与充分性

- **实验数量**：摘要只报告了GenImage数据集上的平均准确率提升（+11.6%），未提及消融实验、跨数据集验证、不同样本数量影响、多种生成模型细粒度对比等。
- **充分性与公平性**：
  - 实验仅在一个数据集（GenImage）上报告结果，缺乏跨数据集的泛化验证。
  - 未提供与多种基线的详细比较，也未见统计显著性检验或误差分析。
  - 由于信息有限，无法判断实验是否充分、客观、公平。从学术规范角度看，仅摘要中的单一指标不足以充分验证方法的优势。

## 6. 主要结论与发现

- FSD在仅使用10个额外样本的情况下，在GenImage数据集上平均准确率比现有方法提升11.6%，实现了对未见生成模型的少样本泛化。
- 方法能够更好地捕捉未见图像中的类内共性（intra-category commonality），无需进一步训练即可适应新类别。

## 7. 优点

- **创新性**：将小样本学习范式引入AI生成图像检测，解决了传统检测器对未见模型泛化差的问题。
- **实用性**：仅需极少量标注样本（10张），大幅降低了数据收集成本，适应快速演变的生成模型。
- **高效性**：无需重新训练或微调网络，推理时可通过支撑集即插即用。
- **开源**：代码已公开，促进可复现性。

## 8. 不足与局限

- **缺乏可解释性**：论文未涉及模型决策的可解释性分析（如哪些特征用于区分真伪），元数据中也指出“no interpretability”。
- **实验覆盖不足**：仅在一个数据集（GenImage）上报告单一指标，未在多个数据集或真实场景中验证，泛化性有待进一步评估。
- **对比基线不明确**：未列出具体对比方法及它们的设置，无法判断公平性。
- **未讨论失败案例与鲁棒性**：对于复杂伪造（如添加噪声、压缩、混合模型）的场景未提及。
- **资源信息缺失**：未提供算力需求，可能对部署资源有限的应用不够透明。
- **潜在偏差风险**：支撑集样本的选择可能影响结果，未进行稳定性分析。

（完）
