---
title: "Knowledge Image Matters: Improving Knowledge-Based Visual Reasoning with Multi-Image Large Language Models"
title_zh: 知识图像至关重要：利用多图像大语言模型改进知识型视觉推理
authors: "Guanghui Ye, Huan Zhao, Zhixue Zhao, Xupeng Zha, Yang Liu, Zhihua Jiang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1063.pdf"
tags: ["query:xai-objdet"]
score: 5.0
evidence: 基于知识的视觉推理中的物体检测
tldr: 针对知识型视觉推理中多模态大模型对物体信息利用不足的问题，本文提出视觉知识卡（VKC），融合场景感知信息和外部的属性/物体知识，并设计VKC-MIR四阶段流水线。实验证明该方法显著提升了推理性能。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1063/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 775, \"height\": 771, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1063/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 853, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1063/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1550, \"height\": 956, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1063/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 552, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1063/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 773, \"height\": 318, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025.acl-long.1063/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 600, \"height\": 223, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 795, \"height\": 800, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 776, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 711, \"height\": 172, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 790, \"height\": 166, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 781, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 697, \"height\": 145, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 790, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 782, \"height\": 156, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025.acl-long.1063/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 716, \"height\": 177, \"label\": \"Table\"}]"
motivation: 多模态大模型在知识型视觉推理中未能充分利用物体级别的视觉知识。
method: 构建包含场景和物体知识的视觉知识卡，设计四阶段推理流水线。
result: 在多个知识推理基准上取得了先进结果。
conclusion: VKC-MIR有效增强了多模态大模型的视觉推理能力。
---

## Abstract
We revisit knowledge-based visual reasoning (KB-VR) in light of modern advances in multimodal large language models (MLLMs), and make the following contributions: (i) We propose Visual Knowledge Card (VKC) – a novel image that incorporates not only internal visual knowledge (e.g., scene-aware information) detected from the raw image, but also external world knowledge (e.g., attribute or object knowledge) produced by a knowledge generator; (ii) We present VKC-based Multi-Image Reasoning (VKC-MIR) – a four-stage pipeline which harnesses a state-of-the-art scene perception engine to construct an initial VKC (Stage-1), a powerful LLM to generate relevant domain knowledge (Stage-2), an excellent image editing toolkit to introduce generated knowledge into the updated VKC (Stage-3), and finally, an emerging multi-image MLLM to solve the VKC-enhanced task (Stage-4). By performing experiments on three popular KB-VR benchmarks, our approach achieves new state-of-the-art results compared to previous top-performing models.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **研究主题**：知识型视觉推理（KB‑VR），即模型需要结合图像内容与外部世界知识来回答开放域问题。
- **现有不足**：
  - 传统方法将知识表示为文本三元组或场景图，但多模态大模型（MLLM）在处理视觉信息时对“知识图像”这一模态的利用不足。
  - 多图像 MLLM 虽然具备多图理解能力，但若输入图像包含干扰信息，模型反而会困惑。
- **整体含义**：本文首次探索将知识以**图像形式**呈现（称为视觉知识卡 VKC），并利用多图像 MLLM 解决增强后的推理任务，为 KB‑VR 开辟新视角。

### 2. 方法论：核心思想、关键技术细节、算法流程

- **核心思想**：将原始图像中的内部知识（场景感知）与 LLM 生成的外部知识（属性/关系）融合到一张新图像（VKC）中，然后作为额外视觉输入交给多图像 MLLM 进行推理。
- **四阶段流水线**：
  1. **视觉场景感知**：  
     - 使用 HiKER‑SGG 生成场景图（文本三元组，如 `<实体, 空间关系, 实体>`）。  
     - 使用 GLEE 检测并分割出关键实体区域。  
     - 利用 graphviz 将场景图可视化，用实体区域替换节点，得到初始 VKC（场景图像）。
  2. **外部知识生成**（核心算法见 Alg.2）：  
     - 以实体名和问题为输入，用 OPT‑66B LLM 生成属性知识（`<实体, 属性, 值>`）和对象知识（`<实体1, 关系, 实体2>`）。  
     - 从 DBPedia 检索少量三元组作为少样本示例。  
     - 通过规则验证器（检查格式冲突）和排序器（基于 Sentence‑BERT 计算与问题的语义相似度）过滤并选择最相关的知识三元组。
  3. **知识图像编辑**：  
     - 使用 SEED‑X（文本到图像工具）迭代地将选中的知识三元组添加到 VKC 中。每次只添加一条，严格保持其他元素不变。  
     - 属性知识：在实体旁添加值标签并用蓝色箭头连接；对象知识：在实体间添加红色箭头并标注关系。
  4. **多图像推理**：  
     - 将原始图像 `V`、生成的 `VKC` 和问题 `Q` 作为输入，使用 mPLUG‑Owl3（多图像 MLLM）通过跨注意力融合视觉与文本特征，输出答案。

### 3. 实验设计

- **数据集**：三个主流 KB‑VR 基准  
  - **A‑OKVQA**（约 2.5 万题，需常识和世界知识）  
  - **OK‑VQA**（约 1.4 万题，涵盖科学、历史、体育等）  
  - **InfoSeek**（约 135 万样本，需专业领域知识）
- **基准方法**分为四类：  
  1. **纯多模态方法**（未使用 LLM）：LXMERT、KRISP、MAVEx、GPV‑2、UnifER、RZF‑VQA。  
  2. **基于 LLM 的语言方法**：PICa（GPT‑3）、Prophet（GPT‑3）、VCTP（Llama2‑70B）。  
  3. **开源单图像 MLLM**：Qwen‑VL‑Chat、mPLUG‑Owl、LLaVA‑1.5。  
  4. **开源多图像 MLLM**：Mantis、Idefics2、mPLUG‑Owl3（本文默认 MIR 模型）。
- **评估指标**：VQA 准确率（%）。

### 4. 资源与算力

- **GPU**：4 × NVIDIA 3090 24GB。  
- **VKC 生成**：涉及多个 LLM/MLLM 调用，但 VKC 平均大小仅 **1.72M**（与原始图像相当）。  
- **推理时间**：原始任务 ~2.4 小时，增强任务 ~2.6 小时（在 OK‑VQA 上平均），额外开销可忽略。  
- **训练**：整个流水线无需在新数据集上重训练，所有工具均为开源。

### 5. 实验数量与充分性

- **主要结果**（表1）：在三个数据集上与 16 种方法对比，VKC‑MIR 均获得最高分（58.9/64.8/25.1）。
- **模型无关性验证**（表2）：在 6 种不同 MLLM（单/多图像）上替换 VKC 均优于基线，且 VKC 优于场景图（SG）和图像描述（CAP）。
- **消融实验**（表3）：6 种变体（仅 MIR、GS+MIR、Ke+MIR、GS+Ke+MIR、GS→VS+MIR、完整 VKC‑MIR），验证各组件贡献。
- **不同 LLM 作为领域专家**（表4）：OPT‑66B、Llama2‑70B、GPT3‑175B 效果相当。
- **知识验证与排序**（表5）：分别去除验证器或排序器后性能下降。
- **超参数测试**（表6）：在 OK‑VQA 上探索总知识数（4/8/16/32）和每次添加数（1/2/4/8/16），最优为 `#Ke=16, #Kei=1`。
- **知识图像必要性**（表7）：VKC‑image 优于 VKC‑triple。
- **多图像任务**（表8）：在 MIBench 的四个子任务（SD、VRef、VTK、TVK）上 VKC‑MIR 均优于其他 MLLM。
- **与封闭源 MLLM 对比**（图4）：在 A‑OKVQA 上超过 GPT‑4o。
- **综合评估**：实验覆盖主要基准、多种模型、消融、超参数、知识形式、多任务，设计全面、公平（重新运行对比方法代码）。

### 6. 主要结论与发现

- VKC‑MIR 在三个 KB‑VR 基准上均达到 **SOTA**，分别比 Prophet（GPT‑3）高 3.2/3.7/1.9 个百分点，比 VCTP（Llama2）高 4.5/9.9/3.7 个百分点。
- **VKC 形式优于文本形式**：将知识表示为图像比文本三元组带来更显著提升（表7）。
- **多图像 MLLM 优于单图像模型**，且 VKC 可普遍提升各类 MLLM 性能。
- 消融实验表明，每个阶段（场景图、外部知识、图像编辑）均贡献独特增益；逐步添加知识比一次性添加更有效。

### 7. 优点（方法/实验亮点）

- **概念创新**：首次提出“知识图像”（VKC），将知识以直观图像方式呈现，与多图像 MLLM 天然适配。
- **设计巧妙**：
  - VKC 同时包含内部（场景关系）和外部（属性/关系）知识，且任务无关、模型无关。
  - 迭代编辑策略避免了图像质量下降和语义错误。
  - 知识生成阶段引入验证器和排序器，降低幻觉，聚焦问答相关。
- **实验充分**：涵盖多种对比方法、消融、超参数、多任务场景，结果可信度高。
- **实用性**：全开源、无需重训练、计算开销小（仅 0.2 小时额外推理时间），易于部署。

### 8. 不足与局限

- **知识覆盖有限**：只能生成已在原始图像中检测到的实体的知识，无法为“未见实体”生成更深层知识。未来可引入层级计数器扩展。
- **图像编辑依赖模型能力**：SEED‑X 在复杂场景下可能产生错误（如标签重叠、关系缺失），需精细调参。
- **历史矛盾知识处理**：虽然引入了两步验证（RV‑BCK + MV‑HCK），但仅初步探索，仍可能无法完全消除时序冲突。
- **应用场景**：主要验证在单图像任务上，多图像任务（如网页、长视频）虽在 MIBench 上测试，但未构建专用基准。作者已计划构建更全面的评估平台。
- **与封闭源模型比较**：仅与 GPT‑4o 在 A‑OKVQA 上对比，未在所有数据集上系统比较；提示成本和 API 限制是原因之一。

（完）
