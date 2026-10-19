# IT-411 Data Science and Analytics — Practicals (2026–27)

Jupyter notebook solutions for the 14 experiments in the IIIT Bhopal IT-411 Data Science and Analytics Practical Manual 2026–27. All notebooks are self-contained, use fixed random seeds, and have been executed end-to-end from a fresh kernel with their real outputs saved.

## Project structure

```
dsa-practical/
├── datasets/                  # local dataset files (CSV)
├── notebooks/                 # one executed notebook per experiment
│   ├── exp01_eda.ipynb
│   ├── exp02_data_visualization.ipynb
│   ├── ...                    # expNN_<topic>.ipynb
│   └── exp08_pca_wine.ipynb
├── outputs/
│   ├── figures/               # exported plots, named expNN_<topic>.png
│   └── results/               # exported metric tables, named expNN_<topic>.csv
├── reports/observations.md    # observations & conclusions per experiment
├── DSA_IT-411_Practical_Experiments.pdf   # practical manual
├── requirements.txt
├── README.md
└── .gitignore
```

Naming convention: every notebook is `expNN_<topic>.ipynb`, and every exported figure/table carries the same `expNN_` prefix so artifacts of one experiment stay easy to find.

## Setup

Requires **Python 3.12** (tested on 3.12.3).

```powershell
# optional: create a virtual environment
python -m venv .venv
.\.venv\Scripts\Activate.ps1

pip install -r requirements.txt
```

Core dependencies (Experiments 1–8, 11–13): numpy, pandas, scikit-learn, matplotlib, seaborn, scipy. TensorFlow (Experiments 9–10) is a large download — install it only when you reach those experiments. pymongo (Experiment 14) additionally requires a MongoDB Atlas account or local MongoDB server.

## Datasets

All small datasets are stored in `datasets/` (extracted from the course-provided archives) so notebooks run offline.

| File | Used in | Source | Licence |
|---|---|---|---|
| `datasets/titanic_data.csv` | Exp 1, 6, 7 | Kaggle *Titanic* train CSV (891 rows); same data as [seaborn-data titanic.csv](https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv) | Open Database License (ODbL) on Kaggle |
| `datasets/iris.csv` | Exp 2, 12 | [UCI Iris](https://archive.ics.uci.edu/dataset/53/iris) | CC BY 4.0 (UCI) |
| `datasets/california_housing.csv` | — (kept, unused) | Kaggle *California Housing*; Exp 3 uses the scikit-learn built-in `fetch_california_housing()` as the manual specifies (no duplicate needed) | see source page |
| `datasets/breast-cancer.csv` | — (kept, unused) | Kaggle *Breast Cancer Wisconsin (Diagnostic)*; Exp 4/11 use the scikit-learn built-in `load_breast_cancer()` as the manual specifies | CC BY 4.0 (UCI origin) |
| `datasets/spam.csv` | Exp 5 | Kaggle *SMS Spam Collection* ([UCI](https://archive.ics.uci.edu/dataset/228/sms-spam-collection)) | CC BY 4.0 (UCI origin) |
| `datasets/WineQT.csv` | — (not required) | Kaggle *Wine Quality*; kept because Exp 8 uses the **UCI Wine** dataset via `sklearn.datasets.load_wine()` instead | see source page |
| `datasets/penguins.csv` | Exp 13 (planned) | [seaborn-data penguins.csv](https://raw.githubusercontent.com/mwaskom/seaborn-data/master/penguins.csv) | CC0-like public repo; see source |
| MNIST, CIFAR-10 | Exp 9, 10 (planned) | Auto-downloaded by `keras.datasets` on first run | see Keras docs |

## Notebook index

| # | Experiment | Notebook | Dataset | Status |
|---|---|---|---|---|
| 1 | Exploratory Data Analysis (EDA) | [`notebooks/exp01_eda.ipynb`](notebooks/exp01_eda.ipynb) | Titanic | ✅ done |
| 2 | Data Visualization | [`notebooks/exp02_data_visualization.ipynb`](notebooks/exp02_data_visualization.ipynb) | Iris | ✅ done |
| 3 | Linear, Ridge and Lasso Regression | [`notebooks/exp03_regression.ipynb`](notebooks/exp03_regression.ipynb) | California Housing (built-in) | ✅ done |
| 4 | SVM and kNN | [`notebooks/exp04_svm_knn.ipynb`](notebooks/exp04_svm_knn.ipynb) | Breast Cancer (built-in) | ✅ done |
| 5 | Naive Bayes — Text Classification | [`notebooks/exp05_naive_bayes_spam.ipynb`](notebooks/exp05_naive_bayes_spam.ipynb) | SMS Spam | ✅ done |
| 6 | Decision Tree and Random Forest | [`notebooks/exp06_decision_tree_random_forest.ipynb`](notebooks/exp06_decision_tree_random_forest.ipynb) | Titanic | ✅ done |
| 7 | Feature Engineering | [`notebooks/exp07_feature_engineering.ipynb`](notebooks/exp07_feature_engineering.ipynb) | Titanic | ✅ done |
| 8 | Principal Component Analysis | [`notebooks/exp08_pca_wine.ipynb`](notebooks/exp08_pca_wine.ipynb) | Wine (UCI, built-in) | ✅ done |
| 9 | Neural Network | — | MNIST (Keras) | ⬜ pending |
| 10 | Image Classification using CNN | — | CIFAR-10 (Keras) | ⬜ pending |
| 11 | Performance Metrics | — | Breast Cancer | ⬜ pending |
| 12 | k-Means Clustering | — | Iris | ⬜ pending |
| 13 | Hierarchical Clustering | — | Palmer Penguins | ⬜ pending |
| 14 | NoSQL using MongoDB | — | MongoDB Atlas sample | ⬜ pending |

## How to run the notebooks

Open them in Jupyter (run from the project root so `datasets/` resolves):

```powershell
jupyter lab
# or, headless — executes a copy with all outputs regenerated:
jupyter nbconvert --to notebook --execute --inplace notebooks/exp08_pca_wine.ipynb
```

Each notebook also works when launched from inside `notebooks/` (paths auto-detect). Execution is deterministic: `random_state=42` is used for every split/model, and scalers/vectorizers are fit on training data only.

## Progress checklist

- [x] Experiment 1 — EDA (Titanic)
- [x] Experiment 2 — Data Visualization (Iris)
- [x] Experiment 3 — Linear / Ridge / Lasso (California Housing)
- [x] Experiment 4 — SVM and kNN (Breast Cancer)
- [x] Experiment 5 — Naive Bayes text classification
- [x] Experiment 6 — Decision Tree and Random Forest
- [x] Experiment 7 — Feature Engineering
- [x] Experiment 8 — PCA
- [ ] Experiment 9 — Neural Network (needs TensorFlow)
- [ ] Experiment 10 — CNN (needs TensorFlow)
- [ ] Experiment 11 — Performance Metrics
- [ ] Experiment 12 — k-Means Clustering
- [ ] Experiment 13 — Hierarchical Clustering (needs `penguins.csv` download)
- [ ] Experiment 14 — MongoDB (needs Atlas connection string)

## Results so far (Experiments 1–8)

| Exp | Key metrics |
|---|---|
| 1 | 891 passengers, 38.4% survived; female **74.2%** vs male **18.9%**; class 1 **63.0%** → class 3 **24.2%**; Age 19.9% missing (median-filled), Cabin 77% missing (dropped) |
| 2 | Petal length/width separate species almost perfectly (setosa fully isolated ≤ 1.9 cm vs others ≥ 3.0 cm); sepal width weakest |
| 3 | Linear Regression R² **0.576**; Ridge stable across alphas; Lasso: alpha 0.01 slightly better (**R² 0.582**, 7 features), **alpha ≥ 1 → all coefficients zero** |
| 4 | Best: **kNN (k=3) and SVM-RBF tie at 98.25%**; kNN k=1 worst (93.9%); best-model confusion matrix: 0 false benign, 2 missed malignant |
| 5 | Accuracy **96.2%**; spam precision **1.00**, spam recall **0.72**; 4/4 hand-written messages correct |
| 6 | Random Forest **82.7%** > best single tree **79.9%** (overfits: 98.2% train); top feature **Fare** (0.333) |
| 7 | Baseline **78.8%** vs engineered **78.2%** (≈1 passenger; no reliable gain — `is_alone` was the best new feature) |
| 8 | 10 PCs (of 13) retain **96.2%** variance; accuracy **97.2%** = full-feature **97.2%** |

Full write-ups with evidence: [`reports/observations.md`](reports/observations.md).
