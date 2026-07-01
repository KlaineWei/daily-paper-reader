---
title: "TRUST-VL: An Explainable News Assistant for General Multimodal Misinformation Detection"
title_zh: TRUST-VL：面向通用多模态虚假信息检测的可解释新闻助手
authors: "Zehong Yan, Peng Qi, Wynne Hsu, Mong-Li Lee"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.284.pdf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释视觉语言模型用于多模态虚假检测
tldr: 论文针对多模态虚假信息检测中现有方法只能处理单一失真类型且泛化能力差的问题，提出可解释统一框架TRUST-VL。该方法联合训练多种失真类型以共享推理能力，并引入Question-Aware Visual Amplifier模块增强视觉特征。实验表明，TRUST-VL在多个基准上均达到领先性能，同时提供了透明的决策解释。该工作为多模态虚假信息检测提供了可解释且泛化性强的统一方案。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 837, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1320, \"height\": 911, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1650, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1655, \"height\": 277, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 741, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 756, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1654, \"height\": 819, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1574, \"height\": 672, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 683, \"height\": 699, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.284/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1651, \"height\": 1000, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1589, \"height\": 803, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1644, \"height\": 601, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1378, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1198, \"height\": 793, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1396, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 796, \"height\": 135, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.284/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 798, \"height\": 216, \"label\": \"Table\"}]"
motivation: 现有多模态虚假信息检测方法通常只能处理单一失真类型，难以泛化到未见场景，且缺乏可解释性。
method: 提出TRUST-VL，一个统一的、可解释的视觉语言模型，联合训练多种失真类型，并使用Question-Aware Visual Amplifier模块增强视觉特征。
result: 在多个多模态虚假信息检测基准上，TRUST-VL取得了最先进的性能，并提供了可解释的决策依据。
conclusion: TRUST-VL证明了联合训练多失真类型和增强视觉注意力是提升检测泛化性和可解释性的有效途径。
---

## Abstract
Multimodal misinformation, encompassing textual, visual, and cross-modal distortions, poses an increasing societal threat that is amplified by generative AI. Existing methods typically focus on a single type of distortion and struggle to generalize to unseen scenarios. In this work, we observe that different distortion types share common reasoning capabilities while also requiring task-specific skills. We hypothesize that joint training across distortion types facilitates knowledge sharing and enhances the model’s ability to generalize. To this end, we introduce TRUST-VL, a unified and explainable vision-language model for general multimodal misinformation detection. TRUST-VL incorporates a novel Question-Aware Visual Amplifier module, designed to extract task-specific visual features. To support training, we also construct TRUST-Instruct, a large-scale instruction dataset containing 198K samples featuring structured reasoning chains aligned with human fact-checking workflows. Extensive experiments on both in-domain and zero-shot benchmarks demonstrate that TRUST-VL achieves state-of-the-art performance, while also offering strong generalization and interpretability.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **问题**：多模态虚假信息包含文本扭曲、视觉扭曲、跨模态扭曲三种类型，现有方法通常仅针对单一类型设计，难以泛化到未见过的扭曲场景。
- **背景**：生成式AI（如深度伪造、AI生成图像）加剧了虚假信息的传播，例如2024年美国大选中外国势力使用AI深度伪造和篡改媒体干扰选民。当前技术多聚焦于单子任务（如文本事实验证、人脸伪造检测、图文不一致检测），缺乏统一框架。
- **核心假设**：不同扭曲类型共享共性推理能力（如文本分析、视觉理解、证据推理、新闻知识），同时也需要任务特定技能（如语言模式、视觉伪影、语义一致性）。联合训练可促进知识共享，提升泛化性。
- **整体目标**：构建一个统一的、可解释的视觉语言模型（VLM），能够同时处理多种扭曲类型，并提供可解释的推理过程。

## 2. 方法论：核心思想、关键技术细节

### 核心思想
- **统一框架**：将多模态虚假信息检测形式化为一个包含共享推理和专门推理步骤的结构化流程，并通过联合训练增强模型对多种扭曲类型的适应性。
- **可解释性**：通过生成结构化的推理链（类似人工事实核查工作流）输出判断和解释。

### 关键技术细节
#### （1）TRUST-VL架构
- **输入**：图文对（图像CI、文本CT）、外部证据（直接证据Edir、反向证据Einv、上下文证据Ectx）。证据通过跨模态检索（图像检索器基于文本查询，文本检索器基于图像查询）获得。
- **基础VLM**：采用LLaVA架构，包括预训练视觉编码器（CLIP ViT-L/14）、轻量级MLP投影器、大语言模型（Vicuna-13B）。
- **Question-Aware Visual Amplifier (QAVA)**：受Q-Former启发，使用一组可学习的token（默认32个），通过自注意力捕获问题上下文，再通过交叉注意力与图像特征交互，生成任务导向的视觉token。这些token作为软视觉提示输入LLM，增强对细微视觉失真（如表情修改）的敏感度。

#### （2）TRUST-Instruct数据集构建
- **数据来源**：从Factify2（文本扭曲）、DGM4（视觉操纵，人脸交换等）、MMFakeBench（视觉伪造）、NewsCLIPpings（图文不匹配）收集<文本、图像、标签>三元组。
- **生成方法**：利用GPT-4o，基于结构化推理模板（包含共享步骤：文本分析、图像描述；专门步骤：根据扭曲类型细化问题）生成详细推理链。严格检查生成结果，98.5%通过人工验证，最终得到198,253条高质量指令，涵盖三种扭曲类型（视觉54.9%、跨模态37.5%、文本7.6%）。

#### （3）训练策略（三阶段）
- **阶段一**：训练投影模块（1 epoch），使用120万图文对（65.3万News样本+55.8万LLaVA训练语料），对齐视觉特征与语言模型。
- **阶段二**：联合训练LLM和投影模块（1 epoch），使用66.5万LLaVA合成对话样本，提升指令跟随能力。
- **阶段三**：全模型微调（3 epoch），使用19.8万TRUST-Instruct样本，增强虚假信息专用推理能力。

## 3. 实验设计

### 数据集
#### 领域内（In-domain，训练数据来源或同类）
- **MMFakeBench**：混合扭曲类型（1000样本）
- **Factify2**：文本扭曲（3000样本，平衡）
- **DGM4-Face**：视觉扭曲（面部操纵，900样本平衡）
- **NewsCLIPpings**：跨模态扭曲（7264样本平衡）

#### 领域外（Out-of-domain，未见场景）
- **MOCHEG**：文本虚假（400样本平衡）
- **Fakeddit-M**：视觉操纵（400样本平衡）
- **VERITE**：跨模态不匹配（400样本平衡）

### 基线方法
- **通用VLM**：BLIP-2、InstructBLIP、LLaVA、xGen-MM、LLaVA-NeXT、Qwen2-VL、GPT-4o、o1（OpenAI）
- **专用检测器**：SNIFFER（跨模态）、MMD-Agent（多智能体）、LRQ-FACT（多LLM事实核查）

### 评价指标
- 准确率（Acc.）和宏F1（Macro-F1）

### 对比结果（主要发现）
- TRUST-VL在所有数据集上均超越所有基线，平均准确率86.16%，比第二名o1（77.74%）高8.42个百分点。
- 在视觉扭曲任务（DGM4-Face）提升最显著（+31.36% Acc），证明QAVA模块有效。
- 专用检测器（MMD-Agent等）平均准确率低于通用VLM，可能因模块间推理冲突。

## 4. 资源与算力
- **GPU**：8块Nvidia H100 80G GPU。
- **训练时长**：未明确给出总时长，但提及三阶段训练：阶段一1 epoch，阶段二1 epoch，阶段三3 epoch，batch size 128。
- **模型规模**：总参数量约13B（Vicuna-13B + CLIP-L + QAVA）。

## 5. 实验数量与充分性
- **实验组数**：丰富多样。
  - 主实验：7个数据集 × 11个基线 + 自己模型，表3展示了详细结果。
  - 与任务专用模型比较（表4）：3个数据集 × 3个对比模型。
  - 消融实验（表5）：4种变体（w/o Reasoning、w/o Common Reasoning、w/o QAVA、7B backbone）在4个领域内数据集上。
  - 联合训练实验（图6）：热力图展示单类型训练 vs 联合训练效果。
  - QAVA token数影响（图7）：不同token数量（0,16,32,64）在4个数据集上。
  - 证据质量鲁棒性（附录表8）：不同比例错误证据下的性能。
  - 不同backbone对比（附录表7）：LLaVA vs Mistral 7B。
  - MMD-Agent backbone消融（附录表9）：LLaVA vs GPT-4o。
- **充分性评估**：实验设计客观、公平，覆盖了多种扭曲类型、多个领域内外数据集、多种基线（开源/闭源、通用/专用），消融实验全面，并提供了案例分析和鲁棒性测试。结论可靠。

## 6. 主要结论与发现
- **联合训练有效**：共享推理能力可跨任务迁移，联合训练模型优于单类型训练。
- **QAVA模块关键**：任务导向的视觉注意力显著提升视觉失真检测（+15.71%准确率）。
- **结构化推理监督必要**：移除推理步骤会导致性能大幅下降（4-12个百分点），说明可解释推理不仅提升可解释性，也提升检测准确性。
- **统一框架优于多智能体**：端到端优化比松散连接的模块化方法效果更好（平均准确率高30个百分点）。
- **泛化性强**：在未见过的数据集（如MOCHEG、Fakeddit-M、VERITE）上仍保持领先，说明方法跨场景适用。

## 7. 优点
- **方法创新**：QAVA模块设计精巧，将任务导向的视觉注意力注入VLM，有效区分不同失真类型；三阶段渐进式训练策略合理。
- **数据集贡献**：TRUST-Instruct是首个包含多种失真类型、结构化推理链的大规模指令数据集（198K），可推动后续研究。
- **全面实验**：覆盖多领域、多基线、多消融，结果充分支撑结论；在领域外数据集上验证了泛化性。
- **可解释性**：输出结构化推理链，符合人类事实核查流程，实用性强。

## 8. 不足与局限
- **推理模板人工设计**：结构化问题模板由人工设计，而非模型自动学习，引入主观偏见；作者提出未来可结合强化学习提升适应性。
- **视觉证据依赖文本**：虽然检索了视觉证据，但通过图像描述转换为文本进行推理，失去了直接视觉比较的丰富信号。
- **视觉扭曲类型有限**：仅关注人脸操纵（DGM4-Face），未覆盖物体级操纵或视频操纵，限制了通用性。
- **证据质量依赖检索**：外部证据来自开放域检索，可能包含噪声；虽然实验显示鲁棒性，但极端情况下仍可能误导。
- **未讨论跨语言场景**：所有数据均为英文，多语言虚假信息检测未涉及。
- **计算资源需求较高**：13B模型需要8块H80 GPU，推理成本较高，轻量化部署需进一步优化。

（完）
