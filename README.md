# K-Means++ and K-Medians Clustering from Scratch

Implementations of the **K-Means++** and **K-Medians** clustering algorithms, built from scratch in Python (NumPy/Pandas) with a local-search refinement step, and benchmarked against five standard clustering datasets using cluster purity as the evaluation metric.

## Overview

This project (originally a data mining coursework assignment) implements two clustering algorithms without relying on `sklearn`'s built-in clustering methods:

- **K-Means++** — uses the K-Means++ seeding strategy to choose well-spread initial centroids, followed by standard Lloyd's-algorithm iterations, plus a local search step to refine centroid placement.
- **K-Medians** — analogous to K-Means but uses medians (more robust to outliers) instead of means, also with a local search refinement step.

For each dataset, both algorithms are run for multiple iterations (to account for random initialization), and the best result (by purity score) is kept and reported/plotted.

## Datasets

| File | Description | Records |
|---|---|---|
| `iris.data` | Classic Iris flower dataset (3 species) | 150 |
| `glass.csv` | Glass identification dataset (chemical composition) | 214 |
| `R15.data` | Synthetic 2D clustering benchmark (15 Gaussian clusters) | 600 |
| `Aggregation.data` | Synthetic 2D clustering benchmark with irregular cluster shapes | 788 |
| `D31.data` | Synthetic 2D clustering benchmark (31 Gaussian clusters) | 3100 |

## Approach

1. **Data loading** — `read_data()` reads each file (handling different delimiters), label-encodes the true class column, and infers `k` (number of clusters) from the number of unique labels.
2. **Clustering** — Both `KMeans` and `KMedians` classes take the data and `k`, initialize centroids via a K-Means++-style seeding scheme, iterate to convergence, and apply a local search pass that tries moving each centroid to a nearby point to further reduce clustering cost.
3. **Evaluation** — Clustering **purity** is computed by matching each predicted cluster to its majority true label. Each algorithm is run for 10 iterations per dataset, and the best-purity run is reported (and plotted, for the 2D synthetic datasets).
