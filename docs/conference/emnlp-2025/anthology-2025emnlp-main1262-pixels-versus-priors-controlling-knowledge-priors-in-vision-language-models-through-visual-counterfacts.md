---
title: "Pixels Versus Priors: Controlling Knowledge Priors in Vision-Language Models through Visual Counterfacts"
title_zh: 像素与先验：通过视觉反事实控制视觉语言模型中的知识先验
authors: "Michal Golovanevsky, William Rudman, Michael A. Lepori, Amir Bar, Ritambhara Singh, Carsten Eickhoff"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.1262.pdf"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 利用视觉反事实分析知识先验与视觉证据的竞争
tldr: 为了探究多模态大模型推理依赖记忆知识还是视觉输入，构建了视觉反事实数据集。通过将知识先验与视觉证据置于冲突，发现模型预测起初偏向先验，随后在中后层转向视觉证据。该工作为理解VLM推理提供了可解释性视角，但未直接涉及目标检测或异常检测。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 778, \"height\": 948, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1667, \"height\": 674, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 795, \"height\": 520, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1405, \"height\": 898, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1633, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 684, \"height\": 1073, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 804, \"height\": 292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1602, \"height\": 825, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1609, \"height\": 826, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.1262/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1666, \"height\": 622, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1262/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1445, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1262/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1658, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1262/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 639, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1262/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 729, \"height\": 954, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.1262/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 692, \"label\": \"Table\"}]"
motivation: 多模态大模型的推理过程不透明，难以区分其依赖记忆知识还是视觉信息。
method: 构建视觉反事实数据集，将世界知识与视觉输入对立，分析模型层间动态。
result: 发现模型在早期层偏向先验，中后层转向视觉证据。
conclusion: 揭示视觉输入最终主导推理，为解释VLM行为提供了工具。
---

## Abstract
Multimodal Large Language Models (MLLMs) perform well on tasks such as visual question answering, but it remains unclear whether their reasoning relies more on memorized world knowledge or on the visual information present in the input image. To investigate this, we introduce Visual CounterFact, a new dataset of visually-realistic counterfactuals that put world knowledge priors (e.g, red strawberry) into direct conflict with visual input (e.g, blue strawberry). Using Visual CounterFact, we show that model predictions initially reflect memorized priors, but shift toward visual evidence in mid-to-late layers. This dynamic reveals a competition between the two modalities, with visual input ultimately overriding priors during evaluation. To control this behavior, we propose Pixels Versus Priors (PvP) steering vectors, a mechanism for controlling model outputs toward either world knowledge or visual input through activation-level interventions. On average, PvP successfully shifts 99.3% of color and 80.8% of size predictions from priors to counterfactuals. Together, these findings offer new tools for interpreting and controlling factual behavior in multimodal models.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义（研究动机与背景）
- **研究动机**：多模态大语言模型（MLLMs）在视觉问答等任务中表现优异，但其推理过程究竟是依赖**记忆中的世界知识先验**（如“草莓是红色的”）还是**当前输入的视觉信息**（如“这幅图里草莓是蓝色的”），尚不明确。理解这一机制对于提升模型的可靠性、安全性和可解释性至关重要。
- **背景**：在自然语言处理（NLP）中，已有大量工作研究语言模型如何存储和编辑事实性知识（如知识神经元、因果干预），但在多模态领域缺乏相应的**视觉反事实数据集**和**控制模型行为的方法**。现有基准（如VL-Checklist、VALSE）仅改变描述而非同时挑战视觉与语言先验，且图像编辑常引入伪影。
- **整体含义**：该工作旨在揭示MLLMs内部视觉感知与记忆先验的竞争关系，并提供一种可控制的干预手段，以深入理解模型的工作原理，并为未来更可靠的视觉语言系统奠定基础。

## 2. 论文提出的方法论

### 2.1 视觉反事实数据集（Visual CounterFact）
- **核心思想**：构造一系列视觉上逼真的反事实图像，将**世界知识先验**（如“草莓是红的”）与**视觉输入**（如“蓝色草莓”）置于直接冲突中。
- **关键技术细节**：
    - **四步构建流程**：
        1. **挑选具有强视觉先验的物体**：从McRae特征规范（人类标注）、ImageNet、CIFAR-100中筛选，标准是>30%受试者提及某种颜色或基于GPT-4o估计的典型属性。
        2. **检索真实世界图像**：使用Google Images API获取白色背景下的物体图片，并由GPT-4o过滤（要求：物体正确、颜色准确、背景白色、真实感强），最终保留575个物体用于颜色任务，877个物体对用于尺寸任务。
        3. **生成反事实关系**：
            - **颜色任务**：用LLaVA-Next模型预测物体最不可能的5种颜色（如草莓→蓝色），确保与原始颜色视觉上可区分。
            - **尺寸任务**：通过GPT-4o估计物体真实尺寸，选择大小相差至少10倍的物体对，然后反转大小关系（如“苍蝇比草莓大”）。
        4. **编辑图像**：
            - 使用SAM2分割掩模，对颜色任务在HSV色彩空间仅修改色调（保持纹理和饱和度）；对尺寸任务调整掩模大小并放置在水平基线上（消除深度歧义）。
    - **数据集规模**：共2,904张图像（575个颜色原图+575个颜色反事实+877个尺寸原图+877个尺寸反事实），包含动物、家具、水果、工具等多样类别。

### 2.2 早期解码（Early Decoding）
- **方法**：对每一层隐藏状态应用最后的层归一化和反嵌入矩阵，解码出当前层预测的概率分布。用于追踪模型预测从“记忆先验”向“视觉感知”转变的层间动态。
- **发现**：在“最（most）”提示+反事实图像时，模型在中间层概率翻转（从世界知识答案转向反事实答案），表明视觉信息在晚期才压倒先验。

### 2.3 像素 vs 先验导向向量（PvP Steering）
- **核心思想**：通过对比两种提示（强调视觉的“this”提示 vs 强调知识的“most”提示）在最后一层隐藏状态的差异，构造导向向量，在推理时加到目标层以控制模型偏向视觉或先验。
- **公式**：
    - \( S_{\text{CF}}^l = \frac{1}{D} \sum_i ([h_l^n]_{\text{this}}^i - [h_l^n]_{\text{most}}^i) \) （朝向视觉证据）
    - \( S_{\text{WK}}^l = \frac{1}{D} \sum_i ([h_l^n]_{\text{most}}^i - [h_l^n]_{\text{this}}^i) \) （朝向先验）
    - 干预：\( \hat{h}_l^n = h_l^n + S_{\text{CF}}^l \) 或 \( \hat{h}_l^n = h_l^n + S_{\text{WK}}^l \)，应用于连续层 \( [l, l+w] \)。

## 3. 实验设计
- **数据集**：自建Visual CounterFact（颜色575对，尺寸877对），无需外部基准，但对比了不同提示（“this” vs “most”）和不同图像类型（世界知识图像 vs 反事实图像）下的模型表现。
- **模型**：LLaVA-Next-7B、Qwen2-VL-7B、DeepSeek Janus Pro-7B，覆盖主流架构。
- **评估任务**：颜色属性预测、尺寸关系预测。
- **对比方法**：
    - 无干预的基准确率（Table 1）
    - 提示更改（“most” → “this”）对注意力分布的影响（作为对照，非专用方法）。
- **主要实验组**：
    1. **零样本准确率测试**（Table 1）：4种设置（CF+this, WK+this, CF+most, WK+most），每个模型+每个任务共12个数据点。
    2. **层间翻转统计**（Table 2）：计算每样本翻转次数和翻转方向（WK→CF vs CF→WK），三个模型×两个任务×2个方向。
    3. **PvP导向性能**（Table 3）：对模型原本预测错误的子集（初始准确率0%）进行干预，报告成功翻转百分比和关键层范围。每个模型×两个任务×两个方向共12组。
    4. **注意力质量分析**（Figure 5, 6, Table 5）：测量干预前后图像/文本token的注意力质量变化，对比提示更改的效果。
    5. **早期解码可视化**（Figure 4, 12）：展示层间概率演化（LLaVA-Next为主，Qwen和Janus在附录）。

## 4. 资源与算力
- **论文未明确说明所使用的GPU型号、数量、训练时长**等算力资源。文中所有实验均为**推理或轻量级干预**（无模型微调），因此可能不需要大规模训练资源。数据集构建过程中使用了GPT-4o（云API）、Google Images API、SAM2（分段）、LLaVA-Next（预训练模型）等，但未报告具体硬件或时间。

## 5. 实验数量与充分性
- **数量**：总计约30余组定量实验（准确率、翻转统计、导向成功率、注意力变化）加上大量定性分析（早期解码、注意力热图）。数据集包含约2900张图像，三个模型，两个属性任务。
- **充分性**：
    - **优点**：覆盖多种主流模型，任务设计清晰（颜色和尺寸），有详细的消融（对比提示更改 vs 干预）；注意力分析从机制层面解释干预效果。
    - **不足**：
        - 仅涉及**7B规模**的模型，未测试更大模型（如13B、70B）或不同架构（如单流MLLM）。
        - 颜色和尺寸任务代表常见的视觉属性，但未涵盖更多属性（如形状、材质、纹理）。
        - 数据集构建依赖GPT-4o和LLaVA-Next的自动标注，可能存在偏差（如某些物体颜色先验不牢靠）。
        - 实验主要聚焦于“反事实图像”下的表现，未在自然分布下全面评估模型的一般性能。
    - **客观公平性**：所有实验使用相同的提示模板、评价规则，结果可复现；但超参数（导向层范围w）是手工选择的，可能对特定模型有微调。

## 6. 论文的主要结论与发现
1. **视觉输入主导推理**：当图像与先验冲突时，MLLMs倾向于依据图像回答，即使提示词要求陈述一般事实（“most”提示），准确率仍然大幅下降（颜色任务从92%降至47%，尺寸从96%降至40%）。
2. **层间翻转现象**：早期解码显示，模型在中间层开始从先验答案翻转向反事实答案，说明视觉信息在深层才被整合并覆盖记忆知识。
3. **PvP导向有效控制**：在原本预测错误的样本上，导向向量成功将99.3%的颜色预测和80.8%的尺寸预测从先验翻转为反事实；反向（CF→WK）成功率较低，表明视觉证据对抗知识先验时更强。
4. **注意力机制解释**：干预后模型对图像token的注意力质量显著提升（最高40%），效果远超单纯改变提示词（13%），表明导向向量在内部注意力层发挥了实质性调整。
5. **非对称性**：从先验导向视觉比从视觉导向先验更容易，反映模型内在倾向于依赖当下感知。

## 7. 优点
- **新颖的研究范式**：首次系统性地构造**视觉反事实**数据集，专门针对MLLMs中记忆先验与视觉输入的冲突，填补了该方向评测和解释工具的空白。
- **方法简洁且有效**：PvP导向向量基于推理时的激活差异，无需训练或微调，计算成本低，且能精确控制模型行为；注意力分析提供了直接的可解释性证据。
- **跨模型通用性**：在三种主流模型上一致验证了结论，表明发现的动态具有普遍性。
- **贡献数据集**：Visual CounterFact具有2,904张高质量图像，经过人工和自动筛选，可推广作为未来可解释性研究的基准。

## 8. 不足与局限
- **实验覆盖有限**：
    - 仅三种7B模型，未覆盖更大规模或不同架构（如单流MLLM、纯视觉Transformer+LLM组合）。
    - 仅测试颜色和尺寸两种属性，未触及形状、纹理、材质、位置关系等更复杂的特性。
- **数据集偏差风险**：
    - 颜色和尺寸先验依赖GPT-4o或LLaVA-Next的自动判断，可能包含错误或与文化差异相关（例如某些物体在不同文化中典型颜色不同）。
    - 图像均处理为白色背景，与现实场景有差距，限制了结论的生态效度。
- **任务难度不对称**：尺寸任务需要同时检测两个物体并比较大小，本就比颜色任务复杂，导致导向成功率较低（WK→CF 71-90% vs 颜色99%），且干预层窗口更宽、更不稳定。
- **反向导向困难**：CF→WK方向在所有模型中均低于WK→CF，说明模型优先依赖视觉信息，抑制先验相对困难，该现象未被充分解释。
- **实用场景缺失**：论文未在现实应用（如对话、开放域QA）中验证导向方法的鲁棒性、对正常样本的副作用或泛化能力。
- **算力信息缺失**：未提供任何计算资源描述，难以评估方法对大规模应用的可行性。

（完）
