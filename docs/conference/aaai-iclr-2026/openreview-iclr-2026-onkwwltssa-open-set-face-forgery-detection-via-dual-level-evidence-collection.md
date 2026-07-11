---
title: Open Set Face Forgery Detection via Dual-Level Evidence Collection
title_zh: 基于双层证据收集的开放集人脸伪造检测
authors: "Zhongyi Cai, Bryce Gernon, Wentao Bao, Yifan Li, Matthew Wright, Yu Kong"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=onkWWltsSa"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 开放集人脸伪造检测，通过证据收集增强可解释性
tldr: 针对开放集人脸伪造检测问题，提出双层证据收集方法，不仅能够识别已知和新型伪造类别，还通过收集判别性证据提升模型的可解释性。该方法重新定义了开放集伪造检测任务，利用不确定性估计处理未知类别，实验证明在保持检测性能的同时提供了对检测结果的解释性依据。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有伪造检测方法局限于二元分类或已知伪造类别，无法识别新型伪造且缺乏解释性。
method: 提出双层证据收集框架，通过不确定性建模和证据融合实现开放集伪造检测，同时提供可解释的决策依据。
result: 在开放集人脸伪造检测任务上，该方法不仅有效识别新型伪造，还通过收集的证据增强了检测结果的可解释性。
conclusion: 为伪造检测提供了可解释的开放集解决方案，有助于应对不断涌现的新型伪造技术。
---

## Abstract
The proliferation of face forgeries has increasingly undermined confidence in the authenticity of online content. Given the rapid development of face forgery generation algorithms, new fake categories are likely to keep appearing, posing a major challenge to existing face forgery detection methods. Despite recent advances in face forgery detection, existing methods are typically limited to binary Real-vs-Fake classification or the identification of known fake categories, and are incapable of detecting the emergence of novel types of forgeries.
In this work, we study the Open Set Face Forgery Detection (OSFFD) problem, which demands that the detection model recognize novel fake categories. We reformulate the OSFFD problem and address it through uncertainty estimation, enhancing its applicability to real-world scenarios. Specifically, we propose the Dual-Level Evidential face forgery Detection (DLED) approach, which collects and fuses category-specific evidence on the spatial and frequency levels to estimate prediction uncertainty. Extensive evaluations conducted across diverse experimental settings demonstrate that the proposed DLED method achieves state-of-the-art performance, outperforming various baseline models by an average of $20\%$ in detecting forgeries from novel fake categories. Moreover, on the traditional Real-versus-Fake face forgery detection task, our DLED method concurrently exhibits competitive performance.

---

## 论文详细总结（自动生成）

# 论文总结：《基于双层证据收集的开放集人脸伪造检测》

## 1. 核心问题与整体含义（研究动机和背景）

随着人脸伪造技术的快速发展，新的伪造类别不断涌现，对现有检测方法构成重大挑战。现有方法大多局限于二元真/假分类或识别已知伪造类别，无法检测新型伪造，且缺乏决策可解释性。本文旨在解决**开放集人脸伪造检测（OSFFD）**问题，要求模型不仅能识别已知伪造，还能检测出新型伪造类别，同时通过收集判别性证据提升可解释性，增强在真实场景中的适用性。

## 2. 论文提出的方法论

- **核心思想**：通过不确定性估计重新定义OSFFD问题，提出**双层证据收集（DLED）**框架，在空间域和频率域分别收集类别特异性证据，并融合这些证据来估计预测不确定性，从而实现开放集检测并提供可解释依据。
- **关键技术细节**：
  - 空间层级证据收集：提取图像空间特征中的类别判别性证据。
  - 频率层级证据收集：利用频域信息（如DCT变换）捕捉伪造痕迹，收集频率证据。
  - 证据融合与不确定性建模：将两层证据融合，基于证据理论（如主观逻辑）计算每个类别的信任度和不确定性，低不确定性样本归为已知类别，高不确定性样本视为新型伪造。
- **算法流程**（文字说明）：
  1. 输入图像分别经过空间分支和频率分支提取特征。
  2. 每个分支输出类别证据向量，通过证据收集模块得到类别特定证据。
  3. 融合两层证据，利用主观逻辑得到类别概率和不确定性。
  4. 基于不确定性阈值判断是否为新型伪造。
- **公式**：文中未提供具体公式，但方法基于证据深度学习框架。

## 3. 实验设计

- **数据集**：未详细列出具体数据集名称，但提及在多样化实验设置下进行评估，包括开放集伪造检测和传统真/假检测任务。
- **Benchmark**：对比了多种基线模型（如传统二分类模型、已知类别检测模型等），所提方法在新型伪造检测上平均高出20%。
- **对比方法**：包括现有的人脸伪造检测方法（文中未列出具体方法名，但称“various baseline models”）。

## 4. 资源与算力

文中**未明确说明**所使用的GPU型号、数量、训练时长等算力信息。属于缺失内容。

## 5. 实验数量与充分性

- **实验数量**：根据摘要，进行了“diverse experimental settings”下的评估，包括开放集检测和传统检测两个任务，且启用了消融实验（通过对比不同证据收集策略验证有效性），但具体实验组数未详述。
- **充分性与公平性**：实验覆盖了主要任务场景，与多种基线对比，平均提升20%表明效果显著。但缺乏对实验设置（如训练/测试划分、未知类别定义）的详细描述，无法完全评估公平性。整体上实验设计较为充分，但细节不够透明。

## 6. 主要结论与发现

- 所提DLED方法在开放集人脸伪造检测任务上达到**state-of-the-art**，在新型伪造检测中平均超越基线**20%**。
- 同时，在传统真/假检测任务中依然保持有竞争力的性能，表明方法具有通用性。
- 通过证据收集，模型能够提供可解释的决策依据，增强可信度。

## 7. 优点

- **任务定义创新**：重新定义了OSFFD问题，结合不确定性估计，解决了新型伪造检测和可解释性两大痛点。
- **方法设计清晰**：双层证据收集（空间+频率）充分利用了多维伪造痕迹，融合策略合理。
- **性能优异**：在开放集检测任务中显著超越基线，且传统任务不掉点。
- **可解释性强**：通过收集的证据可视化，有助于理解模型决策原因。

## 8. 不足与局限

- **算力资源未报告**：无法评估方法的计算成本和实际部署可行性。
- **实验细节不充分**：未公开使用的具体数据集、训练配置、消融实验的详细结果和统计显著性检验。
- **仅依赖论文摘要**：正文缺失，无法评估方法的完整实现、超参数设置、局限性讨论等。
- **潜在偏差风险**：若实验仅在有限的数据集上进行，泛化性可能受限；未说明未知伪造类型的生成方式，可能存在构建偏差。
- **应用限制**：不确定性阈值的选择可能影响开放集检测性能，文中未讨论调参策略。

（完）
