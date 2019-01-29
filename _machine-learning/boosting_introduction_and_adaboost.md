---
layout: post
title:  "Boosting Part 1: Introduction and AdaBoost"
description: "An introduction to the concept of boosting and a guide to the AdaBoost algorithm."
---

# Boosting Introduction
Boosting is an ensemble machine learning method that converts weak learners (a learner that is slightly better than random guessing) into strong learners. Boosting is a sequential process, each learner is trained using information from the previous learner. This is in contrast to *bagging*, in which the learners are trained in parallel (e.g. in the Random Forest algorithm).

We will look at two boosting algorithms: AdaBoost and Gradient Boosting (see part 2). Both these algorithms create a strong learner from weak learners, however they differ in how they create the weak learners during the training process.

## AdaBoost
AdaBoost (short for **Ada**ptive **Boost**ing) was the first practical boosting algorithm. It was introduced by Freund and Schapire in 1997, who later went on to win the Gödel prize for the work.

AdaBoost works by sequentially training a series of weak classifiers (most commonly decision trees with a single node, known as *decision stumps*), with each classifier giving more weight to training examples that were incorrectly classified in the previous iteration. The final model is a weighted sum of all the classifiers.

The AdaBoost algorithm proceeds as follows:
1. Initialise the observation weights, giving equal weight to each training example: $$w_i$$ = 1/N for a training set with N examples.
2. For $$m$$ in $$M$$ iterations:

    a. Fit a classifier $$G_m(x)$$ to the training data.

    b. Compute the error for this classifier.
     <br/> $$err_m=\frac{\sum^N_{i=1}w_i I(y_i \ne G_m(x_i))}{\sum^N_{i=1} w_i}$$

    c. Compute the weight that this classifier will be given in the final model. $$\alpha_m = log(\frac{1-err_m}{err_m})$$.

    d. Set new weights $$w_i \leftarrow w_i .exp[\alpha_m.I(y_i \ne G_m(x_i))]$$
3. The final model output is givem by:
 $$G(x)=sign[\sum^M_{m=1}\alpha_m G_m(x)]$$

#### Explanation of classifier weighting
Each classifier is given a weighting in the final model (see step 2b) which is a function of its error rate. Plotting this function gives helps give some intuition:
![](\assets/adaboost_clf_weighting.png)
There are three things to note here. Firstly, the classifier weight increases exponentially as the classifier error decreases towards zero, i.e. accurate classifiers are given higher weight. Secondly, classifier weight grows exponentially negative as the error rate approaches 1. This means that classifiers with error rate > 0.5 still contribute to the final model by taking the opposite of their output. Finally, classifiers with error rate of 0.5 are given zero weighting, since they are no better than random guessing.

#### Explanation of training example weighting
The weights are updated by an exponential function. Again, plotting the function helps provide intuition for how this works:
![](\assets/exp.png)

The weight of a training sample will be increased or decreased depending on the sign of $$I(y_i \ne G_m(x_i))$$. The exponential function returns a fraction for negative values and a value $>1$ for positive values. Therefore, incorrectly classified samples will have their weight increased while correctly classified samples will have their weight decreased.

Note that alpha is also included in the weight update function. This takes into account the accuracy of the classifier itself. A less accurate classifier will have a smaller impact on the weights than a more accurate classifier.

#### Adaboost Demonstration in Python
The Scikit-learn library contains excellent implementations of the Adaboost algorithm for both classification and regression tasks. However, for illustration purposes the following code shows the algorithm implemented from scratch, using Scikit learn decision trees as the base learner:

```python
class AdaBoostClassifier:
    def __init__(self, n_iterations):
        self.n_iterations = n_iterations
        self.clfs = []
        self.clf_alphas = []
        self.weights = None

    def fit(self, X, y):
        # Initialise weights if first iteration
        for n in range(self.n_iterations):

            if self.weights is None:
                self.weights = np.ones(len(X)) / len(X)

            # Fit model with weights
            base_clf = DecisionTreeClassifier(max_depth=1)
            base_clf.fit(X, y, sample_weight=self.weights)

            # Get hypothesis of base model
            model_hypothesis = base_clf.predict(X)

            # Calculate error and alpha
            misclassified_bool = model_hypothesis != np.array(y)
            misclassified_i = np.array([int(x) for x in misclassified_bool])
            misclassified_sign = np.array([-1 if x == 0 else 1 for x in misclassified_i])

            err_m = np.dot(self.weights, misclassified_i) / np.sum(self.weights)
            epsilon = 1e-5
            err_m = err_m + epsilon
            alpha_m = 0.5 * np.log((1 - err_m) / err_m)

            # Update weights
            update_factors = np.exp(alpha_m * misclassified_sign)
            updated_weights = self.weights * update_factors
            self.weights = updated_weights

            plt.show()

            self.clfs.append(deepcopy(base_clf))
            self.clf_alphas.append(alpha_m)


    def predict(self, X):
        predictions = []

        for alpha, model in zip(self.clf_alphas, self.clfs):
            prediction = model.predict(X)
            prediction_sign = [-1 if pred == 0 else 1 for pred in prediction]
            weighted_prediction = alpha * np.array(prediction_sign)
            predictions.append(weighted_prediction)

        ensemble_output = np.sum(np.array(predictions), axis=0)
        ensemble_predictions = np.array([0 if pred < 0 else 1 for pred in ensemble_output])

        return ensemble_predictions
```
We can use this code to visualise each iteration of the training process. In the following example, the Adaboost algorithm is used to train a binary classification model. Each set of figures shows the training samples with their relative weights indicated by their transparency (left) and the decision stump decision boundary for that iteration (right).
![](\assets/adaboost_training.png)

The final model is a weighted combination of all the decision stumps:
![](\assets/adaboost_final_model.png)

### Advantages and Disadvantages of Adaboost
#### Advantages
- Simple to implement.
- Relatively fast to train.
- Few parameters to tune (number of iterations and choice of base learner).

#### Disadvantages
- Can overfit.
- Susceptible to uniform noise.
