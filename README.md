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
├── phase1.pdf          # Phase 1 report: data collection plan & methodology
├── phase2.ipynb        # Phase 2 notebook: preprocessing & feature extraction
├── report2.pdf         # Phase 2 written report
└── README.md
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

---

## Tech Stack

| Area | Tools |
|------|-------|
| Audio processing | `librosa`, `soundfile` |
| Feature extraction | MFCC, Log-Mel Spectrogram, Spectral Contrast, ZCR, LPC |
| Data handling | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn` |
| Notebooks | Jupyter |

---

## Getting Started

```bash
git clone https://github.com/IliyaJz/Dialect-Detector.git
cd Dialect-Detector
pip install librosa soundfile numpy pandas matplotlib seaborn jupyter
jupyter notebook phase2.ipynb
```

> The raw audio dataset is hosted separately by the course team. See the Google Drive link in `phase2.ipynb` or contact the project authors.

---

## Course Info

**Course:** Machine Learning Basics — Spring 2026  
**Instructors:** Mohammadreza A. Dehghani, Mostafa Tavassolipour  
**TAs:** Arash Taherifard, Amirhossein Aref, Hamidreza Taleai
