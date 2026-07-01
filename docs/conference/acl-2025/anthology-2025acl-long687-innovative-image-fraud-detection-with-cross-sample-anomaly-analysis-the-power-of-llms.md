---
title: "Innovative Image Fraud Detection with Cross-Sample Anomaly Analysis: The Power of LLMs"
title_zh: 创新的跨样本异常分析图像伪造检测：LLM的力量
authors: "QiWen Wang, Junqi Yang, Zhenghao Lin, Zhenzhe Ying, Weiqiang Wang (王维强), Chen Lin"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.687.pdf"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 跨样本异常检测及可解释的图像伪造检测
tldr: "该论文针对图像伪造检测任务中视觉线索不足的问题，提出基于LLM的跨样本异常检测框架CSIAD。该方法通过分析同类图像间的逻辑不一致性来检测细微篡改痕迹，并天然支持检测结果的可解释性。在新建的真实世界伪造基准CrossCred上，CSIAD的F1分数比现有最优方法提升79.6%，同时部署成本低。工作为可解释伪造检测和异常检测提供了有效新范式。"
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1302, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1579, \"height\": 1458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 775, \"height\": 322, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 775, \"height\": 312, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1647, \"height\": 895, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 523, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 314, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 727, \"height\": 398, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 746, \"height\": 429, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1612, \"height\": 1648, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 834, \"height\": 303, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 837, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 372, \"height\": 48, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.687/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 374, \"height\": 47, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 818, \"height\": 406, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 828, \"height\": 666, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 786, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 772, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 719, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 665, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 296, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1167, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1665, \"height\": 2127, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 913, \"height\": 1486, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.687/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 398, \"height\": 286, \"label\": \"Table\"}]"
motivation: 现有图像伪造检测方法依赖视觉特征，难以识别无视觉篡改痕迹的伪造文档图像。
method: 提出CSIAD框架，利用LLM对相似图像进行跨样本逻辑一致性分析，识别异常并生成自然语言解释。
result: "在CrossCred基准上F1分数提升79.6%，显著优于现有方法，且解释结果可理解。"
conclusion: LLM驱动的跨样本异常分析能有效检测细微伪造，同时提供可解释性，实用价值高。
---

## Abstract
The financial industry faces a substantial workload in verifying document images. Existing methods based on visual features struggle to identify fraudulent document images due to the lack of visual clues on the tampering region. This paper proposes CSIAD (Cross-Sample Image Anomaly Detection) by leveraging LLMs to identify logical inconsistencies in similar images. This novel framework accurately detects forged images with slight tampering traces and explains anomaly detection results. Furthermore, we introduce CrossCred, a new benchmark of real-world fraudulent images with fine-grained manual annotations. Experiments demonstrate that CSIAD outperforms state-of-the-art image fraud detection methods by 79.6% (F1) on CrossCred and deployed industrial solutions by 21.7% (F1) on business data. The benchmark is available at https://github.com/XMUDM/CSIAD.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：金融行业需大量验证文档图像，现有图像伪造检测方法主要依赖视觉特征（如边缘、纹理），但金融文档（如发票、付款凭证）背景简单、布局结构化了，篡改区域几乎无视觉线索，导致SOTA方法在细微篡改场景下失效。此外，现有方法缺乏可解释性，不利于人工快速复核。
- **动机**：人工审核中，审查员可通过对比相似图像间的逻辑不一致性发现伪造。受此启发，提出利用LLM进行跨样本图像异常检测，既提升检测准确率，又提供自然语言解释。
- **整体含义**：证明LLM驱动的跨样本逻辑推理能有效弥补传统视觉方法的不足，为金融文档微伪造检测提供新范式。

## 2. 论文提出的方法论
- **核心思想**：CSIAD（Cross-Sample Image Anomaly Detection）通过两个阶段工作：  
  1. **检索集成**：综合视觉特征（CN-CLIP ViT-B/16）、稠密文本向量（CN-CLIP RoBERTa-base）、稀疏文本向量（HashingVectorizer）进行相似度计算，召回与查询图像相关的图像集合 \(S_q\)。  
  2. **事实驱动的跨样本推理**：  
     - **样本特定规则生成**：利用LLM（Qwen2.5-72B-Instruct）从结构化文本中生成逻辑规则（如“相同账号需对应相同地址”），通过温度采样（T=1.0）增加规则多样性。  
     - **事实驱动的规则验证**：从无异常事实库 \(G\) 中检索相关图像，用LLM检查规则是否在正常样本中成立，仅保留事实一致的规则 \(R_{ver}\)。  
     - **规则驱动的异常检测**：用验证后的规则对 \(S_q\) 逐条检测，生成初始异常结论集合 \(C_{ini}\)。  
     - **事实驱动的异常验证**：再次利用事实库验证异常结论是否与原始文本一致，过滤幻觉结论，得到最终 \(C_{ver}\)。
- **关键技术细节**：  
  - 检索相似度公式：\(s(I_q, I_i) = \alpha \cos(v_q, v_i) + \beta \cos(e_q, e_i) + \gamma \cos(t_q, t_i)\)，权重经网格搜索得 \(\alpha=0.5, \beta=0.1, \gamma=0.4\)。  
  - 规则生成和验证均使用prompt引导LLM进行分步推理。  
  - 事实库来自历史提交图像，经过基础异常过滤确保极低异常率。

## 3. 实验设计
- **数据集与场景**：  
  - 新基准 **CrossCred**：来自真实金融场景，含109个异常案例（共396张图像，平均3.63张/案例）及109张无异常图像，覆盖61种文档类型。每个案例有细粒度人工标注（篡改区域和解释）。对比现有数据集（DocTamper, TextTamper）全为合成数据、单样本、粗粒度标注。  
  - 真实业务数据（Biz.Data）：工业确认的异常案例，用于额外评估。
- **对比方法**：  
  - 传统视觉方法：DTD、Tifdm。  
  - LLM推理基线：CoT Prompt、Self-Consistency、Self-Check、Self-Reflection（均以检索后图像为基础，部分辅以业务规则库BizRule）。  
  - 工业方案：部署在业务系统的方案（方法未公开）。
- **评估指标**：  
  - 粗粒度：Acc, Rec, Pre, F1（二分类判异常）。  
  - 细粒度：Rec†, Pre†, F1†（异常点定位和解释的语义匹配）。

## 4. 资源与算力
- **文中未明确说明GPU型号、数量、训练时长**。仅提到使用了两个LLM：Qwen2-VL（结构化文本提取）和Qwen2.5-72B-Instruct（其余任务）。所有LLM调用温度除规则生成为1.0外均为0.0。未提及任何训练或微调过程，因此算力消耗主要来自推理。

## 5. 实验数量与充分性
- **实验数量**：包含多组实验：  
  - 主表（表2）：在CrossCred上与所有基线对比（粗粒度+细粒度）。  
  - 检索方式对比（Retriever→Single vs Ensemble），并报告Recall@1/3/5（表3）。  
  - 消融实验（表4）：温度采样（TS）、规则生成（RG）、规则验证（RV）、异常验证（AV）的独立移除及组合。  
  - 反射质量分析（表5）：比较不同LLM推理策略下的无效/有毒/有效反射比例。  
  - 与工业方案对比（表6）：CrossCred和Biz.Data上评估。  
  - 错误分析（附录C）：按阶段统计错误分布。
- **充分性**：实验设计较全面，覆盖了核心模块消融、检索策略、反射质量、实际业务场景，且指标兼顾粗粒度和细粒度。对比方法包括传统CV和多种LLM策略，并引入工业方案，客观性较好。但CrossCred规模较小（仅109个异常案例），可能限制了统计显著性。

## 6. 论文的主要结论与发现
- CSIAD在CrossCred上F1达81.9%，比SOTA视觉方法提升79.6%，在真实业务数据上F1达85.7%，比工业方案提升21.7%。  
- 集成检索（视觉+文本）显著提升相关图像召回率（Recall@5从77.7%→90.6%），进而提高检测效果。  
- 事实驱动的规则验证和异常验证有效减少LLM幻觉：在保持高召回的同时，显著提升精确率（消融实验显示移除规则验证后Pre下降14.2%）。  
- 温度采样（T=1.0）有助于生成更多样化的规则，提升召回（+7.31%）。  
- 反射质量分析表明CSIAD的有毒反射率最低（2.1%），有效反射率最高（54.5%），优于自检、自反等方法。

## 7. 优点
- **方法创新**：首次将跨样本逻辑异常检测引入图像伪造检测，利用LLM进行自然语言推理，克服视觉线索不足的瓶颈。  
- **高可解释性**：输出包含违规规则、受影响的记录ID和自然语言解释，便于人工复核和流量监控。  
- **事实驱动验证机制**：利用无异常事实库自动验证规则和结论，减少LLM幻觉，无需人工标注规则。  
- **实际部署价值**：在真实业务数据上显著超越工业方案，低异常率场景下仍有效。  
- **基准构建严谨**：CrossCred来自真实场景，经四步构建（分组、LLM预标注、人工审核、去重平衡），提供细粒度标注，填补了现有基准的空白。

## 8. 不足与局限
- **数据集规模有限**：CrossCred仅含109个异常案例和505张图像，且限定于金融文档，可能无法代表更广泛的伪造场景。数据来源受限于时间范围和隐私保护，类型分布不完全均衡。  
- **依赖LLM能力**：CSIAD需要较强的指令遵循能力和推理能力，使用较小LLM可能导致性能下降。论文未实验替代模型（如开源小模型）的鲁棒性。  
- **检索模块的局限性**：检索阈值δ和权重需手工调优，通用性有待验证。文中仅用网格搜索确定，未探讨自适应方法。  
- **结构化文本误差**：错误分析显示52.38%的失败源于多模态LLM提取文本不准（如模糊、变形），这是当前瓶颈。  
- **未进行跨数据集泛化实验**：仅在CrossCred和业务数据上测试，未在公开文档篡改数据集（如DocTamper）上评估，通用性存疑。  
- **计算成本**：调用大模型（72B）进行多步推理，实时性可能受挑战，论文未讨论推理延迟或成本。

（完）
