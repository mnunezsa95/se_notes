See:
* [[Py - Introduction to Python]]
* [[ML - Machine Learning Basics]]
* [[Py - Sklearn (Models & Model Comparison)]]
* [[ML - Supervised Learning]]
Resources
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Article(s): [MSE](https://statisticsbyjim.com/regression/mean-squared-error-mse/), [RMSE](https://statisticsbyjim.com/regression/root-mean-square-error-rmse/), [MAE](https://deepchecks.com/glossary/mean-absolute-error/),

---
# SciKit - Learn (Sklearn)

## What is Sklearn?
* Sklearn -- a library in Python that provides many unsupervised and supervised learning algorithms
* Sklearn is a source of tools for working with data and models
* Built upon technologies such as: NumPy, Pandas, and Matplotlib

## What functionality does Sklearn Provide?
* The functionality that scikit-learn provides include:
	- **Regression**, including Linear and Logistic Regression
	- **Classification**, including K-Nearest Neighbors
	- **Clustering**, including K-Means and K-Means++
	- **Model selection**
	- **Preprocessing**, including Min-Max Normalization

## Sklearn Library Breakdown
* Sklearn is split up into modules
	* Example: The `tree` module is a module that stores decision trees
* Models correspond to different classes in Sklearn
	* Example: The `DecisionTreeClassifier` is a class for decision tree classifications 


---
---

# Working with Models in Sklearn

### Training the Model
##### `fit()`
* Trains the model using the features and target
	* Arguments
		1) `features` -- the features to use for training
		2) `target` -- the target to use for training
```Python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(random_state=12345, n_estimators=3)
model.fit(features, target)
```

### Making Predictions with Model
##### `predict()`
* Makes predictions and returns the probability estimate
	* Arguments
		1) `target` -- the target to use for making predictions
```Python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(random_state=12345, n_estimators=3)
model.fit(features, target)
model.predict(target)
```

### Threshold Adjustment in Models
##### `predict_proba()`
* Predicts the probability of each class label, and it returns the probability estimates for each possible class label.
	* Arguments
		1) `features` -- the vector to be scored
```Python
# Example
probabilities = model.predict_proba(features)
print(probabilities)
```
* Returns a table-like structure with the following info:
	* Column 1: Negative class probability 
	* Column 2: Positive class probability

```Result
[[0.5795 0.4205]
 [0.6629 0.3371]
 [0.7313 0.2687]
 [0.6728 0.3272]
 [0.5086 0.4914]]
```

```Python
# Example -- Full Example

# Import Libraries
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import precision_score, recall_score

# Import data
data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

# Prepare the features and target
target = data['Claim']
features = data.drop('Claim', axis=1)

# Split the data
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

# Create and train model
model = LogisticRegression(random_state=12345, solver='liblinear')
model.fit(features_train, target_train)

# Predict the probabilities
probabilities_valid = model.predict_proba(features_valid)
probabilities_one_valid = probabilities_valid[:, 1]

# Iterate over range and calculate precision and recall for each threshold
for threshold in np.arange(0, 0.3, 0.02):
    predicted_valid = probabilities_one_valid > threshold
    precision = precision_score(target_valid, predicted_valid)
    recall = recall_score(target_valid, predicted_valid)
    print(
        	'Threshold = {:.2f} | Precision = {:.3f}, Recall = {:.3f}'.format(
            	threshold, precision, recall
        	)
    	)
```

```Result
Threshold = 0.00 | Precision = 0.013, Recall = 1.000
Threshold = 0.02 | Precision = 0.052, Recall = 0.645
Threshold = 0.04 | Precision = 0.061, Recall = 0.609
Threshold = 0.06 | Precision = 0.072, Recall = 0.367
Threshold = 0.08 | Precision = 0.097, Recall = 0.254
Threshold = 0.10 | Precision = 0.112, Recall = 0.178
...
```


---
# Evaluation Metrics in Sklearn
* Sklearn has many functions for calculating metrics, which can be found in the `sklearn.metrics` module
##### `accuracy_score()`
* Calculates and returns the accuracy value of a model
	* Arguments
		1) `y_true` -- a list (or array-like) structure containing the correct answers
		2) `y_pred` -- a list (or array-like) structure containing the predicted labels
```Python
from sklearn.metrics import accuracy_score

test_features = test_df.drop(['last_price', 'price_class'], axis=1)
test_target = test_df['price_class']
test_predictions = model.predict(test_features)

# Finding the accuracy
test_accuracy = accuracy_score(test_target, test_predictions)
```

##### `score()`
* Return the mean accuracy on the given test data and labels.
	* Arguments
		* `features` -- the test samples
		* `target` -- the labels for the test-sample (target)
		* `sample_weight` -- sample weight
* Removes the need to call `predict()` in order to call `accuracy_score()`
```Python
# Importin the RandomForestClassifier class
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(random_state=12345, n_estimators=3)
model.fit(features, target)

# Determining the accuracy
model.score(features, target)
```

##### `recall_score()`
* Computes the recall using the following ratio: `TP` / (`FP` + `FN`) and returns a value between 0 and 1, with 1 being the best
	* Arguments
		1) `target` -- an array-like structure containing the actual (or true) values
		2) `pred` -- an array-like structure containing the predicted values
```Python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import recall_score
from sklearn.model_selection import train_test_split

data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

target = data['Claim']
features = data.drop('Claim', axis=1)

features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

model = DecisionTreeClassifier(random_state=12345)
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)

# Calculate the recall of the model
recall = recall_score(target_valid, predicted_valid)
print(recall) # 0.07100591715976332
```

##### `precision_score()`
* Computes the precision using the following ratio: `TP` / (`TP` + `FP`) and returns a value between 0 and 1, with 1 being the best
	* Arguments
		1) `target` -- an array-like structure containing the actual (or true) values
		2) `pred` -- an array-like structure containing the predicted values
```Python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import precision_score
from sklearn.model_selection import train_test_split

data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

target = data['Claim']
features = data.drop('Claim', axis=1)

features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

model = DecisionTreeClassifier(random_state=12345)
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)

# Calculate Precision
precision = precision_score(target_valid, predicted_valid) 
print(precision) # 0.06779661016949153
```

##### `f1_score()`
* Compute the F1 score (harmonic mean of recall and precision) also known as balanced F-score or F-measure using the following equation `F1 = (2 * Precision * Recall) / (Recall + Precision)`
	* Arguments
		1) `target` -- an array-like structure containing the actual (or true) values
		2) `pred` -- an array-like structure containing the predicted values
```Python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import f1_score

data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

target = data['Claim']
features = data.drop('Claim', axis=1)

features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

model = DecisionTreeClassifier(random_state=12345)
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)

f1 = f1_score(target_valid, predicted_valid)
print(f1) # 0.06936416184971098
```

##### `confusion_matrix()`
* A classification metric that calculates the number of `TP`, `TN`, `FP`, `FN`
* Calculates the confusion matrix
	* Arguments
		1) `target` -- an array-like structure containing the actual (or true) values
		2) `pred` -- an array-like structure containing the predicted values
```Python
import pandas as pd
from sklearn.metrics import confusion_matrix

target = pd.Series([1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1])
predictions = pd.Series([1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 1])

print(confusion_matrix(target, predictions))
```

```Result
[[4 3]
 [2 5]]
```

```Python
# Example -- Full Example

import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import confusion_matrix
from sklearn.model_selection import train_test_split

data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

target = data['Claim']
features = data.drop('Claim', axis=1)

features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

model = DecisionTreeClassifier(random_state=12345)
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)

# Calculating the confusion matrix
c_matrix = confusion_matrix(target_valid, predicted_valid)
print(c_matrix)
```

```Result
[[12331   165]
 [  157    12]]
```

* Calculating the `TP`, `TN`, `FP`, `FN` manually
```Python
# Example
import pandas as pd

target = pd.Series([1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1])
predictions = pd.Series([1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 1])

# Calculate True Positive
tp = ((target == 1) & (predictions == 1)).sum()
print(fp) # 5

# Calculate True Negative
tn = ((target == 0) & (predictions == 0)).sum()
print(tn) # 4

# Calculate False Positive
fp = ((target == 0) & (predictions == 1)).sum()
print(fp) # 3

# Calculate False Negative
fn = ((target == 1) & (predictions == 0)).sum()
print(fn) # 2
```

##### PR-Curve
* PR-Curve -- plots the values of the metrics (Precision and Recall) to show how the curve responds to threshold changing
```Python
# Example -- Plotting a PR-Curve

import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.metrics import precision_recall_curve
from sklearn.linear_model import LogisticRegression

data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

target = data['Claim']
features = data.drop('Claim', axis=1)
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

model = LogisticRegression(random_state=12345, solver='liblinear')
model.fit(features_train, target_train)

probabilities_valid = model.predict_proba(features_valid)
precision, recall, thresholds = precision_recall_curve(
    target_valid, probabilities_valid[:, 1]
)

plt.figure(figsize=(6, 6))
plt.step(recall, precision, where='post')
plt.xlabel('Recall')
plt.ylabel('Precision')
plt.ylim([0.0, 1.05])
plt.xlim([0.0, 1.0])
plt.title('Precision-Recall Curve')
plt.show()
```

##### `roc_auc_score()`
* Computes the Area Under Curve (AUC) of the Receiver Operating Characteristic (ROC) Curve from prediction scores
	* Arguments
		1) `target` -- the target scores
		2) `probabilities` -- the probability estimates of the positive class, confidence values, or non-thresholded measure of decisions
```Python
# Example -- Full Example

# Import Libraries
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import roc_auc_score

# Import data
data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

# Define features and target
target = data['Claim']
features = data.drop('Claim', axis=1)

# Split data
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

# Create and train model
model = LogisticRegression(random_state=12345, solver='liblinear')
model.fit(features_train, target_train)

# Predict probabilities 
probabilities_valid = model.predict_proba(features_valid)
probabilities_one_valid = probabilities_valid[:, 1]

# Calculate AUC
auc_roc = roc_auc_score(target_valid, probabilities_one_valid)
print(auc_roc) # 0.8222607565781999

```

##### `roc_curve()`
* Computes a Receiver operating characteristic (ROC) curve
	* Arguments
		1) `target` -- the target scores
		2) `probabilities` -- the probability estimates of the positive class, confidence values, or non-thresholded measure of decisions
```Python
from sklearn.metrics import roc_curve
fpr, tpr, thresholds = roc_curve(target, probabilities)
```

```Python
# Example -- Full Example

# Import Libraries
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import roc_curve

# Import Data
data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

# Define features and target
target = data['Claim']
features = data.drop('Claim', axis=1)

# Split data
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

# Create and train model
model = LogisticRegression(random_state=12345, solver='liblinear')
model.fit(features_train, target_train)

# Predict probabilities 
probabilities_valid = model.predict_proba(features_valid)
probabilities_one_valid = probabilities_valid[:, 1]

# Plot ROC Curve
fpr, tpr, thresholds = roc_curve(target_valid, probabilities_one_valid)

plt.figure()
plt.plot(fpr, tpr)
plt.plot([0, 1], [0, 1], linestyle='--') # Plot a random model
plt.xlim([0.0, 1.0])
plt.ylim([0.0, 1.0])
plt.ylabel('True Positive Rate')
plt.xlabel('False Positive Rate')
plt.title("ROC curve")
plt.show()
```
* Result 	
	![[ROC-curve-exercise.png]]

##### `mean_squared_error()`
* Calculates the mean squared error in regression tasks
	* Arguments
		1) `y_true` -- an array-like structure containing the actual values 
		2) `y_pred` -- an array-like structure containing the predicted values
		3) `squared=` -- default is `True`, if set to `False`, it will not square the values, returning the RMSE instead
```Python
from sklearn.metrics import mean_squared_error

answers = [623, 253, 150, 237]
predictions = [649, 253, 370, 148]

result = mean_squared_error(answers, predictions)
print(result) # 14249.25
```

```Python
# Example -- Full Example 

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

data = pd.read_csv('/datasets/flights_preprocessed.csv')

target = data['Arrival Delay']
features = data.drop(['Arrival Delay'], axis=1)
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

model = LinearRegression()
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)

# Find the MSE & RMSE
mse = mean_squared_error(target_valid, predicted_valid)

print("MSE =", mse) # MSE = 2129.8240528555298
print("RMSE =", mse ** 0.5) # RMSE = 46.15001682400051
```

```Python
# Example -- Full Example 
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

data = pd.read_csv('/datasets/flights_preprocessed.csv')

target = data['Arrival Delay']
features = data.drop(['Arrival Delay'], axis=1)
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

model = LinearRegression()
model.fit(features_train, target_train)

# Calculate the MSE & RMSE for model
predicted_valid = model.predict(features_valid)
mse = mean_squared_error(target_valid, predicted_valid)
print('Linear Regression')
print('MSE =', mse)
print('RMSE =', mse ** 0.5)

# Calculate the MSE & RMSE for constant
predicted_valid = pd.Series(target_train.mean(), index=target_valid.index)
mse = mean_squared_error(target_valid, predicted_valid)
print('Mean')
print('MSE =', mse)
print('RMSE =', mse ** 0.5)
```

##### `r2_score()`
* Calculates the $R^2$ (coefficient of determination) regression score function
	* Arguments
		1) `target` -- an array-like structure containing the actual values 
		2) `predicted` -- an array-like structure containing the predicted values
```Python
# Example -- Full Example

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import r2_score

data = pd.read_csv('/datasets/flights_preprocessed.csv')

target = data['Arrival Delay']
features = data.drop(['Arrival Delay'], axis=1)
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

model = LinearRegression()
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)

# Calculate R2 Score
print('R2 =', r2_score(target_valid, predicted_valid))
```

##### `mean_absolute_error()`
* Calculates the mean absolute error regression loss
	* Arguments
		1) `target` -- an array-like structure containing the actual values 
		2) `predicted` -- an array-like structure containing the predicted values
```Python
# Example -- Full Example

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error

data = pd.read_csv('/datasets/flights_preprocessed.csv')

target = data['Arrival Delay']
features = data.drop(['Arrival Delay'], axis=1)
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)
model = LinearRegression()
model.fit(features_train, target_train)
predicted_valid = model.predict(features_valid)

# Calculate the MAE
mae = mean_absolute_error(target_valid, predicted_valid)
print(mae)
```



---
# Working with Datasets in Sklearn

### Splitting Data
* Sklearn has functions for dealing with data splitting, which can be found in the `sklearn.model_selection` module
##### `train_test_split()`
* Split arrays or matrices into random train and test subsets
	* Arguments
		1) `array` -- the array (or list) to be split
		2) `test_size=` -- the proportion of the dataset to include in the test split
		3) `train_size=` -- the proportion of the dataset to include in the train split
		4) `random_state=` -- controls the shuffling applied to the data before applying the split. Pass an int for reproducible output across multiple function calls.
		5) `shuffle=` -- `True` by default; determines if data is to be shuffled before split
```Python
# Importing the train_test_split function
from sklearn.model_selection import train_test_split

# Splitting the data into a train and validation dataset
df_train, df_valid = train_test_split(df, test_size=0.25, random_state=12345)
```

```Python
import pandas as pd
from sklearn.model_selection import train_test_split

df = pd.read_csv('/datasets/train_data_us.csv')
df.loc[df['last_price'] > 113000, 'price_class'] = 1
df.loc[df['last_price'] <= 113000, 'price_class'] = 0

# Splitting the data into a train and validation dataset
df_train, df_valid = train_test_split(df, test_size=0.25, train_size=0.75, random_state=12345)

features_train = df_train.drop(['last_price', 'price_class'], axis=1)
target_train = df_train['price_class']
features_valid = df_valid.drop(['last_price', 'price_class'], axis=1)
target_valid = df_valid['price_class']

print(features_train.shape) # (4871, 13)
print(target_train.shape) # (4871, )
print(features_valid.shape) # (1624, 13)
print(target_valid.shape) # (1624, )
```

### Shuffling Data
* Sklearn has a function for shuffling data in the `sklearn.utils` module
##### `suffle()`
* Shuffle arrays or sparse matrices in a consistent way
	* Arguments
		1) `*arrays` -- array-like structures (lists, DataFrames, scipy matrices) to be shuffled
		2) `random_state=` -- Default it is `None`, which sets the pseudorandom to always be  different; a different value can be used to specify the use of the same pseudorandom number
		3) `n_samples=` -- Number of samples to generate. If left to None this is automatically set to the first dimension of the arrays. It should not be larger than the length of arrays.
```Python
# Define function for upsampling
def upsample(features, target, repeat):
	# Split Data
    features_zeros = features[target == 0]
    features_ones = features[target == 1]
    target_zeros = target[target == 0]
    target_ones = target[target == 1]
    
	# Duplicate and create new dataset
    features_upsampled = pd.concat([features_zeros] + [features_ones] * repeat)
    target_upsampled = pd.concat([target_zeros] + [target_ones] * repeat)
    
	# Suffle data
    return shuffle(features_upsampled, target_upsampled, random_state=12345)

# Upsample the data
features_upsampled, target_upsampled = upsample(features_train, target_train, 10)
```

### Cross-Validating Data
*  Sklearn has functions for dealing with data cross-validation, which can be found in the `sklearn.model_selection` module
##### `cross_val_score()`
* Evaluates a score by cross-validation and returns a list of model evaluation scores from each validation
	* Arguments
		* `model` -- the model to use for cross validation, which should be passed in as untrained.
		* `X` (`features`) -- the data to be fit
		* `y` (`target`) -- The target variable to try to predict (in the case of supervised learning)
		* `groups=` -- Group labels for the samples used while splitting the dataset into train/test set
		* `scoring=` -- A str or a scorer callable object / function with signature `scorer(estimator, X, y)` which should return only a single value
		* `cv=` -- the number of blocks to use for cross-validation
```Python
from sklearn.model_selection import cross_val_score
from sklearn.tree import DecisionTreeClassifier 

model = DecisionTreeClassifier() # Defining the model 
cross_val_score(model, features, target, cv=3)
```

```Python
# -- Example

import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import cross_val_score

data = pd.read_csv('/datasets/heart.csv')
features = data.drop(['target'], axis=1)
target = data['target']

# Defining the model
model = DecisionTreeClassifier(random_state=0)

# Saving the cross-validation scores
scores = cross_val_score(model, features, target, cv=5)

# Finding the final score
final_score = scores.mean()

# Results
print(scores) # [0.72131148 0.78688525 0.80327869 0.83333333 0.78333333]
print('Average model evaluation score:', final_score) 
# Average model evaluation score: 0.7856284153005464
```


---
# One-Hot Encoding in Sklearn
* OHE -- a special technique (used in Logistic Regression) for transforming categorical features into numerical features (dummy variables)
```Python
# Using OHE on a specific column
import pandas as pd
data = pd.read_csv('/datasets/travel_insurance_us.csv')

gender_ohe = pd.get_dummies(data['Gender'], drop_first=True)
```

```Result
   M  None
0  1     0
1  0     1
2  0     1
3  0     1
4  1     0
```

```Python
# Using OHE on a an entire dataframe
import pandas as pd

data = pd.read_csv('/datasets/travel_insurance_us.csv')
data_ohe = pd.get_dummies(data, drop_first=True)
```

```Result
   Claim  Duration  Net Sales  ...  Destination_ZIMBABWE  Gender_M  Gender_None
0      0        12       45.0  ...                     0         1            0
1      0        50       22.0  ...                     0         0            1
2      0       251       80.0  ...                     0         0            1
```

```Python
# Example -- OHE Full Example

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression

data = pd.read_csv('/datasets/travel_insurance_us.csv')

# Perform OHE 
data_ohe = pd.get_dummies(data, drop_first=True)
target = data_ohe['Claim']
features = data_ohe.drop('Claim', axis=1)

features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

model = LogisticRegression(solver='liblinear', random_state=12345)
model.fit(features_train, target_train)

print('Trained!')
```


---
# Label  & Ordinal Encoding in Sklearn
* Label Encoding -- an encoding technique that keeps all information about the original variable in one feature by replacing the categories with arbitrary numeric values
##### `LabelEncoder`
* A class from the `sklearn.preprocessing` module that encodes a single column
	* Arguments
		* None
* Methods:
	* `fit()` -- fits the label encoder.
		* Arguments
			* `y` -- the label to be fit
	* `fit_transform()` -- fits the label encoder and returns encoded labels.
		* Arguments
			* `y` -- the label to be fit and transformed
	* `transform()` -- transform labels to normalized encoding
		* Arguments:
			* `y` -- the label to be transformed
```Python
# Import the LabelEncoder class
from sklearn.preprocessing import LabelEncoder

# Import the data
data = pd.read_csv('/datasets/travel_insurance_us.csv')

# Initialize the LabelEncoder
encoder = LabelEncoder()

# Apply LabelEncoder to the gender column
data['gender_encoded'] = encoder.fit_transform(data['gender'])
```

##### `OrdinalEncoder`
* A class from the `sklearn.preprocessing` module encodes two or more columns at a time
	* Arguments
		* `categories=` -- (default is `auto`); holds the categories expected in the ith column. The passed categories should be sorted in case of numeric values.
* Methods:
	* `fit()` -- fits the OrdinalEncoder to X
		* Arguments
			* `X` -- the data to be fit
	* `fit_transform()` -- fits to data, then transforms it
		* Arguments
			* `X` -- the data to be fit and transformed
	* `transform()` -- transforms X to ordinal codes
		* Arguments:
			* `X` -- the data to be transformed
```python
# Importing the OrdinalEncoder class
from sklearn.preprocessing import OrdinalEncoder

# Import the data
data = pd.read_csv('/datasets/travel_insurance_us.csv')

# Creating an instance of the class
encoder = OrdinalEncoder()

# Tuning data to make the encoder recognize categorical features
encoder.fit(data)

# Transforming (encoding) the data
data_ordinal = encoder.transform(data)

# Adding columns names using the DataFrame constructor
data_ordinal = pd.DataFrame(encoder.transform(data), columns=data.columns)
```

```Python
# Importing the OrdinalEncoder class
from sklearn.preprocessing import OrdinalEncoder

# Importing the data
data = pd.read_csv('/datasets/travel_insurance_us.csv')

# Creating an instance of the class
encoder = OrdinalEncoder()

# Fitting and transforming the data at once
data_ordinal = pd.DataFrame(encoder.fit_transform(data), columns=data.columns)
```

```Python
# Example -- Using the categories parameter

# Import the libraries
from sklearn.preprocessing import OrdinalEncoder

# Importing the data
data = pd.read_csv('/datasets/travel_insurance_us.csv')

# Define the desired order of categories for the feature
##  Here, 'small' < 'medium' < 'large'
### so 'small' will be encoded as 0, 'medium' as 1, 'large' as 2
categories = [['small', 'medium', 'large']]

# Create an instance of OrdinalEncoder with specified categories
encoder = OrdinalEncoder(categories=categories)

# Fit and transform the data using the encoder
encoded_data = encoder.fit_transform(data)
```

```Python
# Example -- Full Example

# Import the libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.preprocessing import OrdinalEncoder

# Importing the data
data = pd.read_csv('/datasets/travel_insurance_us.csv')

# Creating an instance of the class
encoder = OrdinalEncoder()

# Fitting and transforming the data at once
data_ordinal = pd.DataFrame(encoder.fit_transform(data), columns=data.columns)

# Defining the target and features
target = data_ordinal['Claim']
features = data_ordinal.drop('Claim', axis=1)

# Splitting the data
features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

# Defining and fitting the model
model = DecisionTreeClassifier(random_state=12345)
model.fit(features_train, target_train)

print('Trained!')
```

* Alternative Mapping to OrdinalEncoder for ordinal variables (a variable with categories where order matters)
```Python
# Define the dictionary and appropiate values
temperature_dict = {'cold': 0, 'warm': 1, 'hot': 2}

# Mapping the values 
df['temperature'] = df['temperature'].map(temp_dict)
```


---
# Feature Scaling in Sklearn
 * Sklearn has a class for standardizing data
#### `StandardScaler`
* A class, located in the `sklearn.preprocessing` module, for standardizing data
	* Arguments
		* None
* Methods
	* `fit` -- computes the mean and std to be used for later scaling
		* `X` -- the features to fit
	* `transform` -- performs standardization by centering and scaling
		* `X` -- the features to transform
```Python
# Imporint the StandardScaler
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler() # Create instance of the class
scaler.fit(features_train) # Tune the class using training data

# Transform the training and validation data
features_train_scaled = scaler.transform(features_train)
features_valid_scaled = scaler.transform(features_valid)
```

```Python
# Example -- Full Example

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

# Disables the SettingWithCopyWarning
pd.options.mode.chained_assignment = None

# Import Data
data = pd.read_csv('/datasets/travel_insurance_us.csv')

# Create target and features
target = data['Claim']
features = data.drop('Claim', axis=1)

# Create train and validation features and target
features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

numeric = ['Duration', 'Net Sales', 'Commission (in value)', 'Age']

# Create instance
scaler = StandardScaler()

# Fit the data
scaler.fit(features_train[numeric])

# Transform the data
features_train[numeric] = scaler.transform(features_train[numeric])
features_valid[numeric] = scaler.transform(features_valid[numeric])

```



---
# Upsampling & Downsampling in Sklearn
* Upscaling and downscaling are used in Classification Tasks

##### Upsampling
* Upsampling -- the process of randomly duplicating observations from the minority class to reinforce its signal.
```Python
# Example -- Full Example

# Import libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.utils import shuffle
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import f1_score

# Import dataset
data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

# Prepare target and features
target = data['Claim']
features = data.drop('Claim', axis=1)

# Split data
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

# Define function for upsampling
def upsample(features, target, repeat):
	# Split Data
    features_zeros = features[target == 0]
    features_ones = features[target == 1]
    target_zeros = target[target == 0]
    target_ones = target[target == 1]
    
	# Duplicate and create new dataset
    features_upsampled = pd.concat([features_zeros] + [features_ones] * repeat)
    target_upsampled = pd.concat([target_zeros] + [target_ones] * repeat)
    
	# Suffle data
    return shuffle(features_upsampled, target_upsampled, random_state=12345)

# Upsample the data
features_upsampled, target_upsampled = upsample(features_train, target_train, 10)

model = LogisticRegression(random_state=12345, solver='liblinear')
model.fit(features_upsampled, target_upsampled)
predicted_valid = model.predict(features_valid)

print('F1:', f1_score(target_valid, predicted_valid)) # F1: 0.13688212927756654
```

##### Downsampling
* Downsampling -- randomly removing observations from the majority class to prevent its signal from dominating the learning algorithm
```Python
# Example -- Full Example

# Import libraries
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.utils import shuffle
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import f1_score

# Import dataset
data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

# Prepare target and features
target = data['Claim']
features = data.drop('Claim', axis=1)

# Split data
features_train, features_valid, target_train, target_valid = train_test_split(
    features, target, test_size=0.25, random_state=12345
)

# Define function for downsampling
def downsample(features, target, fraction):
	# Split Data
    features_zeros = features[target == 0]
    features_ones = features[target == 1]
    target_zeros = target[target == 0]
    target_ones = target[target == 1]
    
	# Randomly drop negative observations and create new tranining sample
    features_downsampled = pd.concat(
        [features_zeros.sample(frac=fraction, random_state=12345)]
        + [features_ones]
    )
    
    target_downsampled = pd.concat(
        [target_zeros.sample(frac=fraction, random_state=12345)]
        + [target_ones]
    )
    
    # Suffle data
    return shuffle(
        features_downsampled, target_downsampled, random_state=12345
    )

# downsample the data
features_downsampled, target_downsampled = downsample(
    features_train, target_train, 0.1
)

model = LogisticRegression(random_state=12345, solver='liblinear')
model.fit(features_downsampled, target_downsampled)

predicted_valid = model.predict(features_valid)

print('F1:', f1_score(target_valid, predicted_valid))
```


---

# Model Parameters vs Hyperparameters

| Parameters                                                               | Hyperparameters                                                                            |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| Parameters are the configuration model, which are internal to the model. | Hyperparameters are the explicitly specified parameters that control the training process. |
| Parameters are essential for making predictions.                         | Hyperparameters are essential for optimizing the model.                                    |
# Hyperparameters
* Hyperparameters -- settings for learning algorithms that help improve the model
	* Hyperparameter values are set by default, but can be adjusted
* There are different kinds of hyperparameters, which can be used with different models and algorithms

##### `random_state=` 
* By default it is `None`, which sets the pseudorandom to always be different; A different value can be used to specify the use of the same pseudorandom number every time the model runs
##### `max_depth=`
* By default, it is unlimited; Sets the maximum depth of a tree
##### `min_samples_split=` 
* Prohibits creating nodes that don't contain enough observations from the training set
##### `min_samples_leaf=` 
* Prevents the algorithm from adding leaf nodes that don't have enough observations from the training set.

### Working with Hyperparameters
* Hyperparameters can be tuned to see which one works best.
* Loops are useful for determining which hyperparameter settings work best

```Python
# Determining which max_depth works best

# Import Libaries
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split

df = pd.read_csv('/datasets/train_data_us.csv')
df.loc[df['last_price'] > 113000, 'price_class'] = 1
df.loc[df['last_price'] <= 113000, 'price_class'] = 0

df_train, df_valid = train_test_split(df, test_size=0.25, random_state=12345)

features_train = df_train.drop(['last_price', 'price_class'], axis=1)
target_train = df_train['price_class']

features_valid = df_valid.drop(['last_price', 'price_class'], axis=1)
target_valid = df_valid['price_class']

for i in range(1,6):
    model = DecisionTreeClassifier(max_depth=i, random_state=12345)
    model.fit(features_train, target_train)
    result = model.predict(features_valid)
    acc = accuracy_score(target_valid, result)
    print(f"max_depth = {i} : {acc}")
```

```Result
max_depth = 1 : 0.8522167487684729
max_depth = 2 : 0.8522167487684729
max_depth = 3 : 0.8466748768472906
max_depth = 4 : 0.8725369458128078
max_depth = 5 : 0.8663793103448276
```