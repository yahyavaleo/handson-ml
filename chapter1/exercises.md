## 1. How would you define machine learning?

A computer program is said to learn from experience $E$ with respect to some class of tasks $T$ and performance measure $P$ if its performance at tasks in $T$, as measured by $P$, improves with experience $E$.

## 2. Can you name four types of problems where it shines?

Machine learning is great for complex problems:

- that have no algorithmic solution available.
- which would require long list of hand-tuned rules.
- where the system needs to adapt to fluctuating environments.
- where information is to be extracted from data.

## 3. What is a labeled training set?

A training set is called a labeled training set if it has labels (desired outcome) for each instance in the dataset.

## 4. What are the two most common supervised tasks?

The two most common supervised tasks are classification and regression.

## 5. Can you name four common unsupervised tasks?

The four common unsupervised tasks are dimenionality reduction, clustering, visualization, and association rule learning.

## 6. What type of machine learning algorithm would you use to allow a robot to walk in various unknown terrains?

Some type of reinforcement learning needs to be used to allow a robot to walk in various unknown terrains, since this problem cannot be easily stated as a supervised learning or unsupervised learning problem.

## 7. What type of machine learning algorithm would you use to segment your customers into multiple groups?

This problem of segmenting customers into multiple groups can be stated as a clustering problem (unsupervised learning) or a classification problem (supervised learning), depending on whether there are labels available for each customer group.

## 8. Would you frame the problem of spam detection as a supervised learning problem or an unsupervised learning problem?

Spam detection is usually stated as a supervised learning (classification) problem.

## 9. What is an online learning system?

An online learning system can learn incremently, as opposed to batch learning where the entire dataset needs to be fed to the system prior to use. This allows the system to adapt to fluctuating environments. This also makes it possible for the model to be trained on a huge amount of data.

## 10. What is out-of-core learning?

In out-of-core learning, the data is divided into small chunks called mini-batches, which are then fed to the system sequentially. This allows the system to be trained on a huge amount of data that cannot fit into the computer's main memory.

## 11. What type of learning algorithm relies on a similarity measure to make predictions?

Instance-based learning algorithms rely on a similarity measure to make predictions.

## 12. What is the difference between a model parameter and a learning algorithm's hyperparameter?

Model parameters are configuration variables that is internal to the model and is estimated from the data. A hyperparameter is a configuration variable that is external to the model and cannot be estimated from the data.

## 13. What do model-based learning algorithms search for? What is the most common strategy they use to succeed? How do they make predictions?

A model-based learning algorithm searches for the optimal values for the model parameters such that it generalizes well to unseen data. The most common strategy to find these optimal model parameters is to minimize a cost function, and additionaly may be a complexity cost if the model is regularized.

The model makes predictions by feeding the new instance's features into the prediction function whose parameters were learned during the training phase.

## 14. Can you name four of the main challenges in machine learning?

Some of the main challenges in machine learning are lack of data, unrepresentative data, uninformative features, correlated features, overly simple models that underfit the data, and overly complex models that overfit the data.

## 15. If your model performs great on the training data but generalizes poorly to new instances, what is happening? Can you name three possible solutions?

If the model performs great on the training data but generalizes poorly to new instances, it is most likely overfitting the training data. To minimize overfitting, we can:

- increase the amount of training data,
- reduce noise in the training data,
- add a regularization to the model, or
- choose a simpler model.

## 16. What is a test set and why would you want to use it?

A test set is holdout set that is used to estimate the model's generalization error.

## 17. What is the purpose of a validation set?

A validation set is another holdout set that is used to compare model's performance and choose the best model. This best model is then tested on the test set. A validation set thereby allows to tune the model's hyperparameters.

## 18. What can go wrong if you tune hyperparameters using the test set?

If the model's hyperparameters are tuned using the test set, then the best model selected would the model that performs good on the test set, and therefore has overfit the test set. Such a model will be optimist and will not generalize well to truly unseen data when launched in production.

## 19. What is cross-validation and why would you prefer it to a validation set?

In cross-validation, the training set is divided into k-folds, and each model is validated on a different fold while trained on the remaining folds. This method is preferrable to the validation set when the training data is small.
