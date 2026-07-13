---
title: "FAMUS: A Few-Shot Learning Framework for Large-Scale Protein Annotation"
title_zh: FAMUS：面向大规模蛋白质注释的少样本学习框架
authors: "Shur, G., Burstein, D."
date: 2026-07-07
pdf: "https://www.biorxiv.org/content/10.64898/2026.03.08.710366v2.full.pdf"
tags: ["query:contrastive"]
score: 8.0
evidence: 对比学习用于蛋白质注释
tldr: 基因功能注释面临依赖单一最相似序列、阈值设定困难及稀疏家族注释不准的挑战。本文提出FAMUS框架，利用对比学习将查询序列与所有profile HMM的相似度向量作为表示，并纳入未注释序列作为负样本训练。在KEGG Orthology和PANTHER家族任务上，FAMUS分别超越KofamScan和InterProScan。该框架是首个基于对比学习的模块化注释系统，支持自定义数据库，易于集成。
source: biorxiv
selection_source: fresh_fetch
figures_json: "[{\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-08-710366-v2/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 900, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-08-710366-v2/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1609, \"height\": 1118, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-08-710366-v2/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 954, \"height\": 1387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-08-710366-v2/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1632, \"height\": 786, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-08-710366-v2/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1603, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/biorxiv/biorxiv-10-64898-2026-03-08-710366-v2/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1607, \"height\": 612, \"label\": \"Figure\"}]"
motivation: 现有自动注释工具依赖单一最相似序列，难以设置阈值，对稀疏家族注释不准确。
method: 提出对比学习框架FAMUS，用查询与所有profile HMM的相似度向量表示序列，并纳入未注释序列作为负样本。
result: 在KEGG Orthology和PANTHER家族注释任务上，FAMUS分别优于KofamScan和InterProScan。
conclusion: 首个基于对比学习的全面模块化注释框架，支持预定义和用户自定义数据库，可集成到分析流程。
---

## 摘要
预测基因功能是基因组和宏基因组数据分析中关键且具有挑战性的步骤。当前的自动注释工具通常依赖查询数据库中单个最相似的序列，并且难以稳健地设置注释的命中阈值。每个注释的蛋白质稀疏性使得对代表性不足的家族进行可靠的功能分配变得困难。在此，我们提出了一种用于功能注释的对比学习框架。FAMUS（使用监督对比学习的功能注释方法）将查询序列与一系列谱隐马尔可夫模型进行比较，并将相似性得分转换到一个紧凑的向量空间中，该空间最小化来自同一家族的蛋白质之间的距离。查询与所有谱的相似性得分被用于其表示，而不仅仅考虑排名最高的命中。在训练过程中，未注释的序列被作为负例纳入，从而无需用户定义阈值即可稳健地检测参考数据库范围之外的蛋白质。使用这种方法，FAMUS在KEGG直系同源注释上优于KEGG原生的KofamScan，在PANTHER家族注释上优于InterPro的InterProScan。因此，我们使用来自KEGG直系同源、InterPro家族、OrthoDB和EggNOG数据库的蛋白质家族创建了四个蛋白质注释模型。所有四个模型均可通过conda包和用户友好的Web服务器获得，使用户能够注释大规模数据集。FAMUS是第一个基于对比学习的全面、模块化注释框架。它支持预定义数据库和用户自定义数据库进行定制注释，并且可以轻松集成到任何基因组和宏基因组分析流程中，以促进准确、大规模的功能注释。

## Abstract
Predicting gene function is a pivotal and challenging step in genomic and metagenomic data analysis. Current automatic annotation tools typically rely on the single most similar sequence from the query database and struggle to robustly set hit thresholds for annotation. The sparsity of proteins per annotation makes it challenging to confidently assign gene function for underrepresented families. Here, we present a contrastive learning framework for functional annotation. FAMUS (Functional Annotation Method Using Supervised contrastive learning) compares query sequences to a full array of profile Hidden Markov Models and transforms the similarity scores into a condensed vector space that minimizes the distance of proteins from the same family. The similarity scores of a query to all profiles are used for its representation instead of considering only the top-ranking hit. Unannotated sequences are incorporated as negative examples during training, enabling robust detection of proteins that fall outside the scope of the reference database without requiring a user-defined threshold. Using this approach, FAMUS outperformed KEGGs native KofamScan for KEGG Orthology annotation and InterPros InterProScan for PANTHER family annotation. We thus created four protein annotation models using protein families from the KEGG Orthology, InterPro family, OrthoDB, and EggNOG databases. All four models are available as a conda package and via our user-friendly web server, allowing users to annotate large-scale datasets. FAMUS is the first comprehensive and modular annotation framework based on contrastive learning. It supports both pre-defined and user-specific databases for tailored annotation, and can be easily integrated into any genomic and metagenomic analysis pipeline to facilitate accurate, large-scale functional annotation.