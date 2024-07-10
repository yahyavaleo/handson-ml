## What linear regression training algorithm can you use if you have a training set with millions of features?

For a training set with millions of features, stochastic gradient descent or mini-batch gradient descent can be used (even batch gradient descent can be used if the data can fit in memory).

However, linear regression models solved using normal equation or singular value decomposition cannot be used since their complexity grows quickly (more than quadratically) with the number of features.

## Suppose the features in your training set have very different scales. What algorithms might suffer from this, and how? What can you do about it?

If the features in the training set have very different scales, the cost function will have the shape of an elongated bowl. Therefore, the gradient descent algorithms will take a longer time to converge.

Moreover, because regularization methods penalize larger weights, if features have different scales, features with smaller values will tend to be ignored compared to features with larger values. This results in a suboptimal solution.

To fix this, the training set should be scaled using, for example, `sklearn.preprocessing.StandardScaler`.

## Can gradient descent get stuck in a local minimum when training a logistic regression model?

No, the gradient descent cannot get stuck in a local minimum when training a logistic regression model because its cost function is convex.

## Do all gradient descent algorithms lead to the same model provided you them run long enough?

If the optimization problem is convex, then all gradient descent algorithms will approach the global minimum (assuming that the learning rate is not too high), and end up producing fairly similar models.

However, if the optimization problem is not convex, batch gradient descent can potentially get stuck in a local minimum, whereas stochastic and mini-batch gradient descent do not get stuck in local minimum. Therefore, batch gradient descent can produce a suboptimal model.

If the learning rate is not reduced gradually, stochastic and mini-batch gradient descent will never truly converge (they will dance around the global minimum). As a result, these gradient descent algorithms can produce slightly different models, even if you let them run long enough.

## Suppose you use batch gradient descent and plot the validation error at every epoch. If you notice that the validation error consistently goes up, what is likely going on? How can you fix this?

If the validation error consistently goes up and the training error also goes up, it is likely that the batch gradient descent is diverging. In this scenario, the learning rate should be decreased.

If the validation error consistently goes up but the training error does not go up, it is likely that the model is overfitting. In this scenario, the training should be stopped and the best model (for which the validation error was minimum) should be used.

## Is it a good idea to stop mini-batch gradient descent immediately when the validation error goes up?

No, mini-batch and stochastic gradient descent do not guarantee that the algorithm gets closer to the global mimumum at every training epoch due to their random nature. As a result, if the training is stopped immediately when the validation error goes up, it is very likely that the algorithm has not yet fully converged.

For these algorithms, it is better to let the training continue even after the validation error goes up. Only when the validation error has not improved for some large enough time should the training be stopped. Consequently, the model should be reverted to the best saved model.

## Which gradient descent algorithm will reach the vicinity of the optimal solution the fastest? Which will actually converge? How can you make the others converge as well?

Stochastic gradient descent is the fastest gradient descent algorithm since it only considers a single training instance at each iteration. As a result, it will reach the vicinity of the optimal solution the fastest.

Only batch gradient descent acutally converges to the global minimum (provided that the cost function is convex). Both stochastic and mini-batch gradient descent bounce around the global minimum. To make them converge, the learning rate should be gradually reduced using a learning schedule.

## Suppose you are using polynomial regression. You plot the learning curves and you notice that there is a large gap between the training error and the validation error. What is happening? What are three ways to solve this?

If there is a large gap between the training error and the validation error, the model is most likely overfitting. To solve this:

- use a model with less bias
- add regularization to the model
- increase the training set size

## Suppose you are using ridge regression and you notice that the training error and the validation error are almost equal and fairly high. Would you say that the model suffers from high bias or high variance? Should you increase the regularization strength hyperparameter or reduce it?

If both the training error and validation error are fairly high and almost equal, the model suffers from high bias. In this case, a simpler model (one with low bias) should be used. In this case, the regularization hyperparameter $\alpha$ should be reduced.

## Why would you want to use: ridge regression instead of linear regression, lasso instead of ridge regression, and elastic-net instead of lasso?

Linear regression is unregularized, which can cause the model to overfit. Therefore, to prevent the model from overfitting, ridge regression is used which adds $l_2$ penalty.

Ridge regression minimizes the model weights, however, it does not fully eradicate them. LASSO, on the other hand, uses $l_1$ penalty which forces some weights down to exactly zero. This is useful when the model has correlated features or when feature selection is to be performed.

However, LASSO behaves erratically in some cases (when several features are strongly correlated or when there are more features than training instances). In such scenarios, elastic-net is preferred over LASSO.

## Suppose you want to classify pictures as outdoor/indoor and daytime/nighttime. Should you implement two logistic regression classifiers or one softmax regression classifier?

If a model needs to classify pictures in two ways: outdoor/indoor and daytime/nighttime, it is a multioutput model. Softmax regression cannot output multiple classes at the same time (it only deals with multiclass problems).

Because the two outputs of our model are not mutually exclusive, we need to train two logistic regression classifiers: one for outdoor/indoor classification and the other for daytime/nighttime classification.
