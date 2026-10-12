# BT4012-Kaggle-Competition

## Project Overview

This project compares different machine learning models for Bitcoin transaction fraud detections. The aim is to find the most suited model.

## Repository Contents

- `model.ipynb`: Main notebook containing data preparation, feature engineering, model training, evaluation and submission-file generation.
- `evaluation.ipynb`: Notebook with all models' evaluation metrics.
- `requirements.txt`: Required Python packages and their versions.

## Data

The data comes from the [competition name](INSERT_COMPETITION_URL).

## Approach

### Feature Engineering

The model inputs contain 200 features:

- 165 original transaction features.
- Five graph features: in-degree, out-degree, total degree, PageRank and approximate betweenness centrality.
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
2. Use Python [version used].
3. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Download the competition data from the Kaggle website and place it in `data/`.
5. Open `model.ipynb` in [Jupyter / your tested environment].
6. Restart the notebook kernel and run all cells from top to bottom.

The notebook saves the competition submission to `[output path/filename]`.

Approximate runtime: [runtime and hardware used].

## Results

The competition evaluation metric is **[metric name]**, where **[higher/lower]** is better.

| Model | Evaluation setting | Score |
|---|---|---|
| Competition baseline | [Evaluation setting] | [Score] |
| Final model: [name] | [Same evaluation setting] | [Score] |

Additional model-comparison results are shown in the notebook. Cross-validation results and Kaggle leaderboard results are reported separately because they use different evaluation data.

## Reproducibility

Package versions are listed in `requirements.txt`. Random seeds used for data splitting, resampling and model training are recorded in the notebook.

Final model: [model name and configuration, or location in notebook].

Kaggle submission score: [score and whether it is from the public or private leaderboard].
