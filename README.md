#  OAI HUTECH 2025 – Mushroom Image Classification Challenge

This repository contains the **final solutions** submitted for the **Mushroom Image Classification Challenge** organized by the **Ho Chi Minh City Computer Association (HCA)** in collaboration with **HUTECH University**.

---

##  Semi-Final Solution

###  Data Preprocessing & Augmentation

After analyzing the original dataset, we realized that using the raw **32×32** resolution images directly in CNN architectures resulted in suboptimal performance. To address this, we applied **Image Super-Resolution (ISR)** to upscale images to **64×64**, allowing the models to learn richer features.

<div align="center">
    <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/semi-final/ISR.png" alt="ISR Image" width="700"/>
</div> 

Additionally, we discovered that **Class 2** was particularly affected by **distracting colorful backgrounds**, leading to misclassifications. To mitigate this, we augmented the dataset by converting each RGB image into an additional **grayscale version**. This technique helped the model focus on **shape and texture features**, while still preserving the ability to learn color-related cues from the original RGB images.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/semi-final/COLOR-XAM.png" alt="Color vs Gray Image" width="700"/>
</div> 

---

###  Model Training & Evaluation

We selected **EfficientNetV2S** for training due to its lightweight architecture — making it well-suited for the relatively small dataset (1,400 training images). Despite its compact size, it delivered strong performance, achieving **91% accuracy** on the public test set, placing our team **12th nationwide**, and earning us a place in the final round.

We also significantly improved the classification performance for **Class 2**, increasing accuracy from **90/150** to **124/150** samples.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/semi-final/EVAL.jpg" alt="Confusion Matrix" width="700"/>
</div> 

---

##  Final Round Solution

###  Data Preprocessing & Augmentation

Building on insights from the semi-final, we resized all images to **96×96** using **BICUBIC interpolation**, as this size provided better results with deep CNNs. We further applied a series of advanced data augmentation techniques to improve model robustness:

* `RandomResizedCrop`
* `RandomHorizontalFlip`
* `RandomRotation`
* `ColorJitter`
* `RandomPerspective`
* `Normalization` (across RGB channels)

---

###  Model Training & Ensemble

For the final round, we implemented a **feature-level ensemble** using two powerful CNN architectures:

* `EfficientNetV2-L`
* `ConvNeXt-Large`

Both models were used as **feature extractors**, and their outputs were **concatenated**. Instead of using a standard linear layer for classification, we employed **KAN (Kolmogorov–Arnold Networks)** to fuse the extracted features and enhance prediction accuracy.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/final/effv2l_convL_kan_ensemble.png" alt="Model Architecture" width="700"/>
</div> 

---

###  Final Results

Our final ensemble model achieved an impressive **98% accuracy**, placing us **9th overall** in the national final leaderboard.

<div align="center">
  <img src="https://github.com/thisisdinhvu/OAI-HUTECH-2025/blob/main/src/final/ranking.png" alt="Leaderboard" width="700"/>
</div> 

---


