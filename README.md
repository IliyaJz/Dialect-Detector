# Dialect Detector

A machine learning project that classifies the **gender** and **regional dialect** of Persian speakers from audio recordings. Built as a university final project for the Machine Learning Basics course (Spring 2026) at the University of Tehran.

---

## Overview

The goal is to build a system that takes a raw audio clip of a Persian speaker and predicts:
- **Gender** — Male / Female
- **Dialect** — one of five regional Persian dialects

The five dialects in the dataset are: **Torki**, **Kordi**, **Mashhadi**, **Isfahani**, and **Gilaki**.

---

## Repository Structure

```
Dialect-Detector/
├── .gitignore              # Git ignore rules for Python, Jupyter & system files
├── README.md               # Project documentation
├── notebooks/              # Jupyter notebooks
│   ├── phase2.ipynb        # Phase 2 notebook: Preprocessing & feature extraction
│   └── phase3.ipynb        # Phase 3 notebook: Supervised modeling & dialect clustering
└── reports/                # PDF reports
    ├── phase1_report.pdf   # Phase 1 report: Data collection plan & methodology
    ├── phase2_report.pdf   # Phase 2 report: Preprocessing & EDA
    └── phase3_report.pdf   # Phase 3 report: Final classification, clustering & evaluation
```

---

## Phases

### Phase 1 — Data Collection
Each group collected 30–40 audio clips (~60 seconds each) for one assigned dialect — 15–20 from male speakers and 15–20 from female speakers. Sources included films, series, interviews, and documentaries (e.g. Telewebion). Files were named with a strict convention:

```
GroupID_Dialect_Gender_SpeakerID_VoiceNumber.mp3
# e.g. G03_Gilaki_Female_F01_Voice01.mp3
```

All group contributions were merged by the course team into a single shared raw dataset used from Phase 2 onward.

### Phase 2 — Preprocessing & Feature Extraction
Working from the combined raw dataset, the pipeline:

1. **Cleans the data** — removes files with heavy noise, dominant background music, or excessive silence; normalizes loudness; resamples to a uniform rate
2. **Extracts features** from each audio file using `librosa`, including:
   - MFCC (mean & std per coefficient → fixed-length vector)
   - Log-Mel Spectrogram statistics
   - Spectral Contrast, Zero-Crossing Rate, and others
3. **Builds a feature table** — one row per audio file, columns for dialect, gender, speaker ID, and all extracted features — saved as CSV/XLSX for use in Phase 3

An initial EDA (PCA visualization, per-dialect feature distributions) is included in the notebook.

### Phase 3 — Modeling, Classification & Clustering
Phase 3 builds the core predictive models and unsupervised clustering analysis:

1. **Supervised Classification**:
   - **Gender Classification**: Trained and evaluated models for binary gender detection.
   - **Dialect Classification**: Evaluated baseline classifiers (Random Forest, SVM, XGBoost, LightGBM, MLP) and implemented **Advanced Feature Fusion** (LDA + PCA & Triple Feature Fusion).
   - **Class Imbalance & Validation**: Utilized **SMOTE** (Synthetic Minority Over-sampling Technique) and group/stratified speaker splits to prevent data leakage.
   - **Ensemble Modeling**: Built a Stacking Classifier and evaluated performance on the official test set.

2. **Unsupervised Dialect Clustering**:
   - Evaluated clustering algorithms: **K-Means**, **Gaussian Mixture Models (GMM)**, **DBSCAN**, and **Agglomerative Clustering**.
   - Evaluated cluster quality via Silhouette Score, Calinski-Harabasz Index, Davies-Bouldin Index, and NMI/ARI metrics.
   - Low-dimensional 2D/3D visualizations using **PCA** and **t-SNE**, alongside per-sample silhouette analysis.

---

## Tech Stack

| Area | Tools |
|------|-------|
| Audio processing | `librosa`, `soundfile` |
| Feature extraction | MFCC, Log-Mel Spectrogram, Spectral Contrast, ZCR, LPC |
| Machine Learning | `scikit-learn`, `xgboost`, `lightgbm`, `imbalanced-learn` (SMOTE) |
| Data handling | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn` |
| Notebooks | Jupyter |

---

## Getting Started

```bash
git clone https://github.com/IliyaJz/Dialect-Detector.git
cd Dialect-Detector
pip install librosa soundfile numpy pandas scikit-learn xgboost lightgbm imbalanced-learn matplotlib seaborn jupyter
jupyter notebook notebooks/phase3.ipynb
```

> The raw audio dataset is hosted separately by the course team. See the Google Drive link in `phase2.ipynb` or contact the project authors.

---

## Course Info

**Course:** Machine Learning Basics — Spring 2026  
**Instructors:** Mohammadreza A. Dehghani, Mostafa Tavassolipour  
**TAs:** Arash Taherifard, Amirhossein Aref, Hamidreza Taleai
