# DATA-SCI-PRACTICE

A learning time capsule preserving my first Data Science notebook, predicting smartphone addiction with K-Nearest Neighbors (`FirstOFMany.ipynb` and `Smartphone.csv` are kept untouched).

[ภาษาไทย](README_TH.md) | [Dataset on Kaggle](https://www.kaggle.com/datasets/jayjoshi37/smartphone-usage-and-addiction-prediction)

## Requirements

The notebook imports Python 3 with `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, and `mlxtend`.

## Setup

Create a virtual environment and install the dependencies used in `FirstOFMany.ipynb`:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install pandas numpy matplotlib seaborn scikit-learn mlxtend jupyter
```

## Run the notebook

Start Jupyter in the repository root so `FirstOFMany.ipynb` can read `Smartphone.csv`:

```bash
jupyter notebook FirstOFMany.ipynb
```

## How the notebook works

1. Loads `Smartphone.csv` (7,500 rows, 16 columns) and checks class balance in `addicted_label` (5,308 addicted, 2,192 not addicted).
2. Fills missing values with `0`, maps `gender`, `stress_level`, `academic_work_impact`, and `addiction_level` to integers, and drops `transaction_id` and `user_id`.
3. Samples 2,000 rows from each class (`random_state=42`) into a balanced 4,000-row subset.
4. Drops `addicted_label` and `addiction_level` (correlation `0.9017` with the target) to leave 12 input features, then scales them with `MinMaxScaler`.
5. Splits the data 80/20 (`test_size=0.2`, `random_state=42`), trains `KNeighborsClassifier(n_neighbors=41)`, and tests `k` from 1 to 110 on the test split to plot error rates.

## Results

At `k=41`, the model reaches `0.8662` accuracy on the 800-row test split.

| Output | Description |
|---|---|
| [Gender count](docs/images/01_gender_count.png) | Distribution of `gender` across all 7,500 rows |
| [Correlation heatmap](docs/images/02_correlation_heatmap.png) | Pairwise correlation across numeric columns |
| [Confusion matrix](docs/images/03_confusion_matrix_knn41.png) | Test predictions for `KNeighborsClassifier(n_neighbors=41)` |
| [Error rate vs K](docs/images/04_error_rate_vs_k.png) | Test error rate across `k=1..110` |

## Project layout

- `FirstOFMany.ipynb` original notebook preserved without edits
- `Smartphone.csv` dataset with 7,500 records
- `docs/images/` plots captured from running `FirstOFMany.ipynb`
- `README.md` and `README_TH.md` documentation in English and Thai
