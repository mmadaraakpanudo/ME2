# Dataset — Warts vs Moles (Skin Disease)

## Source

**Kaggle:** [Skin Disease Dataset](https://www.kaggle.com/datasets/pacificrm/skindiseasedataset)
by **Pacificrm**

## Brief Description

The dataset contains dermoscopic and clinical RGB images of 22 skin disease categories
including Acne, Eczema, Psoriasis, Warts, Moles, and more. For this project only
**Warts** and **Moles** are used — all other 20 classes are excluded. The dataset
provides pre-made `train` and `test` splits; a validation set is constructed at runtime
by holding out **15%** of the Kaggle `train` images per class (stratified, seed 42).
The remaining 85% forms the training set. All images are resized to **224 × 224** pixels
during loading. For full details on collection method and licensing refer to the dataset
page linked above.

## Structure (used subset, after runtime split)

```
skin_split/
├── train/
│   ├── Moles/
│   └── Warts/
├── val/
│   ├── Moles/
│   └── Warts/
└── test/          ← from Kaggle's test/ split directly
    ├── Moles/
    └── Warts/
```

