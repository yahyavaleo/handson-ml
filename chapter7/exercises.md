## If you have trained five different models on the exact same training data, and they all achieve 95% precision, is there any change that you can combine these models to get better results? If so, how? If not, why?

If you have trained five different models and they all achieve 95% precision, it is possible to combine them into a voting ensemble which will often result in a better precision.

It works better if the models are very different (such as one is a support vector machine, the other is a decision tree, and so on). Different models tend to make different types of errors on the same data. By combining them, the errors are averaged out. It is even better if the models are also trained on different random subsets of the training set.

## What is the difference between hard and soft voting?

A hard voting classifier simply counts the votes of each predictor in the ensemble and picks the class with the most votes. A soft voting classifier computes the average estimated probability for each class and picks the class with the highest probability. This gives higher confidence votes more weight and results in better performance.

## Is it possible to speed up training of a bagging ensemble by distributing it across multiple servers? What about pasting ensembles, boosting ensembles, random forests, or stacking ensembles?

It is possible to speed up the training of a bagging ensemble, pasting ensemble, and random forest since each predictor in the ensemble is independent of each other.

However, each predictor in a boosting ensembles is built upon a previous predictor, so the training is strictly sequential. This does not allow the ensemble training to be distributed across multiple servers.

Predictors in a single layer of a stacking ensemble is independent of each other, so the training of the predictors in each layer can be distributed across different servers, but the next layer's predictors can only be trained after the previous layer's predictors are trained.

## What is the benefit of out-of-bag evaluation?

In a bagging (bootstrap aggregation) ensemble, the training set is sampled with replacement. Therefore, only aout 63% of the training set is sampled for each predictor, while the remaining 37% is not sampled for that predictor, and are called out-of-bag instances.

Since the predictor has not been trained on these out-of-bag instances, it can be evaluated on these oob instances, without the need for a separate validation set or cross-validation. The ensemble can itself by evaluated by averaging out the oob evaluations of each predictor.

## What makes extra-trees more random than regular random forests? How can this randomness help? Are extra-trees slower or faster than regular random forests?

An extra-tree (extremely randomized tree) is more random than a regular random forest, since apart from selecting a random subset of features at each split, it also uses a random threshold for each feature instead of searching for the best possible threshold.

This makes the extra-trees faster to train than regular random forests, since finding the best possible threshold for each feature at every node is a very time-consuming task.

## If you AdaBoost ensemble underfits the training data, what hyperparameters should you tweak and how?

If an AdaBoost ensemble underfits the training data, the number of estimators should be increased, the learning rate should be increased, or the regularization hyperparameters of the base estimator should be decreased.

## If your gradient boosting ensemble overfits the training set, should you increase or decrease the learning rate?

If a gradient boosting ensemble overfits the training set, its learning rate should be decreased. Moreover, early stopping should be implemented to find the best number of predictors.
