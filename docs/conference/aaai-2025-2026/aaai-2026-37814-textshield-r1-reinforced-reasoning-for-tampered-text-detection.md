---
title: "TextShield-R1: Reinforced Reasoning for Tampered Text Detection"
title_zh: TextShield-R1：面向篡改文本检测的强化推理
authors: "Chenfan Qu, Yiwu Zhong, Jian Liu, Xuekang Zhu, Bohan Yu, Lianwen Jin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37814/41776"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 使用MLLM进行篡改文本检测并生成推理解释
tldr: 该论文针对篡改文本检测中MLLM难以识别微观伪影、定位精度低且依赖昂贵标注的问题，提出TextShield-R1，首个基于强化学习的MLLM解决方案。通过法医持续预训练和强化学习推理，模型不仅检测篡改文本，还能生成可理解的推理解释。实验证明其在检测精度和解释质量上均取得显著提升，推动了可解释伪造检测的发展。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1789, \"height\": 993, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 857, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 915, \"height\": 446, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 886, \"height\": 179, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 879, \"height\": 596, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 880, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37814/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 878, \"height\": 280, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 752, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1844, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37814/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1826, \"height\": 283, \"label\": \"Table\"}]"
motivation: 现有MLLM在篡改文本检测中定位精度低且依赖昂贵标注。
method: 提出基于强化学习的MLLM，结合法医持续预训练和推理生成可解释结果。
result: 在篡改文本检测和解释生成上达到先进性能。
conclusion: 为可解释伪造检测提供了新范式。
---

## Abstract
The growing prevalence of tampered images poses serious security threats, highlighting the urgent need for reliable detection methods. Multimodal large language models (MLLMs) demonstrate strong potential in analyzing tampered images and generating interpretations.
However, they still struggle with identifying micro-level artifacts, exhibit low accuracy in localizing tampered text regions, and heavily rely on expensive annotations for forgery interpretation. To this end, we introduce TextShield-R1, the first reinforcement learning based MLLM solution for tampered text detection and reasoning. Specifically, our approach introduces Forensic Continual pre-training, an easy-to-hard curriculum that well prepares the MLLM for tampered text detection by harnessing the large-scale cheap data from natural image forensic and OCR tasks. During fine-tuning, we perform Group Relative Policy Optimization with novel reward functions to reduce annotation dependency and improve reasoning capabilities.  At inference time, we enhance localization accuracy via OCR Rectification, a method that leverages the MLLM’s strong text recognition abilities to refine its predictions.
Furthermore, to support rigorous evaluation, we introduce Text Forensics Reasoning (TFR) benchmark, comprising over 45k real and tampered images across 16 languages, 10 tampering techniques, and diverse domains. Rich reasoning-style annotations are included, allowing for comprehensive assessment. Our TFR benchmark simultaneously addresses seven major limitations of existing benchmarks and enables robust evaluation under cross-style, cross-method, and cross-language conditions. Extensive experiments demonstrate that TextShield-R1 significantly advances the state of the art in interpretable tampered text detection.

---

## 论文详细总结（自动生成）

# TextShield-R1 论文详细总结

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：随着图像篡改技术普及，篡改文本图像对安全构成严重威胁。多模态大语言模型（MLLM）虽有潜力分析篡改图像并生成解释，但在篡改文本检测中面临三个关键瓶颈：
  1. **任务对齐不足**：基础MLLM预训练于宏观语义感知任务（如图像描述、目标识别），而篡改文本检测需要微观级别的伪影感知，导致模型混淆或过拟合。
  2. **严重依赖昂贵标注**：现有方法依赖GPT-4o等闭源模型生成的“伪造解释”标注，成本高且存在隐私风险（如身份证、合同图像）；且监督微调会损害模型自身推理能力。
  3. **定位精度差**：MLLM难以预测精确边界框，尤其面对密集文本。外挂传统定位模型会带来延迟和不一致问题。
- **研究意义**：首次提出基于强化学习的MLLM解决方案，实现统一且可解释的篡改文本检测，同时构建了全面的基准TFR，弥补现有基准的七项缺陷（如仅限单一领域、缺乏完全生成图像、无OOD评估等）。

### 2. 论文提出的方法论
- **整体框架**：TextShield-R1基于Qwen2.5-VL-7B，包含预训练、微调、推理三个阶段，不修改模型架构，具有即插即用性。
- **核心思想**：通过低成本数据（自然图像伪造+OCR任务）进行持续预训练，再用强化学习（GRPO）结合精心设计的奖励函数降低对标注的依赖并提升推理能力，最后用OCR矫正增强定位。

#### 关键模块：
- **Forensic Continual Pre-training（FCP）**：
  - **易到难课程**：先利用大规模自然图像伪造数据集（CASIA、IMD20、NIST16等）训练MLLM区分真实/完全生成/局部篡改图像。
  - **3D Forensic Learning**：对局部篡改的自然图像，除了分类外，还要求输出篡改对象的描述（通过Describe Anything Model生成）、边界框坐标、mask字符串（32x32的0/1序列），从三个维度增强监督。
  - **OCR参考接地任务**：为防止遗忘OCR能力，随机插入两种子任务——给定边界框输出文本，或给定文本输出边界框。最终得到一个同时具备法医感知和OCR能力的模型。

- **Group Relative Policy Optimization (GRPO)**：
  - **冷启动**：先用约25%的完整标注数据（含伪造解释）做监督微调，建立初始策略。
  - **奖励函数设计（5个）**：
    1. **真实/伪造分类奖励**：正确分三类（真实、完全生成、局部篡改）得1分，否则0。
    2. **伪造方法检测奖励**：判断是复制-粘贴还是生成，正确得1。
    3. **篡改定位奖励**：IoU>0.5则取IoU值，否则0。
    4. **篡改文本OCR奖励**：1 - 归一化Levenshtein距离。
    5. **格式奖励**：强制输出包含 `<think>...</think>` 和 `<answer>...</answer>` 标签。
  - 通过GRPO，模型从部分标注数据中学会推理，无需完整伪造解释。

- **OCR Rectification**：
  - 推理时，若模型预测图像存在篡改，先用OCR引擎（如通用高精度OCR）提取所有文本内容和边界框。
  - 对每个预测的篡改文本，在OCR结果中寻找匹配项（基于Levenshtein距离）；若找到唯一匹配，则用OCR框替换MLLM的预测框；若多个匹配，选择与MLLM预测框Distance IoU最大的框；若无匹配（距离阈值>0.2），保留原预测。
  - 该方法充分利用MLLM的文本识别能力来弥补其定位弱点。

### 3. 实验设计
- **基准与数据集**：
  - 自建**Text Forensics Reasoning (TFR) benchmark**：45,971张伪造图像 + 45,514张对应真实图像，覆盖文档、场景文本、身份证件三类领域，10种篡改技术（含GPT-4o生成、GAN、Diffusion模型），16种语言。包含三个OOD子集：
    - Cross-Image-Style (CIS)：训练集中未见过的图像风格。
    - Cross-Tampering-Method (CTM)：三种未见篡改方法（TextDiffuser-2、SR-Net、Control-Net）。
    - Cross-Language (CL)：10种未见语言。
  - 训练/测试划分：训练集25,861张，测试集7,174张，CIS 5,481张，CTM 2,373张，CL 5,082张。
  - 提供了详细的推理式伪造解释标注（由GPT-4o生成+人工校对）。
- **对比方法**：
  - 官方预训练版本：GPT-4o、MiniCPM-V 2.6、InternVL3-2B/8B、Qwen2.5-VL-3B/7B。
  - 在TFR全数据集上微调的版本：同上各模型（含FakeShield、SIDA及其替换骨干的变体）。
- **评估指标**：
  - **Cls**：三分类准确率（真实/生成/篡改）。
  - **OCR**：篡改文本识别准确率。
  - **Loc.**：篡改文本定位IoU。
  - **Res.**：推理质量，采用余弦相似度、Rouge-L、BLEU的平均值。

### 4. 资源与算力
- **未明确说明**：论文正文未提及使用的GPU型号、数量、训练时长、总计算开销等具体信息。仅在实现细节中提到LoRA rank=64、AdamW优化器、学习率1e-4衰减至0、预训练1个epoch。训练数据量：预训练阶段使用120K自然局部篡改+120K完全生成+60K真实（COCO）+60K真实（LAION），加上TFR训练集。微调阶段使用TFR训练集（约25.8K张图像）。但具体算力配置缺失。

### 5. 实验数量与充分性
- **实验组数**：主要实验包括：
  - **对比实验（Table 2）**：在4个子集（Test/CIS/CTM/CL）上对比了11种方法（含官方预训练版和微调版），每种方法报告4个指标，共176个数据点。
  - **消融实验**：
    - Table 3：逐步去掉FCP、GRPO、OCR Rectification，共5种设置×4子集×4指标。
    - Table 4：对FCP内部模块消融（自然图像分类、3D-FL、OCR接地），共5种设置×4子集×4指标。
  - 总计约10组（消融+对比）×4子集×4指标 = 160+个数值结果。
- **充分性评估**：
  - 覆盖了多个MLLM架构和尺寸，且同时比较了有/无在TFR上微调的版本，排除因数据量差异导致的偏差。
  - 消融设计清晰，逐步验证各模块贡献，尤其表3中“移除FCP”后性能下降很多，表明预训练至关重要。
  - 设置OOD子集（CIS/CTM/CL）评估泛化性，对比方法也报告了这些结果，增加了公平性。
  - 指标全面（分类、OCR、定位、推理质量），但**推理质量的评估指标（余弦相似度+Rouge-L+BLEU）可能偏向匹配程度而非真正理解深度**，有一定局限性。
  - **样本量充足**：测试集7174张，OOD子集各2000-5000张，统计上可靠。

### 6. 论文的主要结论与发现
1. **TextShield-R1在所有四项指标上显著优于所有对比方法**。在Test集上，分类准确率88.1%（次优Qwen2.5-VL-7B微调版79.1%），OCR准确率47.6%（次优24.3%），定位IoU 57.8%（次优18.2%），推理质量58.8%（次优42.9%）。
2. **FCP是关键**：移除FCP后性能全面下降，甚至低于基线（不微调），说明没有预训练的模型难以从强化学习中有效学习。
3. **GRPO有效降低标注依赖**：完整模型（使用25%标注数据）性能与使用全量标注的模型（w.o. GRPO）相当（Test上Cls 88.1% vs 87.6%，OCR 47.6% vs 46.8%等），证实强化学习能补偿缺少的解释标注。
4. **OCR Rectification提升定位精度**：在Test集上，Loc从42.7%提升至57.8%；在CTM和CL上也有显著提升。
5. **OOD泛化性优秀**：在CIS（未知图像风格）、CTM（未知篡改方法）、CL（未知语言）上，TextShield-R1仍保持领先，尤其CTM上定位IoU达68.3%（次优34.2%），显示出强泛化能力。

### 7. 优点
- **方法创新性**：首次将强化学习（GRPO）用于篡改文本检测，设计针对性奖励函数，减少对人工标注的依赖，同时提升了推理能力。
- **课程预训练设计巧妙**：利用廉价自然图像伪造数据和OCR任务，通过易到难课程弥合宏观预训练与微观篡改检测的差距，并解决了灾难性遗忘问题。
- **OCR Rectification轻量有效**：无需额外训练，直接利用MLLM自身文本识别能力与现有OCR引擎交互，显著提升定位。
- **基准构建全面**：TFR填补了领域、伪造类型、语言、OOD评估等多方面空白，且包含推理标注，可推动可解释检测研究。
- **实验设计严谨**：对比了多种先进MLLM及变体，消融实验完整，OOD设置极具说服力。
- **代码与数据开源**：论文提供了仓库链接，利于复现。

### 8. 不足与局限
- **算力资源未公开**：缺失训练所需GPU数量、型号和时长，影响可复现性评估。对于对资源敏感的读者，难以判断部署成本。
- **推理质量指标有限**：BLEU、Rouge-L、余弦相似度主要衡量生成文本与参考文本的重叠度，对“解释逻辑正确性”的区分度不足，可能无法反映模型是否真正理解伪影。
- **OCR矫正依赖外部OCR引擎**：若OCR引擎本身在特定场景（如艺术字体、严重光照）下表现差，可能会引入错误。论文未讨论OCR引擎选择或鲁棒性。
- **仅测试了Qwen2.5-VL-7B**：虽然声称方法通用，但实验仅在7B模型上进行，未在更大或更小尺度（如3B、72B）上验证，结论的规模泛化性未证明。
- **训练数据领域偏差**：自然图像伪造数据集来自特定来源（如CASIA、IMD20等），可能不覆盖所有现实中的篡改样式，导致模型对某些新型伪造（如最新AIGC）的泛化能力仍待验证。
- **TFR中AIGC图像质量**：虽然使用了GPT-4o等先进模型生成，但人工过滤后仍可能存在低质量样本影响评估。同时，完全生成的图像和局部篡改的图像比例可能不均，论文未分析类别平衡对训练的影响。
- **隐私问题尚未完全解决**：虽然强化学习减少了对敏感图像的标注依赖，但OCR Rectification阶段仍需要OCR引擎处理输入图像，如果OCR引擎部署在云端，仍可能涉及隐私泄露风险。

（完）
