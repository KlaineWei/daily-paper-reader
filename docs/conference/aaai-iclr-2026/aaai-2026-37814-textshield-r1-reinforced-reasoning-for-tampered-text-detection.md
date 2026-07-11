---
title: "TextShield-R1: Reinforced Reasoning for Tampered Text Detection"
title_zh: TextShield-R1：基于强化推理的篡改文本检测
authors: "Chenfan Qu, Yiwu Zhong, Jian Liu, Xuekang Zhu, Bohan Yu, Lianwen Jin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37814/41776"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 基于强化推理的篡改文本检测，具备可解释性
tldr: 本文提出TextShield-R1，首个基于强化学习的多模态大语言模型方案用于篡改文本检测与推理。通过法医持续预训练和强化学习，模型在检测篡改文本区域的同时生成可解释的推理，解决了微伪影定位难和依赖昂贵标注的问题。实验表明其在多种篡改场景下表现优异。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1789, \"height\": 993}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 857, \"height\": 442}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 915, \"height\": 446}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 886, \"height\": 179}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 596}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 880, \"height\": 428}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 878, \"height\": 280}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 353}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 752}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1844, \"height\": 280}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1826, \"height\": 283}]"
motivation: 现有篡改检测方法难以定位微伪影且依赖昂贵标注。
method: 提出TextShield-R1，使用法医持续预训练和强化学习训练MLLM进行检测和推理。
result: 在多个篡改检测基准上取得了最优性能和可解释性。
conclusion: TextShield-R1有效结合了检测与可解释推理。
---

## Abstract
The growing prevalence of tampered images poses serious security threats, highlighting the urgent need for reliable detection methods. Multimodal large language models (MLLMs) demonstrate strong potential in analyzing tampered images and generating interpretations.
However, they still struggle with identifying micro-level artifacts, exhibit low accuracy in localizing tampered text regions, and heavily rely on expensive annotations for forgery interpretation. To this end, we introduce TextShield-R1, the first reinforcement learning based MLLM solution for tampered text detection and reasoning. Specifically, our approach introduces Forensic Continual pre-training, an easy-to-hard curriculum that well prepares the MLLM for tampered text detection by harnessing the large-scale cheap data from natural image forensic and OCR tasks. During fine-tuning, we perform Group Relative Policy Optimization with novel reward functions to reduce annotation dependency and improve reasoning capabilities.  At inference time, we enhance localization accuracy via OCR Rectification, a method that leverages the MLLM’s strong text recognition abilities to refine its predictions.
Furthermore, to support rigorous evaluation, we introduce Text Forensics Reasoning (TFR) benchmark, comprising over 45k real and tampered images across 16 languages, 10 tampering techniques, and diverse domains. Rich reasoning-style annotations are included, allowing for comprehensive assessment. Our TFR benchmark simultaneously addresses seven major limitations of existing benchmarks and enables robust evaluation under cross-style, cross-method, and cross-language conditions. Extensive experiments demonstrate that TextShield-R1 significantly advances the state of the art in interpretable tampered text detection.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：随着图像处理技术的快速发展，篡改文本图像被广泛用于欺诈、谣言传播等恶意目的，构成严重安全威胁。因此，可靠地检测篡改文本成为紧迫的研究课题。
- **现有方法局限**：多模态大语言模型（MLLMs）在分析篡改图像和生成解释方面展现出潜力，但仍面临三大关键挑战：
  1. **任务对齐不足**：现有MLLMs预训练于宏观语义任务（如图像描述、物体识别），而篡改文本检测需要微观级感知语义无关的伪影，任务差距大，导致微调时易混淆和过拟合。
  2. **严重依赖昂贵标注**：当前MLLMs高度依赖昂贵的伪造解释标注（通常通过GPT-4o等闭源模型生成），且涉及隐私敏感图像（如身份证、合同）禁止外部暴露；自动标注易出错，需大量人工清洗。即使有完整标注，“填鸭式”监督微调也会削弱模型内在推理能力。
  3. **定位精度差**：MLLMs难以预测精确边界框，尤其是密集文本场景。简单整合外部定位模型会引入额外延迟和预测不匹配问题。

- **整体目标**：提出首个基于强化学习的MLLM解决方案——TextShield-R1，实现统一的篡改文本检测、定位与可解释推理，同时降低对昂贵标注的依赖。

## 2. 方法论

### 核心思想
通过三阶段流水线解决上述问题：
1. **法医持续预训练（Forensic Continual Pre-training）**：利用大规模、低成本的自然图像伪造数据，通过“由易到难”的课程学习，弥合通用预训练与细粒度法医分析之间的差距。
2. **基于GRPO的强化学习微调**：引入Group Relative Policy Optimization（GRPO），设计五类奖励函数，降低对伪造解释标注的依赖，增强模型推理能力。
3. **OCR校正（OCR Rectification）**：推理阶段，利用任务专用OCR引擎的精确文本检测结果，校正MLLM的文本定位预测，提升定位精度。

### 关键技术细节

#### 法医持续预训练
- **数据来源**：
  - 120k局部篡改自然图像（来自CASIAv1v2、IMD20、NIST16、MIML数据集）
  - 120k完全生成自然图像（来自Community Forensic数据集）
  - 60k真实图像（来自COCO）+ 60k真实图像（来自LAION）
  - 真实文本图像（来自TFR训练集）用于OCR参考接地任务
- **任务设计**：
  - 分类：真实、完全生成、局部篡改三类。
  - 对于局部篡改自然图像，引入**3D法医学习**：除分类外，要求模型输出篡改对象的描述、边界框坐标和掩码字符串（将掩码插值到32×32并编码为0/1串）。
  - 为缓解OCR知识遗忘，穿插**OCR参考接地任务**：给定真实文本图像和随机文本实例，模型需根据边界框输出文本，或根据文本输出边界框。

#### GRPO强化学习微调
- **框架**：基于GRPO，策略模型为Qwen2.5-VL-7B（通过LoRA微调，rank=64），优化器AdamW，学习率从1e-4衰减至0。
- **五类奖励函数**：
  1. **真实/伪造分类奖励**：正确分类真实/生成/篡改得1分，否则0分。
  2. **伪造方法检测奖励**：正确识别篡改区域是复制粘贴还是生成得1分，否则0分。
  3. **篡改定位奖励**：若预测框与真实框IoU > 0.5，奖励值为IoU值；否则为0。
  4. **篡改文本OCR奖励**：使用归一化Levenshtein距离，奖励 = 1 - 归一化距离。
  5. **格式奖励**：鼓励输出符合`<think>...</think>`和`<answer>...</answer>`的结构化格式。
- **训练过程**：首先使用约25%完全标注数据建立冷启动，然后对剩余图像使用GRPO微调（不提供伪影解释标注）。

#### OCR校正
- **流程**：
  1. 对预测包含篡改的图像，通过OCR引擎获取所有检测到的文本内容及其边界框。
  2. 对每个模型预测的篡改文本，在OCR结果中寻找匹配文本（Levenshtein距离最小）。
  3. 若只有一个匹配，直接用OCR框替换模型预测框；若有多个匹配，选择与模型预测框的Distance IoU最大的那个；若无匹配（归一化Levenshtein距离 > 0.2），保留模型原始预测。
- **目的**：利用MLLM强大的文本识别能力，结合OCR引擎的精确定位，解决MLLM定位不准问题。

## 3. 实验设计

### 使用的基准与新数据集

- **TFR基准（Text Forensics Reasoning Benchmark）**：
  - 由作者构建，包含45,971张伪造图像和45,514张真实图像。
  - 涵盖文档、场景文本和身份证件三种图像域；10种篡改方式（包括GAN、扩散模型、GPT-4o生成等）；16种语言。
  - 提供丰富的推理风格文本注释。
  - 设置了三个OOD子集（独立于训练集）：
    - **Cross-Image-Style (CIS)**：训练集中未出现的图像源。
    - **Cross-Tampering-Method (CTM)**：使用训练集未包含的三种篡改方法（TextDiffuser-2、SR-Net、Control-Net）。
    - **Cross-Language (CL)**：10种训练集中未出现的语言。

- **对比方法**：
  - 官方预训练版本：GPT-4o、MiniCPM-V 2.6、InternVL3-2B/8B、Qwen2.5-VL-3B/7B。
  - 在TFR训练集上微调后的版本：同上（含FakeShield、SIDA的微调变体）。

### 评估指标
- **分类准确率**（Cls）
- **篡改文本识别准确率**（OCR）
- **定位IoU**（Loc.）
- **推理质量**（Res.）：余弦相似度、Rouge-L、BLEU的平均分。

### 主要实验结果

- **表2**：对比实验显示，TextShield-R1在所有四个测试集（Test、CIS、CTM、CL）的四个指标上均大幅领先于所有对比方法。例如，Test集上分类88.1%（第二高79.1%）、OCR 47.6%（第二高24.3%）、定位57.8%（第二高18.2%）、推理58.8%（第二高42.9%）。
- **表3**：消融实验逐步去除模块——去除法医持续预训练（FCP）后性能显著下降（甚至低于基线），去除GRPO后推理质量下降，去除OCR校正后定位IoU明显降低。
- **表4**：法医持续预训练消融——单独预训练分类会损害OCR/定位，加入3D法医学习改善定位但OCR仍低，最终模型（含OCR参考接地）取得最佳综合性能。

## 4. 资源与算力

论文中未明确说明具体使用的GPU型号、数量及训练时长。仅在实现细节中提到：
- 模型使用LoRA微调（rank=64），优化器为AdamW，学习率从1e-4衰减至0。
- 预训练在收集的数据上训练了1个epoch。
- 微调阶段在TFR训练集上进行。
- 未提及具体硬件配置或计算成本。

## 5. 实验数量与充分性

- **实验组数**：
  - 主对比实验（表2）：对比了4个基础MLLM的预训练版和微调版、2个现有MLLM方法（FakeShield、SIDA）及其变体，共约12种方法，在4个测试集上测试，总计约192个数据点（12方法×4指标×4测试集）的表格。
  - 模块消融（表3）：5种设置（基线、去掉FCP、去掉GRPO、去掉OCR校正、完整模型），在4个测试集上×4指标，共80个数据点。
  - 预训练消融（表4）：5种设置（无预训练、仅分类、分类+3D-FL、分类+OCR参考接地、全量），同样80个数据点。
  - 另注：表2中还包含了仅TFR微调版本的对比，实际上包含了多种基础MLLM的微调结果，实验量充足。

- **充分性与公平性**：
  - 实验覆盖了多个主流MLLM，且在同一训练/测试条件下对比，公平性较好。
  - 消融实验系统性地验证了每个模块的必要性，逻辑清晰。
  - 加入了OOD测试集（CIS、CTM、CL），检验泛化能力，增加了实验深度。
  - 但论文未报告随机种子或多次重复实验的方差，可能影响统计可靠性。

## 6. 主要结论与发现

1. **TextShield-R1在所有评估维度上显著超越现有方法**，包括图像级分类、篡改文本识别、定位和推理解释质量。
2. **法医持续预训练是关键**：通过大规模自然图像伪造数据预训练，有效弥合通用MLLM与篡改文本检测任务之间的差距；同时保留OCR能力。
3. **GRPO强化学习有效降低标注依赖并增强推理**：仅使用25%完全标注数据，性能与全标注微调相当（表3中设置3 vs 5），说明奖励函数成功引导模型自主学习。
4. **OCR校正显著提升定位精度**：在Test、CIS、CTM、CL四个测试集上，定位IoU分别从42.7提升至57.8、56.6→61.0、57.9→68.3、32.3→40.6。
5. **TFR基准填补了现有基准的七项空白**：涵盖多域、多语言、多种篡改技术（含最新AIGC方法），并支持跨风格、跨方法、跨语言的OOD评估。

## 7. 优点

- **创新性**：首次将强化学习（GRPO）引入篡改文本检测任务，设计针对性奖励函数，且无需模型架构修改，易于迁移至其他MLLM。
- **实用性**：
  - 法医持续预训练利用廉价自然图像数据，降低任务门槛。
  - OCR校正无需额外训练，直接利用现有OCR引擎提升定位，计算开销小。
- **全面性**：构建的TFR基准规模大（>45k）、覆盖广（多域、多语言、多篡改方式），且首个包含推理注释，对社区贡献较大。
- **可解释性**：模型输出结构化推理过程（`<think>`），提升可信度。

## 8. 不足与局限

- **实验覆盖方面的局限**：
  - 未提供多次重复实验的统计方差，无法评估结果稳定性。
  - 未对比其他强化学习方法（如PPO、DPO），仅用GRPO。
  - 未在真实生产环境（如大规模在线系统）中测试延迟和吞吐量。
- **偏差风险**：
  - TFR基准虽覆盖16种语言，但训练集语言分布不均（英语22312、中文13303，其余较少），可能对少数语言表现偏差。
  - 伪造图像生成方式（如GPT-4o生成）可能引入特定伪影模式，与真实世界伪造存在分布差异。
- **应用限制**：
  - 模型以Qwen2.5-VL-7B为基础，参数量较大（7B），推理资源需求高，不利于轻量级部署。
  - OCR校正依赖外部OCR引擎的可用性和准确性，在文本极度密集或字体罕见时可能匹配失败。
  - 论文未讨论对对抗性篡改（如精心设计规避检测的伪造）的鲁棒性。
- **资源未明确**：未报告训练所需硬件配置和时间，影响可复现性。

（完）
