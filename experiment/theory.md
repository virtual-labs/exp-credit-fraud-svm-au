#### **Introduction**

Credit card fraud remains one of the most serious threats in digital payments, resulting in billions of dollars in annual losses worldwide. As fraudsters continually evolve with sophisticated techniques, traditional rule-based systems struggle to detect novel and subtle attack patterns.

Machine learning, particularly classification algorithms, has become essential for proactive fraud detection by learning complex patterns from historical transaction data.  
This experiment investigates the application of **Support Vector Machines (SVM)** — a powerful supervised learning algorithm renowned for its effectiveness in high-dimensional spaces and strong theoretical foundation — to the task of credit card fraud detection.

#### **Support Vector Machine (SVM)**

SVM constructs an optimal **hyperplane** that separates classes while **maximizing the margin** — the distance to the nearest points (support vectors) from each class.

##### **Key Concepts**

- The data points closest to the hyperplane are called **support vectors**. Only these points influence the position and orientation of the final hyperplane.
- Maximizing the margin improves generalization performance on unseen data.
- For datasets that are not perfectly separable, SVM introduces **slack variables** (ξᵢ) and a regularization parameter **C** to allow controlled misclassifications (soft margin SVM).


**Primal Optimization Problem (Soft Margin SVM):**

**`min (1/2) ||w||² + C Σ(i=1 to n) ξᵢ`**

Subject to:  
**`yᵢ (wᵀ φ(xᵢ) + b) ≥ 1 − ξᵢ`** and **`ξᵢ ≥ 0  ∀i`**

##### **Why SVM is Effective for Fraud Detection**

- Naturally handles high-dimensional feature spaces (common in anonymized transaction datasets)
- Robust to noise and outliers when properly regularized
- Performs well with relatively small numbers of positive (fraud) examples
- Offers strong theoretical guarantees on generalization

#### **Linear vs. Non-Linear SVM**

| Type               | When to Use                                        | Decision Boundary            |
|--------------------|----------------------------------------------------|------------------------------|
| **Linear SVM**     | Classes nearly separable by a straight line        | Straight hyperplane          |
| **Non-Linear SVM** | Real-world fraud: complex, overlapping patterns    | Curved/flexible boundary     |

Fraud data is almost always **non-linearly separable** → kernel SVM is essential.

#### **Kernel Functions (The Kernel Trick)**

| Kernel                  | Formula                                                      | Best For / Characteristics                              |
|-------------------------|--------------------------------------------------------------|----------------------------------------------------------|
| **Linear**              | **`K(xᵢ, xⱼ) = xᵢᵀ xⱼ`**                                    | Fast, good when data is almost linearly separable       |
| **Polynomial**          | **`K(xᵢ, xⱼ) = (γ xᵢᵀ xⱼ + r)ᵈ`**                          | Captures polynomial patterns; d = degree                 |
| **RBF / Gaussian**      | **`K(xᵢ, xⱼ) = exp(−γ ||xᵢ − xⱼ||²)`**                     | Most popular for fraud detection — highly flexible        |
| **Sigmoid**             | **`K(xᵢ, xⱼ) = tanh(γ xᵢᵀ xⱼ + r)`**                       | Rarely used in practice                                   |

**RBF kernel almost always wins** in credit card fraud tasks.

#### **Important Hyperparameters**

| Parameter | Role                                                      | Effect of Values                                           |
|----------|-----------------------------------------------------------|------------------------------------------------------------|
| **C**    | Controls penalty for misclassification                     | Small C → softer margin, more tolerant<br>Large C harder margin, less tolerant (can overfit) |
| **γ (gamma)**  | How far the influence of a single training point reaches   | Small γ smooth boundary<br>Large γ tight, complex boundary (overfitting risk) |

Optimal (C, γ) are usually found via grid/random search with cross-validation.

#### **Challenges in Credit Card Fraud Detection**

- Extreme class imbalance (fraud < 0.1–1% of transactions)
- Concept drift (fraud patterns change over time)
- Need for very high recall on fraud class while keeping false positives low

Because of imbalance, **accuracy is misleading**. Preferred metrics are:

- **Precision**, **Recall**, **F1-score** (especially on the fraud class)
- **Precision-Recall AUC** (PR-AUC) — more informative than ROC-AUC in highly imbalanced settings
- **Confusion Matrix** and **Cost-sensitive evaluation**