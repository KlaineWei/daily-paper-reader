---
title: Identity-Aware Vision-Language Model for Explainable Face Forgery Detection
title_zh: 身份感知视觉语言模型用于可解释人脸伪造检测
authors: "Junhao Xu, Jingjing Chen, Yang Jiao, Jiacheng Zhang, Zhiyu Tan, Hao Li, Yu-Gang Jiang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38108/42070"
tags: ["query:xai-objdet"]
score: 10.0
evidence: 身份感知视觉语言模型实现可解释人脸伪造检测
tldr: 针对现有伪造检测依赖低级视觉线索、无法捕捉身份语义不一致的问题，本文提出身份感知视觉语言模型，利用个性化VLM检测语义异常并生成自然语言解释。实验表明该方法在跨域和未知伪造类型上表现优异，同时提供可解释性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38108/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 828, \"height\": 681}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38108/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1187, \"height\": 645}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38108/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 945}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 777, \"height\": 684}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 887, \"height\": 527}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 877, \"height\": 288}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 761, \"height\": 312}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38108/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 721, \"height\": 515}]"
motivation: 现有伪造检测方法忽略身份语义一致性且对未知伪造类型泛化差。
method: 提出个性化VLM，结合身份信息进行视觉语言对齐，检测语义不一致并生成解释。
result: 在多个伪造检测基准上，方法在准确率和可解释性上均显著优于已有技术。
conclusion: 该工作将身份语义纳入伪造检测，为可解释AI媒体取证提供了新思路。
---

## Abstract
Recent advances in generative artificial intelligence have enabled the creation of highly realistic image forgeries, raising significant concerns about digital media authenticity. While existing detection methods demonstrate promising results on benchmark datasets, they face critical limitations in real-world applications. First, existing detectors typically fail to detect semantic inconsistencies with the person’s identity, such as implausible behaviors or incompatible environmental contexts in given images. Second, these methods rely heavily on low-level visual cues, making them effective for known forgeries but less reliable against new or unseen manipulation techniques. To address these challenges, we present a novel personalized vision-language model (VLM) that integrates low-level visual artifact analysis and high-level semantic inconsistency detection. Unlike previous VLM-based methods, our approach avoids resource-intensive supervised fine-tuning that often struggles to preserve distinct identity characteristics. Instead, we employ a lightweight method that dynamically encodes identity-specific information into specialized identifier tokens. This design enables the model to learn distinct identity characteristics while maintaining robust generalization capabilities. We further enhance detection capabilities through a lightweight detection adapter that extracts fine-grained information from shallow features of the vision encoder, preserving critical low-level evidence. Comprehensive experiments demonstrate that our approach achieves 94.25% accuracy and 94.08% F1 score, outperforming both traditional forgery detectors and general VLMs while requiring only 10 extra tokens.

---

## 论文详细总结（自动生成）

# 中文总结：Identity-Aware Vision-Language Model for Explainable Face Forgery Detection

## 1. 核心问题与研究动机

### 背景与问题
- 生成式AI（如GAN、扩散模型）可制造高度逼真的伪造人脸图像，对数字媒体真实性构成严峻威胁。
- 现有伪造检测方法存在两大关键局限：  
  - **忽略身份语义一致性**：无法检测到与目标身份不符的行为、着装、环境等语义异常（如某人出现在不可能的场景中）。  
  - **过度依赖低级视觉线索**：仅能识别已知的伪造模式，对新型/未知伪造技术泛化能力差。
- 现有VLM方法（如FFAA、GPT-4V）要么依赖人工标注进行微调（易丢失身份特征），要么缺乏针对身份不一致的专门设计。

### 整体目标
提出一个**个性化的视觉语言模型（VLM）**，能够同时分析低级伪造痕迹和高级语义不一致性，并生成可解释的自然语言理由。

## 2. 方法论

### 核心思想
- 利用**少量真实参考图像**为目标个体编码身份先验，注入到VLM中，通过**两阶段轻量训练**实现身份感知的伪造检测。
- 设计两种特殊标识符 token：`<id_a>`（外观）和 `<id_b>`（行为），分别捕获外观属性与行为模式。
- 每个标识符对应 **N=4个可学习的软token**，总共仅10个额外token。

### 关键技术细节
1. **个性化身份先验注入**  
   - 使用参考图像训练两类任务：外观识别、行为识别。  
   - 训练参数仅包括标识符token、软token和LM head的新增行（权重`W_new`）。  
   - 对比全模型微调，此方法保留了VLM的原始语义能力，同时高效记忆个体特征。

2. **检测适配器（Detection Adapter）**  
   - 从VLM视觉编码器的**浅层特征**中提取低级视觉线索（如压缩伪影、噪声模式）。  
   - 通过轻量投影层`Proj`将其转换为视觉token，与标准视觉token拼接后送入语言模型。  
   - 优势：不参调视觉编码器，保留语义信息，增强对伪造痕迹的敏感性。

3. **两阶段训练**  
   - **Stage 1**：训练检测适配器，使用通用真假图像（无需身份信息），二分类任务（Yes/No）。  
   - **Stage 2**：个性化先验训练，使用目标个体的真实图像和三种方法生成的伪造图（SimSwap、PhotoMaker），训练外观/行为识别任务。  
   - 损失函数：`L_adapter = CE(VLM, y)`，`L_personalization = L_appearance + L_behavior`。

## 3. 实验设计

### 数据集
- **自建IDImage数据集**：包含20位政治和娱乐界公众人物，每人约329张真实照片 + 780张伪造图（训练集） + 50张真实+50张伪造（测试集）。  
- 伪造方法：  
  - 训练集：SimSwap（GAN）、PhotoMaker（扩散）。  
  - 测试集：Roop（GAN）、StoryMaker（扩散）、PuLID（扩散）——**与训练集完全不重叠**，用于评估泛化性。  
- 额外数据规模实验：选取5%~100%训练数据量进行对比。

### 对比方法
- **传统伪造检测器**：Meso4、Xception、Recce、R-MFDN、UCF、RAIRNet、NPR、ESSP。  
- **通用VLM**：GPT-4o、Qwen2.5-VL、LLaVA-1.6-13B。  
- **专用VLM**：FFAA（微调）、Yo’LLaVA（个性化）、LLaVA-SFT（监督微调）。  
- **个性化VLM对比**：对GPT-4o和Qwen2.5-VL分别注入三种先验（文本描述、参考图像、两者结合），LLaVA仅用文本描述。

### 评价指标
- 准确率（ACC）、精确率、召回率、F1分数（将真实图像为正样本，伪造图为负样本）。

## 4. 资源与算力

- **基础模型**：LLaVA-1.6-13B。  
- **训练硬件**：2张NVIDIA A100 GPU。  
- **训练时间**：每个身份仅训练1个epoch，约**20分钟**。  
- 总参数极少：仅10个额外可学习token，无需全模型微调。

## 5. 实验充分性与公平性

### 实验数量
- **主对比实验**：与13种方法对比（表1）。  
- **个性化VLM对比**：与4种VLM在4种注入方式下对比（表2）。  
- **消融实验**（表3）：  
  - 移除检测适配器  
  - 仅使用单个标识符（<id_a>或<id_b>）  
  - 使用统一标识符（不分离外观/行为）  
  - 移除Chain-of-Thought（CoT）解释  
- **训练数据规模影响**（表4）：5%~100%数据量下的性能。  
- **鲁棒性测试**（表5）：JPEG压缩（QF=25）、高斯模糊（核21×21，sigma=8.0），对比RAIRNet、R-MFDN、GPT-4o。

### 公平性分析
- 所有基线方法均使用相同训练数据（或根据各自要求设置）。  
- 传统检测器采用监督训练，VLM采用零样本或微调，对比条件较合理。  
- 但传统检测器未使用身份先验，而本方法使用了，公平性略有不足但仍具可比性（论文给出了R-MFDN等身份辅助方法的结果）。

## 6. 主要结论与发现

- **性能优势**：本方法在IDImage测试集上达到**94.25% ACC**和**94.08% F1**，显著优于所有传统方法和VLM方法（最佳传统ESSP为89.08% ACC，最佳VLM GPT-4o为83.03%）。  
- **泛化能力**：测试集使用完全不同的伪造方法，证明有效跨域检测。  
- **参数效率**：仅10个额外token即可实现高性能，优于需要大量文本描述或参考图像的其他个性化VLM。  
- **解耦标识符更优**：分离外观与行为先验（<id_a> + <id_b>）优于统一标识符。  
- **链式思维（CoT）有效**：带有解释的训练比仅输出二分类效果更好（F1从87.26%提升至94.08%）。  
- **数据效率**：即使仅用10%训练数据（约100张/人），F1仍达81.73%；100%数据时达94.08%。

## 7. 优点

### 方法亮点
- **身份语义对齐**：首次将个性化VLM应用于人脸伪造检测，利用高级语义一致性而非仅低级伪影。  
- **极低参数代价**：仅10个额外token，无需重训整个模型，可快速适配新身份。  
- **可解释性**：模型能生成自然语言解释（如“头发异常长而直，而<id_a>通常有短黑发”），提升可信度。  
- **多级特征融合**：检测适配器保留低级视觉线索，同时VLM保持高级语义分析能力。  
- **训练高效**：单身份20分钟，无需大量人工标注（仅需参考图像和伪造图）。

### 实验亮点
- 测试集伪造方法完全不同于训练集，模拟真实威胁场景。  
- 鲁棒性测试覆盖常见扰动（压缩、模糊），性能下降幅度小。  
- 消融实验覆盖多个关键模块，验证设计合理性。

## 8. 不足与局限

### 实验局限性
- **数据集规模与多样性有限**：仅20个公众人物（政治/娱乐），缺乏种族、年龄、国别等多样性，可能限制了泛化结论。  
- **身份获取成本**：需要每个目标个体的少量真实参考图像（至少约100张），在真实应用中（如普通用户）难以满足。  
- **仅考虑图像模态**：未涉及视频帧间时序一致性检测（该任务可能更易暴露伪造）。  
- **未见身份的情况**：论文未测试当目标身份不在训练集中时的零样本检测能力（需完全依赖通用语义）。  
- **类型覆盖不全**：测试集仅包括五种伪造方法（GAN+扩散），可能遗漏其他常见手法（如图像拼接、重涂等）。

### 潜在偏差与风险
- **公共人物的局限性**：训练数据中的公共人物在媒体中出现频次高，模型可能过度拟合常见行为模式，对普通人身份检测效果未知。  
- **CoT解释可能不精确**：虽然提高了检测性能，但生成的解释可能含有幻觉或错误推理，在司法场景需谨慎。  
- **计算资源假设**：训练需要2×A100 GPU，对中小团队门槛较高；但推理阶段仅需单次前向。  
- **对抗攻击鲁棒性未测试**：论文仅测试了常规扰动，未评估针对模型的对抗样本（如故意制造符合身份的伪造图）。

（完）
