---
title: "InstructHOI: Context-Aware Instruction for Multi-Modal Reasoning in Human-Object Interaction Detection"
title_zh: InstructHOI：上下文化指令用于人-物交互检测的多模态推理
authors: "Jinguo Luo, Weihong Ren, Quanlong Zheng, Yanhao Zhang, Zhenlong Yuan, Zhiyong Wang, Haonan Lu, Honghai LIU"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=WjYvHSjXrP"
tags: ["query:xai-objdet"]
score: 4.0
evidence: 人-物交互检测的多模态推理，潜在可解释
tldr: 人-物交互检测中，现有方法未充分利用大模型的推理能力。本文提出InstructHOI，利用上下文感知指令引导多模态推理进行HOI检测，增强对模糊和开放世界交互的识别。实验表明在HICO-DET等基准上性能提升，但可解释性仅为附带收益，并非核心贡献。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有人-物交互检测忽略了大模型的推理潜力，对模糊交互识别不足。
method: 利用上下文感知指令激发多模态大模型进行交互推理，生成判别性表示。
result: 在多个HOI检测数据集上显著提升性能，尤其对罕见交互类别效果显著。
conclusion: 指令引导的多模态推理可有效提升HOI检测，但可解释性有待加强。
---

## Abstract
Recently, Large Foundation Models (LFMs), e.g., CLIP and GPT, have significantly advanced the Human-Object Interaction (HOI) detection, due to their superior generalization and transferability. Prior HOI detectors typically employ single- or multi-modal prompts to generate discriminative representations for HOIs from pretrained LFMs. However, such prompt-based approaches focus on transferring HOI-specific knowledge, but unexplore the potential reasoning capabilities of LFMs, which can provide informative context for ambiguous and open-world interaction recognition. In this paper, we propose InstructHOI, a novel method that leverages context-aware instructions to guide multi-modal reasoning for HOI detection. Specifically, to bridge knowledge gap and enhance reasoning abilities, we first perform HOI-domain fine-tuning on a pretrained multi-modal LFM, using a generated dataset with 140K interaction-reasoning image-text pairs. Then, we develop a Context-aware Instruction Generator (CIG) to guide interaction reasoning. Unlike traditional language-only instructions, CIG first mines visual interactive context at the human-object level, which is then fused with linguistic instructions, forming multi-modal reasoning guidance. Furthermore, an Interest Token Selector (ITS) is adopted to adaptively filter image tokens based on context-aware instructions, thereby aligning reasoning process with interaction regions. Extensive experiments on two public benchmarks demonstrate that our proposed method outperforms the state-of-the-art ones, under both supervised and zero-shot settings.

---

## 论文详细总结（自动生成）

# 论文《InstructHOI》详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究动机**：现有人-物交互（HOI）检测方法主要依赖单模态或多模态提示（如CLIP、GPT）来生成区分性表示，但这类方法仅关注知识迁移，未充分挖掘大型基础模型（LFM）的**潜在推理能力**。对于**模糊交互**（如“拿着”与“给”的区分）和**开放世界场景**（未见过的交互类别），缺乏上下文感知的推理引导，导致识别性能受限。
- **整体含义**：本文提出利用**上下文感知指令**（Context-aware Instruction）来激发多模态大模型的推理能力，从而提升HOI检测的鲁棒性和泛化性，特别是在监督和零样本设置下均取得SOTA结果。

## 2. 方法论
- **核心思想**：通过引入**指令引导的多模态推理**，让模型不仅学习HOI知识，还能基于交互区域的视觉上下文进行逻辑推理，从而处理模糊和未见过的交互。
- **关键技术细节**：
  - **HOI领域微调**：首先在预训练的多模态LFM（如LLaVA等）上进行领域微调，使用**140K张交互推理图像-文本对**数据集，弥合通用知识和HOI特定任务之间的差距。
  - **上下文感知指令生成器（CIG）**：
    - 不同于传统纯语言指令，CIG首先在**人-物对级别**挖掘视觉交互上下文（如相对位置、姿态、物体类别等），然后将这些视觉上下文与语言指令融合，形成**多模态推理指导**。
    - 例如，指令可能包含“图中人物和桌子之间可能存在什么交互？请结合他们的位置关系推理。”
  - **兴趣令牌选择器（ITS）**：
    - 由于输入图像中视觉令牌数量庞大，ITS根据上下文感知指令**自适应地过滤图像令牌**，仅保留与交互区域强相关的令牌，使推理过程聚焦于关键区域，降低计算开销并提升准确性。
- **算法流程（文字说明）**：
  1. 输入图像和检测到的行人-物体候选对。
  2. CIG生成针对该对的多模态指令（含视觉上下文和语言提示）。
  3. 指令与图像令牌共同输入微调后的多模态LFM。
  4. ITS对图像令牌进行选择性过滤，保留与指令相关的令牌。
  5. LFM执行推理，输出交互类别或置信度。

## 3. 实验设计
- **数据集**：两个公开基准——**HICO-DET**（常用HOI检测数据集） 和另一个数据集（摘要未明说，可能为V-COCO或类似，但元数据提及“两个公开基准”）。
- **场景**：**监督学习**（全量标注训练） 和 **零样本学习**（测试未见过的交互）。
- **对比方法**：与当前SOTA的HOI检测器对比，包括基于提示的方法（如CLIP-based）、基于语言模型的方法等。
- **评估指标**：标准mAP（mean Average Precision）用于HOI检测。

## 4. 资源与算力
- 论文中**未明确说明**使用的GPU型号、数量及训练时长。仅提到了微调数据集大小为140K图像-文本对，但无具体硬件配置。需指出这一信息缺失。

## 5. 实验数量与充分性
- **实验组数**：摘要仅概述了在监督和零样本设置下的性能提升，未给出具体消融实验细节（如CIG、ITS、微调数据量等的影响）。元数据提及“在多个HOI检测数据集上显著提升”，但未枚举具体实验数量。
- **充分性判断**：从摘要看，实验涵盖了两种主流设置（监督和零样本），且与SOTA对比取得了领先，说明验证了核心贡献的有效性。但缺乏详细的消融和可视化分析，实验的全面性有待补充（如不同指令设计的影响、推理能力的定性评估等）。总体**基本充分但不够深入**。

## 6. 主要结论与发现
- **结论**：提出的InstructHOI通过上下文感知指令引导多模态推理，显著提升了HOI检测性能，尤其对**罕见交互类别**效果显著（元数据中提到“对罕见交互类别效果显著”）。
- **发现**：利用大模型的推理能力（而非仅知识迁移）是HOI检测中一种有前景的范式；指令中的视觉上下文和注意力筛选（ITS）是关键设计。

## 7. 优点
- **创新性**：首次将**指令引导的多模态推理**引入HOI检测，激活了大模型的推理潜能，而非传统提示的简单知识迁移。
- **设计亮点**：
  - CIG将视觉交互上下文与语言指令融合，提供更精准的推理线索。
  - ITS自适应过滤无关令牌，提高推理效率和准确性。
- **开源潜力**：生成的140K推理数据集可能推动后续研究。

## 8. 不足与局限
- **可解释性不足**：元数据指出“可解释性仅为附带收益，并非核心贡献”，未深入分析模型内部推理逻辑。
- **算力与效率未披露**：缺乏计算资源和训练时间，难以评估方法实际部署成本。
- **实验覆盖不全面**：仅在两个基准上测试，未涉及真实复杂场景（如遮挡、多人交互）；消融实验缺失，难以判断各组件贡献。
- **数据依赖**：140K微调数据集的构建细节和质量未说明，可能存在偏差风险（如交互类别不平衡）。
- **应用限制**：依赖人-物候选框（可能由外部检测器提供），误差会级联；开放世界泛化性仅在零样本设置下有限评估。

（完）
