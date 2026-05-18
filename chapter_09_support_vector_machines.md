# Chapter 9: Support Vector Machines

## Summary

The SVM is a binary classifier that evolved through three ideas, each solving a limitation of the previous one.

**Maximal Margin Classifier** finds the hyperplane that separates two classes with the largest possible margin. Its fatal flaw is sensitivity: adding a single observation near the boundary can dramatically shift the hyperplane and shrink the margin to near zero, indicating severe overfitting.

**Support Vector Classifier** fixes this by introducing a "soft margin", allowing some observations to violate the margin or even be misclassified. The tuning parameter C controls this: a small C enforces a narrow, strict margin (low bias, high variance); a large C allows many violations, producing a wider, more tolerant margin (higher bias, lower variance). Crucially, only the **support vectors** (observations on or inside the margin) influence the hyperplane. Points far from the boundary have zero effect.

**Support Vector Machine** extends the classifier to non-linear boundaries using **kernels**. Rather than explicitly computing a massive expanded feature space (e.g., adding X², X³, interaction terms), kernels compute inner products between observations in an implicit, potentially infinite-dimensional space at a fraction of the cost. This is the **kernel trick**.

## Kernel Comparison

| Kernel | Decision Boundary | Best When |
|--------|------------------|-----------|
| **Linear** | Straight hyperplane | Classes are largely linearly separable |
| **Polynomial (degree d)** | Smooth non-linear curve | Moderate non-linearity with a known polynomial structure |
| **Radial (RBF)** | Highly flexible, local | Highly non-linear boundaries; only nearby points influence classification |

**Radial kernel behavior:** If a test observation is far from a training observation, the kernel value is near zero, so that training point contributes almost nothing to the classification. This gives the radial kernel purely local behavior.

**When SVM loses to Logistic Regression:** When classes overlap heavily, logistic regression is often preferred. Both methods are closely related: SVM with a linear kernel minimizes hinge loss with an L2 penalty, while logistic regression minimizes log loss. The key difference is that SVM loss hits exactly zero for correctly classified points beyond the margin; logistic loss never reaches zero.

**Multi-class extension:** SVMs are natively binary. For K > 2 classes, two strategies are used:
- **One-Versus-One:** Train a classifier for every pair of classes; assign the class that wins the most pairwise contests.
- **One-Versus-All:** Train K classifiers, each separating one class from the rest; assign the class with the highest confidence score.

## Important Notes

- Only support vectors (points on or violating the margin) determine the hyperplane. Observations far from the boundary have zero influence, unlike logistic regression where every point affects the decision boundary.
- The cost parameter C must be chosen via cross-validation. A very small C can lead to a model that ignores most of the data; a very large C risks overfitting to the training set.
- The kernel trick does not literally expand the feature space. It computes similarities as if it had, without ever constructing the high-dimensional representation. This is what makes SVMs computationally feasible in high-dimensional settings.
- Slack variables ε allow margin violations: ε > 0 means the point is inside the margin; ε > 1 means it is misclassified. The sum of all slack variables is bounded by C, controlling the total amount of violation permitted.
- SVMs do not output probabilities natively. Probability estimates can be obtained (e.g., via Platt scaling) but are not a natural product of the optimization.
- Standardizing predictors before fitting an SVM is important. The margin and kernel distances are based on Euclidean distance, so variables on larger scales will dominate.

## Questions to Keep in Mind

- **Why does the kernel trick matter computationally?**

  Explicitly constructing a polynomial or radial feature expansion can require an astronomically large, or even infinite, number of features. The kernel trick computes the inner products of those expanded features directly from the original data, achieving the same result without ever materializing the high-dimensional space.

- **What actually happens to a non-support vector if you remove it from the training data?**

  Nothing. The hyperplane stays exactly the same. Only the support vectors (points on or violating the margin) determine the model. This is fundamentally different from logistic regression, where every single observation influences the decision boundary.

- **Why does a large C not always mean a better model, even though it tolerates fewer errors?**

  A large C forces the margin to be very narrow to avoid violations, making the model highly sensitive to individual training points (high variance). It is fitting the training data more tightly, not learning the true boundary more accurately.
