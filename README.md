# Cats vs. Dogs Image Classifier

> Binary image classification using transfer learning with MobileNetV2 pre-trained on ImageNet.

---

## Experiment Setup

| Parameter | Value |
|---|---|
| Dataset | Cats vs. Dogs |
| Hardware | TPU v5e-1 |
| Model | MobileNetV2 (pre-trained on ImageNet) |
| Image Size | 224 × 224 × 3 |
| Batch Size | 32 |
| Epochs | 5 |
| Train / Val Split | 80% / 20% |
| Optimizer | Adam (lr = 1e-4) |
| Loss Function | Binary Crossentropy |

---

## ️ Architecture

```
MobileNetV2 (frozen)
        ↓
GlobalAveragePooling2D
        ↓
   Dropout (0.4)
        ↓
  Dense(1, sigmoid)
```

---

## Data Augmentation

| Technique | Value |
|---|---|
| Rotation | ± 20° |
| Width / Height Shift | 20% |
| Shear | 20% |
| Zoom | 20% |
| Horizontal Flip | Enabled |
| Pixel Rescaling | [0, 1] normalization |

---

## Training Results

| Epoch | Train Acc | Train Loss | Val Acc | Val Loss | Time |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | 71.45% | 0.5547 | 95.58% | 0.1556 | 545s |
| 2 | 94.19% | 0.1654 | 96.36% | 0.1101 | 541s |
| 3 | 95.40% | 0.1250 | 96.22% | 0.0950 | 540s |
| **4** | **95.86%** | **0.1104** | **97.18%** | **0.0836** | **539s** |
| 5 | 96.22% | 0.0985 | 96.92% | 0.0814 | 541s |

** Best validation accuracy: 97.18% at Epoch 4**  
**Final validation loss: 0.0814**  
**Total training time: ~45 minutes**

---

## Accuracy & Loss Curves

![Training curves](<img width="599" height="263" alt="image" src="https://github.com/user-attachments/assets/997e8b2d-3d63-4e83-9eed-32d05d21665b" />)

---

## Possible Improvements

- **Fine-tuning** — Unfreeze top 20–30 layers with a reduced learning rate (1e-5) for 5–10 additional epochs
- **More epochs** — Extend to 15–20 epochs with learning rate scheduling
- **Stronger backbone** — Replace MobileNetV2 with EfficientNetB3, ResNet50, or InceptionV3 for richer feature extraction
- **Error analysis** — Examine misclassified images, identify failure patterns, and collect targeted data for weak cases

---

## Conclusion

The model achieved **97.18% validation accuracy** in just ~45 minutes of training. Transfer learning with MobileNetV2 proved highly efficient — strong performance was visible from the very first epoch, with minimal overfitting thanks to data augmentation. Training remained smooth and stable throughout all 5 epochs.

A practical application for this model would be an **animal shelter classification system**, automatically sorting incoming pet images into cats and dogs. Solid results for minimal training time and compute resources.
