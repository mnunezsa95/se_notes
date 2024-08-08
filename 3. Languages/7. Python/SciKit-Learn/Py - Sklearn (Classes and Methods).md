See:
* [[Py - Introduction to Python]]
* [[ML - Machine Learning Basics]]
* [[Py - Sklearn (Models & Model Comparison)]]
* [[ML - Supervised Learning]]
Resources
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)

---

# Classes

## Classification Tasks
##### `sklearn.tree.DecisionTreeClassifier()`
* A class from the `sklearn.tree` module that is used to create a Decision Tree model for classification tasks
	* Parameters
		* `random_state=` (int) -- (`None`); sets the pseudorandom to always be  different; a different value can be used to specify the use of the same pseudorandom number
		* `max_depth=` (int) -- (unlimited) A different value sets the maximum depth of a tree
		* `class_weight` (str) --  (`None`); sets the class weights to be equivalent;  a different value specifies how to weight the class
			* `'balanced'` -- calculates how many times the class `0` occurs more often than the class `1`
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

##### `sklearn.ensemble.RandomForestClassifier()`
* A class from the `sklearn.ensemble` module, used to create a Random Forest algorithm for classification tasks
	* Arguments
		* `random_state=` (int) -- (`None`); sets the pseudorandom to always be different; a different value can be used to specify the use of the same pseudorandom number
		* `n_estimators=` (int) -- sets the number of trees in the forest
		* `class_weight` --  (`None`); sets the class weights to be equivalent; a different value specifies how to weight the class
			* `'balanced'` -- calculates how many times the class `0` occurs more often than the class `1`
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

##### `sklearn.linear_model.LogisticRegression()`
* A class from the `sklearn.linear_model` module that computes the probability of an event occurrence. 
* Logistic regression determines the category using a formula consisting of numerical features. 
	* Parameters
		* `random_state=` (int) -- (`None`); sets the pseudorandom to always be different; a different value can be used to specify the use of the same pseudorandom number`
		* `solver=` (str) --  specifies a version of the algorithm that determines how the curve is fit
			* `'liblinear'`
		* `class_weight` (str) --  (`None`); sets the class weights to be equivalent; a different value specifies how to weight the class
			* `'balanced'` -- calculates how many times the class `0` occurs more often than the class `1`
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


## Regression Tasks
##### `sklearn.linear_model.LinearRegression()`
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

##### `sklearn.tree.DecisionTreeRegressor()`
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

##### `sklearn.ensemble.RandomForestRegressor()`
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



## Machine Learning for Texts
##### `sklearn.feature_extraction.text.CountVectorizier()`
* Converts a collection of text documents to a matrix of token counts.
	* Parameters (see complete parameters in [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html))
		* `input` (str) -- (`'content'`); 
			* If `'filename'`, the sequence passed as an argument to fit is expected to be a list of filenames that need reading to fetch the raw content to analyze.
			* If `'file'`, the sequence items must have a ‘read’ method (file-like object) that is called to fetch the bytes in memory.
			* If `'content'`, the input is expected to be a sequence of items that can be of type string or byte.
		* `enocding` (str) --  (`'utf-8'`); Specifies the encoding used to decode If bytes or files are given to analyze
		* `decode_error` (str) -- (`'strict'`); Instruction on what to do if a byte sequence is given to analyze that contains characters not of the given `encoding`.
		* `lowercase=` (bool) -- (`True`); Convert all characters to lowercase before tokenizing.
		* `ngram_range=` (tuple) -- Specifies the min and max n-gram values to use when calculating n-gram count
			* The lower and upper boundary of the range of n-values for different word n-grams or char n-grams to be extracted. All values of n such such that min_n <= n <= max_n will be used
		* `stop_words=` (list) -- (`None`); Removes the specified stop words from the text;
			* If a list, that list is assumed to contain stop words, all of which will be removed from the resulting tokens
			* If `'english'`, a built-in stop word list for English is used. There are several known issues with ‘english’ and you should consider an alternative
	* Methods
		* `fit_transform()` -- Learns the vocabulary dictionary and returns a matrix, where rows represent texts, and the columns display unique words from the corpus
			* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects.
		* `fit()` -- Learns a vocabulary dictionary of all tokens in the raw documents.
		* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects.
		* `get_feature_names_out()` -- Get output feature names for transformation.
			* `input_features=` (str); Not used, present for API consistency by convention.
	* Attributes
		* `shape` -- Returns the shape of the model
```Python
# Creating a bag-of-words

# Import Class
from sklearn.feature_extraction.text import CountVectorizer

# Create an instance of the class
count_vect = CountVectorizer()

# Fit the model to the dataset
bow = count_vect.fit_transform(corpus)

# Get list of features
count_vect.get_feature_names()
```

```Python
# Calculating n-grams

# Import Class
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer

data = pd.read_csv('/datasets/imdb_reviews_small_lemm.tsv', sep='\t')

# The corpus 
corpus = data['review_lemm']

# Create an instance of the class & specify the max and min ngram_range
count_vect = CountVectorizer(ngram_range=(2,2))
n_gram = count_vect.fit_transform(corpus)

print('The size of 2-gram:', n_gram.shape)
```


##### `sklearn.feature_extraction.text.TfidfVectorizer()`
* Convert a collection of raw documents to a matrix of TF-IDF features.
	* Parameters (see complete parameters in [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html))
		* `input` (str) -- (`'content'`); 
			* If `'filename'`, the sequence passed as an argument to fit is expected to be a list of filenames that need reading to fetch the raw content to analyze.
			* If `'file'`, the sequence items must have a ‘read’ method (file-like object) that is called to fetch the bytes in memory.
			* If `'content'`, the input is expected to be a sequence of items that can be of type string or byte.
		* `enocding` (str) --  (`'utf-8'`); Specifies the encoding used to decode If bytes or files are given to analyze
		* `decode_error` (str) -- (`'strict'`); Instruction on what to do if a byte sequence is given to analyze that contains characters not of the given `encoding`.
		* `lowercase=` (bool) -- (`True`); Convert all characters to lowercase before tokenizing.
		* `ngram_range=` (tuple) -- Specifies the min and max n-gram values to use when calculating n-gram count
			* The lower and upper boundary of the range of n-values for different word n-grams or char n-grams to be extracted. All values of n such such that min_n <= n <= max_n will be used
		* `stop_words=` (list) -- (`None`); Removes the specified stop words from the text;
			* If a list, that list is assumed to contain stop words, all of which will be removed from the resulting tokens
			* If `'english'`, a built-in stop word list for English is used. There are several known issues with ‘english’ and you should consider an alternative
	* Methods
		* `fit_transform()` -- Learns the vocabulary dictionary and returns a matrix, where rows represent texts, and the columns display unique words from the corpus
			* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects
		* `fit()` -- Learns the vocabulary and idf from training set.
			* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects
		* `get_feature_names_out()` -- Get output feature names for transformation.
			* `input_features=` (str); Not used, present for API consistency by convention.
	* Attributes
		* `shape` -- Returns the shape of the model
```Python
# Full Example

# Import libraries
import pandas as pd
from nltk.corpus import stopwords as nltk_stopwords
from sklearn.feature_extraction.text import TfidfVectorizer

# Load data
data = pd.read_csv('/datasets/imdb_reviews_small_lemm.tsv', sep='\t')

# Define corpus
corpus = data['review_lemm']

# Define stop words
stop_words = set(nltk_stopwords.words('english'))

# Create instance
count_tf_idf = TfidfVectorizer(stop_words=stop_words)

# Fit the counter instance
tf_idf = count_tf_idf.fit_transform(corpus)

print('The TF-IDF matrix size:', tf_idf.shape) # The TF-IDF matrix size: (4541, 26098)
```

## Unsupervised Learning (Clustering)
##### `sklearn.cluster.KMeans()`
* A class for performing K-Means clustering
	* Parameters
		* `n_clusters=` (int) -- (`8`); The number of clusters to form as well as the number of centroids to generate.
		* `init=` (str or callable array) -- (`'k-means++'`); Method for initialization:
			* `‘k-means++’` -- selects initial cluster centroids using sampling based on an empirical probability distribution of the points’ contribution to the overall inertia.
			* `‘random’` -- choose `n_clusters` observations (rows) at random from data for the initial centroids.
			* If an array is passed, it should be of shape (n_clusters, n_features) and gives the initial centers.
		* `n_init=` (str/int) -- (`'auto'`); Number of times the k-means algorithm is run with different centroid seeds. The final results is the best output of `n_init` consecutive runs in terms of inertia.
		* `max_iter=` (int) -- (`300`); Maximum number of iterations of the k-means algorithm for a single run.
		* `tol=` (float) -- (`1e-4`); Relative tolerance with regards to Frobenius norm of the difference in the cluster centers of two consecutive iterations to declare convergence.
		* `random_state=` (int) -- (`None`); Determines random number generation for centroid initialization. Use an int to make the randomness deterministic.
		* `verbose=` (int) -- (`0`); Verbosity mode
		* `algorithm=` (str) -- (`'lloyd'`); Sets the K-means algorithm to use.
			* `'elkan'`
			* `'lloyd'`
	* Attributes:
		* `cluster_centers_` -- Coordinates of cluster centers.
		* `labels_` -- Labels of each point
		* `inertia_` -- Sum of squared distances of samples to their closest cluster center, weighted by the sample weights if provided.
		* `n_iter_` -- Number of iterations run.
		* `n_features_in_` -- Number of features seen during fit.
		* `feature_names_in_` -- Names of features seen during fit. Defined only when X has feature names that are all strings.

```Python
import pandas as pd
import numpy as np
from sklearn.cluster import KMeans

data = pd.read_csv('/datasets/segments.csv')
centers = np.array([[20, 80, 8], [50, 20, 5], [20, 30, 10]])

model = KMeans(n_clusters=3, random_state=12345)
model.fit(data)

print('Cluster centroids:')
print(model.cluster_centers_)

# Training a model with initial centroids
model = KMeans(n_clusters=3, random_state=12345, init=centers)
model.fit(data)

print('Cluster centroids of the model with initial centroids:')
print(model.cluster_centers_)
```

```
Cluster centroids:
[[40.14472236 15.00741697  8.56      ]
 [10.90357994 29.90244865 15.096     ]
 [10.68632155 98.90275017 10.856     ]]
 
Cluster centroids of the model with initial centroids:
[[10.68632155 98.90275017 10.856     ]
 [50.06201472 19.62701512  1.808     ]
 [20.56550497 20.14513373 15.204     ]]
```

##### `sklearn.ensemble.IsolationForest()`
* A class to create Isolation Forest Algorithm.
* Returns the anomaly score of each sample using the IsolationForest algorithm
	* Parameters (see complete list of parameters [here](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.IsolationForest.html))
		* `n_estimators=` (int) -- The number of base estimators in the ensemble.
		* `max_samples=` (str) -- The number of samples to draw from `X` to train each base estimator.
			* If int, then draw `max_samples` samples.
			* If float, then draw `max_samples * X.shape[0]` samples.
			* If `“auto”`, then `max_samples=min(256, n_samples)`.
		* `verbose=` (int) -- (`0`); Controls the verbosity of the tree building process.
		* `random_state=` (int); (`None`); Controls the pseudo-randomness of the selection of the feature and split values for each branching step and each tree in the forest.
	* Methods
		* `decision_function()` -- Returns average anomaly score of X of the base classifiers.
			* `X` -- The input samples
		* `fit()` -- Perform fit estimator
			* `X` -- The input samples
		* `fit_predict()` -- Perform fit on X and returns labels for X.
			* `X` -- The input samples
		* `predict()` -- Predicts if a particular sample is an outlier or not.
			* `X` -- The input samples

```python
# Performing Isolation Forest Algorithm

# Import the class
from sklearn.ensemble import IsolationForest

# Create the model
isolation_forest = IsolationForest(n_estimators=100)

# Reshape the data
sales = df['Sales'].values.reshape(-1, 1)

# Select features to be checked for anomalies
data = df[['Sales', 'Profit']]

# Train the data
isolation_forest.fit(data)

# Get anomaly scores
anomaly_scores = isolation_forest.decision_function(data)

# Determine if features are anomalies or not
estimator = isolation_forest.predict(data)

# fit_predict() can be used if anomaly estimates aren't necessary
# estimator = isolation_forest.fit_predict(data)
```

```Python
# Performing Isolation Forest Algorithm

import pandas as pd
from sklearn.ensemble import IsolationForest

df = pd.read_csv('/datasets/sales.csv')

isolation_forest = IsolationForest(n_estimators=100)
data = df[['Sales', 'Profit']]
estimator = isolation_forest.fit_predict(data)

outliers = []
for e in estimator:
    if e == -1:
        outliers.append(e)

print('Number of anomalies: ', len(outliers))
# Number of anomalies:  1029
```

# Methods
