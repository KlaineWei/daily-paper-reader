---
title: "DivScene: Towards Open-Vocabulary Object Navigation with Large Vision Language Models in Diverse Scenes"
title_zh: DivScene：面向开放词汇目标导航：在多样化场景中利用大型视觉语言模型
authors: "Zhaowei Wang, Hongming Zhang, Tianqing Fang, Ye Tian, Yue Yang, Kaixin Ma, Xiaoman Pan, Yangqiu Song, Dong Yu (于东)"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.513.pdf"
tags: ["query:slm-rl"]
score: 4.0
evidence: 利用大型视觉语言模型进行开放词汇目标导航
tldr: 针对大型视觉语言模型在具身环境中导航能力不足的问题，构建了包含大量房屋和场景类型的大规模数据集DivScene，用于开放词汇目标导航。评估了多种基于LVLM的方法，发现现有模型仍存在不足。该工作为VLA场景提供了导航基准，但与长程规划强化学习主题仅有间接关联。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 772, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1492, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 642, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 800, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 500, \"height\": 637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 508, \"height\": 667, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 500, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 503, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 505, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 401, \"height\": 734, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 501, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.513/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 505, \"height\": 508, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 783, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1506, \"height\": 983, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1329, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 822, \"height\": 410, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1517, \"height\": 328, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1656, \"height\": 653, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1638, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1624, \"height\": 811, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 868, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1621, \"height\": 780, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1155, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1157, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1158, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1162, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1201, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1201, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.513/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 733, \"height\": 521, \"label\": \"Table\"}]"
motivation: 现有数据集多样性不足以充分评估LVLM在物体导航中的能力。
method: 构建包含81种场景类型和5707种目标物体的DivScene数据集，并评估多种LVLM导航方法。
result: 发现当前LVLM在开放词汇目标导航上性能有限，需要进一步改进。
conclusion: DivScene为VLA导航研究提供了重要的基准和挑战。
---

## Abstract
Large Vision-Language Models (LVLMs) have achieved significant progress in tasks like visual question answering and document understanding. However, their potential to comprehend embodied environments and navigate within them remains underexplored. In this work, we first study the challenge of open-vocabulary object navigation by introducing DivScene, a large-scale dataset with 4,614 houses across 81 scene types and 5,707 kinds of target objects. Our dataset provides a much greater diversity of target objects and scene types than existing datasets, enabling a comprehensive task evaluation. We evaluated various methods with LVLMs and LLMs on our dataset and found that current models still fall short of open-vocab object navigation ability. Then, we fine-tuned LVLMs to predict the next action with CoT explanations. We observe that LVLM’s navigation ability can be improved substantially with only BFS-generated shortest paths without any human supervision, surpassing GPT-4o by over 20% in success rates.

---

## 论文详细总结（自动生成）

## 详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：大型视觉语言模型（LVLMs）在视觉问答等任务上表现出色，但其在具身环境中的**物体导航能力**尚未得到充分探索。现有导航数据集（如 Matterport-3D、ProcTHOR）场景和物体种类极其有限（Matterport-3D 仅 21 种目标物体、90 个房屋；ProcTHOR 仅 16 种物体、4 类房间），无法有效评估和理解 LVLMs 在**开放词汇（open-vocabulary）** 场景下的导航能力。
- **研究意义**：本文首次系统研究开放词汇物体导航任务，旨在推动 LVLMs 向更真实的开放世界场景迁移，弥合具身智能与环境理解的鸿沟。

### 2. 方法论：核心思想、关键技术细节

- **核心思想**：构建大规模、多样化场景数据集 DivScene，并基于**模仿学习（Imitation Learning）** 微调 LVLM，使其学会从最短路径轨迹中理解导航决策逻辑，而非仅依赖人工演示或复杂奖励设计。
- **关键技术细节**：
  - **数据集构建（DivScene）**：基于 MIT Scenes 数据集补充得到 81 种场景类型（商店、家庭、公共空间、休闲、工作场所等5大类），利用 GPT-4 自动生成房屋属性描述（如“带格子花纹墙壁的面包店”），然后调用 Holodeck 框架在 AI2THOR 平台上自动化构建 4,614 个房屋。
  - **轨迹采样（DivScene_ep）**：将房屋离散化为 0.25m × 0.25m 的网格地图，随机采样初始位置和目标物体（共 22,696 种物体类型），使用 BFS（广度优先搜索）寻找最短路径，并转换为动作序列（MoveAhead/RotateRight/RotateLeft/Done），最终得到约 23K 条训练用轨迹。
  - **NatVLM 模型**：以 Idefics 2（8B）为骨干，设计**指令模板**（包含任务描述、当前观测、最近 M=8 步历史动作与 K=4 步历史图像），并人工编写**链式思维（CoT）解释轨迹**（比较位置差→检查障碍→决策动作），通过行为克隆（Behavior Cloning）最小化负对数似然损失进行微调。
  - **数据后处理**：对 MoveAhead 动作下采样（保留 25%）以平衡类别，并剔除同一场景中不同轨迹导致的冲突样本。

### 3. 实验设计：数据集、基准与方法对比

- **数据集与场景**：
  - **训练集**：DivScene 的 4,506 个房屋（每个房屋采样 5 条轨迹）。
  - **验证集**：27 个房屋（每个房屋 4 条轨迹，共 108 条）。
  - **测试集**：81 个房屋（每种场景类型随机选一个，每个房屋 4 条轨迹，共 324 条）。
  - **零样本迁移测试**：iTHOR（120 个房间）、ProcTHOR（120 个房间）、HM3D（完整集）。
- **基准方法**：
  - **随机基线**（Random）。
  - **盲大语言模型**（Blind LLMs）：Llama 2 (7B/13B)、Llama 3.1 (8B)、Mistral (7B) —— 仅基于文本指令预测动作。
  - **大语言模型 + 图像描述**（LLMs w/ Captions）：使用 Llava 1.5 生成图像描述，再用上述 LLM 预测。
  - **开源 LVLMs**：Qwen-VL (7B)、Llava 1.5 (7B/13B)、Idefics 2 (8B)、Qwen2.5-VL (7B)、InternVL3 (8B)、Gemma3 (12B) —— 直接测试，无微调。
  - **闭源 API LVLMs**：GPT-4v、GPT-4o。
  - **细调 LVLM**：Idefics 2 微调（无 CoT 解释）。
  - **NatVLM（本文）**：Idefics 2 + 最短路径 + CoT 解释。
- **评价指标**：Success Rate (SR)、Success weighted by Path Length (SPL)、Success weighted by Episode Length (SEL)。成功条件：目标物体在自中心视图中且距离 <1.5m。

### 4. 资源与算力

- **训练**：使用 **8 块 NVIDIA A100 GPU** 对 Idefics 2（8B）全部参数（LLM、视觉编码器、投影器）进行 BF16 精度微调，训练 1 个 epoch，学习率 2e-5，batch size 64。无 CoT 时约 **10 小时**，加入 CoT 解释后约 **17 小时**。
- **推理**：单个 A100 GPU 上，无 CoT 每步平均生成时间 0.28 秒，有 CoT 每步 1.03 秒。
- **数据集构建**：基于 Holodeck 和 GPT-4 API，未报告具体 API 调用开销。

### 5. 实验数量与充分性

- **主要评估**：表 2 报告了全部方法在验证集、测试集和平均上的 SR、SPL、SEL，共 14 种方法对比。
- **消融实验**：表 3 包括去除 CoT 解释、加入位置真值标签、差分方程提示等共 5 组消融。
- **设计调查**：
  - 图像数量（2/4/6/8 张）实验（图 4、表 14）。
  - 历史动作步数（4/8/12/16 步）实验（表 4、表 15-16）。
  - 两种提示模板（默认 vs 差分方程）下的对比。
- **少样本学习**：使用 20%/40%/60%/80% 数据训练，并与 GPT-4o 对比（表 5、表 17-18）。
- **零样本迁移**：在 iTHOR、ProcTHOR、HM3D 三个独立数据集上测试（表 6、表 19），并与多种零样本/细调方法对比（如 ZSON、ESC、VLFM、SG-Nav、InstructNav 等）。
- **案例分析**：图 5 展示一个失败路径案例。
- **充分性评价**：实验覆盖全面，包含多种基线、多种训练数据比例、多种输入配置、跨数据集迁移，消融设计合理，结果对比清晰。但未进行长程导航的针对性实验，且仅在 AI2THOR 平台上评估，未在真实机器人或 Habitat 等不同模拟器上验证。

### 6. 主要结论与发现

- **现有 LVLMs 在开放词汇导航上表现不佳**：大多数方法（包括闭源 GPT-4o）的 SR 仅 30% 左右，远低于实际应用需求，且略高于随机基线（约 8%）。
- **仅用 BFS 生成的最短路径即可显著提升导航能力**：NatVLM（默认 CoT）在验证集上 SR 达 57.41%，测试集 54.94%，**超过 GPT-4o 约 20 个百分点**（表 2）。
- **CoT 解释轨迹至关重要**：去除 CoT 后 SR 下降约 28 个百分点（表 3），而仅提供位置真值标签帮助有限。
- **少样本能力强**：仅使用 20% 训练数据即可达到与 GPT-4o 相当的性能（表 5）。
- **零样本迁移良好**：在 iTHOR（SR 72.79%）和 ProcTHOR（53.12%）上大幅领先所有基线，在 HM3D 上也优于多数零样本方法（SPL 34.1%）。
- **设计选择影响显著**：提供 4 张最近图像、8 步历史动作是最优配置；更多图像/步骤不一定带来提升。

### 7. 优点

- **数据集质量高、多样性极强**：81 种场景、22,696 种物体类型、5,707 种目标物体，远超此前所有工作，更逼近真实开放世界。
- **方法简洁高效**：无需昂贵的人类演示或复杂强化学习，仅利用自动生成的最短路径和人工设计的 CoT 模板，即可大幅提升 LVLM 导航能力。
- **CoT 解释设计合理**：人工编写的三步推理（位置差→障碍检查→动作决策）使模型学到导航内在逻辑，而非简单模仿表面模式。
- **实验设计全面公正**：与多种包括闭源模型在内的强基线对比，进行了充分的消融、少样本、迁移和多配置探索。
- **代码与数据开源**：有利于社区复现和进一步研究。

### 8. 不足与局限

- **长程导航失败**：如图 5 所示，对于需要较长轨迹（>40 步）的任务，模型容易在局部区域徘徊，探索能力不足，缺乏全局规划。
- **上下文窗口限制**：仅能提供最近 8 步历史，无法有效记忆早期信息，导致长程导航中容易丢失方向。
- **仅评估 RGB 图像**：未利用深度、语义分割等额外模态，与一些复杂导航框架（如 SG-Nav、InstructNav）相比信息维度单一，公平性上仍有待改进（作者已指出这些方法使用更多资源）。
- **平台单一**：仅在 AI2THOR 上训练和评估，未在 Habitat、真实机器人等平台验证，泛化到真实世界的效果未知。
- **CoT 模板依赖人工设计**：虽然效果好，但针对不同场景（如障碍物模式）的模板可能不通用，且有一定手工成本。
- **数据后处理可能引入偏差**：对 MoveAhead 下采样和冲突过滤可能会改变轨迹分布，影响学习到的策略。

（完）
