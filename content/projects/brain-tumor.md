---
title: "Brain Tumor Detection"
date: 2025-06-01
author: ["Ashish Mathew"]
tags: ["Computer Vision","PyTorch","Deep Learning"]
summary: "Built a Convolutional Neural Network in PyTorch to identify brain tumors in MRI scans."
editPost:
    URL: "https://github.com/ashishmathew98/brain-tumor-detection"
    Text: "GitHub"
showToc: true
disableAnchoredHeadings: false
---

## Overview

Brain tumor detection through MRI scans is a critical step in early diagnosis and treatment planning.  
This project leverages **deep learning** techniques — specifically **Convolutional Neural Networks (CNNs)** — to identify the presence of brain tumors from medical images.

The model was designed, trained, and evaluated using **PyTorch**, following a reproducible and interpretable workflow.

## Dataset

The dataset consisted of 4,500 MRI scans evenly split between tumor non-tumor classes. The data was split into train, validation and test sets using a 70:15:15 split respectively.

## Methodology

Images were resized and augmented (flipping, rotation) to provide more training data to downstream CNN models.
<img width="793" height="860" alt="image" src="https://github.com/user-attachments/assets/cafb88eb-e365-4a1b-b0fe-2939dcf829ea" />

Two models were trained, one was a simple CNN model with 3 convolutional layers and 3 dense layers, the second was a pretrained VGG-16 model finetuned for brain tumor detection. This was done to evaluate the benefit of using larger pretrained models compared to developing a model from scratch.

## Results

Both models achieved similar out-of-sample accuracy of 95% with the pretrained VGG-16 model achieving steady performance in fewer epochs compared to the simple CNN model.

<img width="1484" height="336" alt="image" src="https://github.com/user-attachments/assets/17d8550d-8a58-4617-bc7b-4f29eddb080b" />

*Correctly classified cases (VGG-16)*

<img width="1484" height="336" alt="image" src="https://github.com/user-attachments/assets/77395931-5cd3-40fc-ac27-df6e00728744" />

*Misclassified cases (VGG-16)*
