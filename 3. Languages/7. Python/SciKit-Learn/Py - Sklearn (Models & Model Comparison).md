See:
* [[Py - Introduction to Python]]
* [[Py - Sklearn (SciKit Learn Library)]]
Resources
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)

----
# Model Comparison

| Name                     | Type           | Accuracy | Speed | Accuracy Rank | Speed Rank |
| ------------------------ | -------------- | -------- | ----- | ------------- | ---------- |
| `DecisionTreeClassifier` | Classification | Low      | High  | 3             | 2          |
| `RandomForestClassifier` | Classification | High     | Low   | 1             | 3          |
| `LogisticRegression`     | Classification | Medium   | High  | 2             | 1          |

| Name                    | Type       | Accuracy | Speed | Accuracy Rank | Speed Rank |
| ----------------------- | ---------- | -------- | ----- | ------------- | ---------- |
| `DecisionTreeRegressor` | Regression |          |       |               |            |
| `RandomForestRegressor` | Regression |          |       |               |            |
| `LinearRegression`      | Regression |          |       |               |            |

---
# Model Definitions
* Decision Tree
	* A non-parametric supervised learning algorithm, which is utilized for both classification and regression tasks
* Random Forest 
	* A commonly used ML algorithm that trains a large quantity of independent tress and makes a decision by voting for both classification and regression tasks


----
# Models in Sklearn


##### `DecisionTreeClassifier()`
* A class from the `sklearn.tree` module that is used to create a Decision Tree model for classification tasks
	* Parameters
		* `random_state=` -- Default it is `None`, which sets the pseudorandom to always be  different; a different value can be used to specify the use of the same pseudorandom number
		* `max_depth=` -- By default, it is unlimited; A different value sets the maximum depth of a tree
		* `class_weight` --  Default it is `None`, which sets the class weights to be equivalent;  a different value specifies how to weight the class
			* `balanced` -- calculates how many times the class `0` occurs more often than the class `1
```Python
# Importing the DecisionTreeClassifier class
from sklearn.tree import DecisionTreeClassifier

# Creating an instance of the class
model = DecisionTreeClassifier()
```

```Python
# Example -- Full Example

# Import the require libraries
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score

# Import the train dataset
df = pd.read_csv('/datasets/train_data.csv')

# Prepare the train data for use
df.loc[df['last_price'] > 5650000, 'price_class'] = 1
df.loc[df['last_price'] <= 5650000, 'price_class'] = 0

# Defining the featrues and target to be used
features = df.drop(['last_price', 'price_class'], axis=1)
target = df['price_class']

best_model = None
best_result = 0

# Iterating through different depths of the DecisionTreeClassifier, specifically from depths 1 to 5
for depth in range(1, 6):
	model = DecisionTreeClassifier(random_state=12345, max_depth=depth)
	model.fit(features, target)
	predictions = model.predict(features) 
	result = accuracy_score(target, predictions) 
	if result > best_result:
		best_model = model
		best_result = result
        
print("Accuracy of the best model:", best_result)

# Declaring a function to count errors
def error_count(answers, predictions):
    count = 0
    for i in range(len(answers)):
        if answers[i] != predictions[i]:
            count+=1 
    return count

# Printing number of errors
print('Errors:', error_count(test_target, test_predictions))
```

##### `RandomForestClassifier()`
* A class from the `sklearn.ensemble` module, used to create a Random Forest algorithm for classification tasks
	* Arguments
		* `random_state=` -- Default it is `None`, which sets the pseudorandom to always be different; a different value can be used to specify the use of the same pseudorandom number
		* `n_estimators=` -- sets the number of trees in the forest
		* `class_weight` --  Default it is `None`, which sets the class weights to be equivalent; a different value specifies how to weight the class
			* `balanced` -- calculates how many times the class `0` occurs more often than the class `1`
```Python
# Importing the RandomForestClassifier class
from sklearn.ensemble import RandomForestClassifier

# Creating an instance of the model with 3 trees 
model = RandomForestClassifier(random_state=12345, n_estimators=3)

# Training the model
model.fit(features, target)

# Determining the accuracy
model.score(features, target)
```

```Python
# Example -- Full example

# Importing the libraries
import pandas as pd
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split

# Importing the dataset
df = pd.read_csv('/datasets/train_data_us.csv')

# Preparing the data
df.loc[df['last_price'] > 113000, 'price_class'] = 1
df.loc[df['last_price'] <= 113000, 'price_class'] = 0

# Splitting the source data
df_train, df_valid = train_test_split(df, test_size=0.25, random_state=54321)

# Determining out the test & validation features and target
features_train = df_train.drop(['last_price', 'price_class'], axis=1)
target_train = df_train['price_class']
features_valid = df_valid.drop(['last_price', 'price_class'], axis=1)
target_valid = df_valid['price_class']

# Determining the best score for a model using 1-10 trees
best_score = 0
best_est = 0
for est in range(1, 11): 
    model = RandomForestClassifier(random_state=54321, n_estimators=est) 
    model.fit(features_train, target_train) 
    score = model.score(features_valid, target_valid) 
    if score > best_score:
        best_score = score
        best_est = est

print("Accuracy of the best model on the validation set (n_estimators = {}): {}".format(best_est, best_score))

# Updating the final model to the right number of estimators
final_model = RandomForestClassifier(random_state=54321, n_estimators=10) 
final_model.fit(features_train, target_train)
```

---
##### `LogisticRegression`
* A class from the `sklearn.linear_model` module that computes the probability of an event occurrence. 
* Logistic regression determines the category using a formula consisting of numerical features. 
	* Parameters
		* `random_state=` -- Default it is `None`, which sets the pseudorandom to always be different; a different value can be used to specify the use of the same pseudorandom number`
		* `solver=` --  specifies a version of the algorithm that determines how the curve is fit
			* `'liblinear'`
		* `class_weight` --  Default it is `None`, which sets the class weights to be equivalent; a different value specifies how to weight the class
			* `balanced` -- calculates how many times the class `0` occurs more often than the class `1`
```Python
# Importing the LogisticRegression class
from sklearn.linear_model import LogisticRegression

# Creating an instance of the LogisticRegression model
model = LogisticRegression(random_state=12345, solver='liblinear')

# Training the model
model.fit(features, target)

# Determining the accuracy
model.score(features, target)
```

```Python
# Example -- Full

# Importing the libraries
import pandas as pd
from sklearn.metrics import f1_score
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression

# Importing the dataset
data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

# Preparing the train and validation features
target = data['Claim']
features = data.drop('Claim', axis=1)

# Splitting the source data
features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

# Creating th model
model = LogisticRegression(random_state=12345, solver='liblinear', class_weight='balanced')

# Finding the accruacy
score_train = model.score(features_train, target_train)  
score_valid = model.score(features_valid, target_valid)  

# Training the model
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)


print("Accuracy of the logistic regression model on the training set:", score_train)
print("Accuracy of the logistic regression model on the validation set:", score_valid)

print('F1:', f1_score(target_valid, predicted_valid)) # F1: 0.08698830409356724
```

---
# Regression Models
##### `LinearRegression()`
* A class from the `sklearn.linear_model` module that performs an ordinary least squares Linear Regression.
	* Arguments
		* `fit_intercept=` -- `True` by default; A boolean representing whether to calculate the intercept for the model. If set to `False`, no intercept is used in calculations
		* `copy_X=` -- If `True`, X will be copied
		* `n_jobs=` -- the number of jobs to use for the computation.
		* `positive=` -- `False` by default; When set to `True`, it forces all coefficients to be positive
* Methods
	* `score()` -- returns the coefficient of determination ($R^2$) of the prediction
		* Arguments
			* `X` -- array-like structure with test samples (features)
			* `y` -- array-like structure with true values (target)
```Python
# Example -- Full

# Importing the libraries
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

# Importing the dataset
df = pd.read_csv('/datasets/train_data_us.csv')

# Preparaing the data
features = df.drop(['last_price'], axis=1)
target = df['last_price'] / 1000000

# Preparing the train and validation features
features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

# Creating, training and making predictions with model
model = LinearRegression()
model.fit(features_train, target_train) 
predictions_valid = model.predict(features_valid) 

# Finding the rmse value
result = mean_squared_error(target_valid, predictions_valid)**0.5
print("RMSE of the linear regression model on the validation set:", result)
```

##### `DecisionTreeRegressor()`
* A class from the `sklearn.tree` module that is used to create a Decision Tree model for regression tasks
	* Arguments
		* `random_state=` -- Default it is `None`, which sets the pseudorandom to always be different; a different value can be used to specify the use of the same pseudorandom number
		* `max_depth=` -- By default, it is unlimited; A different value sets the maximum depth of a tree
* Methods
	* `score()` -- returns the coefficient of determination ($R^2$) of the prediction
		* Arguments
			* `X` -- array-like structure with test samples (features)
			* `y` -- array-like structure with true values (target)
```Python
import pandas as pd
from sklearn.tree import DecisionTreeRegressor
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

# Importing the data
df = pd.read_csv('/datasets/train_data_us.csv')

# Preparding the data
features = df.drop(['last_price'], axis=1)
target = df['last_price'] / 1000000

# Determining out the test & validation features and target
features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

best_model = None
best_result = 10000
best_depth = 0

# Training and predicting based on the number of depths
for depth in range(1, 6): 
    model = DecisionTreeRegressor(random_state=12345, max_depth = depth)
    model.fit(features_train, target_train) 
    predictions_valid = model.predict(features_valid) 
    result = mean_squared_error(target_valid, predictions_valid)**0.5
    if result < best_result:
        best_model = model
        best_result = result
        best_depth = depth

print(f"RMSE of the best model on the validation set (max_depth = {best_depth}): {best_result}")
```

##### `RandomForestRegressor()`
* A class from the `sklearn.ensemble` module, used to create a Random Forest algorithm for regression tasks
	* Arguments
		* `random_state=` -- Default it is `None`, which sets the pseudorandom to always be different; a different value can be used to specify the use of the same pseudorandom number
		* `n_estimators=` -- sets the number of trees in the forest
* Methods
	* `score()` -- returns the coefficient of determination ($R^2$) of the prediction
		* Arguments
			* `X` -- array-like structure with test samples (features)
			* `y` -- array-like structure with true values (target)
```Python
# Example -- Full example

# Importing the libraries
import pandas as pd
from sklearn.ensemble import RandomForestRegressor	
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

# Importing the dataset
df = pd.read_csv('/datasets/train_data_us.csv')

# Splitting the source data
features = df.drop(['last_price'], axis=1)
target = df['last_price'] / 1000000

# Determining out the test & validation features and target
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345) 

best_model = None
best_result = 10000
best_est = 0
best_depth = 0

# Training and predicting based on the number of depths and estimators
for est in range(10, 51, 10):
    for depth in range (1, 11):
        model = RandomForestRegressor(random_state=12345, n_estimators=est,
	        max_depth=depth)
        model.fit(features_train, target_train)
        predictions_valid = model.predict(features_valid)
        result = mean_squared_error(target_valid, predictions_valid)**0.5
        if result < best_result:
            best_model = model
            best_result = result
            best_est = est
            best_depth = depth

print("RMSE of the best model on the validation set:", best_result, "n_estimators:", best_est, "best_depth:", depth)
```
