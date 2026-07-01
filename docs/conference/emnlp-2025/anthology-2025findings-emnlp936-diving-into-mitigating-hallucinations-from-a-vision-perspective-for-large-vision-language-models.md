---
title: Diving into Mitigating Hallucinations from a Vision Perspective for Large Vision-Language Models
title_zh: 从视觉角度深入缓解大视觉语言模型的幻觉
authors: "Weihang Wang, Xinhao Li, Ziyue Wang, Yan Pang, Jielei Zhang, Peiyi Li, Qiang Zhang, Longwen Gao"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.936.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: LVLM细粒度物体幻觉基准
tldr: 该论文针对大视觉语言模型（LVLM）中物体幻觉问题，从视觉编码器角度进行系统分析，并提出VHBench-10基准。基准涵盖十种细粒度幻觉类别，揭示不同训练范式下编码器的归纳偏差对幻觉的影响。该工作为可解释目标检测中的幻觉分析提供了细粒度评估工具，有助于理解模型决策中的错误根源。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.936/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 767, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.936/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 733, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.936/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 736, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.936/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1304, \"height\": 688, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.936/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 516, \"height\": 677, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.936/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 517, \"height\": 679, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1650, \"height\": 557, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 799, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 796, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1648, \"height\": 767, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 798, \"height\": 155, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1651, \"height\": 420, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1647, \"height\": 753, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 793, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1636, \"height\": 1350, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.936/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1641, \"height\": 1730, \"label\": \"Table\"}]"
motivation: 现有基准只关注粗粒度幻觉，无法捕捉编码器不同训练范式导致的细粒度差异。
method: 构建VHBench-10基准，包含十类细粒度幻觉，并系统分析不同视觉编码器的影响。
result: 实验表明不同编码器在特定幻觉类别上有显著差异，验证了假设。
conclusion: 该基准为LVLM物体幻觉的可解释性分析提供了重要资源。
---

## Abstract
Object hallucinations in Large Vision-Language Models (LVLMs) significantly impede their real-world applicability. As the primary component for accurately interpreting visual information, the choice of visual encoder is pivotal. We hypothesize that the diverse training paradigms employed by different visual encoders instill them with distinct inductive biases, which leads to their diverse hallucination performances. Existing benchmarks typically focus on coarse-grained hallucination detection and fail to capture the diverse hallucinations elaborated in our hypothesis. To systematically analyze these effects, we introduce VHBench-10, a comprehensive benchmark for evaluating LVLMs across ten fine-grained hallucination categories. Our evaluations confirm encoders exhibit unique hallucination characteristics. Building on these insights and the suboptimality of simple feature fusion, we propose VisionWeaver, a novel Context-Aware Routing Network. It employs global visual features to generate routing signals, dynamically aggregating visual features from multiple specialized experts. Comprehensive experiments confirm the effectiveness of VisionWeaver in significantly reducing hallucinations and improving overall model performance. Our code and benchmark are available at https://github.com/whwangovo/VisionWeaver.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大视觉语言模型（LVLM）在描述图像时频繁产生物体幻觉（Object Hallucination），即描述图像中不存在或属性错误的物体，严重阻碍了其在真实世界中的可靠性。
- **研究背景**：现有幻觉评估基准（如POPE）仅关注粗粒度的“物体是否存在”检测，忽略了幻觉的细粒度差异。不同视觉编码器因预训练范式不同而具有独特的归纳偏差，导致各自擅长的视觉子任务（如检测、分割、定位、分类）各不相同，从而产生不同类型的幻觉。
- **研究动机**：探索视觉编码器选择如何影响幻觉模式，并设计一种能够整合多种编码器优势的方法，以系统性降低幻觉。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：通过构建细粒度幻觉基准（VHBench-10）揭示不同视觉编码器的特性，并设计上下文感知路由网络（VisionWeaver）动态聚合多专家特征，取代简单的特征融合。
- **关键技术细节**：
  - **VHBench-10基准**：基于2000张图像（来自LLaVA-ReCap-118K），每张图像通过GPT-4o-mini生成10种细粒度幻觉描述（包括检测、分割、定位、分类四大类，共10个子类：类别幻觉、计数幻觉、遮挡幻觉、文本幻觉、形状幻觉、绝对位置幻觉、相对位置幻觉、颜色幻觉、动作幻觉、相对交互幻觉）。每个样本为三元组 (I, R, H)。
  - **VisionWeaver网络**：
    - **上下文感知专家选择**：使用CLIP编码器的[CLS] token作为全局视觉信号，通过一个可学习的函数f生成各专家的软权重，再通过softmax得到路由权重，选择top-k专家。
    - **专家表示融合**：将选中的专家特征（经过线性适配器对齐到1024维）与CLIP的Patch token通过残差连接相加，得到最终视觉表示\(\hat{I} = I_P + Y\)，其中Y为加权专家特征之和。
    - 整体架构：以LLaVA-1.5为基础，保留CLIP作为基础编码器，增加DINOv2、Vary、SAM、ConvNext、EVA-02五个专家编码器，所有专家输入分辨率统一为336×336，输出token数固定为576，维度统一为1024。

- **算法流程**（文字说明）：
  1. 输入图像，分别通过所有视觉专家编码器获得特征\(Z_i\)。
  2. 提取CLIP的[CLS] token \(I_C\)，通过路由网络f生成权重向量A。
  3. 对A施加softmax得到权重W，选择top-k专家。
  4. 对选中的专家特征按权重求和得到Y。
  5. Y与CLIP的Patch token \(I_P\)相加得到最终视觉特征\(\hat{I}\)。
  6. 视觉特征经投影器映射到LLM的嵌入空间，输入LLM生成文本。

## 3. 实验设计：数据集、基准、对比方法

- **数据集/基准**：
  - 主要幻觉评估：POPE（随机/流行/对抗设置）、AutoHallusion（合成/现实场景）、VHBench-10（自行构建）。
  - 通用视觉语言基准：MME、MMStar、MMBench、OCRBench、MathVista。
- **对比方法**：
  - 基础基线：LLaVA-1.5（Vicuna-7B），以及替换为Llama3.2-3B或Qwen2.5-3B的版本。
  - 多编码器基线：简单特征加法/拼接融合五种专家。
  - 其他SOTA方法：SEOSS、OHD-Caps、DAMRO、DeCo。
- **消融实验**：单独使用每个专家编码器、不同数量的专家组合、不同融合策略（加法、拼接、VisionWeaver）。

## 4. 资源与算力

- 文中明确说明：实验在**8块Nvidia A100 GPU**上完成。
- 预训练阶段：批次大小256，学习率2×10⁻⁴，训练**1个epoch**，耗时约**8小时**。
- 监督微调阶段：批次大小128，学习率2×10⁻⁵，训练**1个epoch**，耗时约**16小时**。
- 此外，模型大小方面，5个视觉专家编码器合计约10亿参数，LLM为3B参数。

## 5. 实验数量与充分性

- **实验组数**：至少包括以下多组实验：
  - 在POPE和AutoHallusion上的主实验结果（表1），包含3种LLM、3种配置（单CLIP、多编码器无路由、多编码器+VisionWeaver）。
  - 在5个通用基准上的结果（表2），同样对比3种配置。
  - 专家选择消融（表3）：对比6种单个专家、不同专家组合（4个、5个、6个）的加法融合、拼接融合、VisionWeaver。
  - 与SOTA方法在POPE上的对比（表4）。
  - 计算效率对比（表5）：测量预填充和生成时间。
  - VHBench-10上的10种细粒度幻觉误差率（表6）。
  - 参数效率实验（附录E）：冻结视觉部分、全参数微调、LoRA微调。
- **充分性评估**：
  - 实验设计较为全面，覆盖了主流幻觉基准、通用基准、细粒度基准，消融研究系统。
  - 对比了多种SOTA方法，并考虑了不同模型规模和不同融合策略。
  - 公平性：所有实验遵循相同训练流程，控制变量（如输入分辨率、token数量等）。
  - 不足：仅基于LLaVA-1.5架构进行改造，未在其他主流LVLM（如Qwen-VL、InternVL）上验证泛化性（论文在局限中提及算力限制）。

## 6. 论文的主要结论与发现

- **不同视觉编码器具有显著不同的幻觉倾向**：例如Vary在文本任务上表现好，DINOv2在颜色/动作等细粒度属性上更优，CLIP在全局物体存在识别上占优。
- **简单特征融合（加法/拼接）效果不如单个最优专家，甚至可能劣化**，说明需要更智能的聚合方式。
- **VisionWeaver在所有评估基准上持续降低幻觉率**，并在POPE和AutoHallusion上获得最高平均性能（68.5%），同时提升了通用基准（如MMBench、OCRBench）上的准确率。
- **上下文感知路由机制有效选择最相关的专家**，且计算开销可忽略（预填充时间仅增加约48ms，推理时间甚至略有减少）。

## 7. 优点

- **细粒度诊断能力**：VHBench-10将幻觉解耦为10个子类，直接对应经典视觉任务能力（检测、分割、定位、分类），有助于定位模型具体视觉缺陷，比POPE等粗粒度基准更具可解释性。
- **新颖的路由融合策略**：利用CLIP [CLS] token这一全局语义特征作为路由信号，避免了简单融合的次优性，设计简洁且高效。
- **轻量化设计**：仅增加约1B参数的视觉专家（相对于3B+的LLM），推理时通过KV缓存仅多一次前向，额外延迟极低，适合端侧部署。
- **实验全面且严谨**：覆盖幻觉和通用基准，消融研究充分，对比多种SOTA方法，并验证了参数效率（LoRA也能保持优势）。

## 8. 不足与局限

- **模型范围有限**：仅基于LLaVA-1.5架构和3B/7B规模模型，未在更大模型（如13B、70B）或其他主流LVLM（如Qwen-VL、InternVL）上验证，泛化性有待确认。
- **基准构建依赖GPT-4o-mini**：生成的幻觉描述可能引入轻微误差，且某些图像无法产生所有10类幻觉（如无文本的图像无法生成文本幻觉），导致类别样本数不均。
- **未能覆盖所有幻觉类型**：约20%的真实样本难以分类到现有10个子类，涉及更复杂的场景。
- **计算资源限制**：仅使用8块A100，训练仅1个epoch，可能未达到充分收敛。
- **路由机制的深入分析不足**：论文未详细分析路由权重如何随输入变化，也未探索最优专家数量与组合的通用规律。

（完）
