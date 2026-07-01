---
title: "GuavaVision AI: An Explainable Deep Learning Framework for Automated Classification, Lesion Localization, and Segmentation of Guava Diseases"
title_zh: "GuavaVision AI: 一个可解释的深度学习框架，用于番石榴病害的自动分类、病灶定位与分割"
authors: "Biswas, J., Islam, M., Bangabashi, M. M., Akter, M., Nishi, T. S., Sheikh, M. K., Mia, M. R., Anwar, M. M."
date: 2026-06-23
pdf: "https://www.biorxiv.org/content/10.64898/2026.06.18.733093v1.full.pdf"
tags: ["query:xai-objdet"]
score: 7.0
evidence: 可解释深度学习用于植物病害目标检测与定位
tldr: "针对番石榴叶片和果实病害症状重叠、诊断困难的问题，提出一个集图像级分类、病斑定位与像素级分割于一体的深度学习框架。通过标准增强、结构化增强和GAN合成将数据集扩至约7000张图像，采用ResNet50+DenseNet121融合模型实现98.20%分类准确率，并用YOLOv8-seg实现高精度检测与分割（mAP@0.5达0.907）。引入可解释AI增强模型透明度，评估轻量级模型以适应网络部署，为番石榴病害自动化管理提供了有效方案。"
source: biorxiv
selection_source: fresh_fetch
motivation: 现有植物病害诊断方法多限于图像级分类，缺乏同时进行病斑定位和分割的统一框架，且对番石榴病害的自动化分析不足。
method: 采用三种数据增强策略扩充数据，融合ResNet50与DenseNet121进行图像分类，使用YOLOv8-seg进行病斑检测和分割，并结合可解释AI提升透明度。
result: "模型融合分类准确率98.20%，YOLOv8-seg检测mAP@0.5为0.907，分割mAP@0.5为0.889，性能优于Mask R-CNN。"
conclusion: 模型融合、数据增强与分割感知检测有效提升了番石榴病害诊断的准确性和可解释性，具备实际部署潜力。
---

## 摘要
番石榴种植受叶片和果实病害的显著影响，这些病害重叠的症状和环境变化使得田间准确诊断具有挑战性。已有大量研究致力于寻找植物病害诊断的有效方法，但大多数集中在图像级分类，并未在单一分析框架中包含病灶定位或像素级分割。本研究提出了一个综合框架，利用自动化图像分析对番石榴叶片和果实病害进行图像级分类、病灶定位，并从不同生长条件下收集的同一病害类型的多幅图像中进行像素级分割。数据集通过三种增强策略得到丰富，包括标准预处理、结构化增强和基于GAN的合成图像生成，将有效训练数据扩展到约7000张图像，同时采用5折交叉验证策略指导模型选择，最终在留出测试集上评估性能。对多种最先进卷积神经网络（CNN）在番石榴叶片和果实病害分类中的实验评估表明，使用ResNet50+DenseNet121模型融合生成的模型达到了98.20%的最高分类准确率。在病灶检测和分割方面，YOLOv8-seg优于Mask R-CNN，检测和分割的mAP@0.5分别达到0.907和0.889，mAP@0.5:0.95分别达到0.783和0.769，且具有平衡的精确率-召回率曲线。采用可解释人工智能（XAI）技术通过识别图像中对实际病灶重要的区域来增加该模型的透明度。该框架进一步考虑了实际的网页部署，评估了轻量级和高容量模型以平衡计算效率与预测准确性。研究表明，使用模型融合、数据增强和分割感知的病灶检测可以为有效管理番石榴病害提供解决方案。

## Abstract
Guava cultivation is considerably influenced by foliar and fruit diseases whose overlapping symptoms and environmental variability make accurate field-level diagnosis challenging. Numerous studies have been conducted to find efficient methods of diagnosing plant diseases, but most focus on image-level classification and do not include lesion localization or pixel-level segmentation of the images within a single framework of analysis. This study proposes a comprehensive framework for utilizing automated image analysis to classify guava leaf and fruit diseases at the image level, locate lesions, and segment lesions at the pixel level from multiple images of the same type of disease collected from various growing conditions. The dataset was enriched through three augmentation strategies including standard preprocessing, structured augmentation, and GAN-based synthetic image generation, expanding the effective training data to approximately 7,000 images, while a 5-fold cross-validation strategy guided model selection and final performance was assessed on a held-out test set. The experimental evaluation of multiple state-of-the-art Convolutional Neural Networks (CNNs) for the classification of guava leaf and fruit diseases indicated that the model generated using the ResNet50+DenseNet121 model fusion achieved the highest classification accuracy of 98.20%. For lesion detection and segmentation, YOLOv8-seg outperformed Mask R-CNN, achieving mAP@0.5 of 0.907 and 0.889, and mAP@0.5:0.95 of 0.783 and 0.769 for detection and segmentation, respectively, with a balanced precision-recall profile. The techniques of Explainable AI (XAI) were used to increase the transparency of this model by identifying areas in the image that are significant to the actual lesion. The framework was further designed with practical web-based deployment in mind, evaluating both lightweight and high-capacity models to balance computational efficiency against predictive accuracy. From this research, it was concluded that using model fusion, data augmentation, and segmentation-aware lesion detection would provide a solution for managing guava diseases effectively.