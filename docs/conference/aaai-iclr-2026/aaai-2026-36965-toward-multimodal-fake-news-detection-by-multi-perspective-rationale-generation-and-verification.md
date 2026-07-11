---
title: Toward Multimodal Fake News Detection by Multi-perspective Rationale Generation and Verification
title_zh: 面向多模态假新闻检测的多视角理由生成与验证
authors: "Junyang Chen, Yueqian Li, Ka Chung Ng, Huan Wang, Liang-Jie Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/36965/40927"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 多视角理由生成实现可解释的多模态假新闻检测
tldr: 本文提出多视角理由生成与验证框架用于多模态假新闻检测。现有MLLM方法容易产生幻觉和错误推理。所提方法从来源可信度、跨模态矛盾、情感偏差等维度生成理由并加以验证，增强了可解释性。在多个基准数据集上，该方法优于现有方法，并能提供清晰的检测理由。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 447, \"height\": 410}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 404, \"height\": 408}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 638, \"height\": 383}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1838, \"height\": 852}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 883, \"height\": 678}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-36965/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1840, \"height\": 321}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-36965/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1825, \"height\": 1022}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-36965/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1843, \"height\": 357}]"
motivation: 现有MLLM假新闻检测方法易产生幻觉，缺乏可解释性。
method: 提出多视角理由生成与验证框架，从多个维度生成并验证检测理由。
result: 在多个假新闻检测数据集上取得最优性能，同时提供可解释的理由。
conclusion: 多视角理由生成能有效提升假新闻检测的可解释性和准确性。
---

## Abstract
The rapid proliferation of social media platforms has led to a surge in multimodal fake news, where deceptive content often combines text and images to mislead audiences. Traditional unimodal detection methods struggle to address the complexity of such content, necessitating holistic multimodal approaches. While the latest advancements in Multimodal Large Language Models (MLLMs) offer new opportunities for enhancing detection performance by analyzing multi-dimensional features, including source credibility, cross-modal contradictions, emotional bias, and manipulative writing patterns, these methods suffer from a key flaw: a susceptibility to hallucinations or erroneous reasoning, which can lead to flawed conclusions and ultimately biased detection results. We propose the Multimodal Fake News Detection via Multi-perspective Rationale Generation and Verification (MMRGV) model to mitigate this challenge. Our method employs a cross-verification mechanism to screen and reconcile contradictions among different rationales, thereby preserving the LLM's analytical advantages while mitigating the impact of erroneous reasoning or hallucinations on the final detection. Subsequently, these optimized rationales are fused via an adaptive weighting strategy to output a robust final prediction. Extensive experiments on three benchmark datasets (Twitter, Weibo, and GossipCop) demonstrate the superiority of our method, achieving state-of-the-art accuracy of 0.9972, 0.9663, and 0.8772, respectively, and significantly outperforming existing baselines. These results validate the effectiveness of multi-perspective rationale generation and cross-verification in enhancing multimodal fake news detection, offering a resilient solution to combat misinformation in the era of generative AI.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将根据您提供的论文内容，生成一份结构化、深入、客观的中文总结。

### 论文核心总结

#### 1. 核心问题与整体含义（研究动机和背景）

*   **核心问题**：社交媒体上多模态假新闻（结合文本和图像）泛滥，传统单模态检测方法难以胜任。虽然多模态大语言模型（MLLM）展现出强大的分析能力，但它们普遍存在**幻觉**（生成看似合理但虚假的细节）和**错误推理**的问题，直接用于假新闻检测会导致不可靠甚至偏颇的结论。
*   **研究动机**：如何利用MLLM强大的推理能力，同时有效抑制其产生的幻觉和错误，构建一个可靠、可解释的多模态假新闻检测系统，是本文的核心动机。
*   **整体含义**：本文提出了一种新颖的“生成-验证”范式，通过多视角生成推理路径并进行交叉验证，来增强检测的鲁棒性和可解释性，为应对生成式AI时代的信息误导问题提供了新思路。

#### 2. 方法论：核心思想、关键技术细节

*   **核心思想**：提出 **MMRGV**（Multi-perspective Rationale Generation and Verification）框架。该框架不直接信任MLLM的最终判断，而是先让其从多个固定视角生成详细的推理过程（即“理由”），然后通过一个专门的交叉验证机制来筛选和融合这些理由，最终做出可靠预测。
*   **关键技术细节**：
    1.  **多视角理由生成（Multi-perspective Rationale Generation）**：利用MLLM（本文采用Qwen2-VL）和思维链（Chain-of-Thought, CoT）提示，从以下三个核心视角为每条新闻生成理由：
        *   **文本描述 (Textual Description, TD)**：分析新闻文本的来源、风格、情感等语言线索。
        *   **图文一致性 (Image-Text Consistency, ITC)**：核对图像与文本在时间、地点、人物等关键要素上是否一致。
        *   **图像描述 (Image Description, ID)**：分析图像的来源、是否被篡改等图像取证线索。
    2.  **多视角交叉验证 (Multi-perspective Cross-Verification)**：这是框架的核心，用于过滤MLLM理由中的错误信息。包含三个子模块：
        *   **特征提取**：使用`RoBERTa`提取文本和理由特征，使用`Swin-T`提取图像特征，并通过对比损失`LC`对齐图像特征与其对应的ID理由（仅监督正确的理由对）。
        *   **理由内容门控融合 (Rationale Content Gate Fusion, RCGF)**：对每个视角，使用缩放点积注意力机制融合该视角的特征（`Xv`）和理由（`Rv`）。然后通过一个“理由门控网络”（Rationale Gate Net），根据融合后的特征预测该理由的“正确概率”（使用Focal Loss `LA`训练），并据此生成一个门控值`gv`，用于过滤和加权该视角的理由。
        *   **多视角聚合 (Multi-View Aggregation, MA)**：将经过门控加权的三个视角的理由特征与原始新闻文本特征（经注意力池化处理）拼接，形成一个4x矩阵`M`。然后通过一个多层的视角间协同注意力机制，迭代地更新和融合这些信息，用于最终的分类。
    3.  **训练目标**：采用两阶段训练。第一阶段仅优化对比学习损失`LC`；第二阶段联合优化分类损失`Lcls`（对于不平衡数据集使用Focal Loss）和辅助损失`LA`（控制理由验证）、`LJ`（辅助MLLM判断预测，用于知识蒸馏）。

#### 3. 实验设计

*   **数据集**：使用了三个公开的真实世界数据集，覆盖不同平台和语言：
    *   **Weibo**：中文数据集，比较平衡。
    *   **Twitter**：英文数据集，比较平衡。
    *   **GossipCop**：英文数据集，高度不平衡（假新闻仅占22%）。
*   **Benchmark方法**：与多类先进方法对比，包括：
    *   纯大模型：`Qwen2-VL`、`DeepSeek-R1`。
    *   传统小模型：`RoBERTa`。
    *   多模态小模型：`FSRU`、`CSFND`。
    *   大模型与小模型协作模型：`ARG`（基于GPT-3生成理由，本文用`Qwen2-VL`复现）。
*   **评估指标**：采用`Macro-F1`、`Accuracy`、以及分别针对`Real News`和`Fake News`的`Precision`、`Recall`和`F1`分数，非常全面。

#### 4. 资源与算力

*   论文明确提到，所有实验在**单个 NVIDIA Tesla A800 GPU** 上完成。
*   用于生成理由和图像标题的MLLM是`Qwen2-VL-72B`大型模型。
*   文中**未说明**具体的训练时长或推理时长。

#### 5. 实验数量与充分性

*   实验较为充分，主要涵盖以下方面：
    1.  **主实验**：在三个数据集上与所有基准方法进行性能对比（共7种方法 * 3个数据集 = 21组对比）。
    2.  **视角消融实验**：分别去除`TD`、`ITC`、`ID`三个视角，观察性能变化（共3组实验 * 3个数据集）。
    3.  **组件消融实验**：去除关键模块（理由对齐`RA`、特征增强`EF`、理由门控融合`RCGF`、多视角聚合`MA`），分析其贡献（共4组实验 * 3个数据集）。
    4.  **鲁棒性分析**：详细分析了MMRGV对MLLM错误判断的纠正能力（在Weibo数据集上进行，可视化四种结果组合）。
*   **公平性与客观性评价**：实验设计较为客观公平。对比的基准方法覆盖了主流范式，消融实验设计合理，能证明各组件和各视角的有效性。对`ARG`方法的复现也尽力保证了公平性。值得注意的是，论文指出Twitter数据集可能已接近饱和，这是一个诚实的体现。

#### 6. 主要结论与发现

*   **性能领先**：MMRGV在三个数据集上均取得了最优或极具竞争力的性能，尤其是在高不平衡的GossipCop数据集上，对假新闻的F1分数（0.6886）远超其他所有方法（如CSFND的0.4585）。
*   **文本视角最为重要**：在所有消融实验中，去除文本描述（TD）视角对模型性能的损害最大，凸显了文本推理在假新闻检测中的核心地位。
*   **有效纠正MLLM错误**：鲁棒性分析表明，MMRGV能够纠正超过90%的MLLM初始错误判断，同时很少引入新错误，证明了其交叉验证机制的有效性。
*   **多视角融合是关键**：虽然各视角重要性不同，但它们的互补性整合对于处理数据不平衡和提升模型鲁棒性至关重要。

#### 7. 优点

*   **方法创新性强**：提出了“生成-验证”新范式，巧妙地结合了MLLM的深层推理能力和专用模型的精确验证，有效解决了MLLM的幻觉问题。
*   **可解释性高**：模型最终预测不是黑盒，而是基于三个明确视角的可解释推理理由（TD, ITC, ID），增强了用户对检测结果的信任。
*   **鲁棒性优异**：通过交叉验证和多视角融合，模型对MLLM的噪音、数据不平衡（GossipCop）等问题表现出很强的鲁棒性。
*   **实验设计系统全面**：从性能、消融到鲁棒性分析，层层递进，论据充分，结论可信度高。

#### 8. 不足与局限

*   **依赖MLLM质量**：模型的性能上限受限于MLLM生成理由的质量。手动设计的提示可能无法捕获所有微妙的假新闻线索。
*   **计算成本高**：多视角生成和复杂的验证机制显著增加了推理的计算开销，不利于实时部署。
*   **视角固定**：目前采用的三个固定视角是手工定义的，可能不适用于所有领域或所有类型的假新闻，缺乏动态适应性。
*   **实验局限性**：
    *   虽然进行了消融，但对各视角重要性的分析主要基于性能下降绝对值，缺乏更深层的定性分析。
    *   模型对生成对抗性样本的鲁棒性未作测试。
*   **未来方向**：论文也承认了上述局限，并指出了未来的改进方向，包括**自动化提示优化**、**提升推理速度**和**探索视角的自动选择**。

（完）
