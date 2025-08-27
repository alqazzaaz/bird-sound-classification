# bird-sound-classification
Bird sound classification using deep learning (BirdCLEF 2025, score: 0.872)

# Bird Sound Classification (BirdCLEF 2025)

This repository contains our solution to the **BirdCLEF 2025** competition, where the task was to detect bird species from complex soundscape recordings.  
We developed a **deep learning ensemble** based on CNNs with attention mechanisms, achieving a final score of **0.872**.

---

## Project Overview
BirdCLEF 2025 provides 60-second soundscape recordings containing multiple overlapping bird species.  
Our pipeline transforms audio into **mel spectrograms** and applies an **ensemble of CNN-based models (TimmSED)** to perform multi-label classification across **207 bird species**.

---

## Approach

### 1. Dataset
- **Source**: BirdCLEF 2025 dataset  
- **Training**: Labeled bird vocalizations  
- **Test**: Unlabeled 60-second .ogg soundscapes  
- **Preprocessing**:  
  - Sample rate: 32 kHz  
  - Chunking: 60s → 12 × 5s segments  
  - Features: Mel spectrograms (128 mel bands, 50–16,000 Hz)  

### 2. Model Architecture
- **Backbone**: eca_nfnet_l0 (via timm library)  
- **Framework**: Custom TimmSED architecture with attention (AttBlockV2)  
- **Output**: Multi-label sigmoid scores per 5s chunk  

### 3. Inference & Postprocessing
- **Ensemble**: 3 trained models (sed0, sed1, sed2)  
- **Averaging**: Logit averaging + sigmoid  
- **Power correction**: Penalizes low-confidence classes  
- **Temporal smoothing**: Reduces flickering across 5s chunks  

---

## Results
- **Baseline (EfficientNet B0)**: 0.68  
- **Improved Model (TimmSED + Ensemble)**: **0.872**  
- Gains achieved through **attention mechanisms, ensembling, and smarter postprocessing**.  

---

## Repository Structure
- el-grande.ipynb – Main Kaggle notebook with full pipeline  
- poster/ – Project poster summarizing our approach and results
- score-screenshot – Screenshot showing our best score in the competition
- README.md – Project documentation (this file)  

---

## Team
- Malek  
- Wael  
- Abdullah  
- Amjad
- Ebru  

Supervised by **Simon Klüttermann, Steffen Maletz, Tim Katzke, Lars Grönberg**  
(Data Mining Cup, Summer Term 2025)

---

## References
- [BirdCLEF 2025 Competition](https://www.kaggle.com/competitions/birdclef-2025)  
---

## Key Takeaways
- **Attention + Ensembles = Better performance**  
- **Postprocessing** (power correction & smoothing) improved real-world robustness  
- Final score: **0.872**
