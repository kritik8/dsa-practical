# IT-411 Data Science and Analytics — Practicals (2026–27)

Jupyter notebook solutions for Experiments 1–13 in the IIIT Bhopal IT-411 Data Science and Analytics Practical Manual 2026–27. Experiment 14 (MongoDB) is intentionally outside this implementation. Completed notebooks are self-contained, use fixed random seeds, and preserve real outputs from fresh-kernel execution.

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
| `datasets/breast-cancer.csv` | Exp 11 | Kaggle *Breast Cancer Wisconsin (Diagnostic)*; compatible CSV used for the metric comparison | CC BY 4.0 (UCI origin) |
| `datasets/spam.csv` | Exp 5 | Kaggle *SMS Spam Collection* ([UCI](https://archive.ics.uci.edu/dataset/228/sms-spam-collection)) | CC BY 4.0 (UCI origin) |
| `datasets/WineQT.csv` | — (not required) | Kaggle *Wine Quality*; kept because Exp 8 uses the **UCI Wine** dataset via `sklearn.datasets.load_wine()` instead | see source page |
| `datasets/penguins.csv` | Exp 13 | Palmer Penguins CSV extracted from supplied `archive (3).zip`; official CSV URL is the fallback | CC0-like public repo; see source |
| `datasets/mnist/` | Exp 9 | IDX files extracted locally from supplied `archive (2).zip`; ignored by Git because of their size; Keras loader is the fallback | see Keras docs |
| CIFAR-10 | Exp 10 | Supplied `data_batch_1.zip` contains only one training batch; the complete dataset is loaded from Keras | see Keras docs |

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
| 9 | Neural Network | [`notebooks/exp09_neural_network.ipynb`](notebooks/exp09_neural_network.ipynb) | MNIST (supplied IDX files) | ✅ done |
| 10 | Image Classification using CNN | [`notebooks/exp10_cnn_image_classification.ipynb`](notebooks/exp10_cnn_image_classification.ipynb) | CIFAR-10 (Keras; supplied archive incomplete) | ✅ done |
| 11 | Performance Metrics | [`notebooks/exp11_performance_metrics.ipynb`](notebooks/exp11_performance_metrics.ipynb) | Breast Cancer (local CSV) | ✅ done |
| 12 | k-Means Clustering | [`notebooks/exp12_kmeans_clustering.ipynb`](notebooks/exp12_kmeans_clustering.ipynb) | Iris (local CSV) | ✅ done |
| 13 | Hierarchical Clustering | [`notebooks/exp13_hierarchical_clustering.ipynb`](notebooks/exp13_hierarchical_clustering.ipynb) | Palmer Penguins (supplied CSV) | ✅ done |
| 14 | NoSQL using MongoDB | — | MongoDB Atlas sample | Out of scope |

## How to run the notebooks

Open them in Jupyter (run from the project root so `datasets/` resolves):

```powershell
jupyter lab
# or, headless — executes a copy with all outputs regenerated:
jupyter nbconvert --to notebook --execute --inplace notebooks/exp13_hierarchical_clustering.ipynb
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
- [x] Experiment 9 — Neural Network (MNIST)
- [x] Experiment 10 — CNN (CIFAR-10)
- [x] Experiment 11 — Performance Metrics
- [x] Experiment 12 — k-Means Clustering
- [x] Experiment 13 — Hierarchical Clustering
- Experiment 14 — MongoDB (intentionally out of scope)

## Results (Experiments 1–13)

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
| 9 | MNIST neural network: **97.00%** test accuracy, **0.0994** test loss after 5 epochs |
| 10 | CIFAR-10 CNN: **70.71%** test accuracy, **0.8756** test loss after 10 epochs (CPU) |
| 11 | Logistic Regression: **98.25%** accuracy and **0.9954** AUC; Decision Tree: **92.11%** accuracy and **0.9163** AUC |
| 12 | Iris k-Means (k=3): **0.4590** silhouette, **0.6201** adjusted Rand index |
| 13 | Penguins hierarchical clustering: Ward linkage best, **0.9159** adjusted Rand index |

Full write-ups with evidence: [`reports/observations.md`](reports/observations.md).
