# Linear Classifier in python

## Applying logistic regression and SVM

```{python}
# Mathematical functions for logistic and hinge losses
def log_loss(raw_model_output):
   return np.log(1+np.exp(-raw_model_output))
def hinge_loss(raw_model_output):
   return np.maximum(0,1-raw_model_output)

# Create a grid of values and plot
grid = np.linspace(-2,2,1000)
plt.plot(grid, log_loss(grid), label='logistic')
plt.plot(grid, hinge_loss(grid), label='hinge')
plt.legend()
plt.show()
```

```{python}
# The squared error, summed over training examples
def my_loss(w):
    s = 0
    for i in range(y.size):
        # Get the true and predicted target values for example 'i'
        y_i_true = y[i]
        y_i_pred = w@X[i]
        s = s + (y_i_true - y_i_pred)**2
    return s

# Returns the w that makes my_loss(w) smallest
w_fit = minimize(my_loss, X[0]).x
print(w_fit)

# Compare with scikit-learn's LinearRegression coefficients
lr = LinearRegression(fit_intercept=False).fit(X,y)
print(lr.coef_)
```
If the prediction is right, `raw_model_output and the y[i]` have the same sign
If the prediction is wrong, have opposite sign.
In the `log_loss()`function ,The more below zero ,the bigger the `log_loss()`is


```{python}
def log_loss(raw_model_output):
   return np.log(1+np.exp(-raw_model_output))
# The logistic loss, summed over training examples
def my_loss(w):
    s = 0
    for i in range(y.size):
        raw_model_output = w@X[i]
        s = s + log_loss(raw_model_output * y[i])
    return s

# Returns the w that makes my_loss(w) smallest
w_fit = minimize(my_loss, X[0]).x
print(w_fit)

# Compare with scikit-learn's LogisticRegression
lr = LogisticRegression(fit_intercept=False, C=1000000).fit(X,y)
print(lr.coef_)
```


### Multi-class logistic regression

#### 1. Combining binary classifiers with one vs rest

```{python}
lr0.fit(X, y == 0)
lr1.fit(X, y == 1)
lr2.fit(X, y == 2)
```
```{python}
#get raw model output
lr0.decision_funtcion(X)[0]
lr1.decision_funtcion(X)[0]
lr2.decision_funtcion(X)[0]
```

See which one get the most probability
| one vs rest | "Multinominal" or "softmax" |
|-------------|-----------------------------|
|fit a binary classifier for each class   | fit a single classifier for all class |
|predict all, take the largest output     | prediction directly outputs best class  |
|pro: simple, modular                     | con: more complicated, new code         |
|con: not directly optimizing accuracy    | pro: tackle the problem directly        |
|common for SVMS as well                  | possible for SVMs, but less common      |
|`lr_ovr = LogisticRegression()`          | `lr_mn = LogisticRegression(multi_class = "multinomial", solver = "lbfgs")` |

## support vector machines
### support vectors

Support vectors are defined as training examples that influence the decision boundary.

- Linear Classifiers
- Trained using the hinge loss and L2 regularization

- the SVM maximizes the "margin" for linearly separable datasets
- Margin: distance from the boundary to the closest points

### Logistic regression VS SVM

| Logistic regression     | SVM         |
|-------------------------|--------------|
|is a linear classifier   | is a linear classifier  |
| can use with kernels, but slow | can use with kernels, and fast |
|outputs meaningfu probabilities | Does not naturally output probabilities|
| can be extended to multi-class | can be extended to multi-class   |
| all data points affect fit | Only "supports vectors" affect fit |
| L2 or l1 regularization | conventionally just l2 regularization |

1. Logistic Regression in sklearn:

`linear_model.LogisticRegression`

key hyperparameters in sklearn

- C (inverse regularization strength)
- penalty (type of regularization)
- multi_class (type of multi-class)

2. SVM in sklearn
 
`svm.LinearSVC` and `svm.SVM`

key hyperparameters:

- C (inverse regularization strength)
- kernel ( type of kernel)
- gamma (inverse RBF smoothness)

## SGDClassifier

```{python}
from sklearn.linear_model import SGDClassifier
logreg = SGDClassifier(loss = 'log')
linsvm = SGDClassifier(loss = 'hinge')
```

`SGDClassifier` hyperparameters alpha is like `1/C`


