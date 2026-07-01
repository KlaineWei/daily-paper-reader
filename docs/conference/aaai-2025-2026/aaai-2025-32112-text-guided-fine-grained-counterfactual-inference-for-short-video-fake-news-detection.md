---
title: Text-Guided Fine-grained Counterfactual Inference for Short Video Fake News Detection
title_zh: 文本引导的细粒度反事实推理用于短视频假新闻检测
authors: "Linlin Zong, Wenmin Lin, Jiahui Zhou, Xinyue Liu, Xianchao Zhang, Bo Xu, Shimin Wu"
date: 2025-04-11
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/32112/34267"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 使用反事实推理实现可解释的假新闻检测
tldr: 本文针对短视频假新闻检测中模态异质性问题，提出文本引导的细粒度反事实推理框架TGFC-SVFN。通过因果推理提示文本作为教师模型，消除模态偏见并进行知识蒸馏，利用反事实推理提供可解释的决策依据。实验表明该方法在性能优于现有方法的同时，提供了可解释性分析，是面向假新闻检测的可解释方法。
source: AAAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32112/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32112/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 843, \"height\": 312, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32112/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1656, \"height\": 813, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32112/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32112/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 839, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32112/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 832, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2025-accepted/aaai-2025-32112/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 841, \"height\": 266, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32112/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 744, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32112/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 778, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2025-accepted/aaai-2025-32112/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1316, \"height\": 689, \"label\": \"Table\"}]"
motivation: 现有方法忽视模态异质性，导致检测性能次优。
method: 提出文本引导的反事实推理，通过教师模型知识蒸馏和多头注意力融合多模态。
result: 在短视频假新闻数据集上取得领先性能。
conclusion: 方法结合因果推理实现可解释的假新闻检测。
---

## Abstract
Detecting fake news in short videos is crucial for combating misinformation. Existing methods utilize topic modeling and co-attention mechanism, overlooking the modality heterogeneity and resulting in suboptimal performance. To address this issue, we introduce Text-Guided Fine-grained Counterfactual Inference for Short Video Fake News detection (TGFC-SVFN). TGFC-SVFN leverages modality bias removal and teacher-model-enhanced inter-modal knowledge distillation to integrate the heterogeneous modalities in short videos. Specifically, we use causality-based reasoning prompts guided text as teacher model, which then transfers knowledge to the video and audio student models. Subsequently, a multi-head attention mechanism is employed to fuse information from different modalities. In each module, we utilize fine-grained counterfactual inference based on a diffusion model to eliminate modality bias. Experimental results on publicly available fake short video news datasets demonstrate that our method outperforms state-of-the-art techniques.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **问题**：短视频平台上的假新闻检测面临严重的**模态异质性**问题（视频、音频、文本、评论等模态格式与特征差异大）。现有方法（如主题建模、共注意力机制）忽视模态间的异构性，导致融合效果次优。
- **核心挑战**：  
  - **模态偏见放大**：某些模态中的虚假相关（如“real”关键词与真实标签的虚假关联）会通过知识蒸馏放大，影响检测。  
  - **教师模型不充分**：现有跨模态知识蒸馏直接将完整特征序列作为教师，引入与任务无关的干扰信号，误导学生模型学习。
- **背景**：短视频平台已成为假新闻传播的主要渠道，现有研究多聚焦于文本-图像双模态，缺乏针对短视频多模态（视频、音频、文本、评论、用户信息）的完整解决方案。

## 2. 论文提出的方法论

### 核心思想
提出 **TGFC-SVFN**（Text-Guided Fine-grained Counterfactual Inference for Short Video Fake News Detection）：
- 以**文本模态作为教师模型**（因其在假新闻检测中优势明显），通过**因果推理提示**增强教师模型能力，再通过**知识蒸馏**将知识传递给视频和音频学生模型。
- 在每个模块（教师、学生、融合）中引入**基于扩散模型的细粒度反事实推理**，消除模态偏见。

### 关键技术细节

1. **因果推理提示生成**  
   - 利用 ChatGPT-3.5 对每条新闻进行三步推理（初步信息检查 → 常识与逻辑判断 → 最终结果与解释），得到推理文本 \( g \)，用于指导教师模型聚焦关键语义特征。

2. **特征提取**  
   - 文本：BERT（标题、转录、评论、用户信息、推理文本）  
   - 视频：VGG19（关键帧）+ C3D（视频片段）  
   - 音频：VGGish

3. **教师模型学习**  
   - **多文本对齐**：使用 GPT-2 分析长文本时序演化，再用跨模态 Transformer（CMT）进行语义对齐，拼接得到融合特征 \( F_{TG} \)。  
   - **因果推理提示引导**：计算推理特征 \( f_g \) 与 \( F_{TG} \) 的 KL 散度损失 \( L_g \)。  
   - **反事实去偏**：对 \( F_{TG} \) 施加扩散模型的前向加噪构造 \( T \) 个反事实场景 \( x_t \)，保留反向去噪过程，计算反事实预测与事实预测的差值（总间接效应 TIE）作为去偏后的预测概率，构建去偏损失 \( L_{debiase} = \mu_1 L_C + \mu_2 L_d \)，其中 \( L_C \) 为交叉熵，\( L_d \) 为扩散重建损失。

4. **学生模型学习**  
   - 视频、音频分别独立训练。使用 CMT 进行多模态对齐得到 \( F_V, F_A \)。  
   - 知识蒸馏：采用**皮尔逊相关系数**作为度量，计算师生模型之间类间和类内相关性，得到蒸馏损失 \( L_{dis} \)。  
   - 同样施加反事实去偏。

5. **多模态融合与分类**  
   - 多头注意力机制融合教师与学生特征得到 \( F_M \)，再次施加反事实去偏。总体损失 \( L = L_{debiase} + \alpha L_{CE} \)。

### 公式流程（文字描述）
- 训练过程：教师模型通过因果提示和反事实去偏学习；学生模型通过跨模态对齐、蒸馏损失和反事实去偏学习；融合模块整合所有特征并最终去偏。
- 推理时：教师模型用事实特征直接预测（不减去反事实），学生与融合模块同理。

## 3. 实验设计

### 数据集
- **FakeSV**（唯一公开的短视频假新闻基准数据集），包含视频、音频、评论、标题、用户信息等丰富内容。
- 分割方式：**按事件分割**（event）和**按时间分割**（time）。

### 基准（Benchmark）与对比方法
- **单模态基线**：关键帧、视频片段、音频、用户、评论、标题&转录。
- **多模态基线**：FANVM、CAFE、MultiEMO、SV-FEND、SV-FEND-SNEED、MMCAN。
- **LLM 基线**：ChatGPT-3.5-direct、ChatGPT-4-direct、ChatGPT-3.5-CR（使用因果推理提示）。

### 评估指标
F1-score、宏平均 Recall、宏平均 Precision、Accuracy。

## 4. 资源与算力

文中明确说明：
- **硬件**：单张 **RTX 3090 Ti GPU**。
- **框架**：PyTorch（Python 3.9.18）。
- **超参数**：学习率 教师 0.0004，视频 0.0005，音频 0.01；batch size 64；优化器 Adam。
- **未说明**：训练时长、总参数量、分布式设置等细节。

## 5. 实验数量与充分性

**共进行了多组实验，覆盖全面：**
1. **主对比实验**（表1）：在按时间和按事件划分的数据集上，与 6 个多模态基线、3 个单模态组、3 个 LLM 基线对比，报告 F1/Rec/Pre/Acc，共 2 种划分 × 多种方法。
2. **消融实验**（表2）：对 GPT-2、CMT、反事实推理（CI）、因果提示（CR）、知识蒸馏（KD）五个组件分别移除，分析贡献。
3. **适用性研究**（表3）：将提出的三个组件（CI+CR+KD）分别及组合集成到两个强基线（MultiEMO、SV-FEND）中，验证通用性。
4. **反事实推理策略研究**（图5a）：比较四种“事实±反事实”策略。
5. **损失约束策略研究**（图5b）：比较有无扩散损失、特征相似损失、蒸馏损失类型（KL vs Pearson）。
6. **案例研究**（图6）：展示两个案例直观说明因果提示和反事实推理如何帮助纠正错误。
7. **超参数分析**（图7）：对 \( \mu_1, \mu_2, \alpha \) 在 [0.1, 0.9] 范围内进行单变量敏感性分析。

**充分性评价**：实验设计较完整，覆盖主要对比、组件分析、通用性验证、策略对比和案例解释。但**仅在一个数据集**（FakeSV）上验证，缺少跨数据集或真实场景的泛化实验，可能影响结论的稳健性。

## 6. 论文的主要结论与发现

1. **方法性能**：TGFC-SVFN 在两种划分方式下均超越所有基线，在时间划分数据集上 Acc 达 **91.99%**（相比次优 MMCAN 的 85.98% 提升约 6 个百分点）。
2. **因果推理提示作用**：显著提升教师模型学习效率，对性能贡献最大（消融实验中移除 CR 后 F1 从 91.50% 降至 82.01%）。
3. **反事实推理作用**：有效消除各模态中的局部偏见，提升泛化能力，且减法策略（事实减反事实）最优。
4. **知识蒸馏**：基于 Pearson 相关系数的蒸馏损失优于传统 KL 散度。
5. **模块通用性**：提出的组件可迁移至其他多模态方法，提升其性能（如 SV-FEND+All 提升至 89.05% F1）。

## 7. 优点

1. **创新性地结合因果推理提示与扩散模型反事实推理**：粗粒度反事实（整体替换）提升为细粒度（局部加噪），可更精确地定位偏见元素。
2. **完整的模态异质性解决方案**：从教师增强、学生蒸馏到融合，每个阶段都融入去偏机制，形成闭环。
3. **教师模型设计合理**：利用 LLM 的推理能力生成因果提示，且通过特征相似性损失引导，而非直接硬标签。
4. **蒸馏损失改进**：采用皮尔逊相关系数捕捉线性相关，比 KL 散度更适合多模态任务。
5. **实验分析细致**：包含策略选择、损失对比、案例展示等，为方法效果提供实证。
6. **对短视频场景的针对性强**：充分利用了文本（标题、评论、用户、推理文本）、视频（帧+片段）、音频等多种信息。

## 8. 不足与局限

1. **数据集单一**：仅在 FakeSV 上测试，未在其它短视频平台（如 TikTok、快手）或跨领域数据上验证，泛化性存疑。
2. **计算开销**：每个模块都需运行扩散模型反事实场景（T个时间步），且需要调用 LLM（ChatGPT-3.5）生成因果提示，推理和训练效率可能较低；文中未报告训练与推理耗时。
3. **LLM 依赖风险**：因果提示来自外部 API（ChatGPT-3.5），存在稳定性、一致性及成本问题；未使用开源 LLM 做替代实验。
4. **消融实验不完全透明**：未报告融合模块中单独去偏（MHA后的反事实）的影响，仅整体去除反事实模块。
5. **超参数敏感性区间有限**：仅测试了部分范围（如 μ₁ 在 0.1~0.9），未展示全范围或最优值组合。
6. **反事实构造可能引入新偏差**：扩散模型加噪过程可能破坏原有有效特征，去偏效果依赖于噪声调度和时间步选择。
7. **可解释性未深入分析**：虽使用因果推理提示和案例，但未对反事实推理得出的偏见元素进行系统性可视化或量化。

（完）
