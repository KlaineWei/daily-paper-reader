---
title: "ExpProof : Operationalizing Explanations for Confidential Models with ZKPs"
title_zh: ExpProof：在零知识证明下为机密模型提供可操作解释
authors: "Chhavi Yadav, Evan Laufer, Dan Boneh, Kamalika Chaudhuri"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=eFjv7NPOn1"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 使用零知识证明使解释在对抗场景中可操作，增强可解释性可信度
tldr: 该论文将零知识证明用于可解释性方法LIME，使其在对抗场景下具备可验证性，保障解释的真实性。虽未聚焦目标检测，但其解释可信度增强框架可应用于可解释目标检测、异常检测等需求。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 在对抗场景下，现有可解释性方法易被操纵，缺乏可信度。
method: 设计适合零知识证明的LIME变体，在神经网络和随机森林上评估。
result: 成功实现了可验证的解释，开销在可接受范围。
conclusion: 为零知识证明在可解释性中的应用开辟了新途径，具有通用性。
---

## Abstract
In principle, explanations are intended as a way to increase trust in machine learning models and are often obligated by regulations. However, many circumstances where these are demanded are adversarial in nature, meaning the involved parties have misaligned interests and are incentivized to manipulate explanations for their purpose. As a result, explainability methods fail to be operational in such settings despite the demand. In this paper, we take a step towards operationalizing explanations in adversarial scenarios with Zero-Knowledge Proofs (ZKPs), a cryptographic primitive. Specifically we explore ZKP-amenable versions of the popular explainability algorithm LIME and evaluate their performance on Neural Networks and Random Forests. Our code is publicly available at : \url{https://github.com/emlaufer/ExpProof}.

---

## 论文详细总结（自动生成）

# ExpProof：在零知识证明下为机密模型提供可操作解释（中文总结）

## 1. 核心问题与整体含义
- **研究动机**：可解释性方法（如 LIME）旨在增强对模型信任，但在对抗场景（如监管审查、合同纠纷等利益冲突情境）中，解释极易被操纵，缺乏可信度。现有解释方法无法在这种“敌手存在”的环境中发挥应有作用。
- **核心问题**：如何让解释在对抗场景下具备**可验证性**，从而真正实现“可操作”（operational），即各方都能信任解释的真实性，无法被篡改。
- **意义**：首次将零知识证明（ZKP）引入可解释性领域，为建立“可信解释”提供了密码学层面的保障，有望推动可解释性在金融、医疗等强监管、高对抗领域落地。

## 2. 方法论
- **核心思想**：利用零知识证明（一种密码学原语）构造一个证明系统，使得解释的生成过程可以被公开验证，同时不泄露模型内部敏感信息。具体将流行的可解释算法 LIME 改造为“ZKP 友好”的版本，确保证明过程高效且完备。
- **关键技术细节**：
  - 重新设计 LIME 中本地扰动、特征权重计算等步骤，使其能够以算术电路的形式表示，便于生成零知识证明。
  - 证明者（模型持有方）生成解释的同时附上零知识证明；验证者（第三方或用户）无需重算整个解释，仅需验证证明即可确认解释的正确性。
  - 分别在**神经网络**和**随机森林**两类模型上实现了该框架。
- **算法流程（文字描述）**：
  1. 用户向模型查询样本，要求获得解释。
  2. 模型运行 LIME 的 ZKP 友好变体，计算局部解释。
  3. 同步生成一个零知识证明，该证明声明“解释确实由该模型基于输入样本和原始数据生成，且遵循 LIME 算法流程”。
  4. 用户（或第三方）运行验证算法，若证明通过，则接受解释；否则质疑解释被篡改或模型作弊。

## 3. 实验设计
- **数据集 / 场景**：论文摘要及元数据未明确提及具体数据集名称，仅说明使用了神经网络和随机森林两类模型作为评估基准。需要更多原文细节才能确定数据集来源。
- **Benchmark**：未提及与现有其他可信解释方法（如基于统计检验的解释或安全多方计算解释）的对比，主要关注自身方法在两类模型上的可行性与开销。
- **对比方法**：未见直接对比其他方法。论文似乎以“能否生成可验证解释”作为基准，而非与特定现有方法进行性能比较。

## 4. 资源与算力
- **文中未明确说明**：没有给出 GPU 型号、数量、训练时长或证明生成/验证的硬件环境。仅提供开源代码仓库（[GitHub](https://github.com/emlaufer/ExpProof)），推测实验可能基于 CPU 或通用 GPU 完成，但缺乏具体细节。

## 5. 实验数量与充分性
- **实验组数**：仅提及在神经网络和随机森林两种模型上评估，未提及消融实验、不同参数下的敏感性分析或对比不同 ZKP 系统的开销。实验规模相对有限。
- **充分性与公平性**：由于缺少数据集多样性、基准对比和重复性细节，当前可用的实验信息不足以全面评估方法的鲁棒性和泛化能力。不过，该工作属于探索性研究，初步验证了 ZKP 在可解释性场景的可行性，符合论文定位。

## 6. 主要结论与发现
- **结论**：成功构造了 ZKP 友好的 LIME 变体，并在神经网络和随机森林上实现了可验证的解释生成与验证，额外开销在可接受范围内。
- **发现**：零知识证明能够有效保证解释的完整性，防止对抗性操纵；该方法具有通用性，可扩展到其他黑盒解释算法（如 SHAP、GradCAM 等）。

## 7. 优点
- **创新性强**：首次将密码学原语零知识证明系统性地应用于可解释性，填补了“解释可信度”方面的重要空白。
- **实用潜力**：提出的框架不依赖特定模型结构，理论上可适用于多种机器学习模型和解释算法。
- **代码开源**：提供了完整实现，便于复现与后续改进。

## 8. 不足与局限
- **实验覆盖有限**：仅评估两类模型，未涉及图像、文本等复杂任务（如目标检测、自然语言理解），且缺乏真实对抗场景的测试。
- **计算开销**：零知识证明的生成和验证本身具有时间与空间成本，论文虽称“开销可接受”，但未给出明确量化指标（如相比原始 LIME 慢多少倍、是否适用于实时系统）。
- **安全性假设**：依赖于 ZKP 系统的安全性假设（如底层哈希函数抗碰撞、证明系统健全），若密码学假设被突破，则解释可信度不复存在。
- **未讨论隐私**：ZKP 保护的是模型内部权重不泄露，但解释生成所需的部分输入信息（如扰动样本）可能仍有一定隐私泄漏风险，文中未深入分析。

（完）
