---
title: Learning Real Facial Concepts for Independent Deepfake Detection
title_zh: 学习真实人脸概念以实现独立深度伪造检测
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0177.pdf"
tags: ["query:xai-objdet"]
score: 6.0
evidence: 通过学习真实人脸概念进行深度伪造检测
tldr: 该论文面向深度伪造检测任务，提出通过学习真实人脸的概念（如肤色、纹理等）来区分真假。方法首先从真实人脸中提取可解释的概念特征，然后利用这些特征训练检测器。实验表明，基于概念的检测器不仅性能优异，还能提供直观的视觉解释。该工作为可解释伪造检测提供了新途径。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-177/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 890, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-177/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-177/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 593, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-177/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 837, \"height\": 387, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-177/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 845, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-177/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 775, \"height\": 1239, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-177/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 881, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-177/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1620, \"height\": 553, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-177/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 850, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-177/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 855, \"height\": 221, \"label\": \"Table\"}]"
motivation: 现有深度伪造检测方法缺乏可解释性，难以理解判决依据。
method: 学习真实人脸的概念特征，并基于概念进行检测。
result: 在多个伪造数据集上检测精度高，且可解释性强。
conclusion: 利用真实概念可同时提升检测性能和可解释性。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有深度伪造检测模型在面对未见过的数据集时泛化能力差，常将真实样本误判为伪造。作者认为根本原因在于模型过度依赖伪造伪影（forgery artifacts），而对真实人脸的概念理解不足，导致决策失衡。
- **研究动机**：真实人脸特征在训练集中分布过于集中，而伪造特征分布较散，模型容易过拟合真实样本的共性，忽视真实人脸多样性。此外，传统二分类器的“此消彼长”逻辑使模型一旦检测到伪造伪影就直接判定为假，缺乏对真实人脸的独立判定能力。
- **整体含义**：提出通过学习更全面的真实人脸概念，并让模型同时基于“真实概念”和“伪造伪影”独立做出判决，从而提升跨数据集的泛化能力。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：构建两个模块——**RealC²（真实概念捕获模块）** 和 **IDC（独立双决策分类器）**。前者通过多原型记忆机制学习真实人脸的多类原型；后者将传统二分类器扩展为独立双决策，并加入正则项，使模型能基于真实概念而非仅依赖伪造伪影做出判断。
- **关键技术细节**：
  - **RealC²模块**：
    - 初始化K个真实原型向量 \( \mathcal{M}_R = \{m_1,...,m_K\} \)。
    - 每次迭代中，计算每个原型与批量中真实特征的相似度，得到垂直/水平归一化的匹配权重 \( w_{i,j} \) 和 \( v_{i,j} \)。
    - 每个样本被分配到最近的原型，然后原型通过加权和更新：\( m_k \leftarrow \text{Normalize}(m_k + \sum_{f_j \in U_k} v'_{k,j} f_j) \)。
    - 设计了两个损失函数：
      - **原型区分损失** \( \mathcal{L}_{\text{Distinction}} \)：拉近真实特征与其最近原型及均值原型，推远与伪造原型及均值伪造原型的距离。
      - **原型多样性损失** \( \mathcal{L}_{\text{Diversity}} \)：鼓励真实特征与第二近原型保持一定距离（margin α），防止原型坍缩。
  - **IDC模块**：
    - 将二分类器输出维度扩展为4维：\( \hat{f}_j = [\hat{f}_j^0, \hat{f}_j^1, \hat{f}_j^2, \hat{f}_j^3] \)，分别代表属于真实、伪造的概率以及两个辅助分量。
    - 新增正则项 \( R \)：对于真实样本，使伪造概率 \( \hat{f}_j^1 \) 向辅助分量 \( \hat{f}_j^3 \) 接近；对于伪造样本，使真实概率 \( \hat{f}_j^0 \) 向辅助分量 \( \hat{f}_j^2 \) 接近。从而削弱“正确概率上升则错误概率必然下降”的依赖关系。
- **算法流程**：
  1. 使用特征提取器 \( E(\cdot) \) 从输入图像得到特征图，经池化展平得到特征向量 \( F \)。
  2. 利用RealC²模块更新真实原型，并计算 \( \mathcal{L}_{\text{Distinction}} \) 和 \( \mathcal{L}_{\text{Diversity}} \)。
  3. 通过IDC分类器得到4维输出，计算交叉熵损失 \( \mathcal{L}_{\text{CE}} \) 和正则项 \( R \)。
  4. 总损失 \( \mathcal{L}_{\text{total}} = \mathcal{L}_{\text{CE}} + \lambda_1 \mathcal{L}_{\text{Diversity}} + \lambda_2 \mathcal{L}_{\text{Distinction}} + \lambda_3 R \) 进行端到端优化。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **训练数据集**：FF++（FaceForensics++），包含1000个真实视频和5种伪造方法共6000个视频。
- **测试数据集**：五个广泛使用的跨数据集基准：Celeb-DF、DFD、DFDC、DFDCp、UADFV。
- **评估指标**：AUC（ROC曲线下面积）。
- **对比方法**：包括EfficientNet、Face X-ray、CORE、RECCE、SBI、UCF、FoCus、Qiao et al.、GRU、ProDet等10种SoTA方法。部分方法作者自行复现（标注‡），其他引用原论文结果。

## 4. 资源与算力

- 论文在“Implementation”部分明确提到：使用单张RTX 3090 GPU，batch size为16。未提及训练时长或使用多少张GPU并行。其他算力信息未提供。

## 5. 实验数量与充分性

- **主要实验**：
  - 跨数据集测试：在5个测试集上对比10种方法（表1）。
  - 不同骨干网络实验：使用Xception、ViT-L-32、ViT-B-16三种骨干，对比有无RealID（表2）。
  - 消融实验：分别去除RealC²、IDC模块，在4个测试集上比较（表3）。
  - 损失函数消融：对比有无 \( \mathcal{L}_{\text{Diversity}} \) 和 \( \mathcal{L}_{\text{Distinction}} \)（表4）。
  - 超参数分析：对三个λ参数在[0,2]范围内进行网格搜索，并在Celeb-DF和DFDC上展示性能变化（图4）。
  - 定性分析：热力图对比（图5）、t-SNE可视化（图6）。
- **充分性评价**：实验设计较为全面，覆盖了主要数据集、多种骨干、关键模块及损失函数的消融，以及超参数敏感性。但未做跨训练数据域的验证（例如换用其他训练集），也未报告统计显著性或多次运行的标准差。整体上实验充分且客观，对比公平（均基于FF++训练）。

## 6. 论文的主要结论与发现

- 所提出的RealID方法在五个跨数据集测试中平均AUC达到91.06%，比当前最好方法SBI（89.32%）提升1.74%，显著优于其他方法。
- RealID能有效减少真实样本被误判为伪造的情况（t-SNE图显示红色大圆点（误判真实样本）大幅减少）。
- 两个模块RealC²和IDC均贡献显著，且两者组合效果最佳（在Celeb-DF上AUC从64.59%提升至95.16%）。
- 原型区分损失 \( \mathcal{L}_{\text{Distinction}} \) 比多样性损失 \( \mathcal{L}_{\text{Diversity}} \) 更重要，但两者结合能取得最好效果。
- 方法在不同骨干网络（Xception、ViT）上均有效，表明通用性强。

## 7. 优点

- **创新性**：首次系统性地针对“真实人脸概念”学习设计专门模块，而不是单纯增强伪造特征捕获，视角独特。
- **模块化设计**：RealC²和IDC可即插即用，不改变主干网络结构，易于集成。
- **实验验证充分**：在多个数据集、多种骨干、多项消融实验上验证，定性定量结合，结论可靠。
- **问题分析深入**：明确指出模型倾向于将真实样本误判为伪造的根本原因（真实特征分布窄、分类器依赖伪造伪影），并针对性地提出解决方案。

## 8. 不足与局限

- **实验覆盖**：未在更大规模或更多样化的训练集（如KoDF、DF-Platter）上验证跨数据域泛化，仅依赖FF++训练。此外，未评估在低质量视频或压缩场景下的表现。
- **计算开销**：Multi-Real Memory需要维护多个原型并计算大量相似度，可能增加存储和计算成本，论文未提供速度或参数量对比。
- **超参数敏感**：从图4可见，λ值超过一定阈值后性能急剧下降，实际应用中需要仔细调参，泛化到新场景可能需重新调整。
- **偏差风险**：训练集FF++中真实样本相对单一（YouTube视频），可能无法覆盖真实世界中的所有真实人脸分布，导致所学“真实概念”仍有偏。
- **仅涉及图像级检测**：未考虑视频时序信息或音频模态，而现代深度伪造常伴随多模态特征。
- **可复现性**：虽然提供了超参数设置，但未公开代码或预训练模型（论文未提及开源），可能限制后续研究。

（完）
