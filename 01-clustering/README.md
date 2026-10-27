# Customer Segmentation via Clustering

Unsupervised segmentation of the [UCI Wholesale Customers](https://archive.ics.uci.edu/dataset/292/wholesale+customers) dataset by annual spending across product categories.

## Pipeline

1. **EDA & preprocessing:** distribution checks, outlier detection (boxplots + Z-scores), standardization.
2. **Dimensionality reduction for visualization:** PCA and t-SNE projections.
3. **Clustering:** K-Means, Spectral Clustering, and Gaussian Mixture Models, each run for K = 2, 3, 4.
4. **Model selection:** compared every (algorithm, K) combination across five internal validation metrics — Silhouette Score, Davies-Bouldin Index, Calinski-Harabasz Index, Dunn Index, and the Gap Statistic (to check cluster structure against random data) — then automatically selected the best-performing configuration.
5. **Cluster profiling:** interpreted the winning clusters against the original (unscaled) spending data.

## Result

**K-Means with K = 3** was selected as the best model, as logged by the notebook:

| Metric | Value |
|---|---|
| Silhouette Score | 0.5483 |
| Davies-Bouldin Index | 0.9279 (lower is better) |
| Calinski-Harabasz Index | 140.14 |
| Dunn Index | 0.0288 |
| Gap Statistic | 3.4709 |

It outperformed Spectral Clustering and GMM on Silhouette Score and Davies-Bouldin across the K values tested, and showed meaningful structure relative to the Gap Statistic's random-data baseline.

## Skills demonstrated

Full unsupervised-learning workflow: outlier handling, feature scaling, dimensionality reduction for visualization vs. clustering, and — importantly — comparing models with multiple complementary validation metrics rather than relying on a single score.

`AML-REPORT-proj1.pdf` documents every notebook cell's purpose; `project1_AML.ipynb` is the original, unedited notebook.
