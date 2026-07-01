---
title: "MemeDetoxNet: Balancing Toxicity Reduction and Context Preservation"
title_zh: MemeDetoxNet：平衡毒性降低与上下文保留
authors: "Gitanjali Kumari, Jitendra Solanki, Asif Ekbal"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.1286.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 利用CLIP可解释性进行有毒模因检测，与伪造检测解释性相关
tldr: 针对网络环境中有害模因的泛滥问题，提出MemeDetoxNet框架，利用CLIP的可解释性识别模因中的视觉和文本毒性元素，并通过大语言模型替换冒犯性文字和模糊毒性区域，在降低毒性的同时保持上下文语义。实验表明该方法有效平衡了毒性降低与内容保留。该工作展示了可解释性技术在内容安全检测中的实际应用价值。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 425, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 683, \"height\": 273, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 490, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1133, \"height\": 1066, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1134, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025.findings-acl.1286/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1122, \"height\": 781, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 803, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 659, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1662, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1504, \"height\": 216, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 668, \"height\": 642, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 808, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1171, \"height\": 297, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1166, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1662, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 662, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1235, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1295, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1231, \"height\": 570, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1551, \"height\": 1299, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1546, \"height\": 1349, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1175, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025.findings-acl.1286/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1660, \"height\": 275, \"label\": \"Table\"}]"
motivation: 现有模因毒性检测缺乏可解释性，无法定向降低毒性。
method: 利用CLIP可解释性定位毒性区域，结合LLM替换文本和模糊图像。
result: 在毒性降低和上下文保留上取得平衡，优于基线。
conclusion: 可解释性方法能有效指导模因去毒，促进内容安全。
---

## Abstract
Toxic memes often spread harmful and offensive content and pose a significant challenge in online environments. In this paper, we present MemeDetoxNet, a robust framework designed to mitigate toxicity in memes by leveraging fine-tuned pre-trained models. Our approach utilizes the interpretability of CLIP (Contrastive Language-Image Pre-Training) to identify toxic elements within the visual and textual components of memes. Our objective is to automatically assess the immorality of toxic memes and transform them into morally acceptable alternatives by employing large language models (LLMs) to replace offensive text and blurring toxic regions in the image. As a result, we proposed MemeDetoxNet that has three main primitives: (1) detection of toxic memes, (2) localizing and highlighting toxic visual and textual attributes, and (3) manipulating the toxic content to create a morally acceptable alternative. Empirical evaluation on several publicly available meme datasets shows a reduction in toxicity by approximately 10-20%. Both qualitative and quantitative analyses further demonstrate MemeDetoxNet’s superior performance in detoxifying memes compared to the other methods. These results underscore MemeDetoxNet’s potential as an effective tool for content moderation on online platforms.

---

## 论文详细总结（自动生成）

# MemeDetoxNet：平衡毒性降低与上下文保留——详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：社交媒体上模因（meme）结合图像与文字传播有毒内容（如仇恨、歧视、色情等），现有检测模型多聚焦于分类（toxic/non-toxic），但缺乏**可解释性**和**主动去毒能力**，无法精准定位并修改具体的有毒属性。
- **必要性**：单纯“检测”不足以遏制有害内容传播；需要一种既能识别毒性又能生成道德可接受替代品的框架，同时保持模因的原始语境与意图。
- **整体意义**：提出 **MemeDetoxNet**，利用 CLIP 的可解释性（GradCAM + 词掩码）定位图像与文本中的有毒区域，再通过 LLM 替换有毒文本、高斯模糊有毒图像区域，实现毒性降低（~10-20%）平衡上下文保留，为内容审核提供可解释、可操作的解决方案。

## 2. 论文提出的方法论

### 2.1 核心思想
- 基于 **CLIP** 微调，联合编码文本与图像特征；利用 **GradCAM** 获取图像注意力热点，通过 **逐词掩码** 计算每个词对毒性得分的贡献，从而定位有毒元素。
- 对定位到的有毒部分进行干预：图像用**高斯模糊**掩盖，文本用**大语言模型（LLM）** 通过指令微调替换为中性词汇。

### 2.2 关键技术细节
1. **编码阶段**：输入模因文本 \(T_i\) 和图像 \(I_i\)，分别通过 CLIP 编码器得到文本特征 \(f_i^t\) 和图像特征 \(f_i^v\)。
2. **检测阶段**：特征拼接后经线性层+ReLU+Dropout+LogSoftmax 输出二元分类（toxic/non-toxic）。
3. **毒性定位**：
   - **图像**：计算预测概率对最后一层特征图的梯度，生成 GradCAM 热力图，得到每个像素区域的毒性贡献分数。
   - **文本**：对每个词 \(w_i\)，构造掩码（mask）后重新输入分类器，计算原始概率与掩码后期望概率的差值作为该词的重要性分数 \(R_{w_i}\)。
4. **去毒操作**：
   - **图像去毒**：\(I_{\text{dehatified}} = I \odot (1-M) + \text{GaussianBlur}(I) \odot M\)，其中 \(M\) 为有毒区域二值掩码。
   - **文本去毒**：使用 LLM（Gemini 1.0, GPT-3.5-Turbo, Mistral-7B, Llama 3.1）替换有毒词汇，提示词要求生成意义不变的非有毒替代。

### 2.3 辅助模块：Meme Immorality Recognizer (MIR)
- 在大型伦理数据集 ETHICS 上预训练的文本分类器，用于**零样本评估去毒效果**，接受 CLIP 联合嵌入（文本+图像）并输出不道德概率。

## 3. 实验设计

### 3.1 数据集
- **MAMI**（Misogynous Meme Identification）：10,000 训练 / 1,000 测试，性别歧视模因。
- **FHM**（Facebook Hateful Memes）：8,500 训练 / 1,000 测试，合成仇恨模因。
- **Memotion2**：7,500 训练 / 1,500 测试，冒犯/幽默模因（隐式毒性）。
- **MIMIC**：4,044 训练 / 1,010 测试，印地语-英语混合语言性别歧视模因。
- **ETHICS**：用于训练 MIR，含公正、美德、义务论、功利主义、常识等分类 > 13,000 文本样本。

### 3.2 对比方法（Benchmark）
- **VisualBERT**、**MOMENTA**、**PromptHate**、**Pro-Cap**、**LLaVA**（多模态模型）。
- 对比指标：宏 F1 下降率（toxicity reduction）、MIR 评分、BERTScore、人工评分（知识相关性 KR、上下文保留 CP、毒性降低 TR）。

### 3.3 实验数量与充分性
- **主要实验**：
  1. 四组数据集上宏 F1 下降率（表 3），含三种策略（仅模糊、仅文本替换、两者结合）共 12 组结果。
  2. MIR 评估各模型去毒后毒性降低百分比（表 1）。
  3. 人工评估（表 2、4、5），含 KR/CP/TR 及 Cohen's Kappa 一致性检验。
  4. 跨数据集泛化实验（表 18）：在一个数据集训练，在其他三个测试，共 16 组。
  5. 消融：不同 LLM 对比（Gemini、GPT-3.5、Mistral、Llama）及文本替换效果（表 4）。
  6. 可解释性可视化（图 3、4）、误差分析（图 9）。
- **充分性**：覆盖多种毒性类型（显式、隐式、混合语言）、多种去毒策略、人工+自动评估、跨域测试，实验设计较为全面客观。

## 4. 资源与算力
- **GPU**：单张 NVIDIA-GTX-1080Ti（32 GB GPU，实际显存为 8GB？原文 table 6 注释为 32GB，但 A.2 说单张 GTX-1080Ti，可能矛盾，但明确提到算力）。
- **训练配置**：epoch=60，batch size=64，学习率 3e-5 / 1e-4，Adam 优化器，图像大小 224×224，随机种子 42。
- **混合精度**：16-bit 混合精度训练。
- **库**：PyTorch, torchvision, transformers, lightning 等（附录表 6）。
- **未说明**：完整训练总时长（未见直接报告），但数据集规模较小，单 GPU 即可完成。

## 5. 实验数量与充分性总结
- **组数**：约 10+ 组主要定量实验（含自动指标和人工评分），加上消融和跨域泛化共 30+ 组数据点。
- **客观性**：采用宏 F1 下降率、BERTScore、MIR 评分等多角度自动评价，并辅以人工评分及一致性校验，方法对比涉及 5 种主流多模态模型，基准覆盖充分。
- **局限性**：所有实验均在公开英文/印地-英语数据集上，未涉及其他语言或真实在线平台流数据，模拟环境可能高估效果。

## 6. 论文的主要结论与发现
1. **MemeDetoxNet 有效降低毒性 10-20%**，在显式毒性数据集（MAMI、FHM）上效果显著，对隐式毒性（Memotion）和代码混合语言（MIMIC）也具有较好鲁棒性。
2. **同时进行图像模糊与文本替换的策略（Both）优于单一策略**，宏 F1 下降率平均高出 3-5 个百分点。
3. **可解释性定位（GradCAM + 逐词掩码）是实现定向去毒的关键**，避免了盲目修改。
4. 人工评估表明，MemeDetoxNet 在**知识相关性（KR）和上下文保留（CP）** 上表现良好，但存在**隐式毒性误判**和**过度消毒**的挑战。
5. 跨数据集实验显示模型泛化能力中等，对同类型显式毒性迁移较好，对差异大的数据集下降明显。

## 7. 优点（方法或实验设计亮点）
- **创新性**：首次将可解释性（CLIP + GradCAM）融入模因去毒，实现了“检测-定位-修改”全流程自动化。
- **多模态协作**：同时处理文本和图像毒性，保持模态间语义一致性。
- **评估体系完善**：综合自动指标（F1、BERTScore）、自定义 MIR 评分、人工评分（KR/CP/TR）、一致性检验，全面反映去毒质量。
- **消融全面**：分别验证模糊、文本替换、两者结合的效果，并对比多种 LLM。
- **跨域验证**：在四个不同特征的数据集上测试，增加可信度。

## 8. 不足与局限
1. **隐式毒性误判**：对讽刺、文化梗等含蓄有害内容定位不准确，导致去毒不彻底。
2. **过度消毒**：有时会修改无害内容（如幽默词汇），破坏原有语境。
3. **数据集多样性有限**：全部为公开学术数据集，缺乏真实平台流数据、多语言（除印地语外）覆盖不足。
4. **计算依赖**：强依赖 CLIP 和 LLM 的预训练能力，在资源受限场景下部署困难。
5. **模糊操作粗糙**：高斯模糊可能扭曲非毒性元素，影响用户体验。
6. **人类评估规模小**：仅使用 2 名专家标注 100 个样本，可能存在标注偏差。
7. **未讨论对抗性攻击**：模型可能被刻意设计的毒模因绕过。

（完）
