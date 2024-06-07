See: 
* [[Py - Introduction to Python]]
* [[Py - NumPy (Vectors)]]
* [[Py - NumPy (Matrices)]]
* [[Py - NumPy (Methods)]]
Resources:
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)

---

# Linear Regression Model - Basics
* **Linear Regression** -- a method used to predict a target based on a set of features
	* LR evaluates the model's prediction performance (MSE)
* In matrix notation, the features are represented by a matrix of observations denoted as $𝑋$. 
	* Columns -- Features
	* Rows -- Observations
	![Matrix Notation Features](matrix-notation-features.png) 
* The prediction of a model ($𝑎$) is calculated by multiplying the feature matrix $X$ by the weight vector ($𝑤$), and adding the bias value ($𝑤_0$). 
	* $𝑤$ -- a vector that is a parameter of the model 
	* $𝑤_0$ -- a scalar that is a parameter of the model $$𝑎 = (X * 𝑤) + 𝑤_0$$
	* When the feature matrix $X$ has only one feature, the model equation resembles that of a straight line: $$y = mx + b$$
		![[prediction-model.png]]
		
* The number of model parameters is one more than the length of the features vector. 
	* Adjusting the parameters $w$ and $w_0$ results in a different straight line. 
		* Changing $w_0$ shifts the line vertically (see below)
		* Changing $w$ alters the slope. 
		![[adjust-w0.png]]
	
- The model aims to adjust parameters to closely align the line with the data points.
- MSE increases with greater distances between the line and data points.


# The Training Objective
* The objective of training is to discover the optimal values for parameters ($w$ and $w_0$)

#### The Objective Function
- **Objective Function** -- a function aimed to minimize or maximize to solve optimization problems
    - Inputs: Data and model parameters
    - Output: Numeric value
- Objective Function of Linear Regression:
    - In Linear Regression, the objective function is the loss function, calculating the MSE (Mean Square Error).
        - Linear Regression performs optimally when the MSE is at its minimum.

### Prediction Process
* Obtaining the prediction vector $a$ involves the following steps:
	1. Add a column consisting only of ones to the beginning of matrix $X$.
	2. Add $w_0$ to the beginning of the $w$ vector.
	   ![Image](improve-equation-for-model-prediction.png)
	3. Take the dot product of the $X$ matrix and the $w$ vector.
		* Formula: $$ a = X \cdot w $$
	4. Find the optimal values for the weights using Mean Squared Error (MSE) minimization.
		* Formula: $$ w = \text{argmin}(MSE(Xw, y)) $$
		     - $y$ -- the target vector from the data
		     - `argmin()` -- returns the values for the minimized result.
		     
		 - Formula: Can be expressed in Matrix form $$w = (X^T X)^-1 X^Ty$$
			 - 𝑤 -- the vector of regression weights
			 - 𝑋 -- the matrix of observations with the features
			 - 𝑦 -- the column vector of observations with the target


# Training Linear Regression
* Understanding the Formula in Matrix Form 
	* Formula: $$w = (X^T X)^-1 X^Ty$$
		* The transposed feature matrix is multiplied by itself. $$(X^TX)$$
		* The matrix inverse to that result is calculated  $$(X^TX)^-1$$
		* The inverse matrix is multiplied by the transposed feature matrix $$(X^TX)^-1 X^T$$
		* The result is multiplied by the vector of the target values $$ (X^T X)^-1 X^Ty $$
```Python
# Example -- Manually creating Linear Regression Model
import numpy as np
import pandas as pd
from sklearn.metrics import r2_score

columns = ['bedrooms', 'total area', 'kitchen', 'living area', 'floor', 'total floors', 'price']

data = pd.DataFrame([
    [1, 38.5, 6.9, 18.9, 3, 5, 84000],
    [1, 38.0, 8.5, 19.2, 9, 17, 70000],
    ...
    [3, 69.3, 8.5, 39.3, 4, 9, 228000],
    [3, 89.8, 11.2, 58.2, 24, 25, 326000],
], columns=columns)

features = data.drop('price', axis=1)
target = data['price']

class LinearRegression:
    def fit(self, train_features, train_target):
        X = np.concatenate((np.ones((train_features.shape[0], 1)), 
	        train_features), axis=1)
        y = train_target
        w = np.linalg.inv(X.T.dot(X)).dot(X.T).dot(y)
        self.w = w[1:]
        self.w0 = w[0]
        
    def predict(self, test_features):
        return test_features.dot(self.w) + self.w0
    
model = LinearRegression()
model.fit(features, target)
predictions = model.predict(features)
print(r2_score(target, predictions))
```