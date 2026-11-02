# IT-411 Data Science and Analytics Practicals

This repository contains the **15 updated, renumbered lab notebooks**, executed outputs, saved figures/results, experiment notes, and editable Mermaid diagrams. The syllabus-aligned experiment list and detailed theory/procedure/observation notes are in [`reports/observations.md`](reports/observations.md).

> **Status:** All 15 notebooks have been executed from top to bottom. Each contains the faculty-required Aim, Libraries, Theory, Procedure/Implementation/Code, Observation, and Result sections. The dataset, runtime, and model limitations are documented below and in the relevant experiment notes.

## Faculty-required sections

Each final lab experiment should contain, in this order:

1. Aim
2. Libraries / software requirements
3. Theory
4. Procedure and implementation (including complete, runnable code)
5. Observations (actual outputs, tables, plots, and measured values)
6. Result / conclusion

The notebook implementations and the measured result summaries below are the reference for preparing the final lab file. Re-run a notebook if the environment, dataset, or code changes; do not present these sample datasets as reserved or unique to a candidate.

## Updated experiment index

| No. | Experiment | Reference section | Candidate-specific dataset / source guidance |
|---:|---|---|---|
| 1 | Exploratory Data Analysis (EDA) on a Real-World Dataset | [Experiment 1](reports/observations.md#experiment-1) | A documented real-world tabular dataset |
| 2 | Data Visualization: Charts, Histograms, and Scatter Plots | [Experiment 2](reports/observations.md#experiment-2) | A dataset with numeric and categorical variables |
| 3 | Linear, Ridge, and Lasso Regression | [Experiment 3](reports/observations.md#experiment-3) | A real-valued prediction dataset |
| 4 | SVM and KNN Classifiers | [Experiment 4](reports/observations.md#experiment-4) | A labeled classification dataset |
| 5 | Naive Bayes for Text Classification | [Experiment 5](reports/observations.md#experiment-5) | A labeled text corpus |
| 6 | Decision Tree and Random Forest | [Experiment 6](reports/observations.md#experiment-6) | A labeled tabular classification dataset |
| 7 | Dimensionality Reduction Using PCA | [Experiment 7](reports/observations.md#experiment-7) | A numeric dataset with several correlated features |
| 8 | Artificial Neural Network (ANN) | [Experiment 8](reports/observations.md#experiment-8) | A labeled dataset suitable for multiclass classification |
| 9 | CNN to Classify Bird Species | [Experiment 9](reports/observations.md#experiment-9) | A properly licensed, labeled bird-image dataset |
| 10 | K-Means for Data Segmentation | [Experiment 10](reports/observations.md#experiment-10) | Unlabeled numeric observations; labels only for optional evaluation |
| 11 | Performance Metrics | [Experiment 11](reports/observations.md#experiment-11) | A labeled classification dataset with class imbalance considered |
| 12 | Hierarchical Clustering and Dendrogram Analysis | [Experiment 12](reports/observations.md#experiment-12) | A manageable numeric dataset |
| 13 | Hadoop Installation and Basic HDFS Commands | [Experiment 13](reports/observations.md#experiment-13) | A small, non-sensitive text or CSV file |
| 14 | Apache Spark Installation and Core Features | [Experiment 14](reports/observations.md#experiment-14) | A small, non-sensitive CSV/JSON dataset |
| 15 | NoSQL Database Operations Using MongoDB and Python | [Experiment 15](reports/observations.md#experiment-15) | Candidate-created or approved sample documents |

## Notebooks and verified outcomes

| No. | Notebook | Verified outcome / key result |
|---:|---|---|
| 1 | [EDA](notebooks/exp01_eda.ipynb) | Titanic dataset: 891 rows × 12 columns; survival 38.4% overall, 74.2% female and 18.9% male. |
| 2 | [Data visualization](notebooks/exp02_data_visualization.ipynb) | Iris charts, histograms, scatter plots, box plots, and pair plot saved. |
| 3 | [Regression](notebooks/exp03_regression.ipynb) | California Housing: Lasso at α=0.01 achieved test R² 0.5816; Linear and Ridge were about 0.5758. |
| 4 | [SVM and KNN](notebooks/exp04_svm_knn.ipynb) | Breast Cancer: best KNN (k=3) and RBF SVM both reached 98.25% test accuracy. |
| 5 | [Naive Bayes](notebooks/exp05_naive_bayes_spam.ipynb) | SMS spam: 96.23% accuracy; spam precision 1.00 and recall 0.718. Confusion matrix figure and metrics CSV saved. |
| 6 | [Decision Tree and Random Forest](notebooks/exp06_decision_tree_random_forest.ipynb) | Titanic: Random Forest accuracy 82.68%; depth-3 tree 79.33%. |
| 7 | [PCA](notebooks/exp07_pca.ipynb) | Wine: 10 of 13 components retained 96.2% variance; logistic-regression accuracy was 97.22% with either 10 PCs or all features. |
| 8 | [ANN](notebooks/exp08_ann.ipynb) | MNIST test accuracy 96.8%, loss 0.1014 after five epochs. |
| 9 | [Bird-species CNN](notebooks/exp09_bird_species_cnn.ipynb) | CUB-200-2011 subset: five species, 176/44/55 train/validation/test images; test accuracy 98.18%, loss 0.1312. This small, image-level split may overstate generalization to new birds. |
| 10 | [K-Means](notebooks/exp10_kmeans_clustering.ipynb) | Iris, k=3: silhouette 0.4590; adjusted Rand index 0.6201. |
| 11 | [Performance metrics](notebooks/exp11_performance_metrics.ipynb) | Breast Cancer: logistic regression accuracy 98.25%, malignant recall 97.62%, AUC 0.9954; decision tree accuracy 92.11%, AUC 0.9163. |
| 12 | [Hierarchical clustering](notebooks/exp12_hierarchical_clustering.ipynb) | Palmer Penguins ARI: Ward 0.9159, complete 0.8949, single 0.6572. |
| 13 | [Hadoop / HDFS](notebooks/exp13_hadoop_hdfs.ipynb) | WSL Ubuntu, Temurin Java 17.0.21, Hadoop 3.4.2; upload/list/read/download round trip verified. |
| 14 | [Apache Spark](notebooks/exp14_apache_spark.ipynb) | PySpark 4.3.0 local[2]; all four regional totals matched the pandas calculation. |
| 15 | [MongoDB / Python](notebooks/exp15_mongodb.ipynb) | mongomock CRUD: inserted 3, updated 1, deleted 1; 2 documents remained. No live MongoDB server was used. |

Saved plots and tabular outputs are in [`outputs/figures/`](outputs/figures/) and [`outputs/results/`](outputs/results/). Large source datasets and downloaded archives are intentionally excluded from version control.

## Dataset uniqueness requirement

The faculty's note is interpreted as **each candidate must use a dataset distinct from those selected by other candidates**. It does not mean that all 15 experiments must use different datasets within one candidate's manual. Before implementation, each candidate should:

- Propose a dataset and experiment number to the instructor and maintain a class dataset register.
- Record the dataset title, provider/source URL, license, version or download date, selected columns/labels, and any preprocessing.
- Confirm that another candidate has not registered the same dataset for that experiment. If a dataset is used in multiple experiments by the same candidate, explain the reuse and obtain approval if needed.
- Prefer public, licensed data; do not include private, personal, or credential-bearing data in notebooks or screenshots.

The per-experiment dataset notes in the reference brief are suggestions, not claims that a dataset is already reserved or unique in the class.

## Repository contents and reproducibility

- [`notebooks/`](notebooks/) contains exactly one executed notebook per updated experiment.
- [`outputs/figures/`](outputs/figures/) contains the generated, experiment-numbered plots. [`outputs/results/`](outputs/results/) contains metrics and result tables.
- [`datasets/`](datasets/) contains small sample inputs. CUB-200-2011 source archive and extracted images are local-only and ignored by Git; the notebook downloads/extracts them when needed.
- [`reports/observations.md`](reports/observations.md) provides the per-experiment aim, libraries, theory, implementation guidance, actual observations, and result.
- [`reports/diagrams/`](reports/diagrams/) contains editable Mermaid diagrams; render these if the final manual format does not support Mermaid.
- [`requirements.txt`](requirements.txt) lists the tested Python packages. Experiment 13 additionally requires WSL/Ubuntu, Java, and Hadoop; consult its notebook for setup details.

Run Python notebooks with Python 3.12 and the listed requirements installed. Execute from the repository root or use Jupyter's notebook execution support; notebook paths resolve relative to the repository. Experiment 9 needs access to the CUB source archive and pretrained MobileNetV2 weights on first run. Experiment 13 is specific to the tested WSL setup. Experiment 14 runs Spark locally, not on a distributed cluster.

## Run and maintain the notebooks

The Python notebooks were tested with Python 3.12.3 and the packages pinned in [`requirements.txt`](requirements.txt). From the repository root, install those packages and use Jupyter to open/run notebooks. Experiment 9 requires the CUB-200-2011 archive and network access to obtain MobileNetV2 pretrained weights on a first run. Experiment 13's setup commands target WSL/Ubuntu; Hadoop is not installed system-wide. Experiment 14 demonstrates Spark local mode, not a distributed cluster. Experiment 15 uses mongomock and does not connect to a live MongoDB instance.

When adapting an experiment to a candidate-approved dataset:

1. Use a fresh kernel and keep all paths relative to the project root (or resolve them robustly).
2. Include deterministic seeds where supported; document nondeterministic GPU/runtime behavior.
3. Split data before fitting preprocessing steps; fit scalers, imputers, and vectorizers on training data only.
4. Show the data shape, class distribution, key intermediate results, and evaluation measures.
5. Include readable, labeled figures with captions and save them under `outputs/figures/` using the **new** experiment number.
6. Save tables/metrics where useful under `outputs/results/`; then update the observation and result from the actual run.
7. Record external downloads and environment-specific setup steps instead of implying that a network download, Hadoop daemon, Spark runtime, or MongoDB server is always available.

## Diagrams

- [End-to-end data-science workflow](reports/diagrams/data_science_workflow.mmd)
- [Regression and classification model workflow](reports/diagrams/supervised_learning.mmd)
- [PCA and neural-network workflows](reports/diagrams/pca_ann.mmd)
- [Bird-species CNN workflow](reports/diagrams/bird_cnn.mmd)
- [K-Means and hierarchical clustering](reports/diagrams/clustering.mmd)
- [Hadoop HDFS and Spark workflow](reports/diagrams/hadoop_spark.mmd)
- [MongoDB document CRUD workflow](reports/diagrams/mongodb_crud.mmd)
