# Human Activity Classification

Classification of the activity a person is doing from five physiological signals, with exploratory analysis, visualization, a benchmark of eight classifiers, hyperparameter tuning, statistical comparison of models and dimensionality reduction.

## Problem

Each sample has five numeric signals: `SL`, `EEG`, `BP`, `HR` and `CIRCULATION`. The goal is to predict `ACTIVITY`, a label with 6 classes encoded as `0`–`5`. The dataset does not describe what each class means.

- Training set: 11,999 labelled rows. Test set: 4,383 unlabelled rows, used for the competition submission.
- The classes are moderately imbalanced: class 0 has 27.9% of the rows and class 1 only 3.1%.
- The signals have very different scales, from hundreds for `BP` and `HR` to millions for `SL` and `EEG`, with long right tails.

## Notebooks

All notebooks are written in Spanish.

| # | Notebook | What it does | Open |
|---|---|---|---|
| 1 | [`E1_AnalisisDatos.ipynb`](E1_AnalisisDatos.ipynb) | Exploratory analysis with pandas: shapes, types, descriptive statistics, class distribution, extreme values, per-class statistics and five questions about the data. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/santiagodie/human-activity-classification/blob/main/E1_AnalisisDatos.ipynb) |
| 2 | [`E1_Visualizacion.ipynb`](E1_Visualizacion.ipynb) | Visualization with matplotlib and seaborn: class counts, histograms, density plots, per-class boxplots, correlation heatmap, scatter plots, pairplot and t-SNE. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/santiagodie/human-activity-classification/blob/main/E1_Visualizacion.ipynb) |
| 3 | [`E1_ComparativaClasificadores.ipynb`](E1_ComparativaClasificadores.ipynb) | Benchmark of 8 scikit-learn classifiers with default settings, using 3 and 5 features, a log transform of `SL` and `CIRCULATION`, and a stratified 75/25 hold-out split. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/santiagodie/human-activity-classification/blob/main/E1_ComparativaClasificadores.ipynb) |
| 4 | [`E1_Adicional1_Descriptores_e_Hiperparámetros.ipynb`](E1_Adicional1_Descriptores_e_Hiperpar%C3%A1metros.ipynb) | Feature engineering (HR/BP ratio, product and difference) and hyperparameter search with `RandomizedSearchCV` for Random Forest, Decision Tree, KNN and MLP. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/santiagodie/human-activity-classification/blob/main/E1_Adicional1_Descriptores_e_Hiperpar%C3%A1metros.ipynb) |
| 5 | [`E1_Adicional2_AnalisisEstadistico.ipynb`](E1_Adicional2_AnalisisEstadistico.ipynb) | 10-fold stratified cross-validation, per-class reports, statistical comparison of models with `StatisticalAnalysis.compare_methods`, confusion matrix, feature importances and learning curve of the best model. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/santiagodie/human-activity-classification/blob/main/E1_Adicional2_AnalisisEstadistico.ipynb) |
| 6 | [`E1_Adicional3_ReduccionDimensionalidad.ipynb`](E1_Adicional3_ReduccionDimensionalidad.ipynb) | Dimensionality reduction: PCA (explained variance, 2D and 3D), t-SNE (2D, 3D and the effect of perplexity) and UMAP. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/santiagodie/human-activity-classification/blob/main/E1_Adicional3_ReduccionDimensionalidad.ipynb) |
| 7 | [`envio.ipynb`](envio.ipynb) | Trains the final Random Forest on the full training set and writes the `submission.csv` file for the competition. | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/santiagodie/human-activity-classification/blob/main/envio.ipynb) |

## Key results

All figures come from the saved notebook outputs.

**Classifier benchmark** (default settings, stratified hold-out of 3,000 rows, accuracy):

| Model | 3 features (`BP`, `HR`, `CIRCULATION`) | 5 features |
|---|---|---|
| Random Forest | 0.6900 | **0.7467** |
| Decision Tree | 0.6837 | 0.6800 |
| KNN (k=5) | 0.6177 | 0.6360 |
| MLP (100, 100) | 0.5817 | 0.6053 |
| Logistic Regression | 0.3043 | 0.3133 |
| Linear SVM | 0.2813 | 0.3017 |
| Perceptron | 0.2663 | 0.2257 |
| Sigmoid SVM | 0.1863 | 0.1740 |

The linear models stay below 0.32, which matches what the visualizations showed: the classes are not linearly separable.

**Tuning and feature engineering** (`RandomizedSearchCV`, 5-fold CV on the training split, evaluated on the same hold-out):
- Random Forest: 0.7467 → 0.7510 after tuning. The engineered HR/BP features did not help (0.7347).
- MLP benefited most: 0.6053 → 0.6530 after tuning, and 0.6877 with the engineered features.
- Decision Tree and KNN barely changed (0.67–0.68 and 0.64).

**10-fold cross-validation** (mean accuracy ± std): Random Forest 0.7595 ± 0.0081 · Decision Tree 0.6810 ± 0.0105 · MLP 0.6598 ± 0.0128 · KNN 0.6416 ± 0.0155.

**Statistical comparison** (`compare_methods`):
- Normality (Shapiro-Wilk, p = 0.000014) and homoscedasticity (Levene, p = 0.00024) were both rejected, so a non-parametric test was applied (Quade).
- Random Forest (0.7588 ± 0.0109) was significantly better than every other model, with large effect sizes (Cohen's d from 7.18 to 15.40).

**Best model, per class** (Random Forest, 10-fold CV): recall is 0.965 for class 0, 0.782 for class 1, 0.739 for class 2, 0.710 for class 3, 0.641 for class 4 and 0.580 for class 5. Macro F1 is 0.7417. Most errors are confusions between classes 3, 4 and 5.

**Dimensionality reduction:**
- The first principal component explains 62.14% of the variance and two components explain 81.99%. Four components are needed to pass 99% (99.62%).
- PCA, t-SNE and UMAP all separate class 0, while classes 2–5 stay overlapped.

## Tech stack

Python · pandas · NumPy · scikit-learn · SciPy · matplotlib · seaborn · StatisticalAnalysis · umap-learn · Google Colab

## How to run

Open a notebook in Google Colab with the badges above. Extra dependencies are installed inside the notebooks. These are the install commands as they appear in the notebooks (not re-verified):

```bash
pip install seaborn -Uq           # E1_Visualizacion.ipynb
pip install -q StatisticalAnalysis  # E1_Adicional2_AnalisisEstadistico.ipynb
pip install -q umap-learn         # E1_Adicional3_ReduccionDimensionalidad.ipynb
```

pandas, NumPy, scikit-learn, SciPy and matplotlib come preinstalled in Colab, and no versions are pinned. `E1_Adicional2_AnalisisEstadistico.ipynb` also downloads a helper script (`plot_curves.py`) from an external GitHub repository to draw the learning curve.

The notebooks download `train.csv`, `test.csv` and `sample.csv` with `wget` from a URL that has been replaced by the placeholder `DATA_URL` (see [Data](#data)). To run them, put your own copy of the data in place of `DATA_URL` or upload the CSV files to the Colab session.

## Data

The data comes from a private Kaggle competition organised for the course. It is not published in this repository, and the original download URLs in the notebooks (both in code and in outputs) have been replaced by the placeholder `DATA_URL`.

## Known limitations

- Model selection in notebooks 3 and 4 relies on a single hold-out split. The 10-fold CV in notebook 5 is the more reliable estimate.
- The Random Forest hyperparameters used in notebook 5 and in `envio.ipynb` (`n_estimators=500`, `max_depth=20`, `min_samples_split=5`, `max_features=0.5`) do not match the best parameters printed by the search in notebook 4 (`n_estimators=321`, `max_depth=30`, `min_samples_split=5`).
- `compare_methods` receives unscaled data, so KNN (0.611) and MLP (0.306) score much lower there than with standardized inputs. Only the Random Forest result in that comparison is directly comparable.
- The log transform of `SL` and `CIRCULATION` is applied in notebooks 3, 4 and `envio.ipynb`, but not in the cross-validation of notebook 5.
- The competition leaderboard score of the submission is not recorded in the notebooks.

---

Built for the Artificial Intelligence course at the University of La Rioja (2025–26).
