---
title: A Symbolic Adversarial Learning Framework for Evolving Fake News Generation and Detection
title_zh: 一种用于进化式假新闻生成与检测的符号对抗学习框架
authors: "Chong Tian, Qirong Ho, Xiuying Chen"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.619.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 检测代理使用结构化辩论识别逻辑和事实缺陷，提供可解释的检测依据
tldr: 针对大规模语言模型带来的日益复杂的假新闻生成风险，论文提出符号对抗学习框架SALF。该框架引入生成代理和检测代理的对抗训练，其中检测代理通过结构化辩论识别逻辑和事实缺陷，从而实现可解释的假新闻检测。实验表明该方法能有效应对动态演变的假新闻。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.619/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 802, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.619/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1630, \"height\": 807, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025.emnlp-main.619/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 761, \"height\": 392, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 757, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1661, \"height\": 631, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 761, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1664, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 737, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 682, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1620, \"height\": 754, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025.emnlp-main.619/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 887, \"height\": 1840, \"label\": \"Table\"}]"
motivation: 现有假新闻检测方法难以应对动态演变的假新闻，且缺乏可解释性。
method: 提出符号对抗学习框架，通过代理符号学习优化过程，检测代理利用结构化辩论进行可解释检测。
result: 在动态假新闻生成环境下，检测性能优于基线方法，并提供了可解释的检测依据。
conclusion: 所提框架兼具检测准确性和可解释性，为假新闻检测提供了新范式。
---

## Abstract
Rapid LLM advancements heighten fake news risks by enabling the automatic generation of increasingly sophisticated misinformation. Previous detection methods, including fine-tuned small models or LLM-based detectors, often struggle with its dynamically evolving nature. In this work, we propose a novel framework called the Symbolic Adversarial Learning Framework (SALF), which implements an adversarial training paradigm by an agent symbolic learning optimization process, rather than relying on numerical updates. SALF introduces a paradigm where the generation agent crafts deceptive narratives, and the detection agent uses structured debates to identify logical and factual flaws for detection, and they iteratively refine themselves through such adversarial interactions. Unlike traditional neural updates, we represent agents using agent symbolic learning, where learnable weights are defined by agent prompts, and simulate back-propagation and gradient descent by operating on natural language representations of weights, loss, and gradients. Experiments on two multilingual benchmark datasets demonstrate SALF’s effectiveness, showing it generates sophisticated fake news that degrades state-of-the-art detection performance by up to 53.4% in Chinese and 34.2% in English on average. SALF also refines detectors, improving detection of refined content by up to 7.7%. We hope our work inspires further exploration into more robust, adaptable fake news detection systems.

---

## 论文详细总结（自动生成）

# 论文总结：A Symbolic Adversarial Learning Framework for Evolving Fake News Generation and Detection

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：大规模语言模型（LLM）的快速发展显著降低了生成复杂假新闻的门槛，使得假新闻日益逼真且动态演变。而现有的检测方法（包括微调的小模型和基于LLM的检测器）往往依赖特定时段的数据或静态提示，难以应对这种不断进化的假新闻。
- **整体含义**：本文提出了一种**符号对抗学习框架（SALF）**，通过生成代理与检测代理之间的对抗训练，让检测器能够动态适应新出现的假新闻策略，同时整个过程具有可解释性（通过自然语言形式的符号损失和梯度），为假新闻检测提供了一种新的自适应范式。

## 2. 方法论：核心思想、关键技术细节、算法流程

- **核心思想**：借鉴生成对抗网络（GAN）的对抗概念，但将数值更新替换为**代理符号学习**。生成代理和检测代理的“权重”由自然语言提示（prompt）表示，通过模拟反向传播和梯度下降（使用自然语言形式的损失、梯度和参数更新）进行迭代优化。
- **关键技术细节**：
  - **生成代理**：根据当前提示θ_G对假新闻f进行改写，生成更逼真、更难被检测的版本f'。
  - **检测代理**：采用**结构化辩论**机制，包括三个辩论者（正反双方）进行开场陈述、提问与反驳、结束陈述三个阶段，最后由法官（Judge）评估辩论记录并输出检测结果J（1表示成功检测为假新闻，0表示漏检）。
  - **生成代理优化**（每轮执行）：
    1. **符号损失**：由LLM分析假新闻f和辩论记录R，输出自然语言描述的弱点（Lsym）。
    2. **优化方向**：另一LLM分析Lsym和当前提示θ_G，生成改进方向（∇sym）。
    3. **提示更新**：LLM根据∇sym更新θ_G为θ'_G。
    4. **生成新内容**：使用θ'_G生成新的假新闻f'。
  - **检测代理优化**（仅在漏检时执行）：将生成代理的策略（提取自θ_G的关键部分）融入反驳方代理的提示中，增强其针对该类欺骗策略的警惕性。
- **算法流程**（Algorithm 1）：
  - 初始化生成器和检测器的提示。
  - 循环直到收敛或最大迭代次数T：
    1. 生成器根据当前提示生成新的假新闻。
    2. 检测器执行辩论并得到判决J。
    3. 若J=0（漏检），则更新检测器提示（融入生成策略）。
    4. 计算生成器的符号损失和梯度，更新生成器提示。
  - 收敛条件：生成器和检测器的奖励函数（Reward_G和Reward_D）变化小于阈值ε（如0.05），或达到预设迭代次数。

## 3. 实验设计

- **数据集**：
  - **Weibo21**：中文微博平台大型假新闻检测基准。
  - **GossipCop**：英文名人八卦领域假新闻数据集。
- **基准方法（Baselines）**：
  - **LLM-only**：GPT-4o mini、DeepSeek V3（直接用于检测）。
  - **SLM-only**：ENDEF（基于因果学习的小模型实体去偏框架）。
  - **SLM+LLM**：ARG和ARG-D（ARG集成LLM和SLM，ARG-D是蒸馏版本）。
- **评估指标**：Accuracy、Macro F1、F1_real（真实新闻检测能力）、F1_fake（假新闻检测能力），重点关注F1_fake。
- **实现细节**：使用GPT-4o-mini-2024-07-18进行辩论和符号优化，DeepSeek V3用于假新闻生成；所有LLM通过API调用。

## 4. 资源与算力

- 文中未明确说明使用的GPU型号、数量或训练时长。
- 提到每个样本每次迭代平均消耗约4000 tokens（GossipCop约4115 tokens，Weibo21约4013 tokens），并声称相比其他多代理框架更高效（节省2-5倍tokens）。
- 整体计算成本较低，属于黑盒API调用，无需本地训练大规模模型。

## 5. 实验数量与充分性

- **主实验**：在Weibo21和GossipCop上分别测试了5种基线方法在原始假新闻和SALF精炼后假新闻上的表现（共10组对比，见表1）。
- **检测器优化实验**：比较了原始辩论检测器与SALF精炼检测器在首轮精炼假新闻上的表现（两个数据集，表2）。
- **消融实验**：通过对比“原始检测”与“SALF精炼后检测”隔离生成器贡献；通过对比“辩论检测器”与“SALF精炼检测器”隔离检测器贡献。
- **人类评估**：每个数据集随机选取100个精炼假新闻样本和100个真实新闻样本，由评估者判断真假（表4）。
- **收敛分析**：进行了第二轮优化，证明效果继续提升但边际收益递减（表5），并计算了Reward_G等指标（附录E）。
- **案例研究**：一个英文案例（表3）和一个失败案例（附录D）。
- **充分性评价**：实验覆盖了两种语言、多种基线模型、消融、人类评估和收敛分析，较为全面，但人类评估样本量较小（仅100个），且缺乏跨领域或更多样化的数据集验证。

## 6. 主要结论与发现

- SALF生成器能够产生高度逼真的假新闻，使现有检测器的F1_fake平均下降53.4%（中文）和34.2%（英文），尤其对LLM-only检测器打击最大（最高下降85%）。
- SALF精炼后的检测器在针对精炼假新闻时，F1_fake提升7.3%（中文）和7.7%（英文）。
- 人类评估表明，SALF精炼的假新闻更难被人类识别（GossipCop上F1_fake从0.615降至0.214）。
- 两轮迭代后接近收敛（边际收益小于阈值0.05），表明框架效率较高。
- 案例显示SALF通过语言润色、情绪克制、专业归因等方式提升假新闻可信度。

## 7. 优点

- **可解释性强**：整个对抗训练过程使用自然语言表示损失、梯度和更新，易于理解与调试。
- **黑盒友好**：不需要访问模型内部参数，仅需API调用，避免昂贵反向传播。
- **动态自适应**：生成器和检测器共同进化，能应对不断演变的假新闻策略。
- **结构化辩论检测**：多角色辩论从多角度审视新闻，增强了检测的全面性和批判性思维。
- **实验设计合理**：从生成器、检测器两方面评估，包含消融、人类评估和收敛分析，结果一致且可信。
- **伦理考虑充分**：在论文中公开讨论潜在风险，并限制代码和提示的发布条件。

## 8. 不足与局限

- **自动指标依赖**：主要采用检测器性能作为代理，人类评估样本量小（仅100个），对真实人类感知的验证不足。
- **数据集与模型范围有限**：仅使用两个数据集（中文微博和英文八卦），且实验主要基于商用API模型（GPT-4o mini、DeepSeek V3），未涵盖更多开放模型（如LLaMA）和跨领域场景。
- **超参数敏感性**：对抗训练可能对超参数（如α、阈值ε）敏感，且可能遇到模式崩溃或收敛慢的问题（虽通过符号优化缓解）。
- **检测器基线绝对性能不高**：精炼后的检测器F1_fake仍低于SOTA模型（如ARG），作者解释为内容更难，但自身检测器架构简单。
- **算力信息缺失**：未提供GPU型号、数量、训练时长等具体资源消耗，影响可复现性评估。
- **潜在滥用风险**：尽管作者强调了伦理控制，但框架本身生成高质量假新闻的能力可能被恶意利用，文中只依赖技术复杂度作为屏障。

（完）
