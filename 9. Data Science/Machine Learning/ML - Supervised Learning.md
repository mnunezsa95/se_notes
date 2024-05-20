See:
* [[DS - What is Data Science?]]
* [[ML - Machine Learning Basics]]
* [[Py - Pandas (Methods)]]
Resources
* [TripleTen Knowledge Base](https://tripleten.netlify.app/DS/SL)
* [Confusion Matrix](https://docs.kolena.com/metrics/tp-fp-fn-tn/#:~:text=The%20counts%20of%20true%20positive,accuracy%2C%20precision%2C%20and%20recall.)
* [Target Leakage](https://www.kaggle.com/code/alexisbcook/data-leakage)


---
# Definitions
* High Cardinality Variable -- a variable with alot of categories
* Ordinal Variable -- a variable where the categories have an implicit order, like "warm", "cold", "hot"
* Nominal Variable -- a variable where the categories do not have an implicit order, like "surf plan", "ultimate plan", "family plan"
* Feature Scaling -- a technique to standardize the independent features present in the data in a fixed range. 

---
# Types of Machine Learning Models

## Logistic Regression Model
* Logistic Function -- a machine learning model used for classification tasks
	* Has a sigmoid curve shape
	* Y-axis has a range from 0 to 1 and represents the probability of an event. 
	* X-axis plots variables that affect the probability
* Formula
	* p -- probability of the label being 1
	* $1-p$ -- probability of the label being 0
	* $x_1$ -- the feature
	* $b_1$ -- a feature weight (curve steepness)
	* $b_0$ -- an intercept (curve shift)
$$ln(p/(1-p)) = b_0 + b_1 * x_1$$
* Logistic Regression 
	* **Purpose**: Logistic regression is a classification algorithm used to predict the probability of a binary outcome (e.g., yes/no, 1/0).
	* **Model**: It uses the logistic function (sigmoid curve) to model the relationship between the independent variables (features) and the probability of the outcome.
	* **Output**: The output of logistic regression is a probability score between 0 and 1, representing the likelihood of the positive class.
	* **Interpretation**: The model calculates class proximity (log-odds) based on feature weights (coefficients) and an intercept. Positive proximity favors one class, negative favors the other.
	* **Training**: The algorithm adjusts coefficients during training to minimize the difference between predicted probabilities and actual labels.
	* **Features**: Logistic regression can handle multiple features simultaneously, with each feature contributing differently (based on its coefficient) to the predicted probability.
	* **Usage**: It's effective for binary classification tasks when the relationship between features and the outcome is expected to be linear.


## Linear Regression 
* Linear regression is a **linear model**, e.g. a model that assumes a linear relationship between the input variables (x) and the single output variable (y)
* **Linear Regression is used for Regression tasks**
* Formula:
	* $y$ -- the target (dependent variable)
	* $a$ -- the slope 
	* $x$ -- the independent variable (features)
	* $b$ -- the intercept
		* a feature-independent parameter that shifts the line along the y-axis.
$$y = ax + b$$

----
---
# Types of Datasets
### Training Datasets
* Training dataset -- a set of data used by Machine Learning Models to gather and classify knowledge, discover dependencies, and gain experience

### Validation Dataset
* Validation dataset -- a set of data that shows how the model acts in the field and helps reveal overfitting
* Validation datasets are separated from the source data before the model is trained.

### Testing Datasets
* Testing dataset -- a set of data used by Machine Learning Models to evaluate the performance and progress of the algorithm


---
# Working with Data

### Data Sourcing 
* Data typically comes from a company
* Open source data can also be used (found on open-source sites like Kaggle)

### Data Splitting
* There are two ways to split out data
	* **Scenario 1:** Test Dataset already exists separately
		* Source Dataset is divided into 2 parts, using a 3:1 split
			* Training Dataset (75%)
			* Validation Dataset (25%)
			![[3-1-data-split.png]]
	* **Scenario 2:** Test Dataset DOES NOT exist
		* Source dataset is divided into 3 parts, using a 3:1:1 split
			* Training Dataset (60%)
			* Validation Dataset (20%)
			* Testing Dataset (20%)
			![[3-1-1-data-split.png]]

### Data Labeling
- If data is missing, consider utilizing unlabeled data and engage in data labeling or annotation.
- **Unlabeled Data** -- data pieces lacking identifying characteristics, properties, or classifications.
    - Unlabeled data lacks labels or targets for prediction and comprises solely of features representing the data.
- **Data Labeling / Data Annotation** -- involves identifying raw data (such as images, text files, videos) and adding informative labels to provide context, enabling machine learning models to learn effectively from it.

### Labeling Quality Control
* Labeling Quality Control Methods are used to improve data quality by labeling observations multiple times to form a final answer
	* Majority Vote Method:
		* Each observation is labeled by multiple assessors
		* The final label is determined by the majority vote among the assessors
```Python
import pandas as pd

data = pd.read_csv('/datasets/heart_labeled.csv')
target = []
for i in range(data.shape[0]):
    labels = data.loc[i, ['label_1', 'label_2', 'label_3']]
    true_label = int(labels.mode() > 0.5)
    target.append(true_label)
    
data['target'] = target
print(data.head())
```

### Target Leakage
- To ensure the highest-quality model, it's important to prevent target leakage.
- **Target Leakage** -- occurs when training data includes information about the target that won't be available during prediction.
    - Consequences include:
        - High performance during training (and validation).
        - Poor performance in real-world applications.

### Cross-Validation 
* **Cross - Validation** (k-fold cross-validation) --  a technique that will help train and test a model using several randomly formed samples
	* It minimizes the randomness of data splitting and gives a more accurate result
* How it works:
	* Decide on a value for $k$ (the number of equal subsets to divide dataset into)
	* Divide the dataset using the value for $k$
	* Iterate over the subsets and assign different purposes for each one
		* Iteration 1: Subset 1 to be used for validation, remaining four used for training
		* Iteration 2: Subset 2 to be used for validation, remaining four for training 
		* $...$
		![[k-fold-cross-validation-visual.png]]
	* Evaluate the final model using the mean across all $k$ evaluation scores
* Cross-Validation is useful for:
	* Comparing models
	* Selecting hyperparameters
	* Evaluating usefulness of features
```Python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier

data = pd.read_csv('/datasets/heart.csv')
features = data.drop(['target'], axis=1)
target = data['target']

scores = [] 

# Set the block size if there are only three of them
sample_size = int(len(data)/3)

for i in range(0, len(data), sample_size):
    valid_indexes = list(range(i, i + sample_size))
    train_indexes = list(range(0, i)) + list(range(i + sample_size, len(data)))
    
    features_train = features.iloc[train_indexes]
    features_valid = features.iloc[valid_indexes]
    
    target_train = target.iloc[train_indexes]
    target_valid = target.iloc[valid_indexes]
    
    model = DecisionTreeClassifier(random_state=0)
    model = model.fit(features_train, target_train)
    score = model.score(features_valid, target_valid)
    
    scores.append(score)
 
final_score = sum(scores) / len(scores)
print('Average model quality score:', final_score)
```



---
## Encoding Overview
| Type                       | Best For              | Pros                                                                                                                                                           | Cons                                                                                                                                                                                                                                                                                                |
| -------------------------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| One-Hot Encoding <br>(OHE) | Regression Taks       | Ensures equal importance and independence among categories.<br><br>Works well with ML algorithms that consider all features simultaneously  (like regressions) | High memory consumption and data sparsity, especially with high cardinality variables                                                                                                                                                                                                               |
| Label & Ordinal Encoding   | Tree-Based Algorithms | Works well with tree-based ML algorithms where the order of labels matters more than their scale.                                                              | Risk of the model misinterpreting encoded values as meaningful scalar quantities <br><br>May lead to nonsensical splits in tree-based algorithms if labels are not correctly ordered.<br><br>Not suitable for maintaining equal importance among categories, particularly in regression algorithms. |
##### Summary:
* **OHE** is recommended for:
	1) Regression-based algorithms
	2) Nominal variables (when the categories have no implicit order)
	3) It is a low cardinality variable

- **Ordinal Encoding** is recommended for:
	1) Tree-based algorithms
	2) Ordinal variables (when the categories have an implicit order)


---
## Types of Encoding
#### One-Hot Encoding (OHE)
* OHE -- a special technique (used in Logistic Regression) for transforming categorical features into numerical features (dummy variables) using two steps:
	1) Add a separate column for each feature value
	2) If the category fits the observation, 1 is assigned; otherwise, 0 is assigned
* OHE can lead to the **"the dummy trap"**
	* High correlations between new columns cause confusion for the model.
		* Preventing **"the dummy trap"**
			1) Remove any one of the newly created columns since the the model can infer its values based on the other columns
* Example:
	* Create a separate column for each `Gender` value (`F, M, None`):
		* If the value is `F`, 1 goes to the `Gender_F` column
		* if the value is `M`, then 1 goes to `Gender_M` column
		* If the value is `None`, then 1 goes to `Gender_None` column
		![[ohe-example.png]]


#### Label Encoding
* Label Encoding -- an encoding technique that keeps all information about the original variable in one feature by replacing the categories with arbitrary numeric values
	* Used to encode categorical features for tree-based algorithms
* Sklearn has two classes located inside the `sklearn.preprocessing` module for Label Encoding, that work by assigning numbers to categories in alphabetical order
	* `LabelEncoder` -- used for encoding a single column at a time
	* `OrdinalEncoder` -- used for encoding two or more columns at a time
		* Encoding of an ordinal variable with numeric labels arranged in a specific natural order, usually done by manual enumeration of labels.
* Example:
	* Keeps one Gender column, but gives each category a different numerical value
		* `F` is given a 0
		* `M` is given a 1
		* `None` is given a 2
		![[label-encoing-example.png]]


---
## Feature Scaling
* Feature Scaling -- a technique to standardize the independent features present in the data in a fixed range. 
	* It is performed during the data pre-processing to handle highly varying magnitudes or values or units.
* Feature Scaling
	* Features can be scaled by **standardizing the data**
		* The new feature has a
			* Mean = 0
			* Variance = 1
$$ New\;Value = (Old\;Value - M) / sqrt(Var) $$

---

# Balance and Imbalance of the Classes
* Binary Classification has two classes
	* Majority Class -- the class that makes up most of the data
	* Minority Class -- the class that makes up less of the data
* Class Imbalance 
	* Observed when the ratios of the two classes is NOT `1:1`
* Class Balance
	* Observed when the ratio of the two classes is approx. `1:1`
* Positive and Negative
	* A class labeled `'1'` is called positive
	* A class labeled `'0'` is called negative

# Class Weights
* In Classification tasks, Machine Learning algorithms consider all observations in the training set to be equally weighted by default
	* Weights need to be manually assigned if some observations are more important than others

# Upsampling
* Upsampling is a common technique used in classification tasks
* Upsampling -- the process of randomly duplicating observations from the minority class to reinforce its signal.
* Steps to perform Upsampling
	1) Split the training sample into negative and positive observations
	2) Duplicate the positive observations several times
	3) Create a new training sample based on the data obtained
	4) Shuffle the data: identical questions following one another will not help the training

# Downsampling
* Downsampling is a common technique used in classification tasks
* Downsampling -- randomly removing observations from the majority class to prevent its signal from dominating the learning algorithm.
* Steps to perform Downsampling
	1) Split the training sample into negative and positive observations
	2) Randomly drop a portion of the negative observations
	3) Create a new training sample based on the data obtained
	4) Shuffle the data. Make sure the positive data doesn't follow the negative data: this will make it harder for the algorithms to learn

# Classification Threshold
* Classification Threshold -- a critical cut-off point that distinguishes between the different class labels in a binary or multi-class classification
	* A value above that threshold indicates "spam"
	* A value below indicates "not spam."
* The classification threshold is typically 0.5 but this is NOT always true.
* Changing the threshold, will change the evaluation metrics


---
# Confusion Matrix

## What is a Confusion Matrix
* Confusion Matrix -- a table-like matrix that summarizes the performance of a machine learning model on a set of test data for the four divisions

| Metric         | Abbr. | Description                                                       |
| -------------- | ----- | ----------------------------------------------------------------- |
| True Positive  | TP    | Predicted & actual (target) values are positive                   |
| True Negative  | TN    | Both predicted & actual (target) values are negative              |
| False Positive | FP    | Predicted value is positive but actual (target) value is negative |
| False Negative | FN    | Predicted value is negative but actual (target) value is positive |
## Structure a Confusion Matrix
* Matrix Structure
	* 2x2 Grid
		* Horizontal Axis is labeled "Predictions" and has values `0` and `1`
		* Vertical Axis is labeled "Answers" and has values `0` and `1`
	* Division Metric Placement
		* `TN`  -- top left corner
		* `TP` -- bottom right corner
		* `FP` -- top right corner
		* `FN` -- bottom left corner
	![[confusion-matrix.png]]

---
# Evaluation Metrics
* There are four main metrics in Classification Tasks:
	* Accuracy
	* Recall
	* Precision
	* F1 Score
	* True Positive Rate (TPR)
	* False Positive Rate (FPR)
	* PR Curve
	* ROC Curve (AUC)
* There are additional metrics in Regression Tasks
	* Mean Square Error (MSE)
	* Root Mean Squared Error (RMSE)
	* Coefficient of Determination ($R^2$)
	* Mean Absolute Error (MAE)
* Why are evaluation metrics important?
	* Measure the quality of a model and can be expressed numerically.
* Priority of Evaluation Metrics
	* Recall is a priority when it's important to find ALL required observations at the cost of making alot of errors
	* Precision is a priority when the goal is to minimize errors even if it means alot of cases go undetected


## Evaluation Metrics in Classification
### Accuracy
* Accuracy -- the ratio of the number of correct answer to the total number of question
$$ Accuracy = (Num\;Total\;Questions - Number\;Errors) / (Num\;Total\;Questions)$$

### Recall
* Recall -- measures the proportion of correctly identified positive answers (True Positives, `TP`) out of all answers that are actually positive (`TP` + False Negatives, `FN`)
	* Interpreting the Value:
		* Closer to 1 -- model is good at identifying true positives
		* Closer to 0 -- model is bad at identifying true positives
$$Recall = (TP) / (TP + FN)$$
### Precision
* Precision -- measures the proportion of correctly identified positive outcomes (True Positives, `TP`) out of all instances predicted as positive by the model (both True Positives, `TP` and False Positives, `FP`).
	* Interpreting the Value:
		* Closer to 1 -- the model is precise at identifying true positives
		* Closer to 0 -- the model is not precise at identifying true positives
$$ Precision = (TP) / (TP + FP) $$
### F1 Score
* F1 Score -- measures the harmonic mean of recall and precision
	* It combines the precision and recall scores of a model using a 1:1 ratio
	* Interpreting the score
		* Closer to 1 -- the prediction of the class was successful
		* Closer to 0 -- the prediction of the class has failed
* If either, Recall or Precision are close to 0, then the F1 score will also be close to 0
$$ F1\;Score = (2  * Precision * Recall)/(Precision + Recall)$$

```Python
import pandas as pd
from sklearn.metrics import precision_score
from sklearn.metrics import recall_score

target = pd.Series([1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0, 0, 1])
predictions = pd.Series([1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 1])

# Calculate precision, recall, mean
precision = precision_score(target, predictions)
recall = recall_score(target, predictions)
f1 = (2*precision*recall) / (precision + recall)

print('Recall:', recall) # Recall: 0.7142857142857143
print('Precision:', precision) # Precision: 0.625
print('F1 score:', f1) # F1 score: 0.6666666666666666
```

### True Positive Rate (`TPR`)
* True Positive Rate (`TPR`) -- measures  the proportion of actual positive cases that were correctly identified or classified as positive by the model
	* In short, measures the result of the `TP` answers divided by all positive (`P`) answers
	$$TPR = (TP)/P$$
### False Positive Rate (`FPR`)
* False Positive Rate (`FPR`) -- measures the proportion of positive cases that were _incorrectly_ identified or classified as positive in a test
	* In short, measures the result of the FP answers divided by all negative (`N`) answers
	$$FPR = (FP) / N$$
### PR Curve
* PR Curve -- plots the values of the metrics (Precision and Recall) to show how the curve responds to threshold changing
	* Precision is plotted vertically
	* Recall is plotted horizontally
* Interpreting the curve
	* Higher curve = better model
	![[pr-curve.png]]

### ROC Curve
* **ROC curve** (**receiver operating characteristic curve**) -- shows the performance of a classification model at all classification thresholds. 
	* This curve plots two parameters:
		- True Positive Rate (`TPR`) on vertical axis
		- False Positive Rate (`FPR`) on horizontal axis
- Interpreting the graph 
	- Use the AUC (Area Under the Curve) to rate the graph
		- AUC Ranges from 0 to 1
			- 0.5 = A random model (diagonal line)
	- Higher Curve = a greater `TPR` value and greater model quality
	![[ROC-curve.png]]


## Evaluation Metrics in Regression

### Mean Squared Error (MSE)
* Mean Squared Error (MSE) -- measures the amount of error in statistical models and assesses the average squared difference between the observed and predicted values
* Finding the MSE
	1. Calculate the error of each observation
		* Shows the magnitude of discrepancy between the correct answer and prediction$$Observation\;Error = MODEL\;Prediction - CORRRECT\;Answer$$
	
	2. Use the MSE Formula: 
		* $$ MSE = (sum(Sum\;of\;the\;Squares\;of\;the\;Observations\;Errors))/(n)$$
		* Also written:$$ MSE = (sum(y_i - ŷ_i)^2) / (n)$$
		* $y_i$ -- the $i^th$ observed value
		- $ŷ_i$ -- the corresponding predicted value
		- $n$  -- the number of observations.

* Example: Finding MSE
$$MSE = (sum(623-649)^2+(253-253)^2+(150-370)^2+(247-148)^2)/4 = 14249.25$$

### Root Mean Squared Error (RMSE)
* Root Mean Squared Error (RMSE) -- measures the average difference between a statistical model’s [predicted values](https://statisticsbyjim.com/glossary/fitted-values/) and the actual values.
* RMSE is more sensitive to errors or high magnitude, even with a low number of errors because it is a squared metric
* Finding the RMSE
	1. Take the square root of the MSE
		$$RSME = sqrtMSE $$

### Coefficient of Determination ($R^2$)
* Coefficient of Determination ($R^2$) -- divides the model MSE by the mean MSE and subtract the obtained value from one
	* Formula: $$R^2 = 1 - (MODEL\;MSE)/(MEAN\;MSE)$$
* Interpreting the $R^2$ Value
	* _R2_ = 1 
		* MSE Value is zero; model is perfect
	* R2 = 0
		* Model works as well as the mean
	* R2 < 0
		* Model quality is very low


### Mean Absolute Error (MAE)
* Mean Absolute Error (MAE) -- measures of the average size of the mistakes in a collection of predictions, without taking their direction into account
	* The average absolute difference between the predicted values and the actual values and is used to assess the effectiveness of a regression model
* MAE is less sensitive to errors or high magnitude, even with a low number of errors because the metric is not squared
* Goal
	* To minimize mean absolute error MAE
* Formula
	* $y_i$ -- the target (true) value 
	* $ŷ_i$ -- the predicted value
	* $N$ -- the number of observations
	* $sum_{i=1}^{N}$ -- Summation over all observations of the samples ($i$ varies in range from 1 to $N$) $$ MAE = 1/N sum_{i=1}^{N} | y_i-ŷ_i | $$
* Calculating manually:
```Python
import pandas as pd

def mae(target, predictions):
    sum = 0
    for i in range(len(target)):
        sum += abs(target[i] - predictions[i])
    return (sum * 1)/len(target)

target = pd.Series([-0.5, 2.1, 1.5, 0.3])
predictions = pd.Series([-0.6, 1.7, 1.6, 0.2])

print(mae(target, predictions))
```


### sMAPE
* An accuracy measure based on percentage (or relative) errors
* Formula
	* $y_i$ -- the target (true) value 
	* $ŷ_i$ -- the predicted value
	* $N$ -- the number of observations
	* $sum_{i=1}^{N}$ -- Summation over all observations of the samples ($i$ varies in range from 1 to $N$) 
		$$ sMAPE = (1/N)sum_{i=1}^{N}(|y_i-ŷ_i|/(|y_i+ŷ_i|) / 2)  * 100$$

---

