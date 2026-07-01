---
title: "FinGrAct: A Framework for FINe-GRrained Evaluation of ACTionability in Explainable Automatic Fact-Checking"
title_zh: FinGrAct：可解释自动事实核查行动性细粒度评估框架
authors: "Islam Eldifrawi, Shengrui Wang, Amine Trabelsi"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.525.pdf"
tags: ["query:xai-objdet"]
score: 5.0
evidence: 可解释事实核查行动性评估框架，可迁移至检测场景
tldr: 可解释自动事实核查需要评估解释的行动性，即解释能否明确错误、提供正确事实和来源。本文提出FinGrAct框架，通过细粒度标准和网络搜索来评估行动性。该框架填补了评估方法空白，其评估思路可推广至其他可解释检测任务，如假新闻或异常检测的可解释性评估。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.525/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1636, \"height\": 916, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.525/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.525/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 624, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.525/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 829, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.525/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 823, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.525/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 823, \"height\": 1042, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.525/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 884, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.525/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 812, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.525/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.525/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 179, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.525/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.525/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 826, \"height\": 1212, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.525/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 823, \"height\": 780, \"label\": \"Table\"}]"
motivation: 可解释事实核查中解释的行动性（是否准确定位错误并提供事实来源）缺乏评估方法。
method: 提出FinGrAct细粒度评估框架，通过明确定义的标准和网络搜索评估解释的行动性。
result: 框架能够有效区分不同解释的行动性水平，并引入新数据集支持评估。
conclusion: 为可解释事实核查提供首个行动性评估方法，且可迁移至其他可解释检测任务。
---

## Abstract
The field of explainable Automatic Fact-Checking (AFC) aims to enhance the transparency and trustworthiness of automated fact verification systems by providing clear and comprehensible explanations. However, the effectiveness of these explanations depends ontheir actionability—the extent to which an AFC explanation pinpoints the error, supplies the correct fact, and backs it with sources. Despiteactionability being critical for high-quality explanations, no prior research has proposed a method to evaluate it. This paper introducesFinGrAct, a fine-grained evaluation framework that can access the web and is designed to assess actionability in AFC explanations through well-defined criteria. We also introduce a novel dataset to evaluate actionability in AFC explanations. FinGrAct surpasses state-of-the-art (SOTA) evaluators, achieving the highest Pearson and Kendall correlation with human judgments while demonstrating the lowest egocentricbias, making it a more robust evaluation approach for actionability evaluation in AFC.

---

## 论文详细总结（自动生成）

# 论文《FinGrAct: A Framework for FINe-GRrained Evaluation of ACTionability in Explainable Automatic Fact-Checking》中文总结

## 一、核心问题与整体含义（研究动机与背景）

- **研究动机**：可解释自动事实核查（AFC）系统需要生成高质量的解释以增强透明度和信任。解释的质量取决于**行动性（actionability）**——即解释能否准确定位错误、提供正确的事实修正，并引用可靠来源支持。
- **背景与空白**：尽管行动性是解释的关键属性（desideratum），但此前没有任何工作提出自动评估行动性的方法。现有的SOTA评估器（如G-Eval、Prometheus）主要面向摘要任务，无法直接用于AFC解释的行动性评估，且它们缺乏对支持链接的细粒度验证能力。
- **整体含义**：本文旨在填补这一空白，为行动性评估提供自动、可重复、细粒度的框架，从而支撑大规模基准测试和模型训练/选择，加速误信息缓解研究。

## 二、方法论：核心思想、关键技术细节与流程

### 核心思想
采用**分治（divide-and-conquer）**策略，将行动性评估分解为三个子任务：
1. **错误分割与修正（Error Segmentation and Correction）**：基于给定证据，将输入虚假声明分解为原子子声明，识别每个子声明的错误原因和正确修正。
2. **解释评估（Explanation Evaluation）**：检查目标解释是否显式提及前述错误和修正。
3. **来源评估（Source Evaluation）**：核实解释中的链接是否存在、内容是否相关、是否支持修正。来源评估有两种模式：依赖LLM内部知识（无UCR）或使用**URL内容检索器（UCR）** 抓取并总结网页文本。

### 关键技术细节
- **FinGrAct实现**：使用GPT-4-1106-preview作为底层LLM（可替换为开源模型）。
- **错误分割与修正阶段**：输出JSON列表，每一项包含原子子声明（sentence）、错误原因（reason）和正确修正（correction）。例如，声明“Earth is flat and red”会被分割为两个错误。  
- **解释评估阶段**：对每个错误和修正生成“Yes/No”布尔值。  
- **来源评估阶段**（有UCR时）：通过Python `requests`库抓取链接HTML，提取文本，用MiniLM-L6-v2模型摘要后输入LLM，判断链接存在性、相关性和支持性。  
- **评分算法（Algorithm 1）**：
  - 错误检测度：全部错误被检测→2分，部分→1分，无→0分。
  - 错误修正度：全部修正→2分，部分→1分，无→0分。
  - 支持链接度：链接存在（1分）、相关（0.5分）、支持（0.5分），总分最高3。  
  最后将三个维度得分归一化到Likert 0~5量表（通过缩放因子5/3调整）。

### 算法流程（文字说明）
1. 输入：声明、证据、标签、待评估解释（可能含链接）。  
2. 调用LLM进行错误分割与修正，得到错误-修正对列表。  
3. LLM评估解释是否包含每个错误和修正（Yes/No）。  
4. 若有链接，选择无UCR（LLM凭知识判断）或有UCR（抓取网页内容后判断）模式，输出链接是否存在、是否相关、是否支持。  
5. 根据算法1汇总为三个子分数，再归一化为最终0~5分。

## 三、实验设计

### 数据集
- **自建混合数据集**：
  - 来源一：Dai et al. (2022)的反事实解释数据（含错误检测、错误修正、支持链接等6类），以及Kotonya & Toni (2020b)的公共卫生声明解释数据（含4类，True/Partly False/False）。  
  - 最终采样203个样本，每个样本包含四种解释：一个来自原数据集，另三个分别由LLaMA-7B、Mistral-7B、GPT-4生成（用于自我中心偏差分析）。  
  - 三位标注员根据详细指导（含评分示例和迭代反馈）独立评分，取均值归一化至0~5；Krippendorff's alpha达到0.863，一致性很高。

### 对比方法（Baselines）
- **G-Eval**（GPT-4版）：直接给定义进行评估。  
- **Prometheus**（Mistral-7B）：需要评分rubric。  
- 两种方法均适配至AFC场景（修改输入为声明+证据+标签+解释）。  
- 同时测试了**无UCR**和**有UCR**两种条件。

### 实验组
1. **与SOTA方法比较**：整体Pearson和Kendall相关系数（表1）。
2. **UCR组件消融**：对比有无UCR时各方法的相关系数变化（表1）。
3. **自我中心偏差分析**：统计评估器对自己模型生成解释的过高评分比例（表2）。
4. **开源模型上的FinGrAct**：将FinGrAct的prompt应用于LLaMA-3.1-8B和Mistral-7B，对比使用G-Eval、Prometheus prompt时的相关系数（表3）。
5. **不同标注指令影响**（附录C）：对50个子样本，分别使用“仅定义”和“定义+评分rubric”两种标注方式，再次比较各方法相关性（表4）。

### 实验充分性评价
- 覆盖了**总样本203**上的主要对比，**两个相关性指标**，**两种来源评估模式**，**三种评估prompt**，**两种开源LLM**。  
- 进行了自我中心偏差的定量分析（三独立运行取均值）。  
- 附录还包含了人工分析的失败案例，说明评估差异原因。  
- 实验设计较为全面，但缺少在**更多数据集**（如事实核查领域其他基准）上的交叉验证，可能影响泛化性。

## 四、资源与算力

- **未明确说明**：论文未提及使用的GPU型号、数量、训练时长等算力信息，也未说明FinGrAct评估过程的计算开销。只提到使用GPT-4-1106-preview作为主要LLM，以及MiniLM-L6-v2进行摘要（推理型，无需训练）。  
- 由于未进行微调，评估过程属于零样本推理，算力需求相对较低，但依赖商业API。

## 五、实验数量与充分性分析

- **数量**：主要实验有4组，加上附录中1组（不同标注风格），共计5组对比。每组报告了Pearson和Kendall相关系数。  
- **充分性**：  
  - 优点：覆盖了不同SOTA方法、不同模型规模（GPT-4 vs. LLaMA-3.1/Mistral-7B）、不同UCR模式、不同标注指导，且进行了自我中心偏差量化。  
  - 不足：未在**更多AFC数据集**（如FEVER、LIAR-PLUS等）上验证泛化性；实验仅基于一个自建203样本数据集，规模较小；未与其他事实核查专用评估指标（如真实性、忠实度）进行相关性对比。  
  - 公平性：对SOTA方法做了适配（修改输入），但G-Eval和Prometheus的原始设计未考虑行动性，适配后可能不如其原生任务表现良好。

## 六、主要结论与发现

1. **FinGrAct优于所有对比SOTA**：在无UCR条件下，Pearson相关系数0.46（Prometheus 0.328，G-Eval 0.147）；Kendall tau 0.409（Prometheus 0.294）。  
2. **UCR组件提升所有方法**：引入网页内容检索后，FinGrAct的Pearson升至0.520，Prometheus升至0.405，G-Eval升至0.213。  
3. **自我中心偏差最低**：FinGrAct仅有17/203样本（8.4%）高估自身生成，远低于G-Eval（48.7%）和Prometheus（26%）。  
4. **细粒度分解是核心**：将评估分解为错误检测、修正、链接三个子任务，并采用三级分类（0/1/2），使LLM更易对齐人类判断。  
5. **开源模型上同样有效**：FinGrAct prompt在LLaMA-3.1-8B和Mistral-7B上均取得最高相关系数（分别为0.431/0.382、0.293/0.270），证明框架本身而非模型大小是关键。

## 七、优点

1. **首个行动性自动评估器**：填补了可解释AFC领域的重要评估空白。  
2. **细粒度、可解释**：分解为三个子任务，每部分有明确评分标准，易于诊断解释弱点。  
3. **结合外部知识（UCR）**：超越纯内化知识，提升对链接评估的准确性。  
4. **低自我中心偏差**：结构化流程减少LLM对自身生成的偏好。  
5. **方法通用性**：可迁移至其他需要行动性评估的可解释检测任务（如假新闻检测、异常检测）。  
6. **构建了带人类标注的基准数据集**：包含多种行动性梯度，并公开供未来使用。

## 八、不足与局限

1. **UCR仅支持文本**：无法处理图像或JavaScript渲染内容，导致部分包含非文本链接的样本评估错误（占73%的失配案例）。  
2. **零样本限制**：未进行微调，可能限制其在特定领域的表现；微调成本（尤其GPT-4）高昂，文中也承认未探索。  
3. **数据集规模较小（203样本）**：可能不足以充分反映真实世界多样性，泛化性有待验证。  
4. **未考虑其他偏差类型**：仅研究了自我中心偏差，未分析跨模型偏差或其他系统性偏见。  
5. **实验范围**：仅在单一自建数据集上进行，缺乏其他事实核查基准（如FEVER、SciFact）的交叉验证。  
6. **算力信息缺失**：未报告计算资源，不利于复现和成本评估。

（完）
