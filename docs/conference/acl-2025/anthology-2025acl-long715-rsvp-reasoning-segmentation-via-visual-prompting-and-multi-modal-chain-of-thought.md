---
title: "RSVP: Reasoning Segmentation via Visual Prompting and Multi-modal Chain-of-Thought"
title_zh: RSVP：通过视觉提示和多模态思维链实现推理分割
authors: "Yi Lu, Jiawang Cao, Yongliang Wu, Bozheng Li, Licheng Tang, Yangguang Ji, Chong Wu, Jay Wu, Wenbo Zhu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.715.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 通过多模态思维链生成可解释区域提议，与可解释目标检测相关
tldr: 为弥合多模态推理与视觉感知的差距，提出推理分割框架RSVP，通过多模态思维链视觉提示生成可解释的区域提议，进而实现精确定位与分割。实验表明该方法在推理分割任务上性能优异，且提供可理解的目标定位过程。该工作将可解释性融入视觉理解，具有广泛适用性。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 748, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1621, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 789, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 792, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 798, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 139, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 781, \"height\": 594, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 779, \"height\": 598, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 535, \"height\": 711, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.715/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1477, \"height\": 2009, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 819, \"height\": 555, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 598, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 460, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 778, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1663, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 825, \"height\": 173, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 825, \"height\": 372, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 825, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 808, \"height\": 332, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 810, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.715/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 789, \"height\": 520, \"label\": \"Table\"}]"
motivation: 多模态大模型缺乏显式的视觉定位和分割机制。
method: 两阶段框架：多模态思维链生成可解释区域提议，再细化分割。
result: 在推理分割基准上达到领先性能，且推理过程可解释。
conclusion: 可解释的推理分割能有效提升多模态理解能力。
---

## Abstract
Multi-modal Large Language Models (MLLMs) have demonstrated remarkable reasoning capability while lack explicit mechanisms for visual grounding and segmentation, creating a gap between cognitive reasoning and visual perception. To bridge this gap, we introduce Reasoning Segmentation via Visual Prompting (RSVP), a novel framework that unifies multi-step multimodal reasoning with grounded visual understanding. RSVP is a two-stage structuralized framework that integrates reasoning-driven localization with segmentation refinement. In the reasoning stage, RSVP employs multimodal chain-of-thought visual prompts to help MLLMs understand queries and infer targets, generating interpretable region proposals that enhance visual grounding. In segmentation stage, RSVP refines these proposals with a Vision-Language Segmentation Module (VLSM), seamlessly integrates textual and visual cues to produce precise segmentation masks. By explicitly modelling the interaction between multimodal reasoning and segmentation, RSVP introduces a new paradigm for interpretable reasoning segmentation. It exploits MLLMs’ inherent localization capabilities, enabling the models to not only reason about objects but also generate structured visual representations. Our extensive experiments demonstrate that RSVP achieves state-of-the-art performance, surpasses state-of-the-art methods by up to +6.5 gIoU and +9.2 cIoU on ReasonSeg, and achieves 49.7 mAP on SegInW under zero-shot settings. These results validate RSVP as an effective and scalable framework for integrating cognitive reasoning with structured visual understanding.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态大语言模型（MLLMs）虽然拥有强大的推理能力，但缺乏显式的视觉定位和分割机制，导致认知推理与视觉感知之间存在鸿沟。传统推理分割任务需要模型根据复杂、隐式的文本查询推理目标是否存在及其位置，现有的MLLM无法直接生成精确分割掩码，而指代分割模型又缺乏高层推理能力。
- **整体含义**：本文提出RSVP（Reasoning Segmentation via Visual Prompting）框架，旨在弥合多模态推理与结构化视觉理解之间的差距，实现可解释的推理分割，使模型不仅能推理对象，还能生成结构化的视觉表示。

## 2. 论文提出的方法论
### 核心思想
- 采用两阶段结构化框架，将推理驱动的定位与分割细化相结合，无需对MLLM进行微调，利用其固有推理和定位能力。

### 关键技术细节
1. **第一阶段：多模态Chain-of-Thought（CoT）视觉提示**
   - 预处理输入图像：将图像划分为M个水平区域和N个垂直区域，赋予唯一ID。
   - 构造结构化提示，引导MLLM逐步推理：
     - 推断对象名称和属性；
     - 判断对象是否存在于图像中；
     - 确定垂直和水平区域ID；
     - 提供推理依据。
   - MLLM输出结构化提议：对象名称、水平/垂直区域ID列表、推理理由。
   - 区域提议公式化：根据预测的水平/垂直ID构造边界区域，并添加填充以避免截断对象边缘。
   - 若对象不存在，则返回空ID列表。
2. **第二阶段：视觉语言分割模块（VLSM）**
   - 基于SAM框架，融入BEiT-3作为联合视觉语言编码器。
   - 区域裁剪：根据第一阶段输出的边界框裁剪图像区域，并调整到224×224。
   - 多模态特征编码：目标描述经XLMRobertaTokenizer编码，与图像特征通过交叉注意力融合，生成统一跨模态表示。
   - 通过投影器（两层线性+ReLU）映射到256维，送入SAM的提示编码器和分割解码器，得到像素级分割掩码。
   - 训练：在refCOCO上训练，使用LoRA和DeepSpeed，AdamW优化器，学习率1e-4，Dice Loss+BCE Loss，约16,000 epochs，batch size 256。

### 推理流程
- 先由MLLM生成结构化区域提议（CoT区域提议生成），再由VLSM处理生成最终掩码（视觉语言分割步骤）。

## 3. 实验设计
### 使用的数据集与场景
- **推理分割**：ReasonSeg验证集（200样本）和测试集（约770样本，包括短查询和长查询）。
- **开放世界分割**：SegInW零样本基准（25个类别）。
- **指代分割**：refCOCOg（验证和测试集）。

### Benchmark
- 主要指标：gIoU（平均交并比）、cIoU（累积交并比）、mAP（平均精度）。

### 对比方法
- 零样本方法：OVSeg、SEEM、Grounded-SAM、LLaVA+OVSeg、LISA（7B/13B，零样本）。
- 微调方法：LISA（7B/13B，在ReasonSeg训练集微调）、LISA++（微调）。
- 不同底层MLLM：GPT-4o、Gemini-Flash、LLaVA-7B、Qwen2-VL（7B/2B）。

## 4. 资源与算力
- **明确提及**：推理时间测试使用A100 40GB GPU单卡，测量RSVP和LISA的每图推理时间。
- **训练细节**：VLSM训练使用LoRA和DeepSpeed，但未明确说明使用的GPU数量、型号（可能也是A100）、训练总时长。仅提及batch size 256和约16,000 epochs。
- **结论**：文中未给出明确的训练算力统计，仅提供了推理延迟对比（表1）。

## 5. 实验数量与充分性
- **主要实验**：4组核心结果表格（表2: ReasonSeg, 表3: refCOCOg, 表4: SegInW, 表1: 推理延迟）。
- **消融实验**：共6组（表5-8, 表9-13）：
  - 多模态信息蒸馏策略（视觉/文本/两者）
  - 视觉提示密度（5×5, 9×9, 13×13 vs 网格）
  - CoT提示设计（手动多步 vs 简单CoT）
  - VLSM模块替换（OVSeg vs 专用模块）
  - 填充比例（0%、20%、40%）
  - 温度参数（0.0, 0.4, 0.8）
  - CoT框架对比
  - 第一阶段MLLM大小（Qwen 2B vs 7B）
- **充分性评价**：实验设计较为全面，覆盖主要基准、多种对比方法、多个消融维度。但缺乏更大规模消融（如更多视觉提示类型、更复杂的领域适应实验），不过已足以支撑核心论点。公平性方面：零样本设置统一，对比基线包括强基线（微调LISA）和多种零样本方法，结论可信。

## 6. 论文的主要结论与发现
- RSVP在零样本推理分割任务上达到SOTA：在ReasonSeg上gIoU=60.3, cIoU=60.0（GPT-4o作为第一级），超越所有零样本基线，甚至超过部分微调模型。
- 在SegInW开放世界分割中达到49.7 mAP，优于之前方法（如Grounded-SAM 48.7）。
- 证明通过多模态CoT视觉提示激发MLLM的推理和定位能力，可显著提升分割性能且保持可解释性。
- 较强MLLM（GPT-4o）带来更好效果；视觉提示密度需平衡（9×9最佳）；双向模态蒸馏（视觉+文本）必不可少。
- 框架模块化，可替换第一级MLLM或第二级分割模型，扩展性强。

## 7. 优点
- **创新性**：首次将多模态CoT视觉提示用于推理分割，生成可解释的区域提议，连接推理与分割。
- **模块化与零样本**：无需对MLLM进行微调或重训练，可即插即用，节省训练成本。
- **可解释性**：每步推理提供理由，输出结构化区域ID和对象描述，便于理解模型决策。
- **性能优异**：在多个基准上达到领先结果，且鲁棒性强（温度、填充等消融显示稳定）。
- **分析充分**：对CoT设计、视觉提示密度、信息蒸馏方式等进行了详细消融，提供设计指导。

## 8. 不足与局限
- **依赖MLLM能力**：性能高度受限于第一级MLLM的推理和视觉理解质量，弱模型（如2B Qwen）会导致显著下降。
- **视觉提示设计未最优**：区域划分网格密度和标记方式仍需手工调整，未实现自适应最优。
- **计算开销**：两阶段流程增加推理延迟（约10秒/图），虽比LISA-13B快，但实时应用受限制，文中仅建议量化或vLLM优化。
- **数据偏差与泛化**：主要在ReasonSeg和SegInW上评估，对实际开放场景的鲁棒性未充分验证；MLLM可能继承预训练数据中的偏差，影响输出公平性和安全性。
- **未探讨多对象/复杂场景**：实验样本主要为单对象定位分割，多对象关联推理场景未被评估。
- **训练细节缺失**：第二级VLSM训练所需GPU数量和时长未说明，复现成本不透明。

（完）
