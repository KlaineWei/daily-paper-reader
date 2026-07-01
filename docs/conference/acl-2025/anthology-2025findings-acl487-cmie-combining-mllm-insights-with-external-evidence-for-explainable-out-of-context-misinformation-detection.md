---
title: "CMIE: Combining MLLM Insights with External Evidence for Explainable Out-of-Context Misinformation Detection"
title_zh: CMIE：结合多模态大模型洞察与外部证据的可解释上下文外虚假信息检测
authors: "Fanxiao Li, Jiaying Wu, Canyuan He, Wei Zhou"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.487.pdf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释的上下文外虚假信息检测
tldr: 针对多模态大模型在检测上下文外虚假信息时难以捕捉深层语义关系且噪声影响准确率的问题，本文提出CMIE，融合MLLM推理与外部证据进行可解释检测。实验表明该方法显著提升了检测准确性和可解释性。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.487/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 811, \"height\": 680, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.487/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 185, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.487/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 897, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.487/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1664, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.487/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 817, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.487/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 655, \"height\": 404, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.487/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1642, \"height\": 750, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.487/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 639, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.487/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 764, \"height\": 600, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.487/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 715, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.487/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 505, \"height\": 131, \"label\": \"Table\"}]"
motivation: 多模态大模型在检测上下文外虚假信息时面临深层语义理解不足和噪声干扰的挑战。
method: 融合MLLM的推理能力与外部证据，实现可解释的虚假信息检测。
result: 在多个数据集上检测准确率提升，同时提供了可解释的证据。
conclusion: CMIE为可解释的虚假信息检测提供了有效方案。
---

## Abstract
Multimodal large language models (MLLMs) have demonstrated impressive capabilities in visual reasoning and text generation. While previous studies have explored the application of MLLM for detecting out-of-context (OOC) misinformation, our empirical analysis reveals two persisting challenges of this paradigm. Evaluating the representative GPT-4o model on direct reasoning and evidence augmented reasoning, results indicate that MLLM struggle to capture the deeper relationships—specifically, cases in which the image and text are not directly connected but are associated through underlying semantic links. Moreover, noise in the evidence further impairs detection accuracy.To address these challenges, we propose CMIE, a novel OOC misinformation detection framework that incorporates a Coexistence Relationship Generation (CRG) strategy and an Association Scoring (AS) mechanism. CMIE identifies the underlying coexistence relationships between images and text, and selectively utilizes relevant evidence to enhance misinformation detection. Experimental results demonstrate that our approach outperforms existing methods.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）
- **研究背景**：社交媒体上多模态虚假信息（如图文不匹配、上下文外（OOC）图片复用）日益泛滥，传统检测方法依赖小模型训练或检索外部证据但缺乏可解释性。多模态大语言模型（MLLMs）具备强大的视觉推理与文本生成能力，为可解释的OOC检测提供了新可能。
- **核心问题**：作者通过探索性实验发现，MLLM在直接推理时趋于保守（易将弱关联的虚假样本判为真实）；引入外部证据后，MLLM难以捕捉图像与文本之间的**深层语义关系**（如间接主题关联），且**证据噪声**会干扰判断，导致性能提升有限。
- **研究动机**：如何合理融入外部证据，让MLLM既能识别深层关联，又能过滤噪声，实现高效、可解释的OOC检测。

### 2. 方法论：核心思想、关键技术细节、算法流程
- **核心思想**：提出CMIE框架，先利用MLLM生成图像-文本对的**共存关系**（即两者为何能共同出现的深层语义链接），再基于该关系对每条检索到的外部证据进行**关联评分**，筛选高相关证据辅助最终判断。
- **关键技术细节**：
    1. **共存关系生成（CRG）**：  
       输入图像对(I, T)，使用MLLM生成共存关系描述 \( R_{co} \) 和共存分数 \( S_{co} \)（0-10）。公式：\((R_{co}, S_{co}) = MLLM(I, T)\)。
    2. **关联评分机制（AS）**：  
       对每条外部证据 \( E_{ti} \)，结合 \( R_{co} \) 计算相关性分数 \( s_i \) 与解释 \( exp_i \)。公式：\((s_i, exp_i) = MLLM(R_{co}, E_{ti})\)。
    3. **最终判断**：  
       将共存关系、关联分数与解释、证据集、图像实体、原始图像-文本一并输入MLLM，生成预测标签 \( Y_p \) 和解释 \( Y_e \)。公式：\((Y_p, Y_e) = MLLM(R_{co}, \{S, exp, E_t\}, \{E_e\}, (I, T))\)。
- **算法流程（文字说明）**：  
  ① 对输入图像-文本对，通过网页爬虫获取图像出现页面的标题作为外部证据，并通过Google Vision API提取图像实体。  
  ② 若无外部证据，则直接使用MLLM内部知识进行判断。  
  ③ 若有证据，先使用CRG步骤生成共存关系与分数。  
  ④ 使用AS步骤对每一条证据评分，生成评分与解释。  
  ⑤ 将所有信息（共存关系、证据评分、实体等）拼接成提示，由MLLM输出最终标签和可解释理由。

### 3. 实验设计：数据集、基准与对比方法
- **数据集**：NewsCLIPpings 的 Merged/Balance 子集（最大OOC基准），训练集71,072样本，验证集7,024，测试集7,264。
- **对比方法**：
    - **基于内部知识**：CLIP（线性分类器微调）、DT-Transformer（局部Transformer增强）。
    - **基于外部证据**：CCN（循环一致性检查）、SEN（立场提取网络）、SNIFFER（微调InstructBLIP+GPT-4生成解释）、LEMMA（查询生成检索+MLLM）、作者探索的DR（直接推理）和AR（证据增强推理）。
- **评估指标**：准确率（Accuracy）、精确率（Precision）、召回率（Recall）、F1分数（区分真实/虚假样本）。

### 4. 资源与算力
- **论文未明确说明所用GPU型号、数量及训练时长**。CMIE基于OpenAI API（GPT-4o），无模型微调，因此主要算力消耗在推理调用上，文中仅提到API温度设为0.1。SNIFFER需要微调InstructBLIP，计算成本较高，而CMIE无需微调，算力需求相对较低。

### 5. 实验数量与充分性
- **实验数量**：包含6大类实验——主表对比（Table 2）、消融研究（Table 3）、不同MLLM适应性（GPT-4o与Gemini-pro，Figure 5）、稳定性分析（错误传播，Table 4）、Prompt鲁棒性测试（88%和89%准确率）、解释质量人工评估（50个样本，10位评估者，Figure 6）、案例研究（Figure 7）。
- **充分性评价**：实验覆盖全面，从性能对比、组件贡献、多模型迁移、鲁棒性、可解释性等维度验证。消融实验逐步添加组件，清晰展示各模块效果。人工评估设计合理（5分量表，有标签先验）。但仅在单个数据集（NewsCLIPpings）上评测，未涉及其他OOC基准（如VERITE），泛化性验证稍显不足。总体实验设计客观、公平，消融与对比充分。

### 6. 论文的主要结论与发现
- MLLM（GPT-4o）在不微调时即可达到与CCN、SEN等持平的性能，但倾向于保守判断（高召回率识别真实样本，但对虚假样本识别偏弱）。
- 直接融入外部证据（AR）能提升虚假样本召回率，但MLLM易被噪声误导，且无法抓取核心验证线索，导致整体提升有限。
- 提出的CMIE通过CRG捕获深层语义关联，通过AS筛选高相关证据，在准确率（0.91）、虚假样本精确率（0.93）等指标上全面超越所有基线，且生成的可解释理由质量最高（人工评分3.9/5，优于LEMMA的3.5）。
- CMIE能有效缓解上游错误传播（97%的传播错误来自虚假样本，但下游仍保持可接受性能）。

### 7. 优点
- **方法新颖**：首次将“共存关系生成”与“关联评分”引入OOC检测，区别于传统的浅层词汇匹配或单纯证据拼接。
- **无需微调**：完全基于MLLM推理能力，降低计算成本和标注依赖，易于部署。
- **强可解释性**：输出包含共存关系、证据相关性评分、最终推理链，人工评估证明其解释质量高。
- **鲁棒性好**：对提示变化敏感度低，且通过AS机制部分抵御证据噪声和上游误差传播。
- **跨模型迁移**：在GPT-4o和Gemini-pro上均观察到性能提升，说明框架具有通用性。

### 8. 不足与局限
- **数据集单一**：仅在NewsCLIPpings上评测，未在VERITE等其他OOC基准上验证，泛化性有待加强。
- **MLLM幻觉风险**：MLLM自身可能产生虚假的共存关系或评分，影响最终判断（论文承认此局限性并计划未来采用减幻方法）。
- **人工解释差异**：部分生成解释与人类标准仍存在差异，尽管模拟人认知过程，但一致性有待提高。
- **依赖大规模API调用**：实际操作中需反复调用MLLM（CRG、AS、最终判断），推理成本可能较高（论文未量化）。
- **错误传播风险**：虽然稳定性分析显示可缓解，但第一阶段共存关系分类错误（尤其是虚假样本误判为弱关联）仍会导致部分性能下降（召回率降至0.70）。

（完）
