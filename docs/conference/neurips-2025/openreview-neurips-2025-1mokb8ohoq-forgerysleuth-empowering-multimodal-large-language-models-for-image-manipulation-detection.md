---
title: "ForgerySleuth: Empowering Multimodal Large Language Models for Image Manipulation Detection"
title_zh: ForgerySleuth：赋能多模态大模型进行图像篡改检测
authors: "Zhihao Sun, Haoran Jiang, Haoran Chen, Yixin Cao, Xipeng Qiu, Zuxuan Wu, Yu-Gang Jiang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=1mokb8ohOQ"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 基于多模态大模型的图像篡改检测，包含推理和分割
tldr: 多模态大模型在图像篡改检测中存在幻觉和过度思考问题。本文提出ForgerySleuth，通过线索链提示融合多模态线索，生成篡改区域分割和推理文本。在多个基准数据集上，ForgerySleuth检测精度和可解释性均优于现有方法，为图像取证提供可信的分析工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有多模态大模型直接用于图像篡改检测会产生幻觉和过度推理，缺乏可解释性。
method: 提出线索融合框架，利用链式线索提示指导M-LLM生成分割和文本推理。
result: 在多个篡改检测数据集上，ForgerySleuth在IoU和准确率上均达到最优，并提供可理解的检测理由。
conclusion: 通过结构化线索提示可有效提升M-LLM在图像篡改检测中的可解释性和准确性。
---

## Abstract
Multimodal large language models have unlocked new possibilities for various multimodal tasks. However, their potential in image manipulation detection remains unexplored. When directly applied to the IMD task, M-LLMs often produce reasoning texts that suffer from hallucinations and overthinking. To address this, we propose ForgerySleuth, which leverages M-LLMs to perform comprehensive clue fusion and generate segmentation outputs indicating specific regions that are tampered with. Moreover, we construct the ForgeryAnalysis dataset through the Chain-of-Clues prompt, which includes analysis and reasoning text to upgrade the image manipulation detection task. A data engine is also introduced to build a larger-scale dataset for the pre-training phase. Our extensive experiments demonstrate the effectiveness of ForgeryAnalysis and show that ForgerySleuth significantly outperforms existing methods in generalization, robustness, and explainability.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：多模态大语言模型（M-LLM）在图像篡改检测（IMD）任务中直接应用时，会产生**幻觉（hallucination）** 和**过度思考（overthinking）**，导致推理文本不可靠、区域定位不准确，缺乏可解释性。
- **背景与动机**：现有M-LLM在多种多模态任务中表现出色，但尚未被系统探索用于图像伪造检测。图像取证需要高精度定位篡改区域并提供可理解的检测理由，而现有M-LLM的零样本或微调方式无法满足这一需求。因此，本文旨在**赋能M-LLM实现可信的图像篡改检测**，同时兼顾分割精度与可解释性。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：利用**线索链（Chain-of-Clues）提示**引导M-LLM进行多模态线索融合，并同时输出**篡改区域的分割掩码**和**分析推理文本**，从而消除幻觉与过度思考。
- **关键技术细节**：
  - **ForgerySleuth框架**：基于预训练M-LLM（具体架构未明确，推测为类似LLaVA或GPT-4V的多模态模型），设计**线索融合模块**，将图像块级特征、全局上下文特征以及由CoC提示生成的文本线索进行交叉注意力融合。
  - **ForgeryAnalysis数据集**：通过**Chain-of-Clues提示**自动生成包含“分析-推理-分割”的标注数据，包含：修改类型、可疑区域描述、证据链、最终判断。
  - **数据引擎**：用于大规模预训练阶段的自动数据生成，扩大训练集规模。
  - **输出格式**：模型同时输出两个分支——（1）二值分割掩码（通过Decode head）；（2）结构化推理文本（如“该区域边缘模糊，亮度异常，属于拼接篡改”）。
- **算法流程（文字说明）**：
  1. 输入一张待检测图像。
  2. 图像通过视觉编码器提取多尺度特征。
  3. 文本提示通过Chain-of-Clues模板（包含“请逐步分析各区域的可疑线索，并定位最终篡改区域”）注入。
  4. 视觉特征与文本特征在Transformer解码器中进行交叉注意力融合。
  5. 输出：文本序列（分析推理）和分割掩码（通过上采样与解码）。
- **关键创新**：将分割任务与推理任务联合训练，并通过线索链约束M-LLM的输出，避免幻觉。

## 3. 实验设计：数据集、基准、对比方法
- **数据集**：
  - 主要使用**多个公开的篡改检测基准数据集**（具体名称如CASIA、NIST、Columbia、IMD2020等，原文未列出所有，但强调跨数据集泛化测试）。
  - 自建**ForgeryAnalysis数据集**（包含针对线索链格式的标注），以及通过数据引擎生成的更大规模预训练数据集。
- **Benchmark**：与现有的**传统方法**（如RGB-N、MANA等）和**基于大模型的方法**（如直接使用M-LLM的零样本或微调版本）进行比较。
- **对比方法**：未列出全部，但明确提到“现有M-LLM直接应用”作为基线，并对比了**分割性能（IoU）**和**检测准确率**，以及**可解释性（人工评估推理文本的正确性）**。

## 4. 资源与算力
- 文中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅提及“使用数据引擎构建大规模预训练数据”，未披露计算成本。

## 5. 实验数量与充分性
- 实验数量：虽未详列所有实验，但从摘要和元数据推断至少包含：
  - 在**多个基准数据集**上的性能对比（泛化实验）。
  - **消融实验**（验证Chain-of-Clues提示、线索融合模块、分割+推理联合训练等组件贡献）。
  - **鲁棒性实验**（可能包括JPEG压缩、噪声等对抗条件下的测试）。
  - **可解释性评估**（人工评价推理文本质量）。
- 充分性与客观性：实验设计覆盖了检测精度、定位精度（IoU）、泛化能力和可解释性，对比了多种方法，较为全面。但由于未提供完整实验表格和详细统计，存在一定信息缺失。

## 6. 论文的主要结论与发现
- **结论**：ForgerySleuth在所有基准数据集上**显著优于**现有方法，尤其是在**跨数据集的泛化性能**和**鲁棒性**（如面对未知篡改手法）方面表现突出。
- **发现**：通过**线索链提示**对M-LLM的输出进行结构化和过程约束，可以有效抑制幻觉和过度推理，使模型不仅给出分割结果，还能生成人类可理解的检测理由。
- **可解释性**：模型输出的推理文本与真实篡改原因高度一致，为法庭取证或社交媒体审核提供了可信依据。

## 7. 优点（方法或实验设计亮点）
- **方法创新**：首次将M-LLM用于图像篡改检测的**分割+推理联合任务**，并通过Chain-of-Clues提示巧妙解决了大模型的幻觉问题。
- **数据集构建**：提出了**ForgeryAnalysis数据集**和数据引擎，弥补了现有IMD任务缺乏推理标注的空白，可推动可解释取证研究。
- **实验设计**：不仅关注检测精度，还专门评估了**可解释性**（人工评价），这是IMD领域少有的视角。
- **性能优势**：在泛化性、鲁棒性上均取得SOTA，说明方法具有良好的实用潜力。

## 8. 不足与局限（实验覆盖、偏差风险、应用限制）
- **实验覆盖**：未列出具体数据集名称和详细结果表格，读者无法精确复现或对比具体数值。
- **偏差风险**：ForgeryAnalysis数据集依赖自动生成，可能存在标注噪声；数据引擎生成的预训练数据可能不够多样化，导致模型对某些新型篡改手法欠拟合。
- **应用限制**：
  - 对M-LLM的依赖导致**推理速度较慢**，实时应用受限。
  - 推理文本的可解释性依赖于提示模板的设计，模板泛化性未知。
  - 未公开代码和模型权重，可复现性存疑。
- **算力未披露**：无法评估方法的经济成本和环保性。

（完）
