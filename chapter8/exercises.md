## What are the main motivations for reducing a dataset's dimensionality? What are the main drawbacks?

The main motivation for reducing a dataset's dimensionality is to speed up the subsequent training algorithm. In some cases, it makes the estimator perform better, if the dataset contains noise or redundant features. It is also easier to visualize data in lower dimensions. Moreover, it can be used as a way to compress data.

The main drawback is loss of information, which can degrade the performance of subsequent training algorithm. Moreover, the transformed features are hard to interpret, and it is not possible to fully recover the original dataset.

## What is the curse of dimensionality?

The curse of dimensionality refers to the problems that arise in higher dimensions but do not exist in lower dimensions. An example is data sparsity; as dimensions increase, the data becomes sparse which makes clustering and classification tasks challenging. This can cause the model to overfit.

Moreover, distances lose meaning in higher dimensional data, since the difference between data points tends to become negligible. This causes problems for algorithms that rely on distance measure such as K-nearest neighbors.

## Once a dataset's dimensionality has been reduced, is it possible to reverse the operation? If so, how? If not, why?

Reducing a dataset's dimensionality results in loss of information which makes it impossible to recover the original dataset perfectly. Moreover, although some algorithms, such as PCA, have some mechanism to perform the reverse operation, other algorithms, such as t-SNE, do not have this ability.

## Can PCA be used to reduce the dimensionality of a highly nonlinear dataset?

Principal component analysis can be used to reduce the dimensionality of most datasets, even if they are highly nonlinear, because it can get rid of useless dimensions. However, if there are no useless dimensions, such as in the Swiss roll dataset, then PCA will lose too much information.

## Suppose you perform PCA on a 1000-dimensional dataset, setting the explained variance ratio to 95%. How many dimensions will the resulting dataset have?

The number of dimensions in the resulting dataset depends heavily on the nature of the dataset. If the dataset has almost all of its variance along a single axis, the resulting dataset will have only 1 dimension. However, if the data points are scattered completely randomly along the 1000 dimensions, all 1000 dimensions will be required to preserve 95% of the variance.

To calculate the number of dimensions in the resulting dataset, the explained variance can be plotted against the number of dimensions used for PCA.

## In what cases would you use vanilla PCA, incremental PCA, randomized PCA, or kernel PCA?

If the dataset can fit into the memory, regular PCA is used. If the dataset is large (cannot fit into the memory) or it is an online task (new instances arrive and PCA needs to be applied on the fly), incremental PCA is used, however, it is generally slower than regular PCA.

Randomized PCA is used when the dimensionality needs to be reduced considerably and the dataset fits into the memory. Finally, kernel PCA is used for nonlinear datasets.

## How can you evaluate the performance of a dimensionality reduction algorithm on your dataset?

Although dimensionality reduction is an unsupervised task and there is not performance measure available, usually it is used as a preprocessing step for a supervised learning task.

In this case, the performance of the dimensionality reduction algorithm can be implicitly judged by the performance of the subsequent supervised learning algorithm. If the algorithm's performance is almost the same as it was on the original dataset, the dimensionality reduction algorithm is good and did not lose too much information.

Another method would be to apply the reverse transformation and measure the reconstruction error. However, not all dimensionality reduction algorithms provide a mechanism to perform the reverse transformation.

## Does it make any sense to chain two different dimensionality reduction algorithms?

Yes, it can make sense to chain two different dimensionality reduction algorithms. A common example is to use PCA to quickly get rid of a large number of useless dimensions, and then applying another much slower dimensionality reduction algorithm, such as LLE. This two-step approach will likely yield the same performance as using LLE only, but will be much faster.
