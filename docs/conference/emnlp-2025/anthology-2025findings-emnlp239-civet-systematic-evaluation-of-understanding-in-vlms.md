---
title: "CIVET: Systematic Evaluation of Understanding in VLMs"
title_zh: CIVET：视觉语言模型理解的系统评估
authors: "Massimo Rizzoli, Simone Alghisi, Olha Khomyn, Gabriel Roccabruna, Seyed Mahed Mousavi, Giuseppe Riccardi"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.239.pdf"
tags: ["query:xai-objdet"]
score: 8.0
evidence: 以可解释方式系统评估VLM对物体属性和关系的理解
tldr: 该论文针对视觉语言模型（VLM）对场景结构和语义理解不足的问题，提出了CIVET评估框架。CIVET通过控制刺激物，以可解释的方式系统评估VLM对物体属性和关系的理解，避免了标注噪声和数据集偏差。在五个先进VLM上的评估揭示了模型在物体理解方面的不足，为可解释目标检测和场景理解提供了标准化评估工具。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 734, \"height\": 1035, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1222, \"height\": 639, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1588, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 667, \"height\": 665, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1398, \"height\": 731, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 745, \"height\": 737, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1645, \"height\": 864, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 568, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025.findings-emnlp.239/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1616, \"height\": 887, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 548, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 582, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 780, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 722, \"height\": 479, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 691, \"height\": 424, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 678, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 959, \"height\": 725, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 777, \"height\": 726, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 928, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 959, \"height\": 784, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1107, \"height\": 597, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 813, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 558, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1407, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1260, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 766, \"height\": 782, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025.findings-emnlp.239/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 725, \"height\": 420, \"label\": \"Table\"}]"
motivation: 现有评估缺乏对VLM物体属性和关系理解的标准化可解释评估框架。
method: 提出CIVET框架，通过控制刺激物和统计检验系统评估VLM的物体理解能力。
result: 在五个VLM上揭示了物体关系理解的缺陷，验证了框架的有效性。
conclusion: CIVET为可解释目标检测和VLM场景理解提供了可复用的评估方法论。
---

## Abstract
While Vision-Language Models (VLMs) have achieved competitive performance in various tasks, their comprehension of the underlying structure and semantics of a scene remains understudied. To investigate the understanding of VLMs, we study their capability regarding object properties and relations in a controlled and interpretable manner. To this scope, we introduce CIVET, a novel and extensible framework for systemati C evaluat I on V ia controll E d s T imuli. CIVET addresses the lack of standardized systematic evaluation for assessing VLMs’ understanding, enabling researchers to test hypotheses with statistical rigor. With CIVET, we evaluate five state-of-the-art VLMs on exhaustive sets of stimuli, free from annotation noise, dataset-specific biases, and uncontrolled scene complexity. Our findings reveal that 1) current VLMs can accurately recognize only a limited set of basic object properties; 2) their performance heavily depends on the position of the object in the scene; 3) they struggle to understand basic relations among objects. Furthermore, a comparative evaluation with human annotators reveals that VLMs still fall short of achieving human-level accuracy.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

尽管视觉语言模型（VLM）在多项任务中表现优异，但它们对场景的底层结构和语义的理解能力仍未被充分研究。现有评估基准受限于标注噪声、数据集偏差（如物体多出现在中心）、场景复杂度不可控等问题，使得性能提升可能源于统计捷径而非真正的理解。为了填补这一空白，该论文提出**CIVET**框架，旨在通过完全受控的刺激物（Stimuli）对VLM进行系统性、可解释的评估，从而回答三个研究问题：  
- **RQ1**：VLM能否准确识别基本物体属性（形状、颜色、光泽等）？  
- **RQ2**：性能是否对物体位置变化鲁棒？  
- **RQ3**：VLM能否识别物体间的基本关系（相对位置、相对距离、相对大小）？

## 2. 方法论

### 核心思想
CIVET 通过**确定性地生成**视觉场景和对应的自然语言问题，确保每个刺激物都带有精确的结构化表示，从而消除标注错误、位置偏置和场景复杂度等混淆因素。评估时，固定待测方面（如某一属性），在所有其他变量（如位置、颜色）的组合上边缘化，以得到统计无偏的性能度量。

### 关键技术细节
- **世界（World）定义**：每个世界是一个由对象及其属性（形状、颜色、光泽）和关系构成的集合。对象属性值来自预设集合（如4种形状、6种颜色、3种光泽值）。
- **场景生成**：所有场景均为 **9×9 网格**，对象放置在特定格点。生成时保证每个位置、每个属性值组合均匀出现。
- **问题模板**：封闭式问题，附上“Choose from [选项]”，将可能答案作为选项。选项顺序均匀随机洗牌以避免顺序偏置。
- **模型输出控制**：添加指令“Answer with as few words as possible.”，将输出长度限制为1~2个词，便于精确匹配。
- **评估协议**：针对每个研究问题，固定待测方面，生成所有可能配置的刺激物，然后平均计算准确率或F1分数。

### 实验设计中的主要设置
| 实验名称 | 场景描述 | 刺激物数量（场景数） |
|----------|----------|---------------------|
| Single Object | 单个合成物体，81个位置 × (4形状×6颜色×3光泽) = 5832 | 5832 |
| Single Object w. COCO | 单个真实物体（长颈鹿、大象、斑马）从COCO中裁剪，81个位置 × 3类别 = 243 | 243 |
| Relative Position | 两个黄色物体（星形、三角形），所有位置组合（81×80=6480） | 6480 |
| Relative Size | 四个黄色物体（大小不同），所有位置组合（81×80×选择两个物体）≈25920 | 25920 |
| Relative Distance | 三个黄色物体，每个物体放置于9个分区之一，分区内随机格点采样，总配置数4374 | 4374 |

## 3. 实验设计：数据集、基准与对比方法

### 数据集 / 场景
- **合成场景**：由CIVET生成的网格图，背景黑色，物体为基本几何形状（方形、圆形、三角形、星形），颜色（红、绿、蓝、黄、品红、青），光泽（无、哑光、亮光）。
- **真实场景**：从MS COCO图像中提取的单个物体（长颈鹿、大象、斑马），经CLIP筛选和人工确认。

### Benchmark
- **随机基线**：根据问题选项数计算随机猜测准确率。
- **人类表现**：通过Amazon Mechanical Turk招募124人，对81个“黄色星”位置场景进行标注（每个场景8人标注），计算准确率和Fleiss’ κ（0.61，中等一致性）。

### 对比方法
- **LLaVA-NeXT 7B / 13B**：使用CLIP视觉编码器 + Vicuna LLM，仅训练投影层。
- **Molmo 7B-O**：使用CLIP视觉编码器 + LLaMA，全模型微调。
- **Qwen2-VL 7B**：原生支持任意分辨率，联合训练视觉编码器和LLM。
- **CLIP ViT-L/14-336px**：直接作为分类器，将图像与选项文本编码后选相似度最高者。

## 4. 资源与算力

文中明确提到：
- 大部分实验使用 **1张 NVIDIA A100 (40 GiB)**。
- Qwen2-VL-7B 在 1344×1344 图像时需要 **1张 NVIDIA A100 (80 GiB)**。
- 所有评估均为推理（生成回答），未提及训练资源或时长。

## 5. 实验数量与充分性

### 实验数量
- 共执行5大实验（单物体属性、COCO属性、相对位置、相对大小、相对距离），每个实验均包含数千至数万独立场景。
- 另外进行了**图像尺寸消融**（336×336, 672×672, 1344×1344）和**物体尺寸消融**（常规 vs 小尺度1/4）。
- 进行了**人类评价**（81个场景，每个8人标注）。

### 充分性与公平性
- **充分**：覆盖了属性识别、位置鲁棒性、多种关系类型（位置、距离、大小），并且同时使用合成和真实物体。
- **公平**：
  - 所有选项均匀随机排序，避免顺序偏置。
  - 统一使用“Answer with as few words as possible.”促使模型输出简洁，可用于精确匹配（表10显示大部分输出长度1~2词）。
  - 多次实验验证不同图像尺寸、物体尺寸的影响，并选择最佳设置（合成用672×672，COCO用1344×1344）进行主要报告。
  - 人类评价采用多数投票，并与模型在完全相同刺激物上比较。

## 6. 主要结论与发现

1. **属性识别有限**：VLM对形状识别较好（≥95%），但对颜色（尤其青色）和光泽（最佳仅64%）识别较差。
2. **性能严重依赖物体位置**：准确率在网格中非均匀分布（如LLaVA-NeXT在底部区域更好，顶部角落更差；Molmo在右上角表现差）。图2、3、4、5清晰展示了位置依赖性。
3. **基本关系理解困难**：
   - 相对位置：最高46%（Qwen2-VL），特别是同排/同列关系（F1仅18.5%）。
   - 相对距离：LLaVA-NeXT对三角形作为指定物体时准确率极低（F1 10%~14%）。
   - 相对大小：仅Qwen2-VL和CLIP优于随机，其他模型从未正确预测“相同”。
4. **落后于人类**：人类在绝对位置任务上准确率73%，所有VLM均低于此值；人类分配位置时水平中心区域更窄，而模型各有偏差。
5. **增加文本解码器规模不总有益**：LLaVA-NeXT 13B在颜色和位置任务上反而不如7B版本。

## 7. 优点

- **系统性与可控性**：CIVET实现了对场景中所有变量的精确控制，彻底消除了数据偏置和标注噪声，是目前最系统的VLM理解评估工具。
- **统计严谨**：通过边缘化其他变量，获得每个方面的无偏性能估计，支持假设检验。
- **开放与可扩展**：框架和所有材料已开源，鼓励社区扩展至更多属性和关系。
- **人类基准**：提供同条件人工比较，明确揭示VLM与人类差距。
- **全面消融**：包括图像尺寸、物体尺寸、物体类别、位置等多种因素，实验设计严密。

## 8. 不足与局限

- **模型规模受限**：仅测试7B~13B，未评估更大模型（如34B、70B）。
- **物体尺寸变化有限**：仅考虑常规和1/4两种，更丰富的尺寸粒度可能带来不同结论。
- **关系类型覆盖有限**：仅测试位置、距离、大小，未包括遮挡、碰撞、功能性关系等。
- **人类标注者差异**：不同Mechanical Turk工人可能有不同理解，虽然后续质量控制，但数据规模有限（仅81个场景）。
- **未讨论训练数据泄露**：虽然CIVET场景是合成的，但VLM可能在预训练中见过类似网格图，文中未完全排除此风险。
- **计算资源限制**：无法进行更大规模的模型推理或更多重复实验。

（完）
