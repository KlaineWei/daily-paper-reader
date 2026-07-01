---
title: Do What? Teaching Vision-Language-Action Models to Reject the Impossible
title_zh: 怎么执行？教会视觉-语言-动作模型拒绝不可能指令
authors: "Wen-Han Hsieh, Elvis Hsieh, Dantong Niu, Trevor Darrell, Roei Herzig, David M. Chan"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.635.pdf"
tags: ["query:slm-rl"]
score: 9.0
evidence: VLA模型处理假前提指令与拒绝
tldr: 现有VLA模型无法正确处理不可能指令。IVA框架通过指令验证-行动流程，使模型能检测假前提、发起语言澄清并执行可行动作，提升了VLA在长程任务中的鲁棒性。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.635/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 700, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.635/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1650, \"height\": 235, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.635/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1657, \"height\": 591, \"label\": \"Table\"}]"
motivation: VLA模型无法识别用户指令中的虚假前提，导致执行失败。
method: 提出IVA框架，包含检测、澄清和可行动作规划三个步骤。
result: 在模拟和真实机器人任务中有效处理假前提指令。
conclusion: 前提验证能力对VLA模型的安全部署至关重要。
---

## Abstract
Recently, Vision-Language-Action (VLA) models have demonstrated strong performance on a range of robotic tasks. These models rely on multimodal inputs, with language instructions playing a crucial role-not only in predicting actions, but also in robustly interpreting user intent, even when the requests are impossible to fulfill. In this work, we investigate how VLAs can recognize, interpret, and respond to false-premise instructions-natural language commands that reference objects or conditions absent from the environment. We propose — Instruct-Verify-and-Act (IVA) — a unified framework that (i) detects when an instruction cannot be executed due to a false premise, (ii) engages in language-based clarification or correction, and (iii) grounds plausible alternatives in perception and action. Towards this end, we construct a large-scale instruction tuning setup with structured language prompts and train a VLA model capable of handling both accurate and erroneous requests. Our approach leverages a contextually augmented, semi-synthetic dataset containing paired positive and false-premise instructions, enabling robust detection and natural language correction. Our experiments show that IVA can improves false premise detection accuracy by 58.89% over baselines, while increasing successful responses in false-premise scenarios by 27.89%.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有视觉-语言-动作（VLA）模型在执行机器人任务时，只能处理可执行的指令，而无法识别和响应用户指令中的“假前提”（false premise）——即指令中引用了环境中不存在的物体、属性或状态。例如，当用户命令机器人“拿来桌上的红色杯子”但桌面上根本没有红色杯子时，机器人缺乏检测不可能性、进行澄清或建议替代方案的能力，这导致人机交互不安全、效率低。
- **研究动机**：随着VLA模型在开放世界部署，必须处理模糊和不可执行的指令。过往NLP领域已有假前提检测研究（如SQuAD 2.0、False QA），但在具身机器人/视觉-语言-动作领域尚未被探索。本文首次将假前提处理引入VLA模型。
- **整体含义**：赋予机器人不仅执行指令，还能推理用户意图、识别不可行命令并自然语言纠正的能力，是实现安全、高效人机交互的关键一步。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出 **Instruct-Verify-and-Act (IVA)** 框架，将VLA模型的能力扩展为三个阶段：
  1. **检测（Detect）**：识别指令是否因假前提而无法执行。
  2. **澄清/纠正（Clarify/Correct）**：用自然语言向用户解释问题（如“我没看到瓶子，你是不是指抽屉？”），或建议可行的替代目标。
  3. **行动（Act）**：在澄清后（若用户确认），基于正确目标执行动作；若为域外假前提，则直接拒绝并终止交互。
- **关键技术细节**：
  - **基础架构**：基于LLARVA模型（Niu et al., 2024），它使用CLIP ViT-L/14视觉编码器（冻结）、语言编码器（冻结）和自回归Transformer解码器（可训练），输入为视觉观察图像和结构化语言指令（包含机器人类型、控制模式、任务描述、前h步关节状态、未来动作步数），输出为动作序列和2D视觉轨迹。
  - **假前提指令数据集构建**：基于RLBench模拟环境，通过两种方式构造假前提指令：
    - **域内假前提（In-Domain）**：用场景中存在的其他物体替代原目标（如将“关罐子”改为“关蓝色保险箱”），模型应建议正确目标。
    - **域外假前提（Out-of-Domain）**：使用场景中从未出现的物体（如“打开大象”），模型应直接拒绝。
  - **训练数据比例**：每任务800个episode，其中约20%含域外假前提、65%含域内假前提（注入到10%的步骤中）。
  - **训练方式**：端到端指令微调，冻结视觉和语言编码器，使用标准LoRA适配器微调解码器。损失函数为预测token与ground-truth之间的交叉熵。不同于LLARVA的两阶段训练，IVA统一训练。
- **公式/算法流程**：模型输出概率 \( p(\hat{A}_{t:t+n-1}, \hat{P}_{t:N} \mid o_t, l_t) = \prod_{i=1}^{|R|} p_\theta(x_i \mid o_t, l_t) \)，其中 \(x_i\) 为第i个预测token，θ为可训练参数，R为完整响应序列。

## 3. 实验设计：数据集、benchmark、对比方法

- **数据集**：使用Open X-Embodiment (OXE) 进行预训练（继承LLARVA），并在RLBench（James et al., 2019）上构建假前提数据集进行微调和评估。RLBench包含9个任务：meat off grill, open drawer, push buttons, put money in safe, reach and drag, slide block, sweep to dustpan, turn tap, close jar。
- **Benchmark**：每个任务生成25个episode（object位置随机），每个episode配一对指令（真前提和假前提各一种）。总评估集225个episode。
- **对比方法**：以LLARVA（原始版本，仅训练真前提指令）作为基线。IVA与LLARVA在相同任务上比较整体成功率、假前提检测率（域内/域外）、真前提任务成功率。

## 4. 资源与算力

- 论文明确说明：模型在**8个A100 GPU**上微调，训练时长**8小时**。预训练阶段使用了OXE数据集，但未详细说明预训练资源。微调时使用LoRA适配器，参数量和具体配置未详细给出。

## 5. 实验数量与充分性

- **实验数量**：共9个任务 × 25个episode = 225个场景。每个场景测试一种指令（真或假前提），进行一次前向评估（one-pass, end-to-end）。没有重复运行多个随机种子来报告统计方差（仅提到“one fixed seed per task”）。
- **充分性评估**：
  - 实验覆盖了多种任务类型（推、拉、旋转、滑动等），但仅限模拟环境（RLBench），未在真实机器人上验证。
  - 假前提检测率报告了域内和域外两类，但未做消融实验（如不同假前提比例、不同LoRA秩、不同解码策略等）。
  - 对比方法仅LLARVA一个，缺少其他VLA模型（如RT-2、OpenVLA、π0等）作为基线，且未比较不同假前提处理策略。
  - 真前提任务成功率上，IVA为42.67%±8.34%，基线LLARVA为38.67%±8.55%，论文认为差异不显著，但未给出统计检验。
- **公平性**：虽然评估流程清楚（解析文本分类为Accept/Clarify/Refuse，再执行动作判断成功），但假前提检测的评分方法依赖人工解析规则，可能存在主观性。且评估为单次执行，未考虑任务随机性。

## 6. 论文的主要结论与发现

- IVA在假前提检测上取得显著提升：域内假前提检测率100%，域外假前提检测率97.78%（表1中平均为97.56%），而基线LLARVA在两种类别上均为0%。
- IVA在假前提场景中的成功响应率（即正确拒绝或建议）相比基线提高50.78%（表1中Overall Success列：IVA平均约70.2% vs. 基线约19.4%）。
- 真前提任务的成功率上，IVA（42.67%）与基线（38.67%）差异不显著，说明添加假前提处理能力**不会显著降低标准执行能力**。
- 模型能生成上下文恰当的语言澄清（如“I don’t see a tree. Do you mean jar?”）或直接拒绝。

## 7. 优点：方法或实验设计上的亮点

- **首创性**：首次将假前提处理引入VLA领域，填补了机器人VLA模型对不可行指令推理的空白。
- **统一框架**：IVA将检测-澄清-行动整合为一个端到端VLA模型，无需外部对话系统或规划器。
- **数据构造策略**：巧妙利用RLBench构造两类假前提（域内/域外），覆盖从“合理替代”到“完全不可能”的连续谱，使模型学习不同粒度的拒绝行为。
- **性能验证充分**：在9个不同任务上验证，并提供假前提检测率和整体成功率两个指标，且说明真前提性能未下降。
- **代码开源**：承诺发布代码和数据（MIT许可），有利于复现和后续研究。

## 8. 不足与局限

- **数据集局限性**：假前提数据完全来自模拟环境RLBench，物体和场景有限，可能无法反映真实世界复杂性（如光照、遮挡、噪声、语言多样性）。人工平衡的假前提比例（65%域内、20%域外）不代表真实分布。
- **未在真实机器人上验证**：所有实验在仿真中完成，领域迁移（sensor noise、domain gap）未评估。
- **语言澄清能力有限**：模型只能基于训练数据中出现的模式给出建议，对于未见过的域外假前提，只能简单拒绝，缺乏创造性或多轮对话能力。
- **评估指标单一**：仅报告检测率和任务成功率，未评估语言生成质量（如流畅性、合理性、用户满意度）。
- **指令复杂度有限**：评估指令较短且结构化，实际人机交互可能包含更长、更模糊、多轮对话的指令。
- **计算开销**：使用8个A100训练8小时，对于资源受限的机器人平台可能过高；推理时需加载大模型，实时性未讨论。
- **统计严谨性不足**：仅使用一个随机种子，未报告多个种子的平均值和方差，使得性能比较的统计显著性存疑。
- **对比方法不足**：仅与LLARVA对比，缺少与其他假前提处理策略（如专门检测模块+VLA、基于LLM的规划器）的比较。
- **无消融实验**：未分析各组件（如LoRA、不同假前提类型比例、冻结编码器等）的贡献。

（完）
