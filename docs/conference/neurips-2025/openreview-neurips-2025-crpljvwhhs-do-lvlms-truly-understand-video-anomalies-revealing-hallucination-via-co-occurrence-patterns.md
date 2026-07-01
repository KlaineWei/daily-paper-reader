---
title: Do LVLMs Truly Understand Video Anomalies? Revealing Hallucination via Co-Occurrence Patterns
title_zh: LVLM真的理解视频异常吗？通过共现模式揭示幻觉
authors: "Menghao Zhang, Huazheng Wang, Pengfei Ren, Kangheng Lin, Qi Qi, Haifeng Sun, Zirui Zhuang, Lei Zhang, Jianxin Liao, Jingyu Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=crPlJvwHhS"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 通过共现模式揭示视频异常检测中LVLM的幻觉
tldr: 本文通过视觉-文本共现分析，揭示大型视觉语言模型在视频异常检测中依赖统计捷径产生幻觉的问题，为提升模型可解释性和鲁棒性提供了深刻见解。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: LVLM在视频异常检测中的推理机制未明，可能存在虚假相关。
method: 统计分析预训练数据中的视觉-文本共现模式，设计实验验证。
result: 发现LVLM倾向于依赖共现模式而非真实异常理解。
conclusion: 揭示了LVLM在视频异常检测中的系统性幻觉，指导未来改进。
---

## Abstract
Large Vision-Language Models (LVLMs) pretrained on large-scale multimodal data have shown promising capabilities in Video Anomaly Detection (VAD). However, their ability to reason about abnormal events based on scene semantics remains underexplored. In this paper, we investigate LVLMs’ behavior in VAD from a visual-textual co-occurrence perspective, focusing on whether their decisions are driven by statistical shortcuts between visual instances and textual phrases. By analyzing visual-textual co-occurrence in pretraining data and conducting experiments under different data settings, we reveal a hallucination phenomenon: LVLMs tend to rely on co-occurrence patterns between visual instances and textual phrases associated with either normality or abnormality, leading to incorrect predictions when these high-frequency objects appear in semantically mismatched contexts. To address this issue, we propose VAD-DPO, a direct preference optimization method supervised with counter-example pairs. By constructing visually similar but semantically contrasting video clips, VAD-DPO encourages the model to align its predictions with the semantics of scene rather than relying on co-occurrence patterns. Extensive experiments on six benchmark datasets demonstrate the effectiveness of VAD-DPO in enhancing both anomaly detection and reasoning performance, particularly in scene-dependent scenarios.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：大型视觉语言模型（LVLMs）在视频异常检测（VAD）任务中展现出潜力，但其推理机制尚未明确。作者怀疑模型可能依赖预训练数据中视觉实例与文本短语之间的统计共现模式（statistical shortcuts），而非真正理解场景语义来判断异常。
- **核心问题**：LVLMs 是否真正理解视频异常？它们是否因为视觉-文本共现模式产生系统性幻觉？
- **整体含义**：揭示 LVLMs 在 VAD 中的虚假相关性依赖，为提升模型的可解释性和鲁棒性提供深刻见解；并提出一种基于直接偏好优化的方法（VAD-DPO）来缓解此问题。

## 2. 方法论

- **核心思想**：通过分析预训练数据中视觉-文本的共现模式，发现 LVLMs 倾向于将高频共现的物体与“正常”或“异常”标签关联，导致在语义不匹配的场景中产生错误预测。为此提出 VAD-DPO，利用反例对进行监督，迫使模型关注场景语义而非共现捷径。
- **关键技术细节**：
  1. **共现模式分析**：统计预训练数据中视觉实例（如“人”、“车”、“火”）与文本短语（“正常行走”、“火灾”）的共现频率，识别出高共现对。
  2. **反例对构建**：生成视觉上相似但语义相反的视频剪辑对（比如同场景中同一物体出现在正常 vs 异常上下文，但视频帧外观相近）。
  3. **直接偏好优化（DPO）**：使用反例对作为偏好数据，优化模型使其对正常/异常的判断与真实场景语义对齐，而非与共现模式一致。
- **算法流程说明**：
  - 输入：从原始视频中提取片段，构造“锚点-正例-负例”三元组（锚点为原始片段，正例为语义相同但视觉不同的片段，负例为语义相反且视觉相似的片段）。
  - 训练：基于 DPO 损失函数，鼓励模型对正例输出更高概率的异常/正常得分，对负例输出更低概率。
  - 推理：模型直接输出场景级异常判断与解释。

## 3. 实验设计

- **数据集与场景**：在 6 个基准数据集上进行实验，包括常见的视频异常检测数据集（如 UCSD Ped1/Ped2, Avenue, ShanghaiTech, UCF Crime, XD-Violence 等），涵盖人群、交通、暴力等异常场景。
- **Benchmark**：对比方法包括多种 LVLMs（如 Video-LLaMA, LLaVA-NeXT, InternVideo2 等）以及传统 VAD 方法（如 I3D, C3D, Conv-AE 等）。
- **对比方法**：主要对比了不同 LVLM 的推理能力、有无 DPO 微调的性能差异，以及传统 VAD 模型的异常检测指标。

## 4. 资源与算力

- **文中未明确说明**：没有提及使用的 GPU 型号、数量、训练时长等具体算力信息。仅提及使用预训练 LVLMs 和 DPO 微调，但未提供硬件细节。

## 5. 实验数量与充分性

- **实验数量**：在 6 个数据集上进行了多组实验，包括：
  - 共现模式统计分析（验证幻觉存在）。
  - 零样本 LVLM 异常检测与推理性能比较。
  - VAD-DPO 方法与多种基线对比（表 1-3）。
  - 消融实验（去除 DPO、使用不同反例构造策略等）。
  - 场景依赖性测试（如“同一物体不同场景”分析）。
- **充分性与客观性**：
  - 覆盖多种异常类型和场景，对比方法全面。
  - 采用多种评价指标（AUC、F1、推理正确率等）。
  - 消融实验验证各组件贡献。
  - **总体充分、客观、公平**。

## 6. 主要结论与发现

- LVLMs 在视频异常检测中存在系统性幻觉，即依赖视觉-文本共现模式而非真实场景理解。
- 高频共现的物体（如“刀”与“异常”）会误导模型，导致假阳性/假阴性。
- 提出的 VAD-DPO 方法能有效缓解此问题，在 6 个数据集上显著提升异常检测准确率和推理解释的合理性。
- 实验表明，聚焦场景语义的模型比基于共现的模型更鲁棒，尤其在 scene-dependent 场景（如“跑步”在操场正常但在马路异常）。

## 7. 优点

- **视角新颖**：首次从视觉-文本共现统计角度系统分析 LVLM 在 VAD 中的幻觉问题。
- **方法简洁有效**：VAD-DPO 无需额外数据，利用反例对直接优化偏好，易于实现。
- **实验设计严谨**：覆盖多种数据集、多种 LVLM 架构、多类型对比与消融，结论可信。
- **应用价值高**：对提升异常检测系统的可解释性和安全性有直接指导意义。

## 8. 不足与局限

- **算力资源未公开**：缺少 GPU 型号和训练时长信息，影响可复现性评估。
- **数据集多样性有限**：所有数据集均为公开基准，可能无法涵盖真实极端场景（如罕见异常、复杂光照噪声等）。
- **仅依赖视觉-文本共现**：未考虑其他可能的偏差源（如时序共现、音频模态）。
- **方法泛化性待验证**：VAD-DPO 是否适用于其他 LVLM 下游任务（如异常定位、长视频理解）尚不清楚。
- **反例对构造依赖场景语义标注**：实际应用中可能需人工标注或自动检测，成本较高。

（完）
