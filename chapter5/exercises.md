## What is the fundamental idea behind support vector machines?

The fundamental idea behind support vector machines is to select a decision boundary that maximizes its margin from the training instances. In soft margin classification, the SVM tries to find a balance between perfectly separating the two classes and having the maximum margin.

## What is a support vector?

Support vectors are the training instances that lies on or within the maximum margin hyperplane. The decision boundary is solely influenced by the support vectors, while the rest of the training instances have no impact. Once training is done, the predictions are performed using only support vectors and the resulting maximum margin hyperplane.

## Why is it so important to scale the inputs when using SVMs?

Support vector machines are very sensitive to the feature scale. If the features are not scaled, the SVM will tend to ignore smaller features when computing the maximum margin hyperplane.

## Can an SVM classifier output a confidence score when it classifies an instance? What about a probability?

No, by default, an SVM classifier can only calculate the distance between the classified instance and the decision boundary. It has no ability to output a corresponding probability.

## Should you use the primal or dual form of the SVM problem to train a model on a training set with millions of instances and hundreds of features?

For training a model on a training set with millions of instances and hundred of features (instances are much more than the features), it is better to use the primal form of the SVM problem, since the primal form is very efficient at handling a large number of training instances, and there is no need to apply the kernel trick since the number of features is small.

However, if the number of features is much more than the training instances, the dual form should be used, since it allows to use the kernel trick, which makes handling large number of features much more efficient.

## Say you trained an SVM classifier with an RBF kernel. It seems to underfit the training set. Should you increase or decrease the gamma hyperparameter? What about the regularization hyperparameter?

The gamma hyperparameter is the inverse of the radius of influence of each training instance, while the regularization hyperparameter `C` controls the balance between selecting a larger margin and classifying all training points correctly. A smaller `C` will encourage a larger margin at the cost of reducing training accuracy.

If the model is underfitting the training set, the gamma hyperparameter needs to be increased, and the regularization hyperparameter `C` needs to be increased as well. This ensures that the model fits the training set more accurately.

## How should you set the QP parameters ($H$, $f$, $A$, and $b$) to solve the soft margin linear SVM classifier problem using an off-the-shelf QP solver?

To solve the soft margin linear Support Vector Machine (SVM) classification problem using a Quadratic Programming (QP) solver, we need to formulate the SVM problem in the standard form of a QP problem. The standard form of a QP problem is:

$$
\min_{\mathbf{x}} \frac{1}{2} \mathbf{x}^T H \mathbf{x} + \mathbf{f}^T \mathbf{x}
$$

subject to:

$$
A \mathbf{x} \leq \mathbf{b}
$$

For the soft margin SVM, we aim to minimize the following objective function:

$$
\frac{1}{2} \|\mathbf{w}\|^2 + C \sum_{i=1}^{N} \xi_i
$$

subject to the constraints:

$$
y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1 - \xi_i, \quad \xi_i \geq 0, \quad \forall i = 1, \ldots, N
$$

Here, $\mathbf{w}$ is the weight vector, $b$ is the bias term, $\xi_i$ are the slack variables, $C$ is the regularization parameter, $y_i$ are the class labels $(\pm 1$), and $\mathbf{x}_i$ are the input vectors.

To convert this into the QP form, let's define the optimization variables as $\mathbf{x} = [\mathbf{w}^T, b, \xi_1, \xi_2, \ldots, \xi_N]^T$.

1. **Objective Function**: We need to express $\frac{1}{2} \|\mathbf{w}\|^2 + C \sum_{i=1}^{N} \xi_i$ in the form $\frac{1}{2} \mathbf{x}^T H \mathbf{x} + \mathbf{f}^T \mathbf{x}$.

   - The matrix $H$ captures the quadratic terms and is given by:

     $$
     H = \begin{bmatrix}
     I & 0 & 0 \\
     0 & 0 & 0 \\
     0 & 0 & 0
     \end{bmatrix}
     $$

     Here, $I$ is an identity matrix of size $d \times d$, where $d$ is the number of features.

   - The vector $\mathbf{f}$ captures the linear terms and is given by:

     $$
     \mathbf{f} = \begin{bmatrix}
     0 \\
     0 \\
     C \mathbf{1}
     \end{bmatrix}
     $$

     where $\mathbf{1}$ is a vector of ones of length $N$ (the number of training examples).

2. **Inequality Constraints**: We need to express the constraints $y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1 - \xi_i$ and $\xi_i \geq 0$ in the form $A \mathbf{x} \leq \mathbf{b}$.

   - The first set of constraints $y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1 - \xi_i$ can be written as:

     $$
     y_i (\mathbf{w}^T \mathbf{x}_i + b) - \xi_i \geq 1
     $$

     This translates to:

     $$
     A_1 \mathbf{x} \leq \mathbf{b}_1
     $$

     where

     $$
     A_1 = \begin{bmatrix}
     -y_1 \mathbf{x}_1^T & -y_1 & -1 & 0 & \ldots & 0 \\
     -y_2 \mathbf{x}_2^T & -y_2 & 0 & -1 & \ldots & 0 \\
     \vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
     -y_N \mathbf{x}_N^T & -y_N & 0 & 0 & \ldots & -1
     \end{bmatrix}
     $$

     and

     $$
     \mathbf{b}_1 = -\mathbf{1}
     $$

   - The second set of constraints $\xi_i \geq 0$ can be written as:

     $$
     A_2 \mathbf{x} \leq \mathbf{b}_2
     $$

     where

     $$
     A_2 = \begin{bmatrix}
     0 & 0 & -I
     \end{bmatrix}
     $$

     and

     $$
     \mathbf{b}_2 = 0
     $$

3. **Combining Constraints**:

   - Combine $A_1$ and $A_2$ into a single matrix $A$:

     $$
     A = \begin{bmatrix}
     A_1 \\
     A_2
     \end{bmatrix}
     $$

   - Combine $\mathbf{b}_1$ and $\mathbf{b}_2$ into a single vector $\mathbf{b}$:

     $$
     \mathbf{b} = \begin{bmatrix}
     \mathbf{b}_1 \\
     \mathbf{b}_2
     \end{bmatrix}
     $$

Putting it all together, the QP parameters for the soft margin linear SVM are:

- $H = \begin{bmatrix} I & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{bmatrix}$
- $\mathbf{f} = \begin{bmatrix} 0 \\ 0 \\ C \mathbf{1} \end{bmatrix}$
- $A = \begin{bmatrix} A_1 \\ A_2 \end{bmatrix}$
- $\mathbf{b} = \begin{bmatrix} \mathbf{b}_1 \\ \mathbf{b}_2 \end{bmatrix}$

where $I$ is the identity matrix of size $d \times d$, $\mathbf{1}$ is a vector of ones of length $N$, $A_1$ and $A_2$ are as defined above, and $\mathbf{b}_1 = -\mathbf{1}$, $\mathbf{b}_2 = 0$.
