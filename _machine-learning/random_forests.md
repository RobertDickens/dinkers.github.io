---
layout: post
title:  "Random Forests"
description: "Ensemble machine learning algorithm consisting of multiple decision trees."
---

Random forests are an ensemble method for building predictive models. More precisely, random forests are use the ensemble technique of *bagging*. Bagging is a learning approach in which multiple learners are trained on bootstrap samples (samples from the dataset taken with replacement). The output of these learners is then averaged to give a final prediction. The term *bagging* is comes from '**b**oostrap **agg**regating'.  The goal of bagging is to reduce the variance of a model (i.e. prevent overfitting). In the case of random forests, the base learners are decision trees (or decision tree stumps).

# Training random forests and making predictions

The process of training a Random Forest is relatively straightforward and easy to understand if you understand the process of growing a single decision tree.

1. Take a bootstrap sample (i.e. a random sample **with** replacement) from the dataset.
2. Select a subset of features at random.
3. Use the sample and features to grow a decision tree. This decision tree can be grown to the largest extent possible or limited by early stopping.
4. Repeat this process for $$n$$ trees.

To make a prediction on new instance, it is run down each of the trees in the forest to make an individual prediction for that tree. The final prediction is a combination of the output from each tree. For regression, this is an average of the predicted values. For classification, it is the class that has the most 'votes' from all the trees.

## Advantageous Features of Random Forests

### Robust to Overfitting

The averaging effect of bagging (taking bootstrap samples) means that random forests are much less prone to overfitting than single decision trees. In addition, since the trees are independent, increasing the number of trees will never increase the generalization error that arises due to overfitting.

### Requires little data pre-processing

As is the case for decision trees, random forests can trivially handle both categorical and continuous features. They do not require feature scaling and are relatively robust to outliers.

### Provide out-of-bag (OOB) error estimate

Machine learning models usually require cross-validation on separate test sets to give an unbiased estimate of the test set error. Random forests, on the other hand, can estimate the test error internally during training.

Each tree is trained on a bootstrap sample that leaves out around one-third of the cases. The left-out cases can be run down the constructed tree and their prediction error calculated. The average of these cases gives the out-of-bag estimate. Several studies have found this to be a relatively reliable indication of the accuracy on unseen data, although it is generally recommended to use separate test sets for a thorough analysis of model accuracy.

### Feature importance

Random forests can implicitly calculate feature importances by looking at how much the tree nodes reduce the impurity on average (over all trees in the forest). This average is weighted based on the number of training samples associated with each node.

### Parallelizable

Since each tree is trained in isolation with no dependence on the other trees, the random forest algorithm is relatively easily to parallelize.
