---
title: Lightweight Lyrics-Based Music Structure Analysis

---

# Multi-Scale Semantic Tagging for Lyrics-Based Music Structure Analysis Using Lightweight Bidirectional Long Short-Term Memory

Official implementation of the paper:

> **Multi-Scale Semantic Tagging for Lyrics-Based Music Structure Analysis Using Lightweight Bidirectional Long Short-Term Memory**

This repository contains the official implementation of the proposed lyrics-based Music Structure Analysis (MSA) framework, including:

- Proposed model implementation
- Baseline implementations (reproduced by the author)
- Dataset construction pipeline
- Experiment configurations

---

# Overview

Music Structure Analysis (MSA) aims to identify functional song sections such as:

- Intro
- Verse
- Pre-Chorus
- Chorus
- Bridge
- Instruments
- Outro

Unlike conventional MSA systems that rely on audio spectrograms, this work investigates whether **lyrics alone** can provide sufficient structural information.

The proposed framework combines

- Hierarchical RoBERTa embeddings
- Section-level semantic representations
- Position-aware features
- Repetition-aware similarity features
- Lightweight Bi-LSTM sequence modeling

to achieve competitive performance while significantly reducing computational cost.

---

# System Architecture
<!-- 補圖 -->
<!-- -<p align="center"> -->
<!-- -<img src="figures/framework.png" width="900"> -->
<!-- -</p> -->
![Fig1_Overall system architecture'](https://hackmd.io/_uploads/By3K4KEVMg.jpg)

---

# Repository Structure

```text
Lyrics-MSA/
│
├── Proposed Model/
│   ├── Model Code.ipynb
│   ├── Compare 4 Methods of RoBERTa.ipynb
│   ├── Model_Pack_Seed43/
│          ├── report_seed43.json
│          ├── model_weights_seed43.pth
│          ├── metrics_seed43.pt
│          ├── label_encoder.pt
│ 
├── Thesis/
│   ├── Figures/
│          ├── Fig1_Overall system architecture.png
│          ├── Fig2_Performance Comparison with Lyrics-Only and Audio-Only Baselines_F1-Score.png
│          ├── Fig3_Resource Comparison with Baselines.png
│          ├── Fig4_Confusion Matrix.png
│
├── Slides/
│   ├── 2026.7_Slides_Final.pdf
│
└── README.md
```

---

# Execution
Open "Model Code.ipynb" on Google Colab and follow the steps of evey cells.

---

# Dataset

## Dataset Availability

The synchronized dataset used in this work **is NOT included** in this repository.

The dataset is derived from the following publicly available datasets:

- DALI v2.0
- Harmonix Set

Since both datasets are distributed under their own licenses, the merged dataset cannot be redistributed.

Please download the original datasets from their official sources.

---

## Dataset Construction

After downloading the original datasets, reconstruct the synchronized dataset by below steps:


- Metadata matching: Extract common tracks from DALI v2.0 dataset and The Harmonix Set by matching metadata.
- Title Normalization:
- Timestamp Alignment: Matching line-level timestamps from DALI v2.0 dataset with segment-level timestamps from The Harmonix Set.
- Label Fusion: Matching segment-level segment labels from The Harmonix Set with the line-level timestamps, then perform data cleaning
- CSV Generation: Generate CSV files.
- Audio Files Download: Download the audio files from YouTube.
---

## Generated Dataset Format

After reconstruction, each song should have the following structure

```text
dataset/

├── Lyrics/
│   ├── song_001.csv
│   ├── song_002.csv
│   ├── ......

├── Audio/
│   ├── song_001.mp3
│   ├── song_002.mp3
│   ├── ......

├── Spectrograms/
│   ├── song_001.npy
│   ├── song_002.npy
│   ├── ......
```

where each "[Song_Name].csv" contains

| column | description |
|---------|-------------|
| start_time | lyric start timestamp |
| end_time | lyric end timestamp |
| lyrics | lyric text |
| segment | structural label |

---
# Proposed Model

Executed on Google Colab
```
---

# Baseline Implementations

This repository includes reproduced implementations of the following baseline models.

## LongFormer

The LongFormer baseline is independently reproduced by the author according to the original publication.

This implementation is intended solely for experimental comparison and is **not** the official implementation.

---

## SongFormer

The SongFormer baseline is reproduced for fair comparison using the synchronized dataset constructed in this work.

The implementation follows the methodology described in the original paper.

Please refer to the official SongFormer repository for the original implementation.

---

# Reproducing the Paper

The complete experimental pipeline is

Download original datasets
↓
Construct synchronized dataset
↓
Extract RoBERTa embeddings
↓
Generate repetition-aware features
↓
Train the proposed model
↓
Evaluate
↓
Generate experimental results
```
---

# Experimental Results

| Model | Weighted F1 | Accuracy | L-Measure |
|--------|------------|----------|-----------|
| Proposed | 0.7848 | 0.7867 | 0.7948 |
| LongFormer | 0.5672 | 0.6142 | 0.6398 |
| SongFormer | 0.5254 | 0.5448 | 0.6283 |

## Experimental Visualizations

![Fig2_Performance_Comparison_with_Lyrics-Only_and_Audio-Only_Baselines_F1-Score](https://hackmd.io/_uploads/BkE4fUtIGe.png)
![Fig3_Resource_Comparison_with_Baselines](https://hackmd.io/_uploads/H1ONf8Y8fg.png)
![Fig4_Confusion_Matrix](https://hackmd.io/_uploads/H1iNMUFIGg.png)

---

# Citation

If you find this repository useful, please cite

```bibtex
@mastersthesis{YU2026MSA,
  title={Lightweight Lyrics-Based Music Structure Analysis Using Music-Aware Features},
  author={Yu, Shih-Yu},
  school={National Cheng Kung University},
  year={2026},
  type={Master's thesis}
}
```

---

# Code Availability

This repository provides
- Dataset construction steps
- Source code of proposed model and self-implemented baseline models

---

# Dataset License Notice

This repository **does not redistribute any copyrighted datasets**.

The synchronized dataset is constructed from

- DALI v2.0
- Harmonix Set

Users are responsible for downloading the original datasets and complying with their respective licenses.

---

# License

The source code in this repository is released under the MIT License.

See

```
LICENSE
```

for details.

---

# Acknowledgements

This work builds upon the following publicly available resources.

- DALI v2.0
- Harmonix Set
- RoBERTa
- LongFormer
- SongFormer

We sincerely thank the authors for making their work publicly available.