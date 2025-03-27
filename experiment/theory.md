### Introduction

Credit card fraud is a growing concern in the digital age, leading to significant financial losses and security risks. Traditional detection methods often fall short in identifying complex fraud patterns, making machine learning a powerful alternative. This experimet focuses on using Support Vector Machine (SVM), a supervised learning algorithm known for its effectiveness in classification tasks, to predict fraudulent credit card transactions.

### Support Vector Machine (SVM)

Support Vector Machine is a supervised machine learning algorithm primarily used for classification tasks. The main idea behind SVM is to find the optimal hyperplane that best separates the data points of different classes in the feature space. The "support vectors" are the data points that lie closest to the decision boundary and are most critical in defining the hyperplane.

SVM works well for both linear and non-linear classification problems. When data is linearly separable, a Linear SVM is sufficient. However, when data is not linearly separable, Non-linear SVMs are used by applying kernel functions to project the data into a higher-dimensional space where it becomes linearly separable.

### Kernel Functions

Kernel functions allow SVMs to operate in a high-dimensional, implicit feature space without having to compute the coordinates of the data in that space explicitly. Common kernel functions include:

<ul>
  <li>Linear Kernel: Suitable for linearly separable data.</li>

  <li>Polynomial Kernel: Projects data into a higher-dimensional polynomial space.</li>
 
  <li>Radial Basis Function (RBF) Kernel: Also known as the Gaussian kernel, ideal for non-linear data.</li>
  
</ul>

### Credit Card Fraud Detection with SVM

Credit card fraud detection is a vital application of machine learning in the financial sector, where the goal is to accurately identify fraudulent transactions from a large volume of legitimate ones. Due to the highly imbalanced nature of the data—where fraudulent transactions represent a very small portion—detecting fraud becomes a challenging task. Support Vector Machine (SVM) is particularly well-suited for such classification problems because of its ability to find an optimal decision boundary between classes, even in high-dimensional spaces. In fraud detection, SVM helps distinguish between normal and suspicious behavior by creating a hyperplane that maximizes the margin between different classes. Linear SVMs work efficiently when data is linearly separable, but real-world fraud data is often non-linear and complex. In such cases, kernel functions like Polynomial and Radial Basis Function (RBF) are used to transform the data into higher dimensions, allowing for better separation. SVM models are trained and fine-tuned using hyperparameters such as the regularization parameter (C) and the kernel coefficient (γ) to balance accuracy and generalization. By evaluating performance through metrics like precision, recall, and accuracy, SVM proves to be an effective tool for identifying fraudulent credit card transactions and minimizing false positives.
