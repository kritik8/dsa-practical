# IT-411 Data Science and Analytics — Experiment Observations

Practical Manual 2026–27, IIIT Bhopal. One section per experiment; each entry summarises the actual run of the corresponding notebook (all notebooks executed end-to-end from a fresh kernel with fixed seeds).

> Status: Experiments 1–8 completed (Batches 1 and 2). Experiments 9–14 pending.

---

## Experiment 1 — Exploratory Data Analysis (EDA)
**Notebook:** `notebooks/exp01_eda.ipynb` · **Dataset:** `datasets/titanic_data.csv` (891 passengers)

- Shape 891 × 12; missing values: Age 19.9% (filled with median), Cabin 77.1% (dropped), Embarked 0.22% (filled with mode) → 0 missing after handling.
- **Survival by sex: female 74.2% vs male 18.9%** — the "women and children first" protocol is plainly visible.
- **Survival by class: 1st 63.0% → 2nd 47.3% → 3rd 24.2%** (Survived–Pclass correlation −0.338); first-class mean fare 84.15 vs 13.68 for third (Pclass–Fare correlation −0.549).
- Fare correlates +0.257 with survival; Age is almost uncorrelated (−0.065). Overall survival: 38.4%.

## Experiment 2 — Data Visualization
**Notebook:** `notebooks/exp02_data_visualization.ipynb` · **Dataset:** `datasets/iris.csv` (150 flowers, balanced 50/50/50)

- **Petal features separate species best**: setosa is fully isolated in the petal scatter (setosa petal length ≤ 1.9 cm vs ≥ 3.0 cm for others; petal width ≤ 0.6 vs ≥ 1.0); versicolor/virginica partially overlap (4.5–5.1 cm crossing).
- Histograms: sepal width roughly bell-shaped; petal length/width bimodal (setosa vs the rest).
- Per-species means (petal length/width): setosa 1.46/0.24, versicolor 4.26/1.33, virginica 5.55/2.03 cm. Sepal width means barely differ (3.42/2.77/2.97) — the weakest discriminator.
- Box plots and the pair plot confirm the same structure: any chart with petal length vs width separates the classes almost perfectly.

## Experiment 3 — Linear Regression, Ridge and Lasso Regression
**Notebook:** `notebooks/exp03_regression.ipynb` · **Dataset:** California Housing via `fetch_california_housing()` (20,640 × 8; built-in per manual)

- 80:20 split (16,512/4,128), StandardScaler fit on train only. Linear Regression: **test MSE 0.556, R² 0.576**.
- **Ridge is insensitive** to alpha ∈ [0.01, 10] (MSE 0.556–0.559): few features, little overfitting to correct. Top coefficients: MedInc +0.85, Latitude −0.90, Longitude −0.87 (income and location dominate).
- **Lasso is highly alpha-sensitive**: alpha 0.01 keeps 7/8 features and slightly **beats** plain regression (R² 0.582); alpha 0.1 keeps only 3 features (R² 0.481); **alpha ≥ 1 drives every coefficient to exactly zero** (R² ≈ 0, mean-only predictor).
- Conclusion: Ridge = safe default; Lasso = real feature selection whose alpha must be tuned carefully.

## Experiment 4 — Support Vector Machine (SVM) and kNN
**Notebook:** `notebooks/exp04_svm_knn.ipynb` · **Dataset:** Breast Cancer Wisconsin via `load_breast_cancer()` (569 × 30; built-in per manual)

- kNN test accuracy: k=1 **93.9%**, k=3 **98.25%**, k=5 95.6%, k=7 97.4%, k=9 97.4% (k=1 overfits to noisy points; too-large k dilutes the boundary).
- SVM: RBF kernel **98.25%**, linear kernel 97.4% — slightly non-linear boundary; scaler fit on train only.
- Best: **kNN (k=3)** and SVM-RBF tie at 98.25%; tie-break selected kNN (k=3). Its confusion matrix: **0 benign flagged malignant, 2 malignant missed** (40/42 malignant detected).
- For a screening tool the false-benign count (missed cancers) matters most — both top models missed at most 2.

---

## Experiment 5 — Naive Bayes: Text Classification
**Notebook:** `notebooks/exp05_naive_bayes_spam.ipynb` · **Dataset:** `datasets/spam.csv` (5,572 SMS: 4,825 ham / 747 spam)

- TF-IDF (8,126 terms) + MultinomialNB, stratified 80:20 split → **test accuracy 96.2%** on 1,115 messages.
- **Spam precision 1.00** (0 ham falsely flagged) but **spam recall 0.72** (42 of 149 spam missed).
- With ~87% of messages being ham, accuracy alone hides the miss rate; for a spam filter, recall is the costlier metric. Class weighting or a lower threshold would trade precision for recall.
- All 4 hand-written test messages (2 spam, 2 ordinary) classified correctly.

## Experiment 6 — Decision Tree and Random Forest
**Notebook:** `notebooks/exp06_decision_tree_random_forest.ipynb` · **Dataset:** `datasets/titanic_data.csv` (891 rows; 177 missing Ages filled with train median)

- Tree depth comparison (test accuracy): depth 2 = 76.0%, **depth 3 = 79.3%**, depth 4 = 77.7%, depth 5 = 76.5%, unlimited = 79.9% (but 98.2% train → overfitting).
- **Random Forest (100 trees) = 82.7%**, beating every single tree — averaging reduces variance.
- Feature importances: **Fare 0.333 > Sex 0.288 > Age 0.284 > Pclass 0.095**; Sex is the root split of the visualised depth-3 tree.

## Experiment 7 — Feature Engineering
**Notebook:** `notebooks/exp07_feature_engineering.ipynb` · **Dataset:** `datasets/titanic_data.csv` (same split as Exp 6 for a fair comparison)

- Engineered `family_size`, `is_alone`, `age_group`; one-hot encoded Sex/Embarked/age groups; scaled Age/Fare (train-only fit); SelectKBest(k=8) from 12 candidates.
- ANOVA ranking: `Sex_male` F = 306.6 dominates; among new features **`is_alone` ranked 4th (F = 34.6)**, while `family_size` ranked near the bottom (F = 0.52) — the alone flag already contains its signal.
- **Baseline 78.8% vs engineered 78.2%** — a −0.6% change ≈ 1 passenger on the 179-person test set, i.e. within noise. Honest lesson: new features are not automatically better and must always be validated against a baseline.

## Experiment 8 — Principal Component Analysis (PCA)
**Notebook:** `notebooks/exp08_pca_wine.ipynb` · **Dataset:** UCI Wine via `sklearn.datasets.load_wine()` (178 × 13, 3 classes)

- PC1 explains **36.2%**, PC2 **19.2%** (55.4% combined). On the PC1–PC2 scatter, class_0 and class_2 sit at opposite ends of PC1 (mean +2.3 vs −2.8) and class_1 separates along PC2 (mean −1.6).
- **10 of 13 components** are needed for ~95% cumulative variance (94.2% at PC9, 96.2% at PC10) — the features are moderately correlated.
- Logistic Regression: **97.2% with all 13 scaled features vs 97.2% with the first 10 PCs** — discarding 3 low-variance components cost no accuracy.

---

## Pending experiments

| # | Experiment | Status |
|---|---|---|
| 9 | Neural Network (MNIST) | Pending (Batch 3; needs TensorFlow) |
| 10 | Image Classification using CNN | Pending (Batch 3; needs TensorFlow) |
| 11 | Performance Metrics | Pending (Batch 3) |
| 12 | k-Means Clustering | Pending (Batch 4) |
| 13 | Hierarchical Clustering | Pending (Batch 4; needs penguins.csv download) |
| 14 | NoSQL using MongoDB | Pending (Batch 4; needs MongoDB Atlas connection string) |
