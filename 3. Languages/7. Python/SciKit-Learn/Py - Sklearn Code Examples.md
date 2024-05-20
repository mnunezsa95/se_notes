See:
* [[Py - Introduction to Python]]
* [[Py - Sklearn (SciKit Learn Library)]]
* [[Py - Sklearn (Models & Model Comparison)]]
* [[ML - Supervised Learning]]
* [[ML - Machine Learning Basics]]
Resources:
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)

---
# Examples

#### Feature Encoding, Data Splitting & Feature Scaling
```Python

import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

data = pd.read_csv('travel_insurance_us.csv')

data_ohe = pd.get_dummies(data, drop_first=True)
target = data_ohe['Claim']
features = data_ohe.drop('Claim', axis=1)

features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

numeric = ['Duration', 'Net Sales', 'Commission (in value)', 'Age']

scaler = StandardScaler()
scaler.fit(features_train[numeric])
features_train[numeric] = scaler.transform(features_train[numeric])
features_valid[numeric] = scaler.transform(features_valid[numeric])

print(features_train.shape)
```

#### Sanity Checking Accuracy
```Python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split

data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

target = data['Claim']
features = data.drop('Claim', axis=1)

features_train, features_valid, target_train, target_valid = train_test_split(features, target, test_size=0.25, random_state=12345)

model = DecisionTreeClassifier(random_state=12345)
model.fit(features_train, target_train)

predicted_valid = pd.Series(model.predict(features_valid))
class_frequency = predicted_valid.value_counts(normalize=True)

print(class_frequency)
class_frequency.plot(kind='bar')
```