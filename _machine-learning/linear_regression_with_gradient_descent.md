---
layout: post
title:  "Linear Regression with Gradient Descent"
description: "Linear regression from scratch in python."
---

## Linear Regression with Gradient Descent

### Simple Linear Regression

Linear regression is one of the most simple and commonly used techniques in statistical analysis and machine learning. A linear regression model describes a dependent variable as a linear function of one or more independent variables.  

For simplicity, we'll begin with the case of a single independent variable, which is referred to as *simple linear regression*. In this case, the function that models dependent variable *y* with respect to an independent variable *x* has the form:

$$y(x) = mx + c$$

This function is a straight line, with slope *m* and y-intercept *c*


### Gradient Descent
To fit a model in this example, we will use the iterative optimisation algorithm *gradient descent*.

First, we need a quantitative measure of how good our model is. For each individual data point, we can work out the error simply by taking the difference between the actual value and the value predicted by our model:

![](assets/errors.png)

We can then define a *loss function* (also referred to as a *cost function*): a function that evaluates how badly the model fits the data based on all the errors. One of the most common loss functions used for regression tasks is the *mean squared error*:

$$ MSE = \frac{1}{n} \displaystyle \sum_{i=1}^{n}(y_{predicted}^{i} - y_{actual}^{i})^2$$

To calculate MSE, you take the difference between your predictions and the actual values, square it, and average across the whole dataset.

So, to fit a regression model to our training data, we need to change the slope *m* and the intercept *c* in order to **minimize the loss function**. Before going through the mathematics behind this we'll first develop an intuition for what gradient descent is actually doing.

Imagine you're on top of a hill at night. You want to get to the bottom of the hill, but you can't see which way to go. One approach would be to feel around for the direction which takes you downwards from where you're standing, then take a step in that direction. By repeating this process until you can no longer find a direction that will take you downwards, you will have found the *minimum* of the hill. Substitute the hill for the loss function and this is a good analogy for how the gradient descent algorithm works. This is easy to visualise for the MSE, because it's essentially just a square function:

![](\assets/gradient_descent.png)

In each iteration of the algorithm we the find direction that will reduce the output of the loss function and then take a 'step' (i.e. increase or decrease the value of *m* or *c*) in that direction. Mathematically, the way we find direction of steepest descent is by taking the *derivative* of the loss. The loss $$J$$ as a function of the error is:

$$J(Error) = \frac{1}{n} \displaystyle \sum_{i=1}^{n} Error^2_i$$

And the error as a function of the parameters $$m$$ and $$c$$ is:

$$Error(m, c) = mx + c - y_{actual}$$

So, by the chain rule, we can find the loss as a function of $$m$$ and $$c$$:

$$\frac{\partial J}{\partial m} = \frac{\partial J}{\partial Error} \times \frac{\partial Error}{\partial m} =  \frac{1}{n} \displaystyle \sum_{i=1}^{n}2x \times Error_i$$

$$\frac{\partial J}{\partial c} = \frac{\partial J}{\partial Error} \times \frac{\partial Error}{\partial c} =  \frac{1}{n} \displaystyle \sum_{i=1}^{n}2 \times Error_i$$

Now we have the gradient of the loss function we can define the update functions. These will change the values of the parameters at each iteration in order to take a 'step' towards a lower output from the loss function, and therefore a better fit. We also introduce a *learning rate* parameter that will change the size of the step that we take. This is necessary to avoid taking too large a step and overshooting past the minimum.

$$ m' = m - \displaystyle \sum_{i=1}^{n} (mx^{(i)} + c - y_{actual}) \times x^{(i)} \times learning \space rate$$

$$ c' = c - \displaystyle \sum_{i=1}^{n} (mx^{(i)} + c - y_{actual}) \times learning \space rate$$

Note that we are calculating this error over the entire dataset at each iteration. This is known as *batch gradient descent*. If the dataset is large this can be a costly operation, so we could instead update based on a subset of the data at each iteration, which is known as *minibatch gradient descent*. If we reduce the size of the data set to one training example per iteration this is known as *stochastic gradient descent*.

### Simple Linear Regression From Scratch in Python
First, let's create some data which we can use to fit a model. We'll create some data using the function *y = mx + c* setting m=3 and c=5, then add some random noise.

```python
import numpy as np
import pandas as pd
from matplotlib import pyplot as plt

X = np.arange(0, 20)
Y = 3 * X + 2 + np.random.normal(0, 4, len(X))
plt.scattter(X, Y)
plt.show()
```

This function will implement **batch gradient descent**. We'll also log the values of m, c and MSE at each iteration to examine later
```python
def batch_gradient_descent(X, Y, learning_rate=0.001, n_iter=50):
    # Initialise random initial values for slope and y-intercept
    m = random()
    c = random()

    logged_mse = []
    logged_m = []
    logged_c = []

    for _ in range(n_iter):
        predictions = m * X + c
        error = predictions - Y

        # update m and c
        new_m = m - (np.mean(error * X) * learning_rate)
        new_c = c - (np.mean(error) * learning_rate)
        m = new_m
        c = new_c

        # log m, c, and mse
        mse = np.mean((m * X + c - Y)**2)
        logged_mse.append(mse)
        logged_m.append(m)
        logged_c.append(c)

        # make log dataframe
        log = pd.DataFrame({'mse': logged_mse,
                             'm': logged_m,
                             'c': logged_c})

        return m, c, log
```

We'll also write a function to implement stochastic gradient descent, which will update the parameters based on a single training example at a time. This function will have the same logging functionality so we can examine how the behaviour differs. Note the new function argument *epochs*, this is the number of times the algorithm will traverse the entire dataset.

```python
def stochastic_gradient_descent(X, Y, learning_rate=0.001, epochs=5):
    # Initialise random initial values for slope and y-intercept
    m = random()
    c = random()

    logged_mse = []
    logged_m = []
    logged_c = []

    for _ in range(epochs):
        # update m and c
        for ix in range(len(X)):
            prediction = m * X[ix] + c
            error = prediction - Y[ix]

            new_m = m - (error * X[ix] * learning_rate)
            new_c = c - (error * learning_rate)
            m = new_m
            c = new_c

            # log m, c, and mse
            mse = np.mean((m * X + c - Y)**2)
            logged_mse.append(mse)
            logged_m.append(m)
            logged_c.append(c)

    # make log dataframe
    iter_log = pd.DataFrame({'mse': logged_mse,
                             'm': logged_m,
                             'c': logged_c})

    return m, c, iter_log
```

Now we can run both versions of gradient descent and examine how the values of $$m$$ and $$c$$ change as the algorithm progresses:

![](\assets/batch_parameter_update.png)

![](\assets/stochastic_parameter_update.png)

Batch gradient descent progresses smoothly through parameter space towards the minimum, while stochastic gradient descent takes a more erratic path and bounces around the minimum. This behaviour can be both a blessing and a curse. The negative is that it won't converge to real minimum. However this can help the algorithm bounce out of local minima in which batch gradient descent would get stuck. Stochastic therefore has more chance of finding the global minimum that batch.

### Multivariate Linear Regression

The case of more than one independent variable is called *Multivariate Linear Regression*. In this case, the function for the dependent variable $$Y$$ as a function of an arbitrary number of independent $$x$$ variables is:

$$f(x_1, x_2... x_n) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 \dots \theta_n x_n$$

The $$\theta_0$$ term here is the intercept (or bias) term. For convenience, we can set x<sub>0</sub> to always be 1. The function in vector notation is then:

$$ f(\textbf{X}) = \theta^T \textbf{X}$$

The loss function is again the mean squared error:

$$ J(\boldsymbol{\theta}) = \frac{1}{n} \displaystyle \sum_{i=1}^{n} (f(x^{(i)})-y^{(i)})^2$$

As with simple linear regression, we can use the chain rule to find the partial derivative of the cost function for each dependent variable. Noting that:

$$\frac{\partial f}{\partial \theta_m} = x_m$$

it follows that:

$$\frac{\partial \boldsymbol{J}}{\partial \theta_m} =  \frac{1}{n} \displaystyle \sum_{i=1}^{n}(f(x^{(i)}) - y^{(i)}) x_m$$

So, the update function for $$\theta_m$$ at each iteration is:

$$ \theta_m' = \theta_m -  \frac{1}{n} \displaystyle \sum_{i=1}^{n}(f(x^{(i)}) - y^{(i)}) x_m$$


### Linear Regression with Scikit-Learn
In this example we'll use the popular **Scikit-Learn** library to fit a multivariate linear regression model. We'll use publicly available data on Melbourne house prices (available on Kaggle https://www.kaggle.com/anthonypino/melbourne-housing-market/home) to fit a model of house price as a function of land size, number of rooms and house type.

First we'll import the Pandas library, the LinearRegression class from Sklearn and the csv containing the housing data. The pandas `.info()` method provides a convenient way to see some information about the dataframe.  

```python
import pandas as pd
from sklearn.linear_model import LinearRegression

housing_data = pd.read_csv(path_to_csv)
housing_data.info()
```

![](\assets/df_info.png)

We then select the columns we we're interested in and drop and rows with NaN values. The pandas `.head(n)` limits the dataframe to the first *n* features (default n=5).

```python
subset_of_columns = ['Rooms', 'Landsize', 'Type', 'Price']
housing_data = housing_data[subset_of_columns]
housing_data = housing_data.dropna()

print(housing_data.head())
```

![](\assets/first_head.png)

Note that the 'Type' column is not numeric, it is a *categorical variable* with three levels: 'h' (house), 'u' (unit) and 't' (townhouse). The linear regression algorithm can't handle raw categorical variables, so we need to create binary dummy variables for each categorical level.

```python
# Generate dummy columns and join to dataframe
house_type_dummies = pd.get_dummies(housing_data['Type'], drop_first=True)
housing_data = pd.concat([housing_data, house_type_dummies], axis=1)

# Drop categorical variable
housing_data = housing_data.drop('Type', axis=1)
print(housing_data.head())
```

![](\assets/second_head.png)

The dataframe now has dummy columns for the 'townhouse' and 'unit'. Since one level can be inferred from the other two (e.g. if it isn't 'townhouse' or a 'unit' then it must be 'house') the 'house' level has been dropped. This avoids problems with collinearity (the so-called 'dummy variable trap').

We can now fit a model:

```python
# Separate dependent and independent variables
train_input = housing_data.drop('Price', axis=1)
target_input = housing_data['Price']

# Create LinearRegression object and fit to the data
linear_model = LinearRegression()
linear_model.fit(X=train_input, y=target_input)
```

The parameters of the model are stored as attributes:

```python
linear_model.coef_
linear_model.intercept_

# To get a dictionary of the features and their corresponding coefficients:
coefs = dict(zip(train_input.columns, linear_model.coef_))
```

To make predictions using the model we call the `.predict()` method:

```python
linear_model.predict(X=train_input) # returns an array of predicted values.
```