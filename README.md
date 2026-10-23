# BT4012-Kaggle-Competition

## Project Overview

This project compares different machine learning models for Bitcoin transaction fraud detections. The aim is to find the most suited model/models. The data comes from the online Kaggle competition website.

## Repository Contents

- `model_1.ipynb`: Main notebook containing data preparation, feature engineering, model training, evaluation and submission-file generation for the first selected model.
- `model_2.ipynb`: Main notebook containing data preparation, feature engineering, model training, evaluation and submission-file generation for the second selected model.
- `evaluation.ipynb`: Notebook with all models' evaluation metrics.
- `requirements.txt`: Required Python packages and their versions.
- `data/README.md`: Instructions for downloading and organising the data.

## Approach

### Feature Engineering

The model inputs contain 200 features:

- 165 original transaction features.
- 5 graph features: in-degree, out-degree, total degree, PageRank and approximate betweenness centrality.
- 30 neighbour-average features calculated from `feat_1` to `feat_30`.

Approximate betweenness uses up to 256 sampled source nodes with a random seed of `42`.

Neighbour averages use feature values from labelled training transactions, without averaging their labels. Both incoming and outgoing neighbours are considered. Transactions without eligible neighbours receive zero values.

### Model Comparison

I compare five models:

- Logistic Regression
- Decision Tree
- Random Forest
- LightGBM (Ensemble)
- HistGradientBoosting (Ensemble)

All models use the same five stratified cross-validation folds of the original labelled data. Median imputation, scaling and SMOTE are fitted separately within each training fold.

This cross-validation includes the earlier validation subset, so it is an additional model comparison rather than an independent final test.

Graph features are constructed before splitting the data and may include information from validation nodes, but not their target labels. The evaluation therefore assumes that the graph and node features are available together.

## How to Run

1. Download or clone this repository.
2. Use Python.
3. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Download the competition data from the Kaggle website and place it in `data/`.
5. Open `model_1.ipynb`, `model_2.ipynb` in a Jupyter-compatible environment (e.g. VS Code).
6. Restart the notebook kernel and run all cells from top to bottom.

Running the notebook will generate the competition submission file in the repository’s root directory.

## Reproducibility

Package versions are listed in `requirements.txt`. Random seeds used for data splitting, resampling and model training are recorded in the notebook.
