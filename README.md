# UNet-TA-UNet-for-Semantic-Segmentation
implementation of UNet  and TA-UNet for semantic segmentation / Marine dataset 

## Project Level : High-Intermediate
*You may find the report of the project under the name "UNet & TA-UNet for Marine Semantic Segmentation-Solouki.PDF"*

##  Project Highlights
This project focuses on the implementation of two neural network architectures for semantic segmentation: **UNet** and **TA-UNet**.

- **UNet** is a powerful convolutional network architecture designed for semantic segmentation, utilizing a symmetric encoder-decoder structure with skip connections to preserve spatial information.
- **TA-UNet (UNet with Attention)** enhances the original UNet by integrating attention mechanisms to focus on relevant image regions and suppress irrelevant features, improving segmentation accuracy.

The task was performed on a dataset containing **8 segmentation classes** (e.g., fish, starfish, boat, diver) with image dimensions resized from **360×640 to 368×640** as suggested by the base paper.

---

##  Project Goal

To build, train, and evaluate segmentation models that:
- Handle imbalanced data using techniques such as **data augmentation**, **class weighting**, and **custom loss functions**.
- Improve the accuracy and generalizability of predictions across all 8 classes.
![image](https://github.com/user-attachments/assets/1969bec3-0485-4d0d-8643-87951225b641)
![image](https://github.com/user-attachments/assets/597078d2-5707-4ac7-8bcc-ee99a3b87598)

---

##  Models Used

### 1. UNet
A classic encoder-decoder architecture with downsampling and upsampling layers and skip connections, suitable for biomedical and object segmentation tasks.

### 2. TA-UNet (UNet with Attention)
An enhanced version of UNet, augmented with attention mechanisms to help the model focus on essential regions and suppress irrelevant details.

---

## ⚖ Data Handling and Preprocessing

- **Dataset Split**: 90% training, 10% validation.
- **Image Size**: Resized to 368×640.
- **Number of Classes**: 8 (instead of 2 as in the original paper).
- **Normalization**: Z-score standardization was applied.
- **Data Augmentation**: Performed with techniques such as rotation (0.2), flipping, and zooming. These were carefully chosen to preserve the original data distribution, especially suitable for underwater object images.

---

##  Handling Class Imbalance

To address class imbalance, the following strategies were applied:

- **Class-Weighted Loss Function**: Combined **Categorical Cross-Entropy** with **Dice Loss** to ensure attention to minority classes.
- **Advanced Loss Functions**:
  - `Focal Loss` for handling difficult-to-classify examples.
  - `Dice Loss` and `Tversky Loss` for imbalanced segmentation tasks.
- **Augmentation-based Balancing**: Minority classes were enhanced via image augmentations.
- **Model Architectures**: Attention mechanisms and multi-scale feature capturing were used to help detect small or rare objects.

---

##  Training Configuration

- **Loss Function**: Combined `Categorical Cross-Entropy` + `Dice Loss`.
- **Optimizer**: Adam.
- **Metrics**: Loss, Accuracy, and custom `Mean Intersection over Union (mIoU)`.
- **Batch Size**: 16.
- **Epochs**: 20.
- **Callbacks Used**:
  - `ModelCheckpoint`: Save best model based on validation loss.
  - `ReduceLROnPlateau`: Reduce learning rate on plateau in validation loss.
  - `EarlyStopping`: Stop training if no improvement is seen, restoring best weights.

---

##  Evaluation Metrics

### Mean Intersection over Union (mIoU)
This metric calculates the mean IoU across all classes and is useful for overall performance evaluation in multi-class segmentation tasks.

- A higher mIoU indicates better model performance.
- This was implemented from scratch as part of the evaluation framework.

---

##  Results & Observations

- **UNet Model**:
  - Training loss decreased steadily from ~1.2 to ~0.95.
  - Training accuracy improved from ~0.66 to ~0.72.
  - Validation metrics showed good generalization, with some fluctuations.

- **Effect of Combined Loss**:
  - Categorical Cross-Entropy provided lower training loss and higher accuracy.
  - Dice Loss improved performance on minority classes.
  - Models trained with combined loss outperformed those using a single loss.

---

##  Conclusion

This project demonstrates that:
- Combining attention mechanisms and advanced loss functions significantly improves segmentation performance in imbalanced datasets.
- Data augmentation, normalization, and careful architecture design are essential for achieving robust and generalizable models.
- The **UNet** and **TA-UNet** models trained in this project achieved promising results in multi-class underwater object segmentation, and the evaluation metrics (especially mIoU) confirmed effective pixel-level classification.

---
