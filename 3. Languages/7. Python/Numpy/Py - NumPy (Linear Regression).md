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
* In matrix notation, the features are represented by a matrix of observations denoted as $𝑋$. 
	* Columns -- Features
	* Rows -- Observations
	![Matrix Notation Features](matrix-notation-features.png) 
* The prediction of a model ($𝑎$) is calculated by multiplying the feature matrix $X$ by the weight vector ($𝑤$), and adding the bias value ($𝑤_0$). 
	* $X$ -- matrix X
	* $𝑤$ -- the weight vector
	* $𝑤_0$ -- the bias scalar value 
$$𝑎 = (X * 𝑤) + 𝑤_0$$
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
- **Objective Function** -- a function that should be minimized or maximized in order to solve optimization problems
    - **Inputs:** Data and model parameters
    - **Output:** Numeric value
- Objective Function of Linear Regression:
    - **MSE (Mean Square Error)** is the objective 'loss' function of linear regression that measures the model's prediction performance.
        - Linear Regression performs best when the MSE is at its minimum


### Prediction Process
* To obtain the prediction vector $𝑎$ follow these steps:
	1. Append a column of 1s to the start of matrix $X$.
	2. Append $w_0$​ to the start of vector $w$.
		   ![Image](improve-equation-for-model-prediction.png)
	3. Find the optimal values for the weights using Mean Squared Error (MSE) minimization.
		* Formula: in regular form
			* $y$ -- the target vector from the data
		     - `argmin()` -- returns the values for the minimized result $$ w = argmin_w(MSE(Xw, y)) $$
		 - Understanding the Formula in Matrix Form
			- Overall Formula:
				- 𝑤 -- vector of regression weights
				 - 𝑋 -- matrix of observations with the features
				 - 𝑦 -- vector of the target values $$w = (X^T X)^-1 X^Ty$$
			- Steps:
			        1. Multiply the transposed feature matrix by the feature matrix:
			            $w = (X^TX)$
			        2. Calculate the inverse of the resulting matrix:
				        $w = (X^TX)^−1$
			        3. Multiply the inverse matrix by the transposed feature matrix:
			            $w = (X^TX)^−1X^T$
			        4. Multiply the resulting matrix by the vector of target values:
			            $w = (X^TX)^−1X^Ty$

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
	    # Step 1: Append a column of 1s to the start of matrix X
        X = np.concatenate((np.ones((train_features.shape[0], 1)), 
	        train_features), axis=1)
        y = train_target
        
        # Step 3.1: X.T.dot(X) 
	        # -- Multiply the transposed feature matrix by the feature matrix
        # Step 3.2: np.linalg.inv()
	        # -- Calculate the inverse of the resulting matrix
	    # Step 3.3: .dot(X.T)
		    # -- Multiply the inverse matrix by the transposed feature matrix
		# Step 3.4: .dot(y)
			# -- Multiply the resulting matrix by the vector of target values
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