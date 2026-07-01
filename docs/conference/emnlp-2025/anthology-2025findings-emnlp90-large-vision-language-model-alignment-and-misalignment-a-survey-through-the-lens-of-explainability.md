---
title: "Large Vision-Language Model Alignment and Misalignment: A Survey Through the Lens of Explainability"
title_zh: 大型视觉语言模型对齐与错位：可解释性视角的综述
authors: "Dong Shu, Haiyan Zhao, Jingyu Hu, Weiru Liu, Ali Payani, Lu Cheng, Mengnan Du"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.90.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 通过可解释性视角综述LVLM对齐与错位，涵盖目标错位
tldr: 大型视觉语言模型在视觉与文本对齐方面存在挑战。本综述从可解释性角度全面考察了对齐与错位问题，包括表征和行为层面，以及对象、属性和关系三种语义层面的错位。研究揭示了数据、训练等多方面原因导致的错位现象，为后续开发可解释的视觉语言模型提供理论基础。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.90/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.90/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 1052, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.90/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1636, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.90/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 772, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.90/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1628, \"height\": 1545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.90/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 761, \"height\": 447, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.90/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1644, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.90/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1543, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.90/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1538, \"height\": 415, \"label\": \"Table\"}]"
motivation: LVLM中视觉与文本对齐困难导致错位，影响模型可靠性，需要系统分析。
method: 通过可解释性视角，综述对齐机制和错位类型，包括对象、属性、关系三个层级。
result: 揭示了错位来源于多层面的挑战，如数据、训练等。
conclusion: 为理解和改进LVLM对齐提供了可解释性分析框架。
---

## Abstract
Large Vision-Language Models (LVLMs) have demonstrated remarkable capabilities in processing both visual and textual information. However, the critical challenge of alignment between visual and textual representations is not fully understood. This survey presents a comprehensive examination of alignment and misalignment in LVLMs through an explainability lens. We first examine the fundamentals of alignment, exploring its representational and behavioral aspects, training methodologies, and theoretical foundations. We then analyze misalignment phenomena across three semantic levels: object, attribute, and relational misalignment. Our investigation reveals that misalignment emerges from challenges at multiple levels: the data level, the model level, and the inference level. We provide a comprehensive review of existing mitigation strategies, categorizing them into parameter-frozen and parameter-tuning approaches. Finally, we outline promising future research directions, emphasizing the need for standardized evaluation protocols and in-depth explainability studies.

---

## 论文详细总结（自动生成）

# 大型视觉语言模型对齐与错位：可解释性视角的综述 —— 论文总结

## 1. 核心问题与整体含义（研究动机和背景）

- 大型视觉语言模型（LVLMs）在视觉和文本信息处理上取得了显著成果，但视觉与文本表示之间的对齐（alignment）机制尚未被充分理解。
- 对齐不良会导致错位（misalignment）现象，如模型输出与输入图像内容不一致，造成可靠性问题。
- 本文从可解释性（explainability）视角出发，系统梳理LVLM中的对齐与错位问题，旨在为构建更可靠、可信的视觉语言系统提供理论指导和实践框架。

## 2. 方法论：核心思想、关键技术细节、算法流程

- **核心思想**：将对齐拆解为两个层面（表征对齐与行为对齐），将错位按语义粒度分为对象级、属性级和关系级，并从数据、模型、推理三个层面分析错位根源。
- **关键技术细节**：
  - 表征对齐：视觉与文本表示在共享嵌入空间中的相似度（如余弦相似度、互最近邻、核对齐）。
  - 行为对齐：模型在图像描述、视觉问答等任务上的输出准确性。
  - 错位类型：
    - 对象错位：描述中出现了图像中不存在的物体。
    - 属性错位：正确识别物体但属性描述错误（如颜色、大小）。
    - 关系错位：空间或动作关系描述错误。
  - 错位原因：
    - 数据层面：数据不完美（模糊图像、错误标注）、数据不平衡、数据不一致、假阴性、多义性。
    - 模型层面：能力差距（视觉编码器弱于LLM）、预训练-微调知识冲突、知识冲突（视觉信息与LLM先验矛盾）。
    - 推理层面：任务分布偏移（OOD问题）。
- **缓解方法分类**：
  - 参数调优方法：改进训练方案（对比学习、指令微调、RLHF、偏好优化）和改进模型架构（增强视觉编码器、改进连接模块）。
  - 参数冻结方法：增强式（检索增强、生成增强）、推理式（中间表示干预）、解码式（对比解码、注意力重平衡）、后解码式（输出修正）。
- **形式化理论**：视觉和文本是同一潜在语义空间的不同观测投影，用互信息条件独立假设论证对齐的可能性。

## 3. 实验设计：数据集/场景、基准、对比方法

- **POPE基准**：用于评估对象错位，包含三个子集（POPE-Random、POPE-Adversarial、POPE-Popular），评估指标为Accuracy、Precision、Recall、F1。
- **对比方法**：
  - 基线：LLaVa-V1.5-7B
  - 缓解方法：SoM-LLaVA、SID、LogicCheckGPT
- **额外示例**：展示了ChatGPT-4o、Qwen2-VL、DeepSeek-VL2、LLaVa-1.5对三张真实图像（客厅、时代广场、教室）的描述，标注了三种错位类型。
- **基准对比表（附录表3）**：列举了POPE、CHAIR、MME、MMHal-Bench、LLaVa-Bench、LVLM-eHub、GAVIE、CCEval、HaELM等，按评估维度（对象/属性/关系错位、认知推理、指令遵循）和评估方式（传统/第三方模型）分类。

## 4. 资源与算力

- 文中未明确说明大规模训练或进行大量消融实验所需的算力。
- 仅在附录F中提及：示例实验使用A100 PCIE 80GB GPU，float16精度，模型从Hugging Face加载，保持默认参数。这仅用于展示生成示例，并非系统实验。

## 5. 实验数量与充分性

- 本文是一篇综述，本身不包含原创实验。
- 表1只提供了一组小规模对比实验（基线+三种方法在POPE上的表现），用于说明不同方法的性能与计算成本权衡。
- 实验数量少，不足以全面评估缓解方法的普适性；结果仅针对LLaVa-V1.5-7B，缺乏跨模型、跨基准的系统性比较。
- 实验设计尚可：报告了多个指标（Acc、Precision、Recall、F1），并记录了推理时间，揭示了不同方法在精确率与召回率之间的权衡。
- 总体而言，实验部分对于一篇综述来说可接受，但作为方法比较而言不够充分。

## 6. 论文的主要结论与发现

- LVLM的对齐包括表征对齐和行为对齐，二者相互关联。
- 错位可以按照语义粒度分为对象、属性、关系三个层次，这为诊断和缓解提供了清晰框架。
- 错位源于数据、模型、推理三个层面的多种因素，包括数据质量、能力差距、知识冲突、任务分布偏移等。
- 现有缓解策略可分为参数调优和参数冻结两大类，各有优缺点（如RLHF高质量但昂贵，对比解码效率高但可能降低语言理解）。
- 不同缓解方法对同一问题可能产生矛盾的理解（例如注意力不平衡的方向），导致方法设计上的分歧。
- 未来需要标准化评估基准、深入的可解释性分析、架构创新以及真实世界部署验证。

## 7. 优点

- **结构清晰**：从对齐定义、训练流程、理论基础到错位分类、原因分析、缓解策略，形成完整体系。
- **可解释性视角**：强调通过内部表示和行为分析理解对齐机制，与当前可解释AI趋势契合。
- **类别全面**：对缓解方法进行了详细分类（参数调优/冻结，增强/推理/解码/后解码），并分析了每种方法背后的假设和局限。
- **真实案例**：提供了多个流行LVLM的生成示例并标记错位类型，直观说明问题。
- **理论支撑**：借用Platonic Representation Hypothesis和互信息理论为对齐提供理论可能性。

## 8. 不足与局限

- **范围局限**：仅关注视觉与语言两种模态，未涵盖音频、视频、传感器等多模态场景。
- **缺乏统一基准**：指出当前评估标准散乱，缺乏能同时覆盖三种错位类型和推理能力的综合基准。
- **实验验证有限**：综述本身没有大规模实验，单表实验不足以证明方法的优劣；未来需要更系统的比较。
- **偏差风险**：可能偏向于引用某些方法或模型，未完全覆盖所有新兴技术。
- **应用限制**：大部分缓解方法仅在基准上验证，未在自动驾驶、医疗影像等高风险场景中测试，实际可靠性未知。
- **可解释性深度不足**：虽然提出应使用可解释性技术诊断错位，但未给出具体实现案例或验证。

（完）
