---
title: "IAD-R1: Reinforcing Consistent Reasoning in Industrial Anomaly Detection"
title_zh: IAD-R1：强化工业异常检测中的一致推理
authors: "Yanhui Li, Yunkang Cao, Chengliang Liu, Yuan Xiong, Xinghui Dong, Chao Huang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37588/41550"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 工业异常检测结合链式思维推理，通过一致推理提供可解释性
tldr: 针对视觉语言模型在工业异常检测中性能受限的问题，提出通用后训练框架IAD-R1。通过感知激活微调和链式思维数据训练，显著提升异常检测能力，并使模型能输出一致的推理链解释其决策。实验表明该方法适用于不同架构和参数规模的VLM，在多个工业数据集上取得领先结果。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37588/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1844, \"height\": 995, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37588/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 808, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37588/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 883, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37588/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 442, \"height\": 346, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37588/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37588/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1806, \"height\": 978, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37588/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 880, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37588/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37588/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1746, \"height\": 902, \"label\": \"Table\"}]"
motivation: 视觉语言模型在工业异常检测中性能有限，且缺乏可解释的决策推理。
method: 采用两阶段训练：感知激活微调构建高质量链式思维数据，再强化学习优化推理一致性。
result: 在多个工业异常检测数据集上超过现有方法，并能生成可解释的推理过程。
conclusion: 通过链式思维推理增强VLM的异常检测能力与可解释性。
---

## Abstract
Industrial anomaly detection is a critical component of modern manufacturing, yet the scarcity of defective samples restricts traditional detection methods to scenario-specific applications. Although Vision-Language Models (VLMs) demonstrate significant advantages in generalization capabilities, their performance in industrial anomaly detection remains limited. To address this challenge, we propose IAD-R1, a universal post-training framework applicable to VLMs of different architectures and parameter scales, which substantially enhances their anomaly detection capabilities. IAD-R1 employs a two-stage training strategy: the Perception Activation Supervised Fine-Tuning (PA-SFT) stage utilizes a meticulously constructed high-quality Chain-of-Thought dataset (Expert-AD) for training, enhancing anomaly perception capabilities and establishing reasoning-to-answer correlations; the Structured Control Group Relative Policy Optimization (SC-GRPO) stage employs carefully designed reward functions to achieve a capability leap from "Anomaly Perception" to "Anomaly Interpretation". Experimental results demonstrate that IAD-R1 achieves significant improvements across 7 VLMs, the largest improvement was on the DAGM dataset, with average accuracy 43.3% higher than the 0.5B baseline. Notably, the 0.5B parameter model trained with IAD-R1 surpasses commercial models including GPT-4.1 and Claude-Sonnet-4 in zero-shot settings, demonstrating the effectiveness and superiority of IAD-R1.

---

## 论文详细总结（自动生成）

# IAD-R1：强化工业异常检测中的一致推理 — 中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：工业异常检测因缺陷样本稀缺且异常类型多样，传统方法依赖手工特征和领域知识，只能针对单一品类，泛化能力差。视觉语言模型（VLM）虽具多模态理解与泛化优势，但在工业异常检测中表现有限。
- **背景矛盾**：现有两类 VLM 应用策略（异常专家辅助、端到端微调）均存在瓶颈：
  - 异常专家辅助受限于传统算法上限。
  - 端到端微调缺乏高质量推理过程数据，导致模型只学映射、不掌握内在逻辑，且传统强化学习奖励设计粗糙，造成推理与答案不一致。
- **本文目标**：提出 IAD-R1，一个通用后训练框架，通过高质量链式思维（CoT）数据与专门设计的强化学习策略，提升 VLM 的异常检测能力，并实现从“异常感知”到“异常解释”的跃升。

## 2. 方法论：核心思想、关键技术细节
### 2.1 整体框架 (两阶段训练)
- **第一阶段：感知激活监督微调 (PA-SFT)**  
  - 使用自建数据集 **Expert-AD**（首个工业异常检测领域含高质量 CoT 推理的数据集，共 5.9K QA 对）进行监督微调。
  - CoT 模板采用三层递进：空间感知 → 知识驱动分析 → 综合决策，模拟专家检测流程。
  - 训练使模型学习结构化推理与答案之间的对应关系，避免推理与结论矛盾。  
  - 损失函数最大化给定图像和提示下输出序列的条件概率。

- **第二阶段：结构化控制组相对策略优化 (SC-GRPO)**  
  - 以 PA-SFT 后的模型为初始策略模型。
  - **多维奖惩函数**（四个维度）：
    - **一致性奖励 R_con**：强制输出格式符合正常/异常模式，确保推理与答案语义一致。
    - **准确率奖励 R_acc**：检查最终答案（Yes/No）是否正确。
    - **位置奖励 R_loc**：将位置描述映射到 3×3 空间网格，匹配则得奖。
    - **类型奖励 R_type**：采用多级匹配（精确匹配→语义匹配→类别匹配→模糊匹配→组匹配），避免稀疏奖励。
  - **相对优势计算**：在组内对奖励进行归一化，避免价值网络开销，保持优化效率。

### 2.2 数据构造（Expert-AD 数据集）
- 包含 2.9K QA 对用于 PA-SFT 阶段，3K QA 对用于 SC-GRPO 阶段。
- 所有数据来自真实工业场景，包含结构化 CoT 推理，不同与以往只含描述和答案的数据。

## 3. 实验设计
### 3.1 数据集与场景
- **6 个数据集**，分为两类：
  - **工业物体**：MVTec-AD、VisA、MPDD
  - **表面纹理**：DAGM、DTD、SDD
- 评估设置：零样本 (0-shot) 和一样本 (1-shot)。
- 评价指标：**平衡准确率**（克服数据不平衡偏差）。

### 3.2 基准 (Benchmark)
- **商业模型**：GPT-4o、GPT-4.1（系列）、Claude-Sonnet-4
- **开源模型**：LLaVA-OneVision-SI (0.5B/7B)、Qwen2.5-VL-Instruct (3B/7B/72B)、Anomaly-OV、AnomalyGPT、InternVL-2.5 等。
- **骨干网络**：共 7 种不同架构和规模的 VLM，如 Qwen2-VL-2B、Qwen2.5-VL、LLaVA-1.5/1.6、LLaVA-OneVision-SI 等。

### 3.3 对比方法
- 直接对比零样本/一样本下的各模型输出，IAD-R1 模型从结构化标签 `<answer>` 中提取答案，基线模型直接取其输出。

## 4. 资源与算力
- 论文明确提到所有实验使用 **4 块 A100 GPU**，但**未说明训练总时长**。因此无法提供更具体的算力细节。

## 5. 实验数量与充分性
- **主实验（Table 1）**：在 6 个数据集上对比多种商业与开源模型，涵盖 0-shot 和 1-shot 设置。
- **消融实验**：
  - **数据激活方法（Table 2）**：对比 Expert-AD 与仅直接答案的原始数据，在三个模型上验证 CoT 的必要性。
  - **奖励策略（Table 3）**：对比 SC-GRPO 与原始奖励（仅答案正确性），证明多维奖励的重要性。
  - **各奖励函数贡献（Table 5）**：逐一消去 R_con、R_loc、R_type，分析各维度影响。
  - **网格尺寸（Figure 3）**：位置奖励中不同网格划分（1×1 至 5×5）的敏感性分析。
  - **模型推广（Table 4）**：在 7 种不同架构/参数规模的模型上展示 PA-SFT 和 SC-GRPO 分阶段增益。
  - **推理一致性分析（Figure 4）**：可视化对比 IAD-R1 与其他模型输出，展示推理与答案的一致性。
- **总体评价**：实验设计系统、全面，覆盖多种骨干、多种设置、多种消融，结论具有说服力。数据、奖励设计、网格选择等均有严谨验证。

## 6. 主要结论与发现
- **性能显著提升**：IAD-R1 在 7 种 VLM 上均带来大幅提升，DAGM 数据集上 0.5B 模型平均准确率提高 43.3%。
- **小模型超越大模型**：
  - IAD-R1 (0.5B) 在零样本设置下超过 GPT-4.1 和 Claude-Sonnet-4 等商业大模型。
  - IAD-R1 (3B) 超过同系列 72B 模型 4.5%。
- **两阶段依次有效**：PA-SFT 激活感知，SC-GRPO 进一步优化推理质量，且 SC-GRPO 优于传统单奖励强化学习。
- **高一致性推理**：IAD-R1 不仅给出正确答案，还输出与答案一致的推理过程，而其他模型（如 Qwen3、Claude-Sonnet-4）常出现推理错误或矛盾。

## 7. 优点
- **数据创新**：首次构建工业异常检测高质量 CoT 数据集（Expert-AD），填补领域空白。
- **框架通用性**：IAD-R1 可应用于不同架构、不同规模的 VLM，无需额外专家模块，端到端优化。
- **奖励设计巧妙**：针对异常检测任务设计多层级奖励（位置、类型、一致性），兼顾精确性与训练稳定性，避免稀疏奖励问题。
- **参数高效**：通过训练后框架，小模型即可达到甚至超越大模型商业模型性能，适合资源受限环境。
- **可解释性**：模型输出结构化推理过程，增强决策透明度和可理解性。
- **实验充分、公平**：采用平衡准确率避免不平衡偏差，对比多个商业/开源模型，消融实验设计严谨。

## 8. 不足与局限
- **数据集依赖**：Expert-AD 的质量直接影响模型表现，但数据集来源、构建细节（如图像多样性）未深入讨论，可能存在场景覆盖偏差。
- **实验覆盖**：仅针对 6 个工业数据集，未覆盖更广泛的真实工业场景（如不同光照、复杂背景、多类别协变异常），泛化性有待进一步验证。
- **未讨论鲁棒性**：缺乏对噪声、域迁移、对抗样本等场景的测试。
- **计算资源未详述**：虽提及 4×A100，但训练时长、超参数设置、收敛步数等未给出，可重复性受限。
- **失败案例分析缺失**：未分析错误预测的典型情况，无法评估模型在哪些困难模式下依然失败。
- **对极端不平衡数据可能仍存在风险**：虽采用平衡准确率，但数据集中正常与异常比例未详述，潜在影响未被讨论。

（完）
