#### **Introduction**

Credit card fraud remains one of the most serious threats in digital payments, resulting in billions of dollars in annual losses worldwide. As fraudsters continually evolve with sophisticated techniques, traditional rule-based systems struggle to detect novel and subtle attack patterns.

Machine learning, particularly classification algorithms, has become essential for proactive fraud detection by learning complex patterns from historical transaction data.  
This experiment investigates the application of **Support Vector Machines (SVM)** — a powerful supervised learning algorithm renowned for its effectiveness in high-dimensional spaces and strong theoretical foundation — to the task of credit card fraud detection.

#### **Support Vector Machine (SVM)**

Support Vector Machine is a supervised classification (and regression) algorithm that constructs an optimal **hyperplane** to separate classes while maximizing the **margin** — the distance between the hyperplane and the nearest data points from each class.

##### **Key Concepts**

- The data points closest to the hyperplane are called **support vectors**. Only these points influence the position and orientation of the final hyperplane.
- Maximizing the margin improves generalization performance on unseen data.
- For datasets that are not perfectly separable, SVM introduces **slack variables** (ξᵢ) and a regularization parameter **C** to allow controlled misclassifications (soft margin SVM).

The primal optimization problem is:

$$
\min_{w, b, \xi} \frac{1}{2} \|w\|^2 + C \sum_{i=1}^{n} \xi_i \quad 
\text{s.t.} \quad y_i (w^T \phi(x_i) + b) \geq 1 - \xi_i, \quad \xi_i \geq 0
$$

##### **Why SVM is Effective for Fraud Detection**

- Naturally handles high-dimensional feature spaces (common in anonymized transaction datasets)
- Robust to noise and outliers when properly regularized
- Performs well with relatively small numbers of positive (fraud) examples
- Offers strong theoretical guarantees on generalization

#### **Linear vs. Non-Linear SVM**

| Type               | Applicability                                      | Decision Boundary                  |
|--------------------|----------------------------------------------------|-------------------------------------|
| **Linear SVM**     | Data approximately separable by a hyperplane      | Straight line/hyperplane            |
| **Non-Linear SVM** | Complex, overlapping, or irregular patterns       | Curved/complex boundary via kernel trick |

Real-world credit card fraud data is almost always **non-linearly separable**, making kernel-based SVMs particularly valuable.

#### **Kernel Functions** (The Kernel Trick)

Instead of explicitly mapping data to a high-dimensional space (which would be computationally expensive), kernels compute the inner product in the transformed space directly.

| Kernel                  | Formula                                                      | Characteristics                                                                 |
|-------------------------|--------------------------------------------------------------|-------------------------------------------------------------------------|
| **Linear**              | $ K(x_i, x_j) = x_i^T x_j $                                    | Fast, suitable when classes are nearly linearly separable               |
| **Polynomial**          | $ K(x_i, x_j) = (\gamma x_i^T x_j + r)^d $                    | Captures polynomial relationships; degree $ d $ controls complexity   |
| **Radial Basis Function (RBF / Gaussian)** | $ K(x_i, x_j) = \exp(-\gamma \|x_i - x_j\|^2) $ | Most popular for fraud detection; creates highly flexible boundaries   |
| **Sigmoid**             | $ K(x_i, x_j) = \tanh(\gamma x_i^T x_j + r) $                  | Behaves like a two-layer neural network; less commonly used in practice |

In fraud detection tasks, the **RBF kernel** typically outperforms others due to its ability to model intricate, localized patterns.

#### **Important Hyperparameters**

| Parameter | Role                                                                 | Effect of Values                                      |
|-----------|----------------------------------------------------------------------|-------------------------------------------------------|
| **C**     | Trade-off between margin maximization and training error                 | Small C → larger margin, more misclassifications allowed<br>Large C → narrow margin, fewer misclassifications (risk of overfitting) |
| **γ (gamma)** | Controls reach of each training example (only for RBF, polynomial, sigmoid) | Small γ → smooth boundary<br>Large γ → tight, wiggly boundary (overfitting risk) |

Optimal (C, γ) are usually found via grid/random search with cross-validation.

#### **Challenges in Credit Card Fraud Detection**

- Extreme class imbalance (fraud < 0.1–1% of transactions)
- Concept drift (fraud patterns change over time)
- Need for very high recall on fraud class while keeping false positives low

Because of imbalance, **accuracy is misleading**. Preferred metrics are:

- **Precision**, **Recall**, **F1-score** (especially on the fraud class)
- **Precision-Recall AUC** (PR-AUC) — more informative than ROC-AUC in highly imbalanced settings
- **Confusion Matrix** and **Cost-sensitive evaluation**


