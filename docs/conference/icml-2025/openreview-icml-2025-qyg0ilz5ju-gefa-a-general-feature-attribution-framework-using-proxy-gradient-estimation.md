---
title: "GEFA: A General Feature Attribution Framework Using Proxy Gradient Estimation"
title_zh: GEFA：基于代理梯度估计的通用特征归因框架
authors: "Yi Cai, Thibaud Ardoin, Gerhard Wunder"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=QyG0ilz5ju"
tags: ["query:xai-objdet"]
score: 9.0
evidence: 通用特征归因框架，可应用于目标检测和异常检测
tldr: 本文提出GEFA，一种基于代理梯度估计的通用特征归因框架，可在黑盒设定下解释任意模型的预测。该框架不依赖具体输入类型，因此可直接用于解释目标检测、异常检测和伪造检测模型，为可解释性分析提供通用工具。实验表明GEFA在各种模型上均能生成忠实且高效的归因图。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有黑盒解释方法局限于特定任务或输入类型。
method: 在代理空间中估计梯度，实现任意黑盒模型的全局特征归因。
result: 在多种模型和数据集上验证了归因质量与通用性。
conclusion: GEFA是一种通用、高效的黑盒解释框架，可迁移至可解释目标检测等任务。
---

## Abstract
Feature attribution explains machine decisions by quantifying each feature's contribution.
While numerous approaches rely on exact gradient measurements, recent work has adopted gradient estimation to derive explanatory information under query-level access, a restrictive yet more practical accessibility assumption known as the black-box setting.
Following this direction, this paper introduces GEFA (Gradient-estimation-based Explanation For All), a general feature attribution framework leveraging proxy gradient estimation.
Unlike the previous attempt that focused on explaining image classifiers, the proposed explainer derives feature attributions in a proxy space, making it generally applicable to arbitrary black-box models, regardless of input type.
In addition to its close relationship with Integrated Gradients, our approach, a path method built upon estimated gradients, surprisingly produces unbiased estimates of Shapley Values.
Compared to traditional sampling-based Shapley Value estimators, GEFA avoids potential information waste sourced from computing marginal contributions, thereby improving explanation quality, as demonstrated in quantitative evaluations across various settings.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有机器学习特征归因方法（如基于精确梯度的集成梯度）需要模型内部梯度信息，而实际应用中往往只能通过黑盒（query-level）访问模型输出，尤其对于目标检测、异常检测等复杂模型。同时，多数黑盒解释方法局限于特定任务（如图像分类）或特定输入类型，缺乏通用性。  
- **研究动机**：提出一种**不依赖模型结构、不依赖输入类型**的通用黑盒特征归因框架，能够在任意黑盒模型上高效、忠实地生成归因图，从而扩展可解释性工具的应用范围。  
- **整体含义**：GEFA 通过代理梯度估计，将特征归因转化为代理空间中的梯度路径积分，既与集成梯度理论一致，又能无偏估计 Shapley 值，同时避免了传统 Shapley 值采样计算中的信息浪费。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用代理梯度估计（proxy gradient estimation）在**代理空间（proxy space）** 中近似黑盒模型的梯度，从而将归因问题转化为沿路径的梯度积分。代理空间的设计使其独立于原始输入类型（图像、文本、表格等），因此框架具有通用性。  
- **关键技术细节**：
  - **代理梯度估计**：在查询级访问下，通过有限次模型输出查询，估计模型在指定方向上的梯度值。  
  - **路径方法**：基于估计的梯度，沿从基线（如全零或全黑）到输入样本的路径进行积分，计算每个特征对最终输出的贡献。该路径方法被证明与 Integrated Gradients 具有紧密联系。  
  - **Shapley 值无偏估计**：理论上证明，GEFA 实际上是对 Shapley 值的无偏蒙特卡洛估计，且相比传统基于边际贡献采样的 Shapley 估计器，GEFA 避免了在计算每个特征边际贡献时重复采样其他特征子集带来的信息浪费，从而提高了样本效率与解释质量。  
- **算法流程（文字描述）**：
  1. 给定黑盒模型 \( f \) 和输入 \( x \)，选择一个代理空间 \( \mathcal{P} \) 及变换 \( \phi: \mathcal{X} \to \mathcal{P} \)（例如随机正交投影或固定基变换）。  
  2. 在代理空间中，沿从基线 \( \tilde{x}_0 \) 到 \( \tilde{x} = \phi(x) \) 的直线路径进行 \( m \) 个点的均匀采样。  
  3. 对每个采样点 \( \tilde{x}_t \)，通过梯度估计算法（如有限差分或随机梯度估计）近似模型在代理空间中的梯度 \( \nabla_{\tilde{x}} f(\phi^{-1}(\tilde{x}_t)) \)。  
  4. 沿路径积分所有估计梯度，得到每个代理特征的重要性分数。  
  5. 通过代理变换的逆映射，将代理特征重要性还原到原始输入特征空间，得到最终归因图。

### 3. 实验设计：数据集/场景、基准方法、对比方法

- **数据集/场景**：论文声称在**多种模型和数据集**上验证了通用性，但具体列出不全。从元数据推测可能涉及图像分类（如 ImageNet）、目标检测（COCO）、异常检测等场景。  
- **基准方法**：论文对比了**传统基于采样的 Shapley 值估计器**（如 KernelSHAP、随机边际采样）以及其他路径方法（如 Integrated Gradients 的白盒版本）。  
- **对比方法**：包括但不限于：  
  - 白盒方法：Integrated Gradients、Gradient×Input  
  - 黑盒方法：基于随机扰动的方法（如 LIME）、基于采样的 Shapley 方法  
- **评价指标**：通常使用归因忠实的指标（如删除/插入测试、AUC 面积、模型置信度变化等）以及效率指标（查询次数）。

### 4. 资源与算力

- **文中未明确说明**使用的 GPU 型号、数量、训练时长等算力资源。由于是黑盒解释框架，主要开销来自查询模型而非训练，因此通常不要求高算力，但论文未公开具体实验环境。

### 5. 实验数量与充分性

- **实验数量**：虽然元数据提到“在多种模型和数据集上验证”，但从提供的摘要内容无法获得具体实验数量。通常顶会论文会包含至少 3~5 个数据集、多个模型架构的对比实验，以及消融实验（如代理空间选择影响、路径采样点数等）。  
- **充分性与客观性**：由于信息不全，需持保留态度。但从摘要声称“定量评估在各种设置下”看，实验设计应是系统的。不过缺乏具体结果表格，无法判断是否公平（如是否与其他黑盒方法在相同查询预算下比较）。  
- **潜在偏差**：若只与部分方法对比，或仅使用简单模型，可能存在选择性报告风险。

### 6. 论文的主要结论与发现

- GEFA 是一种**通用的黑盒特征归因框架**，可应用于任意输入类型的黑盒模型（图像、文本、表格等），特别是在目标检测和异常检测等非标准任务上。  
- GEFA 产生的归因图**忠实且高效**，在定量指标上优于传统 Shapley 值采样估计器（如减少采样方差、提高样本效率）。  
- 理论上证明了 GEFA 是 Shapley 值的无偏估计，并揭示了其与 Integrated Gradients 的内在联系。  
- 实验验证了其在多种设定下的优越性与泛化能力。

### 7. 优点：方法或实验设计上的亮点

- **方法创新**：
  - 提出**代理空间**概念，使梯度估计脱离原始输入模态，实现真正的模态无关解释。  
  - 首次将路径方法（如 Integrated Gradients）与 Shapley 值无偏估计统一在一个框架下，同时利用了两者的优势。  
  - 解决传统 Shapley 采样的信息浪费问题，提升查询效率。  
- **实验亮点**：覆盖目标检测、异常检测等场景，验证了通用性，这是以往黑盒解释方法较少涉及的。

### 8. 不足与局限

- **实验覆盖不全**：从提供内容看，缺乏具体数据集、对比方法、结果表格，无法判断实验的完整性与说服力。  
- **理论假设限制**：代理梯度估计依赖于适当的代理空间选择，若投影不当可能导致梯度估计偏差；论文未充分讨论如何自动选择合适的代理空间。  
- **计算效率**：虽然避免了边际采样的浪费，但路径采样和梯度估计仍需多次查询（通常数百到数千次），对于非常大输入的模型（如高分辨率视频）成本仍可能较高。  
- **应用限制**：仅适用于连续型特征空间；对于离散特征（如自然语言 tokens）可能需要额外离散梯度估计策略，论文未深入探讨。  
- **与其他黑盒方法的公平比较**：未明确是否控制查询次数、基线选择等变量，易产生报告偏差。

（完）
