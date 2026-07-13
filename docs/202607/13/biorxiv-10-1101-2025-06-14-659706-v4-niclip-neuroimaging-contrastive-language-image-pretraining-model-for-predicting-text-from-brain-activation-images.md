---
title: "NiCLIP: Neuroimaging contrastive language-image pretraining model for predicting text from brain activation images"
title_zh: NiCLIP：用于从脑激活图像预测文本的神经影像对比语言-图像预训练模型
authors: "Peraza, J. A., Kent, J. D., Nichols, T. E., Poline, J.-B., de la Vega, A., Laird, A. R."
date: 2026-07-11
pdf: "https://www.biorxiv.org/content/10.1101/2025.06.14.659706v4.full.pdf"
tags: ["query:contrastive"]
score: 8.0
evidence: 对比学习用于对齐文本和脑图像
tldr: 现有神经影像功能解码方法依赖有限指标，难以捕获文本语义。NiCLIP基于23000余篇神经科学文章，利用对比语言-图像预训练（CLIP）对齐脑激活图与认知文本。评估表明，使用全文文章和精心策划的认知本体时性能最优，领域微调大语言模型（如BrainGPT）与基础模型表现相近。NiCLIP能从人脑连接组计划（HCP）的组级激活图准确预测情感、语言、运动等认知任务，并精确刻画杏仁核、海马体等区域功能，但在噪声个体级激活图上存在局限。该工作为神经影像定量功能解码提供了强大工具，推动了假设生成与科学发现。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-06-14-659706-v4/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1825, \"height\": 1810, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-06-14-659706-v4/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1722, \"height\": 1984, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-06-14-659706-v4/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1711, \"height\": 1868, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-1101-2025-06-14-659706-v4/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1803, \"height\": 1594, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-06-14-659706-v4/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1845, \"height\": 726, \"label\": \"Table\"}, {\"url\": \"assets/tables/biorxiv/biorxiv-10-1101-2025-06-14-659706-v4/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1702, \"height\": 1439, \"label\": \"Table\"}]"
motivation: 现有功能解码方法难以从出版物文本中提取语义，大语言模型与对比学习为文本-脑关联提供了新范式。
method: 利用23000多篇神经科学文章的全文和摘要，训练对比语言-图像预训练（CLIP）模型以学习文本与脑激活模式的关联。
result: NiCLIP在组级激活图上准确预测认知任务，使用全文和认知本体时性能最优，但个体级噪声激活图仍面临挑战。
conclusion: NiCLIP是神经影像功能解码的重要进步，可为科学家提供假设生成和科学发现的量化工具。
---

## 摘要
多年来，从脑激活图中预测认知过程一直是神经科学界的一个悬而未决的问题。元分析功能解码方法旨在通过提供与特定脑区相关的行为特征的定量估计来解决这一问题。现有方法在神经影像元分析中面临固有挑战，特别是在整合出版物中的文本信息时，因为它们依赖于无法捕捉文本语义上下文的有限指标。将大语言模型（LLMs）与先进的深度对比学习模型（例如CLIP）相结合，用于对齐文本和图像，已经革新了神经影像元分析，可能为功能解码挑战提供解决方案。在这项工作中，我们提出了NiCLIP，一个对比语言-图像预训练模型，能够从脑激活模式预测认知任务、概念和领域。我们利用超过23,000篇神经科学文章来训练一个用于文本-脑关联的CLIP模型。对NiCLIP预测的评估表明，当使用全文文章而非摘要，以及使用具有精确任务-概念-领域映射的精选认知本体时，性能达到最优。此外，领域特定的微调LLMs（例如BrainGPT模型）表现出与其基础LLMs在数值上相似的性能。我们的结果表明，NiCLIP能够从人类连接组项目提供的组级激活图中准确预测多个领域（例如情绪、语言、运动）的认知任务，并精确刻画特定脑区（包括杏仁核、海马体和颞顶联合区）的功能角色。然而，NiCLIP在处理嘈杂的个体级激活图时表现出局限性。NiCLIP代表了神经影像定量功能解码的重要进展，为研究人员提供了一个用于假设生成和科学发现的强大工具。

## Abstract
Predicting cognitive processes from brain activation maps has remained an open question within the neuroscience community for many years. Meta-analytic functional decoding methods aim to tackle this issue by providing a quantitative estimation of behavioral profiles associated with specific brain regions. Existing methods face intrinsic challenges in neuroimaging meta-analysis, particularly in consolidating textual information from publications, as they rely on limited metrics that do not capture the semantic context of the text. The combination of large language models (LLMs) with advanced deep contrastive learning models (e.g., CLIP) for aligning text with images has revolutionized neuroimaging meta-analysis, potentially offering solutions to functional decoding challenges. In this work, we present NiCLIP, a contrastive language-image pretrained model that predicts cognitive tasks, concepts, and domains from brain activation patterns. We leveraged over 23,000 neuroscientific articles to train a CLIP model for text-to-brain association. Evaluation of NiCLIP predictions revealed that performance is optimized when using full-text articles instead of abstracts, as well as a curated cognitive ontology with precise task-concept-domain mappings. Furthermore, domain-specific fine-tuned LLMs (e.g., BrainGPT models) show numerically similar performance to their base LLM counterparts. Our results indicated that NiCLIP accurately predicts cognitive tasks from group-level activation maps provided by the Human Connectome Project across multiple domains (e.g., emotion, language, motor) and precisely characterizes the functional roles of specific brain regions, including the amygdala, hippocampus, and temporoparietal junction. However, NiCLIP showed limitations with noisy subject-level activation maps. NiCLIP represents a significant advancement in quantitative functional decoding for neuroimaging, offering researchers a powerful tool for hypothesis generation and scientific discovery.

---

## 论文详细总结（自动生成）

# NiCLIP 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：从脑激活图中推断认知过程（即“反向推理”）是神经科学长期未解决的问题。现有元分析功能解码方法主要依赖脑图谱数据库（如BrainMap、Neurosynth）和传统自然语言处理技术（如TF‑IDF）对文本建模，但TF‑IDF是“词袋”模型，无法捕捉语义上下文和词间关系，并且受限于固定词汇表。
- **整体含义**：结合大语言模型（LLMs）和对比学习（如CLIP）来对齐脑激活图与关联文本，有望实现更准确、更灵活的功能解码。本文提出NiCLIP，首次将LLM驱动的CLIP模型用于正式的反向推理，能够从脑激活模式预测认知任务、概念和领域，为神经影像元分析和假设生成提供强大工具。

## 2. 论文提出的方法论

- **核心思想**：利用对比语言‑图像预训练（CLIP）框架，将来自神经科学文章的文本（全文学术文本）与坐标派生的脑激活图在共享潜在空间中对齐；再通过贝叶斯后验概率和认知本体实现结构化解码（任务→概念→领域）。
- **关键技术细节**：
  1. **数据准备**：从PMC下载约23,865篇fMRI文章，使用Pubget提取全文和激活坐标。文本用预训练LLM（BrainGPT‑7B‑v0.2等）分块平均得到文档级嵌入；脑图使用MKDA（半径10mm球）将坐标转化为二元激活图，并用DiFuMo 512区域图谱降维得到512维嵌入。
  2. **CLIP训练**：文本编码器包含一个投影块和两个残差块，图像编码器包含三个残差块；使用InfoNCE损失和自监督学习，超参数参考NeuroConText（batch size=128，lr=5e-4，weight decay=0.1，epoch=50，early stopping patience=10）。训练采用22‑折交叉验证（验证集）和23‑折交叉验证（测试集）。
  3. **NiCLIP解码**：使用认知本体（Cognitive Atlas）中的任务名称+定义，计算其嵌入与目标脑图嵌入在CLIP潜在空间中的余弦相似度，经softmax得到似然P(A|T)；先验P(T)由任务在训练语料中的平均余弦相似度经softmax确定；后验P(T|A) ∝ P(A|T)P(T)。然后通过 noisy‑OR 模型将任务后验传播到概念P(C|A)和领域P(D|A)。

- **公式描述**（算法流程）：
  - 似然：P(A|T) = softmax(cos(Emb(T), Emb(A)))
  - 先验：P(T) = softmax(mean(cos(Emb(T), all docs)))
  - 后验：P(T|A) = P(A|T)P(T) / Σ P(A|T')P(T')
  - 概念：P(C|A) = 1 - ∏_{T measures C} (1 - P(T|A))
  - 领域：P(D|A) = 1 - ∏_{C in D} (1 - P(C|A))

## 3. 实验设计

- **数据集/场景**：
  - 训练：23,865篇PMC神经科学文章（含有坐标和全文）。
  - 测试与验证：基于HCP S1200的7个任务域（情绪、赌博、语言、运动、关系、社会、工作记忆）的组级平均激活图；个体级激活图（787名受试者）；6个ROI图（杏仁核、海马体、脑岛、纹状体、右颞顶联合区、腹内侧前额叶皮质）；以及变体映射（仅正激活、仅负激活等）。
  - 认知本体：完整Cognitive Atlas（851个任务，912个概念）与精简版（Menuet等提供，常用任务+更完整映射）。

- **Benchmark**：NiCLIP对比Neurosynth相关解码器和GC-LDA（这两者仅输出任务级预测）。此外，在文本‑脑关联评估中对比不同LLM（BrainGPT‑7B‑v0.1/0.2、Mistral‑7B‑v0.1、Llama‑2‑7b‑chat‑hf）和不同文本部分（摘要 vs 全文）；在解码评估中对比本体版本（完整 vs 精简）、嵌入策略（仅任务名 vs 名+定义）。

- **对比方法**：Neurosynth（相关解码器）、GC-LDA（无监督概率主题模型）；以及NeuroConText风格配置（Mistral‑7B‑v0.1 + 全文）。

## 4. 资源与算力

- 论文**未明确说明**所用GPU型号、数量、训练时长等具体算力信息。仅在致谢中提及使用了FIU IRCC的高性能计算资源。因此无法量化训练NiCLIP的硬件细节。

## 5. 实验数量与充分性

- **实验数量**：论文进行了多组实验：
  - CLIP文本‑脑关联评估：4种LLM × 2种文本部分（摘要/全文）= 8个配置，每个配置重复22‑/23‑折交叉验证，报告Recall@10, Recall@100, Mix&Match。
  - NiCLIP解码评估：在HCP组级图上测试了多种配置（LLM种类、文本部分、本体版本、嵌入策略），共约20+种配置（表2），并对比两个基线。
  - 在ROI、个体级、变体映射上也进行了预测实验。
  - 额外在IBC数据集上验证了泛化性（补充材料图S10）。

- **充分性与公平性**：实验设计较为全面。交叉验证降低了过拟合风险；基线方法（Neurosynth、GC-LDA）使用标准实现；消融实验（摘要 vs 全文，本体版本等）揭示了关键因素。但个体级实验仅给出定性结果，未提供统计显著性或置信区间；基线仅在任务级比较，概念/领域级无基线对照。另外，未报告超参数敏感性分析。总体而言，实验覆盖了主要变量，但个体级和跨数据集验证可进一步加强。

## 6. 论文的主要结论与发现

- **最优配置**：使用全文训练CLIP、BrainGPT‑7B‑v0.2、精简版Cognitive Atlas、任务名+定义嵌入时，NiCLIP在组级HCP解码任务上达到最优（任务Recall@4=62.86%，概念43.57%，领域90.48%），显著优于Neurosynth（最高20.71%）和GC-LDA。
- **全文优于摘要**：使用全文训练的模型在所有指标上均优于仅使用摘要。
- **领域LLM优势有限**：BrainGPT（领域微调）与基础模型（Mistral、Llama）在数值上接近，性能差异不显著；作用更显著的是文献全文本和精简本体。
- **组级解码有效，个体级困难**：NiCLIP在组级激活图上预测准确（见图2）；在个体级激活图上表现较差（任务Recall@4=38.19%），仅对个别任务（情绪、社会）较好。
- **ROI解码成功**：NiCLIP能准确刻画6个经典ROI的功能（例如rTPJ-社会认知98.5%，杏仁核-情绪65.5%），且小ROI选择性更高。
- **本体重要性**：精简版Cognitive Atlas（更完整任务‑概念映射）显著优于原始完整本体。
- **模型可生成非明显假设**：如纹状体被预测为语言功能，这反映了训练文献中的共现模式，需谨慎解释。

## 7. 优点

- **方法论创新**：首次将LLM+CLIP框架用于神经影像反向推理，利用对比学习直接学习文本‑脑图共享表示，避免TF‑IDF的语义损失。
- **结构化解码**：利用认知本体实现多层次（任务、概念、领域）预测，提高了解释性。
- **数据规模大**：使用超23,000篇含有全文本和坐标的文献，远超此前元分析工作。
- **充分消融分析**：系统比较了LLM类型、文本部分、本体版本、嵌入策略对性能的影响，提供了实用建议。
- **开源资源丰富**：代码、教程、在线演示均已公开，有利于社区使用和复现。
- **外部泛化验证**：在IBC数据集上获得一致性能（补充材料），表明一定泛化能力。

## 8. 不足与局限

- **训练样本小**：CLIP模型仅用约2.4万对文本‑脑图训练，远小于常规CLIP的百万级，可能限制表示能力。
- **个体级解码失败**：模型在噪声个体级图上表现不佳，实际推广应用受限（研究者通常使用组级图）。
- **训练‑推理文本不匹配**：CLIP训练使用长篇全文，解码时使用短的任务名+定义，存在分布偏移，可能影响任务级精度。
- **先验假设偏差**：先验P(T)基于文献频率，对稀有任务不公，且似然P(A|T)非严格统计似然，后验应视为排名分数而非校准概率。
- **本体不完善**：Cognitive Atlas为社区驱动，任务‑概念映射可能存在偏差或不完整（如运动任务仅与工作记忆关联缺乏“运动”概念）。精简版虽有改善，但仍可能遗漏。
- **仅处理正激活**：训练数据主要来自正激活坐标，解码负激活或双向对比图可能不可靠。
- **缺乏负面结果和统计检验**：实验未报告置信区间或假设检验，部分结论基于数值差异而非统计显著。
- **跨数据集验证有限**：只验证了HCP和IBC，缺乏对更多独立数据集（如ABIDE、ABCD）的评估；泛化性尚需更广泛验证。
- **算力信息缺失**：未提供GPU型号、数量、训练时长等，影响可复现性和资源预估。

（完）
