# ME2 — Warts vs Moles Skin Disease Classifier

## Overview

This project trains a binary image classifier to distinguish **Warts** from **Moles**
using **transfer learning** with MobileNetV2 pre-trained on ImageNet. The model is built
with TensorFlow / Keras and follows a two-phase training strategy: a feature-extraction
phase (frozen base) followed by a fine-tuning phase (top 30 layers unfrozen). The
dataset is a two-class subset drawn from a 22-class skin disease collection that
includes pre-made train and test splits.

---

## Dataset

A brief description of the dataset source is provided in [`dataset/README.md`](dataset/README.md).

**Dataset:** Skin Disease Dataset — Kaggle  
**Classes:** `Moles`, `Warts`  
**Split strategy:** test from Kaggle test split · val carved from Kaggle train split (15%)

---

## Running the App

```bash
cd ME2
streamlit run app.py
```

The app will open automatically at **http://localhost:8501**

**Streamlit Cloud URL:** *https://wartsvsmoles.streamlit.app/*
---

## Environment Setup

### Requirements

Python **3.12** is recommended. All dependencies are pinned in [`requirements.txt`](requirements.txt).

### Install locally

```bash
# 1. Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the app
streamlit run app.py
```

### Key packages

| Package | Version | Purpose |
|---|---|---|
| `tensorflow` | 2.19.0 | Model training |
| `keras` | 3.15.0 | High-level API |
| `scikit-learn` | 1.8.0 | Evaluation metrics |
| `matplotlib` | 3.10.0 | Plotting |
| `seaborn` | 0.13.2 | Confusion matrix heatmap |
| `streamlit` | 1.60.0 | Web UI |

> **Note:** For faster training, use Google Colab with a T4 GPU runtime
> (`Runtime → Change runtime type → T4 GPU`).

---

## Project Structure

```
ME2/
├── dataset/
│   └── README.md          # Dataset source description
├── model/                 # Saved .keras model files
├── notebooks/
│   └── ME2.ipynb          # Full training pipeline
├── results/               # Plots, confusion matrices, learning curves
├── requirements.txt
├── CONTRIBUTORS.md
└── README.md              # This file
```

---

## Challenges & Solutions

| Challenge | Solution / Notes |
|---|---|
| Dataset has 22 classes — only 2 are needed | Filtered by matching `parent.name == 'train'` or `'test'` + class name, ignoring all others |
| No validation split provided | Carved 15% of the Kaggle train split per class as validation |
| Medical imaging — subtle visual overlap between warts and moles | Fine-tuning top 30 MobileNetV2 layers improves discrimination of fine-grained skin texture |
| Class imbalance possible in a clinical dataset | `restore_best_weights=True` guards against training past the best generalisation point |

---

## Possible Improvements

- Experiment with **EfficientNetB0** as an alternative base model
- Extend to multi-class skin disease classification across all 22 classes
- Add Grad-CAM visualisation to highlight decision regions on skin images

---

## Results


> Full learning curves and confusion matrices are saved in `results/`.

## Contributors.

See [CONTRIBUTORS.md](CONTRIBUTORS.md) for the full list of names, GitHub usernames, and registration numbers.

---
