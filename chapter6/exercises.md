## What is the approximate depth of a decision tree trained (without restrictions) on a training set with 1 million instances?

Decision trees are approximately balanced so each each node splits the dataset into two subsets. Therefore, an unrestricted decision tree trained on 1 million instances will have a depth of approximately $\log_2(m) = \log_2(1,000,000) \approx 20$.

## Is a node's Gini impurity generally lower or greater than its parent's Gini impurity? Is it generally lower/greater or always lower/greater?

A node's Gini impurity is generally lower than its parent's Gini impurity. This is ensured by the CART algorithm's cost function, which splits each node in a way that minimizes the weighted sum of its children's Gini impurity.

However, if one child is smaller than the other, it is possible for it to have a higher Gini impurity than its parent, as long as this increase is more than compensated for by the decrease in the other child's Gini impurity.

For example, if a node has four instances of class A and one instance of class B, it has a Gini impurity of $1 - \frac{1^2}{5} - \frac{4^2}{5} = 0.32$. If the dataset is ordered as: A, B, A, A, A, the CART algorithm will split this node as: [A, B] and [A, A, A]. The first child has a Gini impurity of $1 - \frac{1^2}{2} - \frac{1^2}{2} = 0.5$, while the other child has a Gini impurity of $1 - \frac{3^2}{3} = 0$.

So, although the first child has a higher Gini impurity than its parent, it is compensated by the fact that the other child is pure, and the weighted sum of the Gini impurities is lower than its parent: $\frac{2}{5} \times 0.5 + \frac{3}{5} \times 0 = 0.2$, which is lower than the parent's Gini impurity.

## If a decision tree is overfitting the training set, is it a good idea to try decreasing the `max_depth`?

Yes, if a decision tree is overfitting the training set, it is likely that it is dividing the training set into very smaller subsets, which are capturing the noise in the training set. Therefore, it is a good idea to decrease the `max_depth` parameter to constrain the model.

## If a decision tree is underfitting the training set, is it a good idea to try scaling the input features?

Decision trees are insensitive to the feature scale, so if a decision tree is underfitting the training set, scaling the input features will have no effect.

## If it takes one hour to train a decision tree on a training set containing one million instances, roughly how much time will it take to train another decision tree on a training set containing 10 million instances?

The computational complexity of decision trees is $O(n \times m \log(m))$. So, if the training set size is increased by 10 folds, the training time will increase as:

$$
K = \frac{n \times 10m \log(10m)}{n \times m \log(m)} = 10 \frac{\log(10m)}{\log(m)}
$$

If $m = 10^6$, this results in $K \approx 11.7$, so it will take roughly 11.7 hours to train on the 10 million instance dataset.

## If your training set contains 100,000 instances, will setting `presort=True` speed up training?

Presorting the training set helps to decrease the training time if the dataset is smaller than a few thousand instances. However, if the dataset contains 100,000 instances, presorting will considerably increase the training time, since it will take a huge amount of time to sort that many instances.
