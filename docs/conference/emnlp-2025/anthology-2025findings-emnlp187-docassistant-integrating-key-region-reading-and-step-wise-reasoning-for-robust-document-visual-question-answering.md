---
title: "DocAssistant: Integrating Key-region Reading and Step-wise Reasoning for Robust Document Visual Question Answering"
title_zh: DocAssistant：集成关键区域读取与逐步推理的鲁棒文档视觉问答
authors: "Jinxu Zhang, Qiyuan Fan, Yu Zhang"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.187.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 文档VQA可解释性增强
tldr: 现有文档理解模型缺乏可解释性，忽略源文档证据。DocAssistant通过改进视觉编码器聚焦关键信息，并引入逐步推理机制，增强了模型的可解释性，在文档视觉问答任务上取得鲁棒性能。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.187/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 791, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.187/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1484, \"height\": 802, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.187/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1445, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.187/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 781, \"height\": 343, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.187/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1473, \"height\": 846, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.187/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1412, \"height\": 842, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 789, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 439, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1640, \"height\": 734, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 791, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 780, \"height\": 539, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 788, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.187/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1293, \"height\": 486, \"label\": \"Table\"}]"
motivation: 现有文档理解模型难以聚焦关键信息且缺乏可解释性，直接生成答案。
method: 提出有效的视觉语言适应方法，将文本融入视觉编码器，并构建逐步问答数据集。
result: 在文档VQA任务上提升了准确性和可解释性。
conclusion: 逐步推理与关键区域读取能有效提升文档理解模型的可解释性。
---

## Abstract
Understanding the multimodal documents is essential for accurately extracting relevant evidence and using it for reasoning. Existing document understanding models struggle to focus on key information and tend to generate answers straightforwardly, ignoring evidence from source documents and lacking interpretability. In this work, we improve the visual encoder to focus on key information relevant to the question and address the shortcomings of existing document visual question-answering datasets to provide the model with the ability to answer questions step-wise, dubbed DocAssistant. Specifically, for the visual side, we propose an effective vision-language adaptation that fuses text into visual encoders without compromising the performance of the original model. For the language side, we use Multimodal Large Language Models (MLLMs) as data generators and checkers to produce high-quality step-wise question-and-answer pairs for document images. We then use the generated high-quality data to train our enhanced model, specifically designed to solve complex questions that require reasoning or multi-hop question answering. The experimental results demonstrate the effectiveness of the model.

---

## 论文详细总结（自动生成）

# DocAssistant 论文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：现有文档视觉问答（DVQA）模型在回答复杂问题时倾向于直接生成答案，缺乏对源文档中关键信息的定位和利用，也缺乏中间推理步骤，导致可解释性差、准确率低。
- **背景**：多模态大模型在简单文档理解上表现良好，但在复杂布局、需要多步推理的文档（如海报、图表）上仍存在信息定位错误和推理缺失。
- **目标**：设计一个像人类一样先定位问题相关区域、再逐步推理的鲁棒文档理解模型，同时提升准确性和可解释性。

## 2. 方法论
### 核心思想
- 视觉侧：引入轻量级**Mixture-of-Modality Adapter**，插入视觉编码器最后L层，动态调整注意力聚焦问题关键词相关区域，不破坏原有模型能力。
- 语言侧：利用强MLLM（InternVL2-26B）作为数据生成器，通过模板和few-shot生成逐步推理的QA对；再用LLaMA3-70B作为数据检查器，结合OCR/表格工具验证每一步的正确性，过滤噪声数据。
- 训练：使用过滤后的高质量逐步推理数据，在2B规模的InternVL2-Chat模型上微调（仅训练适配器、投影模块和LoRA）。

### 关键技术细节
- **Mixture-of-Modality Adapter**：采用类似LLaMA-AdapterV2的late fusion策略，使用RepAdapter结构，共享下采样投影，公式为 \( Z' = Z + s \cdot f(Z) \)。
- **数据生成**：对现有训练集补充理由（template + MLLM）；对无标注图像生成新三元组（问题、理由、答案）。DocVQA每图生成3个新问题，InfoVQA每图生成4个，ChartQA借助Chart-to-text扩展数据。
- **数据检查**：利用DePlot将图表转为表格，OCR提取普通文档文本作为金标签；LLM逐步骤判断信息提取和推理是否正确，错误则丢弃。过滤比例约16-23%。

## 3. 实验设计
- **数据集**：DocVQA（扫描文档）、InfographicVQA（复杂布局海报）、ChartQA（图表，含人工标注和合成数据）。
- **评价指标**：DocVQA/InfoVQA使用ANLS，ChartQA使用Relax Accuracy。
- **对比方法**：
  - 纯文本：T5
  - 文本+布局+视觉：LayoutLMv3、DocFormerv2
  - 端到端无OCR：Donut、Pix2Struct
  - 多模态大模型：mPLUG-DocOwl2、SMoLA-PaLI-3、ScreenAI、Qwen2-VL、InternVL2（基线）
- **对比策略**：Zero-shot、Few-shot、SFT（使用生成数据训练）。

## 4. 资源与算力
- 文中明确说明：所有实验在**2块80G A100 GPU**上完成。
- 训练设置：**2个epoch**，batch size = 8，学习率 = 4e-5。
- 模型规模：**2B参数**，训练部分为适配器层（N-2）、投影模块和语言模型的LoRA。

## 5. 实验数量与充分性
- **主要结果表（表2）**：对比了11种方法，涵盖不同模态和规模。
- **策略对比（表3）**：Zero-shot、Few-shot、SFT三种策略，分别在三个数据集上测试。
- **消融实验（表4）**：分别验证适配器、数据扩展、数据过滤的效果。
- **问题类型分析（表5）**：将问题分为Color、Text、Spatial、Count、Reasoning五类，分别报告性能。
- **数据规模影响（表7）**：1/3、2/3、全部数据对比。
- **ChartQA细粒度分析（表8）**：区分Augmented和Human子集，按类型细分。
- **定性分析（图5、图6）**：展示注意力热图和输出样例，以及错误案例。
- **充分性评价**：实验设计较为全面，覆盖了主要对比、消融、类型分析、规模影响等，对比方法包括当时主流模型，结论较客观。

## 6. 主要结论与发现
- DocAssistant在三个数据集上均优于除Qwen2-VL外的所有对比模型，尤其在InfoVQA和ChartQA上提升显著（+5.2%、+2.5%）。
- Mixture-of-Modality Adapter在基线基础上带来稳定提升（+1.6%~2.7%）。
- 数据扩展和过滤均带来进一步增益（表4）。
- 逐步推理训练对Count和Reasoning类型问题提升最大（表5）。
- 小模型（2B）通过高质量生成数据可以追赶甚至超越更大模型（如8B、5B）的性能。
- 模型输出具有可解释性，能提供中间步骤和证据。

## 7. 优点
- **轻量有效**：适配器仅插入少量层，不破坏原模型，训练参数少。
- **通用数据生成流水线**：模板+few-shot+检查器，可迁移到其他文档数据集。
- **提升可解释性**：模型输出逐步推理和证据，用户可验证正确性。
- **小模型高效**：2B模型通过数据增强达到大模型级性能，降低计算成本。
- **实验充分且分析细致**：包含多种消融、类型分析、策略对比，结论可靠。

## 8. 不足与局限
- **数据生成依赖MLLM能力**：模板和few-shot可能无法覆盖所有复杂场景，跨领域泛化性未知。
- **视觉编码器仍有瓶颈**：对跨区域、多结构数据（如复杂图表中颜色识别）仍有误识别错误。
- **仅支持单页文档**：无法处理多页文档。
- **问答类型局限**：Color类问题依赖原始视觉编码器能力，提升有限。
- **计算资源要求不低**：尽管模型小，但数据生成和检查需使用26B和70B模型，整体成本较高。

（完）
