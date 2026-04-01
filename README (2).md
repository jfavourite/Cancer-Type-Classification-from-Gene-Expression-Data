# Cancer Type Classification from Gene Expression Data

A machine learning project that classifies cancer types using RNA-seq gene expression profiles from the TCGA Pan-Cancer dataset. The model achieves high accuracy by combining PCA-based dimensionality reduction with a Random Forest classifier.

---

## Overview

The human genome contains over 20,000 genes, and their expression levels can reveal a lot about disease state. This project uses RNA-seq data from 801 cancer patients across 5 cancer types to build a classifier that can predict cancer type purely from gene expression — no clinical metadata required.

The pipeline covers the full ML workflow: data loading, preprocessing, dimensionality reduction, model training, evaluation, and biomarker identification.

---

## Dataset

**TCGA Pan-Cancer (HiSeq)** — sourced from the UCI ML Repository via `ucimlrepo`.

| Property | Value |
|---|---|
| Patients | 801 |
| Features (genes) | 20,531 |
| Cancer types | 5 (BRCA, KIRC, COAD, LUAD, PRAD) |
| Data type | RNA-seq gene expression (HiSeq) |

> The dataset file (`TCGA-PANCAN-HiSeq-801x20531.tar.gz`) must be downloaded separately and placed in the project root before running the notebook. See [Setup](#setup) below.

---

## Methodology

```
Raw Gene Expression (801 × 20,531)
        ↓
  StandardScaler (z-score normalization)
        ↓
  PCA → 50 principal components
        ↓
  Train/Test Split (80/20)
        ↓
  Random Forest Classifier (100 trees)
        ↓
  Evaluation + Biomarker Analysis
```

1. **Preprocessing** — Features are standardized using `StandardScaler` to remove scale differences between genes.
2. **Dimensionality Reduction** — PCA reduces 20,531 gene features to 50 principal components, capturing the most variance while making training tractable.
3. **Classification** — A `RandomForestClassifier` is trained on the PCA-transformed data.
4. **Evaluation** — Performance is assessed via classification report, confusion matrix heatmap, and 5-fold cross-validation.
5. **Biomarker Identification** — The top 10 genes contributing most to PC1 are extracted and visualized as candidate biomarkers.

---

## Results

The model achieves strong classification performance across all 5 cancer types, validated through 5-fold cross-validation. Key outputs include:

- **Classification report** (per-class precision, recall, F1-score)
- **Confusion matrix heatmap** — visualizes where misclassifications occur
- **Cross-validation accuracy** — mean and standard deviation across 5 folds
- **Top 10 biomarker genes** — highest-loading genes on PC1

---

## Setup

### Prerequisites

- Python 3.9+
- Jupyter Notebook or JupyterLab

### Install dependencies

```bash
pip install ucimlrepo pandas scikit-learn seaborn matplotlib numpy
```

### Dataset

Download the TCGA Pan-Cancer HiSeq dataset and place the `.tar.gz` file in the project root:

```
TCGA-PANCAN-HiSeq-801x20531.tar.gz
```

You can obtain it from the [UCI ML Repository](https://archive.ics.uci.edu/dataset/401/gene+expression+cancer+rna+seq) or via the `ucimlrepo` package (see the notebook).

### Run

```bash
jupyter notebook Cancer_types_model.ipynb
```

---

## Project Structure

```
.
├── Cancer_types_model.ipynb      # Main notebook
├── TCGA-PANCAN-HiSeq-801x20531.tar.gz   # Raw dataset (download separately)
└── cancer_data/                  # Extracted data (auto-generated)
    └── TCGA-PANCAN-HiSeq-801x20531/
        ├── data.csv
        └── labels.csv
```

---

## Tech Stack

- **pandas** — data loading and manipulation
- **scikit-learn** — preprocessing, PCA, Random Forest, evaluation metrics
- **seaborn / matplotlib** — confusion matrix and biomarker visualizations
- **ucimlrepo** — dataset retrieval
- **tarfile** — dataset extraction

---

## License

This project is open source and available under the [MIT License](LICENSE).

The TCGA dataset is publicly available for research use. Please cite the original data source if you use it in published work.
