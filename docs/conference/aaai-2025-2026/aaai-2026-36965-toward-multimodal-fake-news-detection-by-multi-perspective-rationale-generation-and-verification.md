---
title: Toward Multimodal Fake News Detection by Multi-perspective Rationale Generation and Verification
title_zh: 面向多模态假新闻检测的多视角理由生成与验证
authors: "Junyang Chen, Yueqian Li, Ka Chung Ng, Huan Wang, Liang-Jie Zhang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/36965/40927"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 假新闻检测中的多视角理由生成
tldr: 针对多模态假新闻检测中现有方法易产生幻觉推理的问题，提出了一种多视角理由生成与验证框架，通过生成源可信度、跨模态矛盾等维度的解释性理由来增强检测的可解释性，实验表明该方法有效提升了检测准确性和推理可靠性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 447, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 404, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 638, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1838, \"height\": 852, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-36965/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 883, \"height\": 678, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-36965/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1840, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-36965/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1825, \"height\": 1022, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-36965/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1843, \"height\": 357, \"label\": \"Table\"}]"
motivation: 现有方法依赖MLLM但易产生幻觉，缺乏可解释性。
method: 提出多视角理由生成与验证框架，从多个维度生成并验证解释性理由。
result: 实验表明该方法提升了检测准确性和推理可靠性。
conclusion: 多视角理由生成增强了假新闻检测的可解释性和鲁棒性。
---

## Abstract
The rapid proliferation of social media platforms has led to a surge in multimodal fake news, where deceptive content often combines text and images to mislead audiences. Traditional unimodal detection methods struggle to address the complexity of such content, necessitating holistic multimodal approaches. While the latest advancements in Multimodal Large Language Models (MLLMs) offer new opportunities for enhancing detection performance by analyzing multi-dimensional features, including source credibility, cross-modal contradictions, emotional bias, and manipulative writing patterns, these methods suffer from a key flaw: a susceptibility to hallucinations or erroneous reasoning, which can lead to flawed conclusions and ultimately biased detection results. We propose the Multimodal Fake News Detection via Multi-perspective Rationale Generation and Verification (MMRGV) model to mitigate this challenge. Our method employs a cross-verification mechanism to screen and reconcile contradictions among different rationales, thereby preserving the LLM's analytical advantages while mitigating the impact of erroneous reasoning or hallucinations on the final detection. Subsequently, these optimized rationales are fused via an adaptive weighting strategy to output a robust final prediction. Extensive experiments on three benchmark datasets (Twitter, Weibo, and GossipCop) demonstrate the superiority of our method, achieving state-of-the-art accuracy of 0.9972, 0.9663, and 0.8772, respectively, and significantly outperforming existing baselines. These results validate the effectiveness of multi-perspective rationale generation and cross-verification in enhancing multimodal fake news detection, offering a resilient solution to combat misinformation in the era of generative AI.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 社交媒体中多模态假新闻（文本+图像）的泛滥对社会造成严重危害。传统的单模态检测方法难以处理跨模态矛盾、事实伪造等复杂模式。
- 最新多模态大语言模型（MLLMs）虽能通过分析源可信度、跨模态矛盾、情感偏见等多维特征提升检测性能，但其存在关键缺陷：易产生幻觉或错误推理，导致最终检测结果有偏。
- 现有方法（如直接使用LLM零样本推理或简单融合）缺乏对LLM推理可靠性的系统性校验，亟需一种既能利用LLM强大分析能力又能抑制其幻觉影响的鲁棒框架。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 核心思想
- 提出 **MMRGV（Multimodal Fake News Detection via Multi-perspective Rationale Generation and Verification）** 框架。
- 两阶段流程：（1）多视角理由生成（由MLLM完成）；（2）多视角交叉验证与自适应融合（由轻量模型完成）。
- 通过将LLM生成的推理路径（理由）作为可验证物，利用专用细调模型进行筛选和校正，最终融合得到稳健预测。

### 关键技术细节
1. **多视角理由生成**：
   - 使用Qwen2-VL-72B，结合少样本Chain-of-Thought提示，从三个视角生成理由：
     - **文本描述（TD）**：分析新闻文本的源、逻辑、情感等语言线索。
     - **图文一致性（ITC）**：检测时间、地点、人物等关键元素的跨模态对齐。
     - **图像描述（ID）**：分析图像来源、篡改痕迹、常识合理性。
   - 每个视角输出一个判断 \( y^{(v)}_J \in \{0,1,2\} \)（0真实/1虚假/2不确定）及对应的理由文本 \( R_v \)。

2. **特征提取与跨模态对齐**：
   - 文本：使用RoBERTa编码新闻文本和理由；图像：使用Swin-T编码图像。
   - 对图文一致性视角，先让MLLM生成图像标题，再与新闻文本拼接编码得到 \( X_{ITC} \)。
   - 对比学习损失 \( \mathcal{L}_C \)（公式1-2）：将图像特征与ID理由特征对齐，只对有正确判断（\( y^{(ID)}_A=1 \)）的样本计算，避免噪声。
   - 辅助任务损失 \( \mathcal{L}_J \)（公式3）：预测MLLM原始判断，蒸馏其推理能力到理由编码器。

3. **理由内容门控融合（RCGF）**：
   - 对每个视角 \( v \)，使用缩放点积注意力融合原始新闻特征 \( X_v \) 和理由特征 \( R_v \)，得到更新表示 \( X'_v, R'_v \)（公式4-6）。
   - 预测理由正确性概率 \( \hat{y}^{(v)}_A \)，使用Focal Loss \( \mathcal{L}_A \) 处理正负样本不平衡（公式7-8）。
   - 门控网络根据 \( X'_v \) 生成门值 \( g_v \)，对理由序列池化向量进行缩放（公式9-10）。

4. **多视角聚合模块**：
   - 对原始新闻文本特征 \( X_{TD} \) 做注意力池化得到 \( x_{TD} \)。
   - 将三个缩放后的理由向量与 \( x_{TD} \) 拼接成 \( M^{(0)} \in \mathbb{R}^{4 \times d} \)（公式11-12）。
   - 通过L层逐视角协同注意力更新（公式13-14），最后用分类头输出预测，使用Focal Loss \( \mathcal{L}_{cls} \)（公式15）。

5. **两阶段训练**：
   - 第一阶段：仅优化对比学习损失 \( \mathcal{L}_C \)，建立跨模态对齐。
   - 第二阶段：联合优化 \( \mathcal{L}_{S2} = \lambda_1 \mathcal{L}_A + \lambda_2 \mathcal{L}_J + \mathcal{L}_{cls} \)（公式16）。

## 3. 实验设计

- **数据集**：三个基准数据集，覆盖不同语言和分布：
  - **Weibo**（中文）：7,853样本，53.6%虚假。
  - **Twitter**（英文）：14,195样本，54.6%虚假。
  - **GossipCop**（英文）：12,331样本，22.0%虚假（高度不平衡）。
  - 均按6:2:2分层划分训练/验证/测试。

- **对比基准**：
  - 直接MLLM方法：Qwen2-VL、DeepSeek-R1。
  - 传统小模型方法：RoBERTa、FSRU、CSFND、ARG（使用Qwen2-VL生成理由重实现）。

- **实验组**：
  - 主性能对比（表1）：在所有三个数据集上报告Macro-F1、准确率、真假类别的精确率/召回率/F1。
  - 视角消融实验（表2）：分别移除TD、ITC、ID视角。
  - 组件消融实验（表3）：移除对比学习损失（RA）、辅助任务损失（EF）、理由门控融合（RCGF）、多视角聚合（MA）。
  - 鲁棒性分析（图3）：在Weibo测试集上比较MLLM原始判断与MMRGV最终预测的纠错情况。

- **评估指标**：宏平均F1、准确率、各类别F1。

## 4. 资源与算力

- 论文明确说明：所有实验在 **单个NVIDIA Tesla A800 GPU** 上完成。
- MLLM使用 **Qwen2-VL-72B**，借助vLLM框架加速推理。
- 训练采用两阶段，但 **未给出具体训练时长**（如小时数或epoch数）。
- 仅微调RoBERTa和Swin-T的最后层，其他层冻结。

## 5. 实验数量与充分性

- **实验数量**：共计包含三大组实验（主对比、视角消融、组件消融），外加一组鲁棒性可视化分析。针对每个数据集均有完整指标。
- **充分性评价**：
  - **充分**：覆盖了三种不同语言、规模、平衡程度的数据集；对比了当前最先进的多类方法（LLM直推、传统小模型、LLM辅助方法）；消融实验既验证了各视角必要性，也验证了各模块贡献。
  - **客观公平**：对ARG方法进行了公平重实现（使用相同MLLM）；所有实验使用相同数据划分；指标全面（Macro-F1+各类别F1）。
  - **鲁棒性分析**额外验证了模型对MLLM错误的纠错能力，增强了可信度。

## 6. 论文的主要结论与发现

- MMRGV在三个数据集上均达到 **最先进性能**：Weibo上Macro-F1 0.9662，Twitter上0.9972，GossipCop上0.8060，显著优于所有基线。
- 在高度不平衡的GossipCop上，MMRGV的虚假新闻F1达到0.6886，远高于第二名CSFND的0.4585，体现强鲁棒性。
- 消融实验表明：
  - 文本描述（TD）视角最重要，移除后性能下降最大。
  - 理由门控融合（RCGF）模块在所有数据集上均关键。
  - 多视角聚合（MA）在不平衡数据集上作用最突出。
- 鲁棒性分析显示：MMRGV能纠正MLLM超过90%的错误判断，且几乎不引入新错误（错误引入率约2%）。

## 7. 优点

- **创新性**：首次将MLLM生成的多视角理由与专用细调模型的交叉验证结合，显著降低了LLM幻觉对检测的负面影响。
- **系统性**：理由视角覆盖了文本、跨模态、图像三个核心维度，形成完整的分析框架。
- **鲁棒性**：门控机制和Focal Loss有效处理了理由正确性的不平衡以及数据集类别不平衡。
- **实验充分性**：在三个代表性数据集上进行了全面的主实验、消融实验和纠错能力验证，消融实验设计严谨，对比基线更新至2025年。

## 8. 不足与局限

- **依赖人工提示词质量**：MLLM生成理由的质量受制于手动设计的CoT提示，可能忽略微妙虚假线索。
- **推理成本高**：多理由生成与多视角交叉验证导致推理延迟增加，不适合实时部署。
- **视角固定**：三个视角是手动定义的，无法自适应不同领域或新兴虚假模式。
- **未评估训练时长**：未提供训练迭代次数或时间，影响可复现性评估。
- **GossipCop上ID视角略有负作用**（移除后性能微升），提示视觉理由在该数据集上可能引入噪声。

（完）
