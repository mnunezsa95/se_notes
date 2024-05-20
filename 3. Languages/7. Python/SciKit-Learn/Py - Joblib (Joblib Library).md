See:
* [[Py - Introduction to Python]]
* [[Py - Sklearn (SciKit Learn Library)]]
Resources
* Documentation: [Joblib](https://joblib.readthedocs.io/en/stable/)

---
# Joblib Library

### What is the joblib Library?
* Joblib -- a set of tools to provide **lightweight pipelining in Python**

## Working with joblib
#### `dump()`
* Saves an arbitrary Python object into one file
	* Arguments
		1) `value` -- the python object to store to disk (can be a model)
		2) `filename` -- a string specifying the file object or path of the file in which it is to be stored
```Python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from joblib import dump

df = pd.read_csv('/datasets/train_data_us.csv')

df.loc[df['last_price'] > 113000, 'price_class'] = 1
df.loc[df['last_price'] <= 113000, 'price_class'] = 0

features = df.drop(['last_price', 'price_class'], axis=1)
target = df['price_class']

model = DecisionTreeClassifier(random_state=12345, max_depth=3)
model.fit(features, target)

# Saving the model 
dump(model, 'model.joblib')
```

#### `load()`
* Reconstructs (or loads) a Python object from a file saved with `joblib.dump()`
	* Arguments
		1) `filename` -- a string specifying the file object or path of the file to be loaded
```Python
import joblib

# Loading the model in the `model.joblib` file to the model variable
model = joblib.load('model.joblib')
```