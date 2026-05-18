# Chapter 12: Unsupervised Learning

## Summary

Unsupervised learning extracts hidden structure from data where **no response variable** is available. The goal is not to predict an outcome, but to discover patterns, representations, or groupings directly from the features. Because there is no "correct answer," unsupervised learning is inherently more exploratory and subjective than supervised learning.

## Methods Overview

**Principal Components Analysis (PCA)** — Addresses the difficulty of understanding high-dimensional data by finding a lower-dimensional representation that preserves as much variability as possible. PCA constructs new variables (principal components) as linear combinations of the original variables, chosen to maximize variance while remaining orthogonal to each other.

**K-Means Clustering** — Partitions observations into a pre-specified number of non-overlapping clusters by minimizing within-cluster variation. The algorithm repeatedly assigns observations to the nearest centroid and updates centroids until convergence. Only guarantees a *local* optimum.

**Hierarchical Clustering** — Builds a tree-like structure (dendrogram) without requiring the number of clusters in advance. The dendrogram can later be "cut" at different heights to yield different numbers of clusters. Similarity is determined by the height at which branches merge, not by horizontal proximity.

**Matrix Completion** — Estimates missing data entries by exploiting correlations among variables and the underlying low-dimensional structure — essentially an extension of PCA applied to incomplete data. This forms the foundation of many recommender systems (e.g., movie recommendation algorithms).

## Important Notes

- PCA creates entirely new variables (principal components); it does **not** select the "most important" original variables.
- Variables should be standardized before PCA or clustering — variables with larger scales dominate the results.
- K-Means only guarantees a local optimum; always run it multiple times with different random initializations.
- In a dendrogram, similarity is determined by the **vertical merge height**, not horizontal distance.
- Hierarchical clustering does not require specifying the number of clusters beforehand.
- Both PCA and clustering are sensitive to outliers because they rely heavily on distances and variances.
- K-Means forces every observation into a cluster, even outliers that may not naturally belong to any group.
- Because there is no response variable, evaluating whether discovered structure is "correct" is often subjective.

## Questions to Keep in Mind

- **What is the main difference between PCA and clustering?**

  PCA seeks a low-dimensional representation that preserves variance, while clustering seeks to discover homogeneous groups among observations.

- **Why must variables usually be standardized before PCA or clustering?**

  Without scaling, variables with naturally larger variances or measurement units dominate the analysis and distort the results.

- **Why must K-Means clustering be run multiple times?**

  The algorithm only guarantees a local optimum; different random initializations can produce different cluster assignments.

- **How should similarity be interpreted on a dendrogram?**

  Similarity is determined by the height on the vertical axis where branches first merge, not by horizontal proximity.

- **Why is unsupervised learning considered more subjective than supervised learning?**

  There is no response variable or objective prediction error to determine whether the discovered structure is truly meaningful.

- **What is the main limitation of K-Means clustering?**

  K-Means assumes compact clusters and forces every observation into a cluster, even when meaningful subgroups may not actually exist.

**How does matrix completion estimate missing values?**

It exploits correlations among variables and underlying low-dimensional structure to simultaneously estimate missing entries and the latent representation.
