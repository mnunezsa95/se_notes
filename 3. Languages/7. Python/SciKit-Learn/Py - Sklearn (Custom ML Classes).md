See:
* [[Py - Introduction to Python]]
* [[ML - Machine Learning Basics]]
* [[Py - Sklearn (Models & Model Comparison)]]
* [[ML - Supervised Learning]]
* [[Py - Sklearn (SciKit Learn Library)]]
* [[Py - NumPy (Vectors)]]
* [[Py - Creating Classes in Python]]
Resources
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)

----
# ML Classes


## Creating a ML Class
To create a ML class:
1. Specify the `class` keyword, followed by the name of the class, using TitleCase
```Python
class ConstantRegression():
```

2. Write class methods:
	* ALWAYS specify the `self` parameter
```Python
# constant_regression.py

class ConstantRegression():
	# Method to fit the model
	def fit(self, features_train, target_train):
		self.mean = target_train.mean()
		
	# Method to predict with the model
	def predict(self, new_features):
        answer = pd.Series(self.mean, index=new_features.index)
        return answer
```

3. Use the class, as needed
```Python
import pandas as pd
from scipy.spatial import distance
from constant_regression import ConstantRegression

columns = ['bedrooms', 'total area', 'kitchen', 'living area', 'floor',
    'total floors','price']

df_train = pd.DataFrame(
    [
        [1, 38.5, 6.9, 18.9, 3, 5, 4200000],
        [1, 38.0, 8.5, 19.2, 9, 17, 3500000],
        ...,
        [3, 69.3, 8.5, 39.3, 4, 9, 11400000],
        [3, 89.8, 11.2, 58.2, 24, 25, 16300000],
    ],
    columns=columns,
)

train_features = df_train.drop('price', axis=1)
train_target = df_train['price']

df_test = pd.DataFrame(
    [
        [1, 36.5, 5.9, 17.9, 2, 7, 3900000],
        [2, 71.7, 12.2, 34.3, 5, 21, 7100000],
        [3, 88.0, 18.1, 58.2, 17, 17, 12100000],
    ],
    columns=columns,
)

test_features = df_test.drop('price', axis=1)

# Use the ML class
model = ConstantRegression()
model.fit(train_features, train_target)
test_predictions = model.predict(test_features)
print(test_predictions)
```

```Python
# Example -- Creating ML Class

import numpy as np
import pandas as pd
from scipy.spatial import distance

columns = ['bedrooms', 'total area', 'kitchen', 'living area', 'floor',
    'total floors','price']

df_train = pd.DataFrame(
    [
        [1.0, 38.5, 6.9, 18.9, 3.0, 5.0],
        [1.0, 38.0, 8.5, 19.2, 9.0, 17.0],
        ...,
        [3.0, 69.3, 8.5, 39.3, 4.0, 9.0],
        [3.0, 89.8, 11.2, 58.2, 24.0, 25.0],
    ],
    columns=columns,
)

train_features = df_train.drop('bedrooms', axis=1)
train_target = df_train['bedrooms']

df_test = pd.DataFrame(
    [
        [1, 36.5, 5.9, 17.9, 2, 7],
        [2, 71.7, 12.2, 34.3, 5, 21],
        [3, 88.0, 18.1, 58.2, 17, 17],
    ],
    columns=columns,
)

test_features = df_test.drop('bedrooms', axis=1)


def nearest_neighbor_predict(train_features, train_target, new_features):
    distances = []
    for i in range(train_features.shape[0]):
        vector = train_features.loc[i].values
        distances.append(distance.euclidean(new_features, vector))
    best_index = np.array(distances).argmin()
    return train_target.loc[best_index]


class NearestNeighborClassifier():
	# Method to fit the model
    def fit(self, features_train, target_train):
        self.features_train = features_train
        self.target_train = target_train
    # Method to predict with the model    
    def predict(self, new_features):
        values = []
        for i in range(new_features.shape[0]):
            vector = new_features.loc[i]
            values.append(nearest_neighbor_predict(
                    self.features_train, self.target_train, vector
                )
            )
        return pd.Series(values)

model = NearestNeighborClassifier()
model.fit(train_features, train_target)
new_predictions = model.predict(test_features)
print(new_predictions)
```