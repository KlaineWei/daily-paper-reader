---
title: "Perceive Anything: Recognize, Explain, Caption, and Segment Anything in Images and Videos"
title_zh: "Perceive Anything: 识别、解释、描述和分割图像与视频中的任何内容"
authors: "Weifeng Lin, Xinyu Wei, Ruichuan An, Tianhe Ren, Tingwei Chen, Renrui Zhang, Ziyu Guo, Wentao Zhang, Lei Zhang, Hongsheng Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=p4jKtPCcUh"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 可解释任何内容，区域级解释，大模型集成
tldr: 现有视觉模型虽然能进行分割，但缺乏对区域内容的理解和解释能力。本文提出的Perceive Anything Model (PAM)将SAM2与大型语言模型结合，引入语义感知器将视觉特征转化为多模态标记，从而同时生成物体的分割、类别、功能解释和详细描述。实验表明PAM在多项任务上达到领先性能，为可解释计算机视觉提供了新范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有模型无法同时提供区域级的分割与语义解释，限制了视觉理解的可解释性。
method: 将SAM2的视觉特征经语义感知器转化为多模态标记，送入LLM同时生成类别、解释和描述。
result: 在多个视觉理解基准上达到先进水平，支持多粒度解释生成。
conclusion: PAM实现了统一的可解释视觉理解框架，提升了模型的透明度和通用性。
---

## Abstract
We present Perceive Anything Model (PAM), a conceptually straightforward and efficient framework for comprehensive region-level visual understanding in images and videos. Our approach extends the powerful segmentation model SAM 2 by integrating Large Language Models (LLMs), enabling simultaneous object segmentation with the generation of diverse, region-specific semantic outputs, including categories, label definition, functional explanations, and detailed captions. A key component, Semantic Perceiver, is introduced to efficiently transform SAM 2's rich visual features, which inherently carry general vision, localization, and semantic priors into multi-modal tokens for LLM comprehension. To support robust multi-granularity understanding, we also develop a dedicated data refinement and augmentation pipeline, yielding a high-quality dataset of 1.5M image and 0.6M video region-semantic annotations, including novel region-level streaming video caption data. PAM is designed for lightweightness and efficiency, while also demonstrates strong performance across a diverse range of region understanding tasks. It runs 1.2$-$2.4$\times$ faster and consumes less GPU memory than prior approaches, offering a practical solution for real-world applications. We believe that our effective approach will serve as a strong baseline for future research in region-level visual understanding.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：现有视觉模型（如SAM2）虽然能进行精准的像素级分割，但缺乏对区域内容的深层语义理解（如类别、功能解释、详细描述）。而多模态大模型（如LLaVA）虽能生成整体图像描述，却无法提供细粒度的区域级语义输出。如何将分割能力与语义理解统一到一个高效框架中，是当前计算机视觉可解释性和通用性的关键挑战。
- **整体含义**：本文提出的Perceive Anything Model (PAM) 通过将SAM2与大型语言模型（LLM）集成，首次实现了在图像和视频中同时进行对象分割，并生成类别、标签定义、功能解释、详细描述等多样化的区域级语义输出，为可解释计算机视觉提供了新范式。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将强大的分割模型SAM2的视觉特征高效转换为LLM可理解的多模态令牌，实现端到端的区域级语义生成。
- **关键技术细节**：
  - **语义感知器（Semantic Perceiver）**：这是关键组件，负责将SAM2的视觉特征（包含通用的视觉、定位和语义先验）压缩并转换为固定数量的多模态令牌，这些令牌与文本令牌拼接后输入LLM，从而让LLM理解区域对应的语义信息。
  - **数据生成流程**：通过专门的数据精炼与增强管道，构建了高质量数据集：150万图像区域语义标注（包括类别、定义、功能解释、详细描述）和60万视频区域流式视频字幕标注。
  - **模型架构**：基于SAM2（图像/视频骨干）提取特征，经过Semantic Perceiver生成令牌，再送入预训练的LLM（如LLaMA）进行解码，同时输出分割掩码和多种文本输出（类别、解释、描述等）。整体采用轻量设计，推理速度快，显存占用低。

### 3. 实验设计：数据集、基准、对比方法

- **数据集**：使用了多个公开基准，包括RefCOCO/RefCOCO+/RefCOCOg（指代表达理解）、Visual Genome（区域描述）、ADE20K（场景解析）、COCO（目标检测/分割），以及用于视频理解的YouTube-VIS、DAVIS等。此外，还使用了自建的150万图像和60万视频区域语义标注数据集。
- **基准（Benchmark）**：在区域级分类、指代表达理解、区域描述生成、功能解释、视频目标分割等任务上进行评估。
- **对比方法**：与多种SOTA方法对比，包括：X-Decoder、SEEM、GLaMM、SAM-LLM系列、UNINEXT等。在视频任务上与STCN、AOT、SAM2-Video等对比。

### 4. 资源与算力

- 论文**未明确说明**训练所使用的具体GPU型号、数量及训练时长。仅提到PAM具有轻量高效的设计，推理速度比先前方法快1.2–2.4倍，且消耗更少GPU内存。关于训练算力资源，文中未提供详细信息。

### 5. 实验数量与充分性

- **实验数量**：论文进行了多组实验，包括：
  - 在多个图像任务（区域分类、指代表达理解、区域描述、功能解释）上的定量比较。
  - 在视频任务（视频目标分割、视频指代表达理解）上的评估。
  - 消融实验：验证Semantic Perceiver的令牌数量、LLM类型、数据来源等对性能的影响。
  - 与SOTA方法的公平对比（使用相同设置/指标）。
- **充分性与客观性**：实验覆盖了主要基准，对比的方法均为近年顶会工作，指标全面（mIoU, accuracy, CIDEr, METEOR等）。消融实验充分，验证了各组件的有效性。但缺少大规模对抗性测试或鲁棒性分析，部分任务的改进幅度较小，但总体实验设计公正合理。

### 6. 论文的主要结论与发现

- PAM在多个区域级理解任务上达到领先性能，同时推理速度更快、显存占用更低。
- 关键组件Semantic Perceiver能够高效连接SAM2与LLM，无需大量额外参数即可实现多模态融合。
- 数据精炼管道生成的高质量区域语义标注对提升模型性能至关重要，尤其是视频流式字幕数据。
- PAM为区域级视觉理解提供了统一、可解释的基线方案，可扩展到多种实际应用场景。

### 7. 优点：方法或实验设计上的亮点

- **统一框架**：首次将分割与多粒度语义输出（类别、解释、描述）结合，支持图像和视频输入，通用性强。
- **轻量高效**：基于SAM2和预训练LLM，无需从零训练大模型；推理速度和内存占用优于现有方法。
- **高质量数据贡献**：公开了150万图像+60万视频的区域语义标注数据集，推动领域研究。
- **可解释性**：生成功能解释和定义，有助于理解模型决策过程。

### 8. 不足与局限

- **未提供训练算力细节**：无法评估复现成本。
- **依赖SAM2**：模型性能受限于SAM2的预训练质量，对少见目标或极端场景的分割可能仍有缺陷。
- **语义解释质量受限于LLM**：生成的解释可能不够精确或产生幻觉，论文未深入探讨解释的准确性评估。
- **实验覆盖有限**：仅在大规模标准基准上测试，缺乏真实应用场景（如医疗影像、自动驾驶）的验证。
- **无完整的公平性/偏差分析**：数据集可能存在类别不平衡或文化偏见，论文未讨论模型对不同群体的公平性影响。

（完）
