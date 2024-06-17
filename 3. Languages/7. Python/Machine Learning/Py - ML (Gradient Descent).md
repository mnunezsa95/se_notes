See:
* [[Py - Introduction to Python]]
* [[Py - NumPy (Vectors)]]
* [[Py - NumPy (Matrices)]]
* [[Py - NumPy (Methods)]]
* [[Py - ML (Algorithm Analysis)]]
* [[Py - Creating Classes in Python]]
Resources:
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* Documentation: [CatBoostClassifier](https://catboost.ai/en/docs/concepts/python-reference_catboostclassifier)

---
# 1. Loss Function Minimization

* Formula: 
	* $y$ -- the number of correct answers
	* $a$ -- the number of predictions
$$w = arg\;min_w\;L(y,a)$$

* Mean Squared Error (MSE) or Quadratic Loss Function
	* Square the difference between number of correct answers and predictions
	* Formula: $$ L(y,a) = sum^n_(i=1)(a_i - y_i)^2 $$
* Absolute Loss Function (MAE) 
	* Less sensitive to outliers
	* Formula: $$L(y,a) = sum^n_(i=1)|a_i - y_i|$$
* Negative Logarithmic Likelihood (Logistic Loss Function) 
	* Adds up the logarithms of probabilities depending on the observation
	* Can be used instead of accuracy because it has a derivative 
	* The Loss function relies on algorithm parameters.
	- Is a vector-valued function, taking a vector as input and producing a scalar output.
	* Fromula: 
		* $a_i$ -- the probability of class 1 for observation with index $i$
			* The value of $a_i$ should be as high as possible for a positive class observation, The value of $a_i$ should be as low as possible for a negative class observation.
$$L(y, a) = - \sum_{i=1}^{n} \left\{ \begin{array}{c} \displaystyle \log_{10} a_i \;\text{ if } y_i = 1 \\[1ex] \displaystyle (\log_{10}(1 - a_i) \; \text{ if } y_i = 0 \end{array} \right.$$
```Python
from math import log10

result = -1 * (log10(1 - 0.2) + log10(1 - 0.4) + log10(0.6) + log10(0.8) + log10(1 - 0.1))

print(result)
```

# 2. Function Gradient
## What is a Function Gradient?
* Function Gradient is a fancy word for derivative 
* The gradient of a vector-valued function is a vector consisting of derivatives of the answer for each argument.
* The gradient shows the direction in which the function increases the fastest
	* Formula: 
		* $(∂f)/(∂x_i)$ -- the partial derivative of the function $f$ for the argument $x_i$
$$∇f(x) = ((∂f)/(∂x_i), (∂f)/(∂x_2), ..., (∂f)/(∂x_n))$$
* The negative gradient shows the direction in which the function decreases the fastest
	* Formula:
$$-∇f(x)$$

### Examples: Finding the Function Derivative (Gradient)
* Example: The function gradient for one argument is the derivative:
$$f(x)=(x-5)^2$$
$$∇f(x) = ∇(x^2 -10x+25) = 2x-10$$
* Example: The function gradient of a three-argument function:
$$f(x,y,z)= x^2 + 2y^2 + 10yz - 5z$$
$$(∂f(x,y,z))/(∂x) = (∂x^2)/(∂x) + (∂(2y^2))/(∂x) + (∂(10yz))/(∂x) - (∂(5z))/((∂x)) = 2x + 0 + 0 +0$$
$$(∂f(x,y,z))/(∂x) =  0 + 4y + 10z +10$$
$$(∂f(x,y,z))/(∂x) = 0 + 0 + 10y - 5$$
$$∇f(x,y,z) = 2x,4y+10z, 10y-5$$
* Example: The function gradient of a two-argument function:
$$f(x,y)=2x^2 + 3y-5x +20$$
$$(∂f(x,y))/(∂x) = (∂(2x^2))/(∂x) + (∂(3y))/(∂x) - (∂(5x))/(∂x) = 4x + 0 - 5 + 0$$
$$(∂f(x,y))/(∂y) = (∂(2x^2))/(∂y) + (∂(3y))/(∂y) - (∂(5x))/(∂y) + 20 = 0 + 3 + 0 +0 $$
$$∇f(x,y) = 4x-5, 3$$

* Example: Find the gradient of a three-argument function:
$$f(x,y,z)= 3x^2 + 2y^2 + 3xy - 3z$$
$$(∂f(x,y,z))/(∂x) = (∂(3x^2))/(∂x) + (∂(2y^2))/(∂x) + (∂(5xy))/(∂x) - (3z)/(∂x) = 6x + 0 + 3y + 0$$
$$(∂f(x,y,z))/(∂y) = (∂(3x^2))/(∂y) + (∂(2y^2))/(∂y) + (∂(5xy))/(∂y) - (3z)/(∂y) = 0 + 4y + 3x + 0$$
$$(∂f(x,y,z))/(∂z) = (∂(3x^2))/(∂z) + (∂(2y^2))/(∂z) + (∂(5xy))/(∂x) - (3z)/(∂z) = 0 + 0 - 0 -3$$
$$∇f(x,y,z) = (6x+3y, 4y+3x, -3)$$

# 3. Calculating Gradient Descent
## What is Gradient Descent?
* **Gradient descent** is an iterative method used to pinpoint the minimum of a loss function. This approach involves consistently moving in the direction opposite to the gradient, gradually moving closer to the minimum value.
	- The process of the gradient descent algorithm can be likened to a continuous descent towards the bottom, achieved through repetitive actions.
	- Reaching the minimum in a single iteration is challenging, as the negative gradient vector guides the descent towards decreasing values rather than directly pinpointing the precise minimum point of the loss function.
	
## How to Perform a Gradient Descent
- Select the **initial value** for the argument (vector _x_), denoted as x⁰.
- Incorporate the negative gradient scaled by the gradient descent magnitude, represented by $mu$.
	- The parameter μ regulates the magnitude of the gradient descent step.
		- When $mu$ is small, the descent progresses through numerous steps, with each bringing the solution closer to the minimum of the loss function.
		- Conversely, if $mu$ is large, there's a risk of overshooting the minimum. $$X^1 - X^0 + mu*(-∇f(x))$$
- Iterate to derive the argument values for subsequent steps. 
	- The number of iterations is denoted by $t$.
- Scale the negative gradient by the step size and add the resulting product to the previous point. $$x^t=x^(t-1)-mu*∇f(x^(t-1))$$
* The gradient descent is complete when:
	* The algorithm completes the required number of iterations
	* The value of $x$ stops changing

## Examples: Finding the Gradient Descent
* Example 1: Calculate the x value and the loss function value after four iterations of gradient descent.
	* $u$ = 0.4
	* $x^0$ = 0 
	* $t$ = 4 $$f(x) = (x-10)^2$$
	* Find the Derivative of $f(x)$: $$f'(x) = 2(x-10)$$
	* Iteration 0: 
		* Set Initial Value:$$x^0 = 0 $$
		* Calculate Iteration: $$f'(x) - 2(0-10) = -20$$
		* Update Rule: $$x^1 = x^0 - mu * f'(x^0) = 0 -0.4*(-20) = 0 + 8 = 8$$
		* Loss Function Value: $$f(x^1) = (8-10)^2 = 4$$
	* Iteration 1:
		* Set Initial Value:$$x^1=8$$
		* Calculate Iteration: $$f'(x^1)=2(8−10)=−4$$
		* Update Rule: $$x^2=x^1−u⋅f'(x^1)=8−0.4*(−4)=8+1.6=9.6$$
		* Loss Function Value: $$f(x^2)=(9.6−10)^2=0.64$$
	* Iteration 2: 
		* Set Initial Value: $$x^2=9.6$$
		- Calculate Iteration: $$f'(x^2)=2(9.6−10)=−0.8$$
		- Update Rule: $$x^3=x^2−u⋅f'(x^2)=9.6−0.4×(−0.8)=9.6+0.32=9.92$$
		- Loss Function Value: $$f(x^3)=(9.92−10)^2=0.032$$
	- Iteration 3: 
		- Set Initial Value: $$x^3=9.92$$
		- Calculate Iteration: $$f'(x^3)=2(9.92−10)=−0.16$$
		- Update Rule: $$x^4=x^3−u⋅f'(x^3)=9.92−0.4×(−0.16)=9.92+0.064=9.984$$
		- Loss Function Value: $$f(x^4)=(9.984−10)^2=0.00256$$
	- Result
	$$x=9.984, f(x)=0.000256$$

# 4. Calculating Gradient Descent in Python
## Steps to create gradient descent in Python
1) In the arguments of the algorithm, set the initial value, x⁰.
2. Calculate the gradient of the loss function (this is the vector of partial derivatives with respect to each argument that takes vector _x_ as input).
3. Find the new value using the formula: 
	* Where $μ$ is the step size, and set in the argument of the algorithm.$$𝑥^1=𝑥^0+𝜇 * (−∇𝑓(𝑥))$$
4. Perform the number of iterations specified in the arguments.
* Example
	* Minimize the function: $f(x1​,x2​)=(x_1​+x_2​ - 1)^2+(x_1​ -x_2​ - 2)^2$
```Python
import numpy as np

def func(x):
    return (x[0] + x[1] - 1) ** 2 + (x[0] - x[1] - 2) ** 2

def gradient(x):
    # Calculate the derivative with respect to X1 and X2
    return np.array([4 * x[0] - 6, 4 * x[1] + 2])

def gradient_descent(initialization, step_size, iterations):
    x = initialization
    for i in range(iterations):
        x = x - step_size * gradient(x)
    return x


print(gradient_descent(np.array([0, 0]), 0.1, 5))
print(gradient_descent(np.array([0, 0]), 0.1, 100))
```

# 5. Gradient Descent for Linear Regression
* Identify Linear Regression Training Task
$$w = arg\;min_w\;MSE(Xw,y)$$

* Train a model using gradient descent. 
	* Write down the loss function in vector form to find its gradient
	* Express MSE as a scalar product of the difference of vectors
	* Formula:
		* $y$ -- the correct answer vector
		* $a$ -- the prediction vector
$$MSE(y,a) = 1 / n sum^n_(i=1)(a_i - y_i)^2 = 1/n (a-y, a-y)$$
* Convert the scalar product to a matrix product
$$(a-y, a-y) = (a-y)^T(a-y)$$
* Combine the MSE and linear regression formulas:
$$MSE(Xw,y) = 1/n(Xw-y)^T(Xw-y)$$
* Find the function gradient for parameter vector $w$. 
$$∇MSE(Xw,y) = 2/nX^T(Xw-y)$$

# 6. Stochastic Gradient Descent
### Mini-Batch Stochastic Gradient Descent (SGD) & Stochastic Gradient Descent (SGD)
* **Mini-Batch Stochastic Gradient Descent (SGD)** and **Stochastic Gradient Descent (SGD)** are variations of the gradient descent that optimize algorithms used to minimize the loss function in machine learning models

### Mini-Batches
* Mini-Batches (or Batches) -- are smaller parts of the data set that can be used to reduce the time of the algorithm
	* In order for the algorithm to "see" the entire training set, the batches at each iteration should change randomly
	
* Steps to obtain mini-batches:
	* Shuffle all the data of the training set and divide the data into parts
		* The batch size is around 100-200 observations
		* The number of epoch depends on the size of training set
			* epoch -- when algorithm goes through all batches one time

### SGD Algorithm
* Here’s how the _SGD_ algorithm works:
	1. **Input hyperparameters:** batch size, number of epochs, and step size.
	2. Define the initial values of the model weights.
	3. Split the training set into batches for each epoch.
	4. For each batch:
		1. Calculate the loss function gradient
		2. Update the model weights (add the negative gradient multiplied by the step size to the current weights).
	5. The algorithm returns the final model weights.


### Computational Complexities
* Definitions:
	* $n$ -- the number of observations in the whole training set;
	* $b$ -- the batch size;
	* $p$ -- the number of features
* Computational Complexities
	* For MSE gradient in linear regression: $$T(n,p) ~ np$$
	* For one batch:$$T(n,b,) ~ bp$$
	* One epoch if the set is divided into batches integrally: $$T(n,b,p) ~ np$$

# 7. SGD in Python
* Creating a SGD Gradient in Python requires the use of Python classes
```Python
# Example - Creating SGD in Python

import numpy as np
import pandas as pd
from sklearn.metrics import r2_score

data_train = pd.read_csv('/datasets/train_data_n.csv')
features_train = data_train.drop(['target'], axis=1)
target_train = data_train['target']

data_test = pd.read_csv('/datasets/test_data_n.csv')
features_test = data_test.drop(['target'], axis=1)
target_test = data_test['target']


class SGDLinearRegression:
    def __init__(self, step_size, epochs, batch_size):
        self.step_size = step_size
        self.epochs = epochs
        self.batch_size = batch_size
        
    def fit(self, train_features, train_target):
        X = np.concatenate(
            (np.ones((train_features.shape[0], 1)), train_features), axis=1
        )
        y = train_target
        w = np.zeros(X.shape[1])
        
        for _ in range(self.epochs):
            batches_count = X.shape[0] // self.batch_size
            for i in range(batches_count):
                begin = i * self.batch_size
                end = (i + 1) * self.batch_size
                X_batch = X[begin:end, :]
                y_batch = y[begin:end]
                
                gradient = 2 * X_batch.T.dot(X_batch.dot(w) - y_batch) / 
	                X_batch.shape[0]              
                w -= self.step_size * gradient
                
        self.w = w[1:]
        self.w0 = w[0]
        
    def predict(self, test_features):
        return test_features.dot(self.w) + self.w0
        
model = SGDLinearRegression(0.01, 10, 100)
model.fit(features_train, target_train)
pred_train = model.predict(features_train)
pred_test = model.predict(features_test)

print(r2_score(target_train, pred_train).round(5)) # 0.21882
print(r2_score(target_test, pred_test).round(5)) # 0.06296
```


# 8. Linear Regression Regularization 
* **Regularization** -- Reduces the overfitting by fining the model if the parameter values complicate the algorithm operation
	* For Linear Regression, regularization implies the limitation of weights
	
* How weights impact linear regression
	* The lower the weights, the easier it is to train the algorithm
* Determining the magnitude of the weights involves several steps:
	* Calculate the distance between the weight vector and the vector consisting of zeros
* Steps:
	* Incorporate the scalar product of the weights into the loss function formula to constrain weight values. The formula becomes: $$L(w) = MSE (Xw, y) + (w,w)$$
	* Derive the gradient of the loss function. The derivative $(w, w)$ equals $2w$. Calculate the gradient as:$$∇L(w) = 2/nX^T(Xw-y) + 2w$$
	* Introduce the regularization weight, denoted as $λ$, to control regularization magnitude. The updated loss function formula is: $$L(w) = MSE(Xw,y) + lambda(w,w)$$
	* Adjust the gradient calculation to account for the regularization weight: $$∇L(w) = 2/nX^T(Xw-y) + 2lambdaw$$
	
```Python
import numpy as np
import pandas as pd
from sklearn.metrics import r2_score

data_train = pd.read_csv('/datasets/train_data_n.csv')
features_train = data_train.drop(['target'], axis=1)
target_train = data_train['target']

data_test = pd.read_csv('/datasets/test_data_n.csv')
features_test = data_test.drop(['target'], axis=1)
target_test = data_test['target']


class SGDLinearRegression:
    def __init__(self, step_size, epochs, batch_size, reg_weight):
        self.step_size = step_size
        self.epochs = epochs
        self.batch_size = batch_size
        self.reg_weight = reg_weight
        
    def fit(self, train_features, train_target):
        X = np.concatenate(
            (np.ones((train_features.shape[0], 1)), train_features), axis=1
        )
        y = train_target
        w = np.zeros(X.shape[1])
        
        for _ in range(self.epochs):
            batches_count = X.shape[0] // self.batch_size
            for i in range(batches_count):
                begin = i * self.batch_size
                end = (i + 1) * self.batch_size
                X_batch = X[begin:end, :]
                y_batch = y[begin:end]
                
                gradient = (2 * X_batch.T.dot(X_batch.dot(w) - y_batch)
                    / X_batch.shape[0]
                )
                reg = 2 * w.copy()
                reg[0] = 0
                gradient += self.reg_weight * reg
                w -= self.step_size * gradient
                
        self.w = w[1:]
        self.w0 = w[0]
        
    def predict(self, test_features):
        return test_features.dot(self.w) + self.w0

print('Regularization:', 0.0)
model = SGDLinearRegression(0.01, 10, 100, 0.0)
model.fit(features_train, target_train)
pred_train = model.predict(features_train)
pred_test = model.predict(features_test)
print(r2_score(target_train, pred_train).round(5))
print(r2_score(target_test, pred_test).round(5))

print('Regularization:', 0.1)
model = SGDLinearRegression(0.01, 10, 100, 0.1)
model.fit(features_train, target_train)
pred_train = model.predict(features_train)
pred_test = model.predict(features_test)
print(r2_score(target_train, pred_train).round(5))
print(r2_score(target_test, pred_test).round(5))

print('Regularization:', 1.0)
model = SGDLinearRegression(0.01, 10, 100, 1.0)
model.fit(features_train, target_train)
pred_train = model.predict(features_train)
pred_test = model.predict(features_test)
print(r2_score(target_train, pred_train).round(5))
print(r2_score(target_test, pred_test).round(5))

print('Regularization:', 10.0)
model = SGDLinearRegression(0.01, 10, 100, 10.0)
model.fit(features_train, target_train)
pred_train = model.predict(features_train)
pred_test = model.predict(features_test)
print(r2_score(target_train, pred_train).round(5))
print(r2_score(target_test, pred_test).round(5))
```

```Result
Regularization: 0.0
0.21882
0.06296

Regularization: 0.1
0.21488
0.07001

Regularization: 1.0
0.16661
0.08061

Regularization: 10.0
0.03945
0.02412
```


# 9. Ensembles and Boosting
#### Ensemble
- An ensemble is a set of models for solving the same problem.
	-  The results of **base** or **weak** learners (the models comprising the ensemble) are averaged
- Ensembles are strong because:
    - The mean error of a group of models is less significant than their individual errors.
- Examples of Ensembles:
	- The Random Forest
		- Base --> decision tree

#### Boosting
* **Boosting** -- an approach to ensemble building
- In boosting:
    - Each subsequent model takes into account the errors of the previous one.
    - The final prediction combines the forecasts of basic learners. 
- Formula:
	- $a_N(X)$ -- the ensemble prediction
	- $N$ -- the number of base learners
	- $b_k(X)$ -- the base learner prediction
	- $y_k$ -- the model weight $$a_N(X) = sum^N_(k=1)y_kb_k(X)$$
* Example: Dealing with Regression Task 
	* Important takeaways:
		* What does the base learner predict at each step of the gradient boost?
			* Residuals at previous step $N-1$
		* What are ensemble residuals at step $N$?
			* The difference between the ensemble at current step N and the actual answers
		* What is minimized at step $N$?
			* The value of the error function to predict the residuals at the previous step
	* Starting Formula: $$MSE(y,a) = 1/n sum^n_(i=1)(a(x_i)-y_i)^2 --> min_(a(x))$$
	* Equate the model weights to unity: $$y_k = 1, \text{for all}\; k =1,...,N $$
	* Results in: $$a_N(X) = sum^N_(k=1)b_k(X)$$
	* Now, create an ensemble of sequential models
		* First build the base learner $b_1$ by solving the minimization task: $$b_1=arg min_b1/n sum^n_(i=1)(b(x_i)-y_i)^2$$
	* The result is this ensemble: $$a_1(X)=b_1(X)$$
	* Indicate the **residual** -- the difference between the prediction at the first step and the correct answers $$e_(1,i) = y_i -b_1(x_i)$$
	* Build a model like this: $$b_2 = argmin_b 1/n sum^n_(i=1)(b(x_i)-e_(1,i))^2$$
	* The ensemble takes the following form: $$a_2(X) = sum^2_(k=1)b_k(X)=b_1(X)+b_2(X)$$
	* Find the residual for each observation $i$: $$e_(2,i) = y_i -a_2(X_i) = y_i - sum^2_(k=1)b_k(X_i)$$
	* At each subsequent step, the algorithm minimizes the ensemble error from the preceding step.
		* At step _N-1_, the residual is calculated as follows: $$e_(N-1,i)=y_i - a_(N-1)(X_i)$$
	* The ensemble itself is represented as the sum of predictions of all the base learners combined up to this step: $$a_(N-1)(X) = sum^(N-1)_(k=1)b_k(X)$$
	* So, at step N, the algorithm will pick the model with the ensemble error at step N-1: $$b_N(X)=argmin_b1/nsum^n_(i=1)(b(x_i)-e_(N-1,i))^2$$

---
# 10. Gradient Boosting
## Introduction to Gradient Boosting?
* Gradient Boosting makes the process minimizing the loss function, even more effective! 
* Gradient boosting is suitable for different loss functions that have derivatives such as:
	* Mean Square in Regression Tasks
	* Logarithmic in Binary Classification Tasks

## Formulas: Gradient Boosting
* Start with the ensemble formula: $$a_N(x) = a_(N-1) + y_Nb_N(x)$$
* At each step, select the answers that will minimize the function: $$L(y,a(x)) --> min_a $$
* Minimize the function with gradient descent, by calculating the negative gradient of the loss function for prediction $g_N$ at each step. $$g_N(x)=-∇L(y,a_(N-1)(x) + a)$$
* To push the predictions towards correct answers, the base learner learns to predict $g_N$: $$b_N(x) arg min_b 1/n sum^N_(i=1)(b(x_i)+g_N(x_i))^2$$
*  Obtain the weight for $y_N$ from the minimization task by iterating various numbers: $$y_N= argmin_yL(y,a_(N-1)(x) + yb_N(x))$$

# 11. Gradient Boosting Regularization
## Introduction to Gradient Boosting Regularization
* Regularization can be used to reduce overfitting during gradient boosting
* If the weights in a linear regression have been reduced, then the gradient boosting regularization is:
	1. Reduce step size
	2. Adjust tree parameters
	3. Subsample randomization for base learners $b_i$

### Reduce Step Size
* Revise the formula for calculating predictions at step N:
	* When the algorithm takes steps too large, it remembers the training set  
	* Formula: $$a_N(x)=a_(N-1)(x) + y_Nb_N(x)$$
* Introduce the $η$ coefficient to control the learning rate and reduce the step size
	* The $η$ coefficient is picked by iterating over different values in the range from 0 to 1.
		* A smaller value means a smaller step towards the negative gradient (derivative) and a higher accuracy of the ensemble
		* If the value is too small, then the training process takes too long
	* Formula: $$a_N(x)=a_(N-1)+η + y_Nb_N(x)$$
### Adjust Tree Parameters
* Limit the tree depth or number of elements in each node to see how it affects the result
* Try different values for the tree depth.

### Subsample Randomization for Base Learners $b_i$
* The algorithm works by training with random subsamples instead of the whole set. 
	* This algorithm version is similar to SGD and is called stochastic gradient boosting.


# 12. Libraries for Gradient Boosting
## Libraries
* There are three popular libraries for gradient boosting
	* XGBoost (extreme gradient boosting) -- a popular gradient boosting library on Kaggle
	* [LightGBM](https://lightgbm.readthedocs.io/en/latest/Experiments.html) (light gradient boosting machine) -- a popular gradient boosting library developed by Microsoft
		* Fast and accurate gradient boost training
		* Directly works with categorical features
	* [CatBoost](https://catboost.ai/#benchmark) (categorical boosting) -- a gradient boosting library developed by Yandex
		* Superior to other algorithms in terms of evaluation metrics
		* Applies various encoding techniques for categorical features (LabelEncoding, One-Hot Encoding)
## Library Comparison

| Library  | Processing of Categorical Features | Rate |
| -------- | ---------------------------------- | ---- |
| XGBoost  | No                                 | Low  |
| LightGBM | Yes                                | High |
| CatBoost | Yes                                | High |

## Working with CatBoost Library
* CatBoost must be installed and imported before use
	* The `CatBoostClassifier()` class has methods similar to sklearn classes for fitting and predicting 
		* Hyperparameters
			* `loss_function=` -- the loss function to use
				* `'Logloss'`
			* `iterations=` -- the number of operations to run
			* `random_seed=` -- the random seed used for training
			* `learning_rate` -- the learning rate used for training
			* `depth` -- the depth to use 
	* Methods:
		* `model.fit()` -- trains the model
			* Arguments
				* `X` -- the train features
				* `y` -- the train target
				* `cat_features=` -- a list of the category features
				* `verbose=` -- specifies the step at which to print information
		* `model.predict()`
			* Arguments
				* `X` -- the valid or test features 
			* Returns 
				* The predictions
```Python
import pandas as pd
from sklearn.model_selection import train_test_split
from catboost import CatBoostClassifier

data = pd.read_csv('travel_insurance_us.csv')

features_train, features_valid, target_train, target_valid = train_test_split(
	data.drop('Claim', axis=1), data.Claim, test_size=0.25, random_state=12345
)

model = CatBoostClassifier(loss_function="Logloss", iterations=10)

cat_features = ['Agency', 'Agency Type', 'Distribution Channel', 'Product Name',
	'Destination', 'Gender']

model.fit(features_train, target_train, cat_features=cat_features, verbose=10)
pred_valid = model.predict(features_valid)
```
