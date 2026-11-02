# IT-411 Practicals — Updated Experiment Briefs, Observations, and Results

This document is the detailed authoring reference for the **updated 15-experiment list**. Each brief is organized to support the faculty-required lab-file sections: **Aim, Libraries, Theory, Procedure/Implementation/Code, Observation, and Result**.

## Notebook and evidence status

The repository now contains all 15 notebooks in the faculty's updated order. Each notebook has been executed top-to-bottom, includes Aim, Libraries, Theory, Procedure/Implementation/Code, Observation, and Result sections, and saves relevant figures or result tables where applicable. Notebook code is the runnable implementation; the notes below summarize its observed run.

All reported values below are measured from the saved notebook outputs and result files in this repository. They are reproducibility examples, not required scores. The selected datasets do **not** establish that a dataset is unique among candidates. Follow the per-candidate uniqueness guidance in [`../README.md`](../README.md#dataset-uniqueness-requirement): register each selected dataset with the instructor, cite its source/license, and obtain approval before submission. The CUB bird archive and extracted subset are local-only and are not committed.

---

<a id="experiment-1"></a>
## Experiment 1 — Exploratory Data Analysis (EDA)

**Aim**
Explore a real-world dataset using Python: inspect its structure, data types, missing values, distributions, relationships, and potential data-quality issues.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, Seaborn. Optional: SciPy for statistical summaries.

**Theory**
EDA combines numerical summaries and visual inspection to understand data before modeling. It can reveal invalid values, missingness, outliers, skew, class imbalance, and associations. Correlation is descriptive and does not establish causation; preprocessing decisions should be justified and documented.

**Procedure / implementation / code blueprint**
1. Select and cite a candidate-approved real-world CSV; record its source, license, dimensions, and meaning of each important column.
2. Load with `pd.read_csv`; display `head`, `shape`, `dtypes`, `info`, and descriptive statistics.
3. Check duplicate rows, missing counts/percentages, unique values, category frequencies, and impossible values.
4. Choose defensible missing-data and outlier handling; preserve the raw DataFrame or describe every transformation.
5. Plot numeric distributions, category counts, and a correlation heatmap for appropriate numeric columns.
6. Summarize findings in plain language; save the figures with axis labels, units, and captions.

**Observation**
The executed Titanic example contains 891 rows and 12 columns. Overall survival was 38.4%; survival was 74.2% among females and 18.9% among males. Age has 177 missing values in the source data; the notebook reports these and saves a correlation heatmap to `outputs/figures/exp01_correlation_matrix.png`. See `notebooks/exp01_eda.ipynb`.

**Result**
Write a conclusion based on the actual EDA: what the data contains, which quality concerns were found, how they were treated, and which patterns merit follow-up. Do not claim causal conclusions from plots or correlation.

---

<a id="experiment-2"></a>
## Experiment 2 — Visualization of Data

**Aim**
Communicate dataset patterns using charts, histograms, and scatter plots in Python.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, Seaborn.

**Theory**
Charts encode values using position, length, color, and shape. Histograms show the distribution of a numeric variable; bar charts compare categories; scatter plots show relationships between two numeric variables. Correct scales, labels, units, legends, and a suitable aggregation are essential to avoid misleading displays.

**Procedure / implementation / code blueprint**
1. Load a registered dataset that has at least two numeric features and, preferably, a categorical grouping variable.
2. Inspect types and missing values; select a small number of questions that plots can answer.
3. Create and label a histogram (distribution), bar/count chart (category comparison), and scatter plot (relationship); use hue only when it clarifies a grouping.
4. Optionally add a box plot or pair plot for a compact multivariate view.
5. Interpret patterns and limitations, then export high-resolution figures with descriptive filenames.

**Observation**
The executed Iris example generates histograms, categorical feature means, box plots, a petal scatter plot, and a pair plot under `outputs/figures/exp02_*.png`. Use the plotted distributions and species overlap as the evidence for the written interpretation; Iris is only a demonstration dataset, not a candidate reservation. See `notebooks/exp02_data_visualization.ipynb`.

**Result**
State which visualization best answered each question and what the plots show. Avoid treating a visible association as proof of causation.

---

<a id="experiment-3"></a>
## Experiment 3 — Linear, Ridge, and Lasso Regression

**Aim**
Fit and compare Linear Regression, Ridge Regression, and Lasso Regression for a continuous target.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, scikit-learn (`train_test_split`, preprocessing, linear models, metrics).

**Theory**
Ordinary least squares minimizes squared residuals. Ridge adds an L2 penalty and shrinks coefficients; Lasso adds an L1 penalty and can set coefficients to zero. Larger regularization strength (`alpha`) increases shrinkage. Feature scaling is important for penalized regression. Preprocessing must be fitted on training data only to prevent leakage.

**Procedure / implementation / code blueprint**
1. Choose a licensed regression dataset; identify a continuous target and justify the input features.
2. Inspect missingness, split into train and test sets with a fixed seed, and scale numeric features using a train-fitted pipeline.
3. Fit `LinearRegression`, `Ridge`, and `Lasso`; evaluate using MAE, MSE/RMSE, and R².
4. Repeat Ridge/Lasso over a documented `alpha` grid; plot score or coefficient magnitude versus `alpha`.
5. Compare model quality and coefficient changes; keep the test set for final evaluation.

**Observation**
On the executed California Housing split, Linear Regression and Ridge achieved test R² about 0.5758. The alpha sweep's best Lasso result was R² 0.5816 at α=0.01 (7 nonzero coefficients); at α≥1, Lasso set all coefficients to zero and R² fell to approximately 0. The comparison and sweep are saved in `outputs/results/exp03_*.csv`; the coefficient plot is `outputs/figures/exp03_coefficients_vs_alpha.png`. See `notebooks/exp03_regression.ipynb`.

**Result**
Conclude which model performed best on the selected data and explain the regularization trade-off. Do not choose a model from training scores alone.

---

<a id="experiment-4"></a>
## Experiment 4 — SVM and KNN Classifiers

**Aim**
Implement and compare Support Vector Machine (SVM) and k-Nearest Neighbors (KNN) classifiers.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, Seaborn, scikit-learn (preprocessing, model selection, SVM, neighbors, metrics).

**Theory**
KNN assigns a label based on nearby training observations; its result depends on distance scaling and the choice of `k`. SVM finds a maximum-margin decision boundary and can use kernels such as RBF for nonlinear boundaries. Both methods generally benefit from scaling. A stratified split preserves class proportions.

**Procedure / implementation / code blueprint**
1. Choose a registered labeled classification dataset; inspect the target balance and feature types.
2. Split with stratification and a fixed seed. Use a `Pipeline` so a `StandardScaler` is fitted only on training data.
3. Fit KNN across several justified `k` values and compare with linear and RBF SVM.
4. Report accuracy and per-class precision, recall, and F1; include a labeled confusion matrix.
5. Select the model using validation evidence and discuss error costs, not accuracy alone.

**Observation**
On the executed Breast Cancer split, KNN with k=3 and RBF SVM both reached 98.25% test accuracy. KNN accuracy varied across the tested k values (93.86%–98.25%). See `outputs/results/exp04_model_comparison.csv`, `outputs/figures/exp04_confusion_matrix.png`, and `notebooks/exp04_svm_knn.ipynb`.

**Result**
Name the best model under the selected evaluation criterion and explain the types of misclassification it makes.

---

<a id="experiment-5"></a>
## Experiment 5 — Naive Bayes for Text Classification

**Aim**
Use a Naive Bayes model to classify text into labeled categories.

**Libraries / software**
Python, Jupyter, pandas, NumPy, scikit-learn (text vectorizers, model selection, Naive Bayes, metrics); optionally NLTK only if a specific preprocessing step requires it.

**Theory**
Naive Bayes applies Bayes' theorem with a conditional-independence assumption between features. Text is converted into numeric features, commonly bag-of-words counts or TF-IDF. Multinomial Naive Bayes is a common baseline for nonnegative word counts. The model's simplicity and speed are useful, but the independence assumption is an approximation.

**Procedure / implementation / code blueprint**
1. Select a licensed, labeled text corpus; identify the text and target columns and inspect class balance.
2. Split into train/test (stratified where possible) before fitting a vectorizer.
3. Build a `Pipeline` with `TfidfVectorizer` or `CountVectorizer` and `MultinomialNB`; fit only on training text.
4. Evaluate accuracy, confusion matrix, per-class precision/recall/F1; inspect a few test predictions and errors.
5. Keep text cleaning minimal and reproducible; do not leak duplicate or near-duplicate messages across splits.

**Observation**
The executed SMS classifier achieved 96.23% accuracy. Spam precision was 1.00 and spam recall was 0.718. Its confusion matrix contains 966 true ham, 0 false spam, 42 missed spam, and 107 correctly detected spam messages. The figure and summary table are `outputs/figures/exp05_confusion_matrix.png` and `outputs/results/exp05_nb_metrics.csv`. See `notebooks/exp05_naive_bayes_spam.ipynb`.

**Result**
Explain whether the classifier is more affected by false positives or false negatives and relate that trade-off to the application's needs.

---

<a id="experiment-6"></a>
## Experiment 6 — Decision Tree and Random Forest

**Aim**
Train and compare a Decision Tree and Random Forest model for a classification task.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, scikit-learn (imputation/encoding, tree models, metrics, plotting).

**Theory**
A decision tree recursively partitions feature space using impurity criteria such as Gini impurity or entropy. Unrestricted trees can overfit. A random forest averages many trees trained with bootstrap samples and randomized feature subsets, generally reducing variance. Feature importance is useful for exploration but can be biased and does not imply causation.

**Procedure / implementation / code blueprint**
1. Select a candidate-approved labeled tabular dataset; identify categorical/numeric fields and target.
2. Split data before fitting imputers/encoders; use a preprocessing pipeline where required.
3. Train a shallow tree for visualization and compare tree depths or pruning settings.
4. Fit a Random Forest with documented tree count and seed; evaluate on the same held-out split.
5. Compare accuracy and class-wise metrics; plot the small tree and feature importances with caveats.

**Observation**
The executed Titanic comparison used a 712/179 train/test split. A depth-3 decision tree achieved 79.33% test accuracy, and the 100-tree Random Forest achieved 82.68%. The unlimited tree reached 98.17% training accuracy but only 79.89% test accuracy, illustrating overfitting. Fare, sex, and age were the leading forest features in this run. See `outputs/figures/exp06_*.png` and `notebooks/exp06_decision_tree_random_forest.ipynb`.

**Result**
Summarize which model generalizes better on this split and whether tree complexity shows evidence of overfitting.

---

<a id="experiment-7"></a>
## Experiment 7 — Dimensionality Reduction Using PCA

**Aim**
Reduce numeric feature dimensionality using Principal Component Analysis (PCA), visualize the transformed data, and quantify retained variance.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, scikit-learn (`StandardScaler`, `PCA`; optionally a classifier for a controlled comparison).

**Theory**
PCA transforms correlated variables into orthogonal components ordered by decreasing explained variance. Components are linear combinations of the original features. PCA is scale-sensitive; standardize features when units/ranges differ. PCA is unsupervised and high explained variance does not guarantee improved prediction.

**Procedure / implementation / code blueprint**
1. Select a numeric dataset with multiple features; document any target label used only for plot coloring or later evaluation.
2. Split first if measuring predictive performance; fit imputation/scaling/PCA on training features only.
3. Fit PCA, report `explained_variance_ratio_` and its cumulative sum, and plot the first two components.
4. Select component count using a stated variance threshold or validation experiment.
5. If comparing predictive utility, train the same downstream model on original and reduced features using leakage-safe pipelines.

**Observation**
The executed Wine example retained 96.2% cumulative variance with 10 of 13 principal components. Logistic Regression achieved 97.22% test accuracy using either the 10 components or all 13 scaled features. New-numbered figures and comparison results are in `outputs/figures/exp07_*.png` and `outputs/results/exp07_accuracy_comparison.csv`; see `notebooks/exp07_pca.ipynb`.

**Result**
State the dimensionality reduction achieved and discuss information retained/lost; do not equate explained variance with classification accuracy.

**Diagram:** [PCA and ANN workflows](diagrams/pca_ann.mmd)

---

<a id="experiment-8"></a>
## Experiment 8 — Artificial Neural Network (ANN)

**Aim**
Implement and evaluate a feed-forward Artificial Neural Network in Python for a supervised classification task.

**Libraries / software**
Python 3.12, Jupyter, NumPy, Matplotlib, scikit-learn, and TensorFlow/Keras 2.21.0.

**Theory**
An ANN consists of connected layers of units. Each unit applies a weighted sum and activation function; training uses backpropagation and gradient-based optimization to reduce a loss function. Architecture, scaling, learning rate, and epochs affect learning. Validation data helps detect overfitting; the test set should be used only for final evaluation.

**Procedure / implementation / code blueprint**
1. Select a registered, labeled dataset appropriate for classification; state input and target shapes.
2. Split into train, validation, and test sets (stratified if appropriate); preprocess using training data only.
3. Define an input layer matching feature count, one or more hidden layers, and an output layer/loss suited to binary or multiclass labels.
4. Train with documented optimizer, batch size, epoch count, and seed; plot training and validation loss/accuracy.
5. Evaluate once on test data; report confusion matrix and class-wise metrics, and show example predictions.

**Observation**
The executed TensorFlow/Keras ANN trained on MNIST for five epochs and achieved 96.8% test accuracy with test loss 0.1014. Sample predictions and training curves are in `outputs/figures/exp08_*.png`; measured metrics are in `outputs/results/exp08_mnist_metrics.csv`. See `notebooks/exp08_ann.ipynb`.

**Result**
Explain whether the network learned effectively and whether validation curves suggest underfitting or overfitting. Include actual measured test results from the new run.

**Diagram:** [PCA and ANN workflows](diagrams/pca_ann.mmd)

---

<a id="experiment-9"></a>
## Experiment 9 — CNN for Bird Species Classification

**Aim**
Implement a Convolutional Neural Network (CNN) using Python to classify bird species from labeled images.

**Libraries / software**
Python, Jupyter, TensorFlow/Keras **or** PyTorch (choose one consistently); NumPy, Matplotlib, scikit-learn for stratified splitting and evaluation. Record CPU/GPU and package versions.

**Theory**
Convolution layers learn local image features using shared filters; pooling reduces spatial resolution. Transfer learning reuses a pretrained CNN feature extractor and adapts its classification head (and selected final layers) to the bird classes. Augmentation can improve robustness but must be restricted to training images. Image-level splits may not generalize to new individual birds or locations.

**Procedure / implementation / code blueprint**
1. Obtain a licensed bird-species image dataset, cite its source and license, record class counts, and verify image-label integrity.
2. Create train/validation/test splits by image source, individual, or location where possible to reduce leakage; preserve class balance.
3. Resize images to 160×160, preprocess them for MobileNetV2, and apply training-only random flip/rotation augmentation.
4. Freeze an ImageNet-pretrained MobileNetV2 feature extractor, train a softmax classification head, then fine-tune its final 20 layers at a low learning rate.
5. Train with early stopping; plot learning curves and evaluate on the untouched image-level test split.
6. Report per-species precision/recall/F1, confusion matrix, sample predictions, and known dataset limitations.

**Observation**
The executed CUB-200-2011 subset contains five species and 275 selected images: 176 train, 44 validation, and 55 test. MobileNetV2 transfer learning stopped after 10 total epochs and achieved test loss 0.1312 and accuracy 98.18%. See `outputs/results/exp09_bird_metrics.csv` and the sample, training-curve, and confusion-matrix figures `outputs/figures/exp09_*.png`. The subset is small and the split is by image rather than bird identity, so the high score should not be interpreted as generalization to unseen individuals. The source archive is downloaded locally and is not committed; see `notebooks/exp09_bird_species_cnn.ipynb`.

**Result**
State the measured test performance and discuss class imbalance, confusing species, image quality, and possible leakage/overfitting. Never invent accuracy before executing the notebook.

**Diagram:** [Bird CNN workflow](diagrams/bird_cnn.mmd)

---

<a id="experiment-10"></a>
## Experiment 10 — K-Means Clustering for Data Segmentation

**Aim**
Use K-Means to group observations into segments based on numeric feature similarity.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, scikit-learn (`StandardScaler`, `KMeans`, clustering metrics).

**Theory**
K-Means assigns observations to the nearest centroid and iteratively updates centroids to reduce within-cluster sum of squares (inertia). It requires `k` in advance, is sensitive to feature scale and initialization, and favors compact, roughly spherical clusters. Inertia decreases as `k` grows; use an elbow plot alongside other evidence, not as a definitive rule. Cluster IDs have no inherent semantic ordering.

**Procedure / implementation / code blueprint**
1. Select an approved numeric dataset; exclude identifiers and any target/ground-truth labels from fitting.
2. Impute and standardize appropriate features; justify the selected feature set.
3. Fit K-Means over a range of `k` values with multiple initializations and a fixed seed; plot inertia.
4. Select a candidate `k`, fit the final model, visualize clusters (PCA projection if needed), and profile each cluster in original units.
5. If true labels exist, use them only for post-fit evaluation (e.g., adjusted Rand index); also report silhouette score where valid.

**Observation**
The executed Iris clustering selected k=3, with inertia 140.97, silhouette 0.4590, and adjusted Rand index 0.6201. Elbow, PCA projection, contingency table, and metrics are saved under `outputs/figures/exp10_*.png` and `outputs/results/exp10_*.csv`. See `notebooks/exp10_kmeans_clustering.ipynb`.

**Result**
Describe segments using their feature profiles and discuss whether the cluster structure is useful and stable.

**Diagram:** [Clustering workflows](diagrams/clustering.mmd)

---

<a id="experiment-11"></a>
## Experiment 11 — Analysis and Implementation of Performance Metrics

**Aim**
Implement and analyze classification performance metrics in Python and explain how metric choice changes model evaluation.

**Libraries / software**
Python, Jupyter, NumPy, pandas, Matplotlib, scikit-learn (`confusion_matrix`, `classification_report`, ROC/AUC utilities).

**Theory**
For binary classification, a confusion matrix contains TP, TN, FP, and FN. Accuracy is `(TP+TN)/N`; precision is `TP/(TP+FP)`; recall/sensitivity is `TP/(TP+FN)`; specificity is `TN/(TN+FP)`; F1 is the harmonic mean of precision and recall. ROC curves show TPR versus FPR across thresholds; AUC summarizes ranking performance. Metrics must match class balance and error costs. Undefined denominators require explicit handling.

**Procedure / implementation / code blueprint**
1. Select a dataset and define the positive class before training; state why that class is important.
2. Split data once with stratification; train at least two classifiers or compare predictions from a supplied model.
3. Generate hard predictions and, when supported, probability/decision scores.
4. Compute the confusion matrix and metrics using scikit-learn; independently calculate key values from TP/TN/FP/FN and verify agreement.
5. Plot labeled confusion matrices and ROC curves; state the decision threshold and class ordering.

**Observation**
On the executed Breast Cancer split, Logistic Regression achieved 98.25% accuracy, malignant-class recall 97.62%, and AUC 0.9954. The Decision Tree reached 92.11% accuracy, 92.86% malignant recall, and AUC 0.9163. Manual metric calculations matched scikit-learn values. See `outputs/results/exp11_metric_comparison.csv`, `outputs/figures/exp11_*.png`, and `notebooks/exp11_performance_metrics.ipynb`.

**Result**
Identify the model preferred under the stated application costs. Explain why accuracy alone may conceal poor minority-class performance.

---

<a id="experiment-12"></a>
## Experiment 12 — Hierarchical Clustering and Dendrogram Analysis

**Aim**
Implement hierarchical clustering, construct dendrograms, and compare linkage strategies.

**Libraries / software**
Python, Jupyter, pandas, NumPy, Matplotlib, SciPy (`linkage`, `dendrogram`), scikit-learn preprocessing and clustering metrics.

**Theory**
Agglomerative hierarchical clustering begins with individual observations and repeatedly merges clusters. A linkage rule defines inter-cluster distance: single uses the nearest pair, complete the farthest pair, and Ward minimizes increases in within-cluster variance. A dendrogram visualizes merge order and distance; a horizontal cut determines cluster assignments. Scaling and distance choice affect results. A full dendrogram can be unreadable for large datasets.

**Procedure / implementation / code blueprint**
1. Select a manageable numeric dataset; document missing-value handling and exclude ID/target columns from clustering.
2. Standardize features; compute linkage matrices for suitable methods (e.g., single, complete, Ward; Ward requires Euclidean geometry).
3. Plot clearly labeled dendrograms; for large data, use a documented sample for display while stating what data the clustering used.
4. Choose a cut/cluster count with a stated rationale; derive cluster assignments and profile clusters.
5. Compare methods with silhouette and, if ground truth exists, external metrics such as ARI used only after clustering.

**Observation**
The executed Palmer Penguins linkage comparison achieved adjusted Rand indices of 0.9159 (Ward), 0.8949 (complete), and 0.6572 (single). Ward performed best for this split. Dendrograms, comparison plot, and contingency tables are saved under `outputs/figures/exp12_*.png` and `outputs/results/exp12_*.csv`. See `notebooks/exp12_hierarchical_clustering.ipynb`.

**Result**
Conclude which linkage produced the most useful/consistent groups for the chosen data and discuss dendrogram readability and sensitivity to scaling.

**Diagram:** [Clustering workflows](diagrams/clustering.mmd)

---

<a id="experiment-13"></a>
## Experiment 13 — Install Hadoop and Explore HDFS

**Aim**
Install/configure Hadoop in a supported environment and demonstrate basic Hadoop Distributed File System (HDFS) operations.

**Libraries / software**
Apache Hadoop distribution, Java runtime/development kit version supported by the selected Hadoop release, terminal/PowerShell or Linux shell, and a small sample text/CSV file. Hadoop's Java requirement is version-dependent; verify the official release documentation before setup.

**Theory**
HDFS stores large files as blocks distributed across a filesystem namespace. In a pseudo-distributed learning setup, NameNode and DataNode services run on one machine to demonstrate commands; this is not a production cluster. HDFS paths are distinct from local filesystem paths.

**Procedure / implementation / code blueprint**
1. Record OS, Java version, Hadoop version, installation source, and environment variables; follow the official guide for that exact platform/version.
2. Configure a local or pseudo-distributed mode only if supported; start required services and verify their status.
3. Demonstrate commands such as `hdfs dfs -mkdir`, `-put`/`-copyFromLocal`, `-ls`, `-cat`, `-get`/`-copyToLocal`, and `-rm`.
4. Use a small, non-sensitive file; show local and HDFS paths and verify content after upload/download.
5. Stop services cleanly and document platform-specific issues. Do not imply that one command sequence works identically on every OS.

**Observation**
The executed notebook used WSL Ubuntu 26.04, Temurin Java 17.0.21, and Hadoop 3.4.2 in a single-machine pseudo-distributed setup with one live DataNode. HDFS directory creation, upload, listing, read, download, and byte-for-byte round trip all succeeded. The notebook starts and stops daemons in its WSL workflow; this is not a multi-node deployment. See `notebooks/exp13_hadoop_hdfs.ipynb`.

**Result**
Summarize which HDFS operations succeeded and distinguish a single-machine learning configuration from a multi-node production cluster.

**Diagram:** [Hadoop and Spark workflows](diagrams/hadoop_spark.mmd)

---

<a id="experiment-14"></a>
## Experiment 14 — Install Apache Spark and Explore Core Features

**Aim**
Install Apache Spark and demonstrate core data processing features using the Python API, PySpark.

**Libraries / software**
Apache Spark, PySpark, a compatible Java runtime, Python, and a small CSV/JSON input. Pin and record mutually compatible Spark/PySpark/Java versions; installation details differ across local, managed, and cluster environments.

**Theory**
Spark provides distributed data processing. A SparkSession is the entry point; DataFrames describe structured data and transformations are generally evaluated lazily when an action is invoked. Spark can run locally for learning without being a distributed cluster.

**Procedure / implementation / code blueprint**
1. Verify and record OS, Python, Java, Spark, and PySpark versions; confirm the local Spark session starts.
2. Create a `SparkSession`; load a small CSV with header and inferred or explicit schema.
3. Demonstrate `printSchema`, `show`, `select`, `filter`, `groupBy`/`agg`, and an action such as `count`.
4. Compare a simple result with a small pandas calculation, making sure null handling and aggregation semantics match.
5. Stop the session and document whether execution was local or on a cluster.

**Observation**
The executed PySpark 4.3.0 notebook ran in local[2] mode. Aggregated sales totals for East, North, South, and West were 23.4, 25.5, 33.5, and 26.1, respectively; every total matched the independent pandas result. See `outputs/results/exp14_spark_region_totals.csv`, `outputs/figures/exp14_spark_sales.png`, and `notebooks/exp14_apache_spark.ipynb`. Local mode does not demonstrate a distributed cluster.

**Result**
Explain which transformations/actions were demonstrated and note that local-mode success does not prove a distributed-cluster deployment.

**Diagram:** [Hadoop and Spark workflows](diagrams/hadoop_spark.mmd)

---

<a id="experiment-15"></a>
## Experiment 15 — NoSQL Database Operations Using MongoDB

**Aim**
Connect to MongoDB from Python and demonstrate basic document-database operations.

**Libraries / software**
Python, Jupyter, PyMongo, and mongomock for an isolated, deterministic in-memory MongoDB-compatible demonstration. A live local/Atlas server is not required for this notebook.

**Theory**
MongoDB stores BSON documents in collections within databases. Documents in a collection need not have identical fields. CRUD means create, read, update, and delete. Schema flexibility does not remove the need for validation, indexes, access control, and careful query design.

**Procedure / implementation / code blueprint**
1. Create a mock client and select a practice database and collection; do not use credentials or a live server for this demonstration.
2. Insert fictional records, query by field, update one record, and delete a known sample record.
3. Verify each operation using returned counts/results and save the CRUD summary.

**Observation**
The executed mongomock run inserted 3 fictional documents, matched and modified 1, deleted 1, and left 2 documents. This is an in-memory mock demonstration, not evidence of a live MongoDB deployment. Counts are in `outputs/results/exp15_mongodb_crud.csv`; see `notebooks/exp15_mongodb.ipynb`.

**Result**
Confirm that the demonstrated CRUD operations worked and state the document fields used. Do not include real personal data, credentials, or destructive commands against a non-practice database.

**Diagram:** [MongoDB CRUD workflow](diagrams/mongodb_crud.mmd)

---

## Submission checklist for every generated notebook

- [ ] Title, experiment number, aim, candidate/dataset identity, and date are present.
- [ ] Libraries and versions are listed; platform-specific setup is explicit.
- [ ] Theory explains the method in the context of the experiment.
- [ ] Procedure runs top-to-bottom from a fresh kernel without relying on hidden state.
- [ ] Dataset citation, license, class counts/shape, and uniqueness approval are recorded.
- [ ] Preprocessing is fitted only on training data wherever a train/test evaluation is used.
- [ ] Code prints verifiable outputs and generates relevant, labeled figures.
- [ ] Observations quote the actual run; figures and reported values agree.
- [ ] Result answers the aim without claiming more than the experiment supports.
- [ ] No secrets or personal data are stored in the notebook or output.
