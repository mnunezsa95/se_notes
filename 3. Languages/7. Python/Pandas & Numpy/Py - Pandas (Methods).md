See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Installing & Importing Pandas)]]
* [[Py - Pandas (DataFrame Object)]]
* [[Py - Pandas (Series Object)]]
Resources:
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

# Pandas Methods

##### `get_dummies()`
* Convert categorical variable into dummy/indicator variables
	* Arguments
		1) `data` -- Array, Series or DataFrame for the data of which to get dummy indicators
		2) `drop_first` -- boolean (`False` by default); specifies whether to drop the first dummy column created
```Python
import pandas as pd
data = pd.read_csv('/datasets/travel_insurance_us.csv')

data_ohe = pd.get_dummies(data, drop_first=True)
```

##### `map()`
* Maps (substitutes) each value in a Series with another value, that may be derived from a function, a `dict` or a `Series`.
	* Arguments
		1) `arg` -- the `dict` or `Series` to use for mapping
```Python
temperature_dict = {'cold': 0, 'warm': 1, 'hot': 2}

df['temperature'] = df['temperature'].map(temp_dict)
```

##### `value_counts()`
* Return a Series (in descending order) containing counts of unique values
	* `normalize=` -- (default is `False`); If `True` then the object returned will contain the relative frequencies of the unique values.
	* `sort=` -- (default is `True`); Sorts by frequency when `True`; preserves order when `False`
	* `ascending=` -- (default is `True`); sorts in ascending order
	* `bins=` -- Rather than counting values, groups them into half-open bins
	* `dropna` -- (default is `True`); specifies to include counts of `NaN`
```python
import pandas as pd

data = pd.read_csv('/datasets/travel_insurance_us_preprocessed.csv')

class_frequency = data['Claim'].value_counts(normalize=True)
print(class_frequency)

class_frequency.plot(kind='bar')
```

```Result
0    0.985136
1    0.014864
```

##### `pd.concat()`
* Concatenate pandas objects along a particular axis
	* Arguments
		1) `objs` -- a sequence or mapping of Series or DataFrame objects
		2) `axis=` -- (default is `0`); the axis to concatenate the string along 
			1) `0` or `index`
			2) `1` or `columns`
```Python
features_zeros = features[target == 0]
features_ones = features[target == 1]

# Duplicate and create new dataset
features_upsampled = pd.concat([features_zeros] + [features_ones] * repeat)
```

##### `sample()`
* Returns a random sample of items from an axis of object
	* Arguments
		* `n=` -- Number of items from axis to return. Cannot be used with `frac`
		* `frac=` -- Fraction of axis items to return. Cannot be used with `n`.
		* `replace` -- (default is `False`); allow or disallow sampling of the same row more than once
		* `random_state` -- Default it is `None`, which sets the pseudorandom to always be different; a different value can be used to specify the use of the same pseudorandom number
```Python
df.sample(frac=0.5, random_state=1)
```

##### `quantile()`
* Return values at the given quantile over requested axis
	* Arguments
		* `q=` -- (default is 0.50); a float or array-like value between 0 and 1 that specifies the quartile to compute
		* `axis=` -- (default is 0); specifies the axis to use
			* `0` -- index (row)
			* `1` -- columns
		* `numerical_only=` -- (default is `True`) ; boolean value to specify whether to include only float, int or boolean data