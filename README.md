# Histopathology Color Normalization

A research project demonstrating H&E stain normalization techniques combined with deep learning for breast cancer histopathological image classification.

**Disclaimer:** This is an educational/research project. Not for clinical use.

---

## Overview

This project explores color normalization methods for histopathological images, specifically focusing on H&E (Hematoxylin and Eosin) stained breast cancer tissue samples. The work consists of three main phases:

1. **Literature Review** - Analysis of the AGDGIF stain normalization method
2. **Custom Filter Pipeline** - Development of a 32-step image preprocessing pipeline  
3. **Transfer Learning Classification** - ResNet50-based breast cancer classification with normalized images

---

## Methodology

### Phase 1: Literature Review
- Reviewed the AGDGIF (Adaptive Gradient Domain-Guided Image Filtering) method by Li et al. (2023)
- Analyzed stain normalization techniques for H&E histological images
- Reference: *Biomedical Signal Processing and Control*, Volume 85, 2023

### Phase 2: Custom Filter Pipeline (32 Steps)
Key innovations:
- **Patch-based region selection** for representative color estimation
- **Cuckoo Search** algorithm for automated λ sparsity parameter optimization
- **HSD color model** weight terms (VR × D, VB × 2×S) for improved stain/background distinction
- **SNMF (Sparse Non-negative Matrix Factorization)** with LARS algorithm for W-matrix estimation
- **Beer-Lambert law** based optical density modeling

Technical details:
- W-matrix estimation: SNMF with LARS algorithm
- H-map estimation: ℓ1-regularized least-squares
- Background removal: HSD color model (S+D channels), Otsu thresholding
- Mini-batch processing with conjugate gradient method

### Phase 3: Transfer Learning with ResNet50
- Two-phase training approach:
  1. **Feature extraction** (frozen convolutional layers)
  2. **Fine-tuning** (unfrozen top layers)
- **Task:** Breast cancer histopathological image classification
- **Dataset:** BreakHis 400× magnification
- **Evaluation:** Comparison between original and filtered images

---

## Results

### Classification Performance

| Metric | Original Images | Filtered Images | Improvement |
|--------|----------------|-----------------|-------------|
| Accuracy | 85.4% | **87.2%** | +1.8% |
| **Recall** | 89.3% | **92.1%** | **+2.8%** |
| Precision | 86.7% | 88.4% | +1.7% |

**Clinical Justification:** Recall was prioritized over accuracy because in medical imaging, **minimizing false negatives** (missing a positive case) is more critical than overall accuracy. A false negative in cancer detection could delay treatment, whereas false positives can be verified through additional testing.

---

## Dataset

This project uses the **BreakHis (Breast Cancer Histopathological Database)** dataset:

### BreakHis Dataset Details
- **Source:** Laboratory of Vision, Robotics and Imaging (VRI), Federal University of Paraná (UFPR), Brazil
- **Images:** 7,909 microscopic images of breast tumor tissue
- **Magnification Levels:** 40×, 100×, 200×, 400×
- **This Project:** 400× magnification images only
- **Classes:**
  - **Benign:** Adenosis, Fibroadenoma, Phyllodes Tumor, Tubular Adenoma
  - **Malignant:** Ductal Carcinoma, Lobular Carcinoma, Mucinous Carcinoma, Papillary Carcinoma
- **Format:** PNG files (RGB, 3-channel color)
- **Resolution:** 700×460 pixels

**Dataset Access:**
- Kaggle: [BreakHis 400×](https://www.kaggle.com/datasets/pankaj4321/breakhis-400x)
- Original Source: [BreakHis Official](https://web.inf.ufpr.br/vri/databases/breast-cancer-histopathological-database-breakhis/)

### Dataset Citation
> Spanhol, F. A., Oliveira, L. S., Petitjean, C., & Heutte, L. (2016). A dataset for breast cancer histopathological image classification. *IEEE Transactions on Biomedical Engineering*, 63(7), 1455-1462.

---

## Technical Stack

- **Language:** Python 3.x
- **Deep Learning:** TensorFlow/Keras, ResNet50 (transfer learning)
- **Image Processing:** OpenCV, NumPy, Scikit-image
- **Optimization:** Cuckoo Search metaheuristic algorithm
- **Color Models:** RGB, HSD, Beer-Lambert optical density
- **Matrix Factorization:** SNMF (Sparse Non-negative Matrix Factorization)
- **Sparse Solver:** LARS (Least Angle Regression)
- **Notebook:** Jupyter

---

## Repository Structure

```text
histopathology-color-normalization/
├── 1-literature-review/
│   └── papers/
│       └── Li-2023-AGDGIF-Stain-Normalization.pdf
├── 2-filter-pipeline/
│   ├── code/
│   │   └── filter_implementation.ipynb
│   ├── diagrams/
│   │   ├── flowchart-detailed.png
│   │   └── flowchart-simple.png
│   └── report/
│       └── methodology.docx
├── 3-transfer-learning/
│   ├── code/
│   │   └── resnet50_training.ipynb
│   ├── results/
│   │   ├── accuracy-loss-original.png
│   │   ├── accuracy-loss-filtered.png
│   │   ├── confusion-matrix-original.png
│   │   └── confusion-matrix-filtered.png
│   └── report/
│       └── final-report.docx
├── samples/
│   └── histopathology-sample.png
├── README.md
└── .gitignore
```
---

## Usage

### Prerequisites
```bash
pip install tensorflow keras opencv-python numpy scikit-image pandas matplotlib
```

### Running the Filter Pipeline
```bash
jupyter notebook 2-filter-pipeline/code/filter_implementation.ipynb
```

### Training ResNet50
```bash
jupyter notebook 3-transfer-learning/code/resnet50_training.ipynb
```

**Note:** The BreakHis dataset must be downloaded separately from the sources listed above.

---

## References

**Primary Literature:**
- Li, X., et al. (2023). "A stain color normalization with robust dictionary learning for breast cancer histological images processing." *Biomedical Signal Processing and Control*, 85, 104978. [DOI](https://doi.org/10.1016/j.bspc.2023.104978)

**Dataset:**
- Spanhol, F. A., et al. (2016). "A dataset for breast cancer histopathological image classification." *IEEE Transactions on Biomedical Engineering*, 63(7), 1455-1462.

**Methods:**
- Vahadane, A., et al. (2016). "Structure-preserving color normalization and sparse stain separation for histological images." *IEEE Transactions on Medical Imaging*, 35(8), 1962-1971.

---

## Academic Context

This research project was conducted during the **ISE 516 - Computer Vision** course at **Sakarya University** (2025-2026 academic year)

**Project Components:**
- Literature review of state-of-the-art stain normalization methods
- Design and implementation of a novel 32-step filter pipeline
- Comparative analysis using ResNet50 transfer learning on BreakHis dataset

---

## Author

**Ihab Al Ramahi**  
MSc Student in AI & Data Science  
Sakarya Üniversitesi  
2025-2027

---

## Contact

**LinkedIn:** [linkedin.com/in/ihab-al-ramahi](https://linkedin.com/in/ihab-ramahi)  
**Email:** ehabramahi1@gmail.com  
**GitHub:** [@eRamahi](https://github.com/eRamahi)

---

## License

This project is for educational and research purposes only. The dataset retains its original license. Code implementations are provided as-is for academic study.

---

## Acknowledgments

- Sakarya University Faculty of Engineering
- Authors of the AGDGIF paper (Li et al., 2023)
- BreakHis dataset creators at Federal University of Paraná

---

*Last updated: April 2026*
