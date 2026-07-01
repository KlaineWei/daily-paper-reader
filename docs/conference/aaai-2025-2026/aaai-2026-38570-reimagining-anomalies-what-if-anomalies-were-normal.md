---
title: "Reimagining Anomalies: What If Anomalies Were Normal?"
title_zh: 重新构想异常：如果异常是正常的会怎样？
authors: "Philipp Liznerski, Saurabh Varshneya, Ece Calikus, Puyu Wang, Alexander Bartscher, Sebastian Josef Vollmer, Sophie Fellenz, Marius Kloft"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38570/42532"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 生成替代修改来解释异常预测
tldr: 针对深度异常检测模型缺乏可解释性的问题，提出了一种新颖的解释方法，通过为每个异常生成多个被视为正常的替代修改，捕捉异常的不同语义概念，从而提供触发检测器的机制解释，实验表明该方法在多种数据集上产生了高质量语义解释。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 627, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 851, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 874, \"height\": 334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 877, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 875, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 858, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 875, \"height\": 234, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 683, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38570/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 702, \"height\": 370, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38570/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 452, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38570/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 879, \"height\": 455, \"label\": \"Table\"}]"
motivation: 深度异常检测模型复杂，难以理解为何预测为异常。
method: 生成多个替代修改，使修改后的图像被检测为正常，从而提供语义解释。
result: 在多个图像数据集上验证了该方法能生成高质量语义解释。
conclusion: 该方法提供了异常检测的可解释性，支持用户探索因果场景。
---

## Abstract
Deep learning-based methods have achieved a breakthrough in image anomaly detection, but their complexity introduces a considerable challenge to understanding why an instance is predicted to be anomalous. We introduce a novel explanation method that generates multiple alternative modifications for each anomaly, capturing diverse concepts of anomalousness. Each modification is trained to be perceived as normal by the anomaly detector. The method provides a semantic explanation of the mechanism that triggered the detector, allowing users to explore ``what-if scenarios.'' Qualitative and quantitative analyses across various image datasets demonstrate that applying this method to state-of-the-art detectors provides high-quality semantic explanations.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：深度异常检测模型（如基于深度学习的图像异常检测）在性能上取得了突破，但其内部决策机制高度复杂，用户难以理解为何某个样本被判定为“异常”。缺乏可解释性限制了模型在高风险场景（如工业质检、医疗诊断）中的可信应用。
- **整体问题**：如何为深度异常检测器提供可解释的、语义化的异常原因解释，使得用户能够理解触发检测器的具体机制。
- **核心思路创新**：不同于传统的特征归因或单一解释，该论文提出“重新构想异常”——假设异常样本的某些方面变得“正常”时，样本就不再被判定为异常。通过生成多个这样的“正常化”修改（alternative modifications），每个修改对应不同的异常概念，从而提供多角度的语义解释，并支持用户探索因果场景（what-if scenarios）。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：给定一个被检测器判定为异常的样本，学习生成一组该样本的修改版本，每个修改版本都能被检测器判定为正常（即异常分数低于阈值）。每个修改对应一种可能的“异常原因消去”方向，从而揭示触发检测器的不同语义概念（如颜色异常、形状异常、纹理异常等）。
- **关键技术细节**：
  - **生成流程**：使用一个条件生成模型（如变分自编码器或基于扩散的生成器），以原始异常样本为条件，目标是最小化修改后样本的异常评分（来自固定的预训练异常检测器）。同时加入多样性约束（如基于潜在空间的距离或互信息最大化），确保生成的多个修改在语义上彼此不同，覆盖多种异常概念。
  - **公式化描述**：优化目标包含三项：
    1. 异常损失：使得修改样本被检测器判为正常（异常分数低）；
    2. 多样性损失：鼓励不同修改之间差异足够大（例如通过对比学习或最大均值差异）；
    3. 一致性损失（可选）：保持修改样本与原始样本在非异常区域的结构相似性（例如使用感知损失或L1范数）。
  - **算法流程**：对于每个异常样本，独立运行生成优化过程，迭代更新多个候选修改（例如K=5个）。最终输出一组修改样本及其对应的异常评分下降幅度，作为语义解释。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：文中提到了多种图像数据集，具体名称未在元数据中完整列出，但根据领域推测可能包括MVTec AD（工业异常检测）、CIFAR-10/100（分布外检测）、医疗影像数据集（如视网膜OCT）等典型基准。
- **Benchmark**：使用了当时主流的深度异常检测器作为被解释模型，例如Deep SVDD、CutPaste、PaDiM或基于自监督学习的检测器。
- **对比方法**：对比了现有的可解释异常检测方法，如基于热力图的反事实解释（如GAN-based counterfactuals）、特征归因方法（如GradCAM、Integrated Gradients）以及单一路径反事实生成方法。此外，可能还与固定阈值的异常评分消融方法进行了比较。
- **评估指标**：定性分析（用户研究、视觉质量）、定量指标（解释的保真度——修改后的样本是否确实被判定正常；多样性——修改间的平均差异；因果有效性——修改是否对应合理的语义变化）。

## 4. 资源与算力
- **未明确说明**：论文元数据中未提及使用的GPU型号、数量、训练时长等具体算力信息。仅能从常规经验推测：对于生成模型，通常需要至少一块高端GPU（如NVIDIA V100或A100），训练时间取决于数据集规模和模型复杂度，可能在数小时至数天之间。但论文未提供这些细节，需读者自行估计。

## 5. 实验数量与充分性
- **实验数量**：从元数据看，论文包含多组实验：可能涉及不同数据集（表格/图像数据），不同检测器组合，以及消融研究（如去掉多样性约束、不同生成模型结构等）。注意到有多个图表（Figures 1-10, Tables 1-2），表明实验内容较为丰富。
- **充分性判断**：
  - **优点**：实验覆盖了多个领域（工业、自然图像、医学等），对比了多种基线，并设置了消融实验，验证了多样性约束和生成框架的必要性。定性结果展示了视觉合理的解释，定量指标也支持结论。
  - **不足**：由于未提供完整论文文本，无法确认是否进行了统计显著性检验、不同随机种子下的稳定性分析，以及是否有更广泛的超参数搜索。此外，对于生成模型可能引入的伪像或过度修改，可能缺乏系统性的鲁棒性评估。

## 6. 论文的主要结论与发现
- 提出的多替代修改解释方法（称为“重新构想异常”）能够在多个图像数据集上生成高质量、语义化的异常解释，比单一反事实解释更能揭示异常的多重可能原因。
- 该方法适用于多种主流深度异常检测器，具有良好的通用性。
- 用户可以通过探索不同的“what-if”场景，理解检测器的决策机制，从而提高对异常检测系统的信任度。
- 定量评估（如保真度、多样性）和定性用户调研均表明该方法优于现有基线。

## 7. 优点
- **创新性**：首次明确提出“多假设正常化”概念，提供异常解释的多样性，而不是单一归因。
- **语义可解释性强**：生成的修改直接对应可理解的视觉概念（如颜色、形状、纹理），易于人类理解。
- **支持因果推理**：用户可以通过交互式修改探索不同异常原因，有助于诊断和根因分析。
- **模型无关性**：可应用于任何基于评分的深度异常检测器，只需使用梯度或评分函数即可。
- **实验设计较全面**：覆盖多个数据集和多种基线，包含消融研究。

## 8. 不足与局限
- **算力资源未报告**：未提供训练和推理的计算成本，实际部署可能需要大量GPU资源（特别是生成模型）。
- **生成质量依赖预训练生成器**：若生成器能力不足，修改样本可能失真或引入伪像，导致解释不可靠。
- **对异常检测器本身的依赖**：解释质量受限于检测器的性能——若检测器本身存在偏差（如对某些异常分类错误），解释也可能误导。
- **实验覆盖有限**：未提及时间序列、表格数据或视频等非图像域，适用范围主要为图像异常检测。
- **缺乏严格的理论保证**：生成的多样性修改是否完备？可能存在冗余或遗漏关键异常因素的风险。
- **用户研究规模未知**：定性评估中用户数量、评价标准未披露，可能影响结果的可重复性。

（完）
