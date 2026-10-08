# Project 3 Reflection — Unsupervised Learning (Customer Segmentation)

**Author:** Shifat Rahman Kabbo
**Batch:** DecodeLabs Industrial Training Kit 2026

---

## 1. Why Scaling Matters Before Clustering

Euclidean distance treats all spatial directions equally — magnitude dictates influence. In the raw dataset:
- **Annual Income** ranges $15k–$137k
- **Spending Score** ranges 1–100

Without scaling, distance would be dominated entirely by Income. A customer earning $100k with a Spending Score of 10 would appear "close" to one earning $100k with a score of 90 — clearly wrong behaviorally.

**StandardScaler** maps every feature to mean=0, std=1, giving equal voting power to each behavioral dimension.

---

## 2. The Curse of Dimensionality & PCA

With many features, points become **equidistant** in high-dimensional space — distance metrics lose meaning. PCA solves this by:

1. Finding orthogonal axes (Principal Components) of maximum variance
2. Projecting the data onto those axes
3. Retaining only the components needed to preserve **95% of total variance**

This strips noise while keeping behavioral signal. The scree plot shows the drop-off clearly.

---

## 3. Proving K Mathematically

K-Means cannot determine K on its own — it simply forces the data into whatever K is given. Two diagnostic gatekeepers must agree:

### Elbow Method
Plots WCSS against K. The "elbow" (inflection point) marks where adding clusters stops yielding meaningful compression. We saw the elbow at **K=5**.

### Silhouette Score
Measures `(b - a) / max(a, b)` where:
- `a` = mean distance to points in the same cluster
- `b` = mean distance to points in the nearest other cluster

Scores near **+1** = excellent separation. Scores near **0** = overlapping. Our best silhouette confirmed **K=5**.

**Both methods agreeing is non-negotiable evidence.**

---

## 4. Reverse-Engineering Centroids

K-Means runs in PCA-space. A centroid like `[-2.14, 0.88]` means nothing to a marketing team. We must **inverse-transform** through:
