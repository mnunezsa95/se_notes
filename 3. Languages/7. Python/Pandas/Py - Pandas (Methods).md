See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Installing & Importing Pandas)]]
* [[Py - Pandas (DataFrame Object)]]
* [[Py - Pandas (Series Object)]]
* [[Py - NumPy (Methods)]]
* [[Py - Matplotlib (Methods)]]
* [[Py - SciPy (Methods)]]
Resources:
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)

---

# Pandas Attributes
##### `df.shape`
* Returns a tuple representing the dimensionality of the DataFrame.
```Python
df = pd.DataFrame({'col1': [1, 2], 'col2': [3, 4]})
print(df.shape) # (2, 2)
```

##### `df.values`
* Returns a Numpy representation of the DataFrame (as an array/vector)
```Python
import pandas as pd

df = pd.DataFrame({'a': [120, 60, 75], 'b': [42, 50, 90]})
matrix = df.values
```


# Pandas Methods

##### `df.idxmin()`
* Returns the index of first occurrence of minimum over requested axis.
	* Arguments
		* `axis=` -- (default is `0`); the axis to use (`0` or `'index'` for row-wise, `1` or `'columns'` for column-wise)
		* `skipna=` -- (default is `True`); Exclude NA/null values. If an entire row/column is NA, the result will be NA.
		* `numeric_only=` -- (default is `False`); include only float, int or boolean data.
```Python
deliveries_in_week_df = pd.DataFrame(
    {'Distance': deliveries_in_week}, index=town
)

print('Warehouse town:', deliveries_in_week_df['Distance'].idxmin())
```

##### `df.plot()` 
* Creates a figure where all of the numeric columns in a DataFrame are plotted on the same axes
* Arguments
	* `title=` -> string to specify the title name
	* `style=` -> a string specifying the style of the plot marker; see options [here](https://matplotlib.org/stable/api/markers_api.html)
	* `x=` -> a string specifying the data to plot on x-axis
	* `y=` -> a string specifying the data to plot on y-axis
	* `xlabel=` -> a string specifying the label of the x-axis
	* `ylabel=` -> a string specifying the label of the y-axis
	* `legend=` -> a boolean to display the legend or not (`True` by default)
	* `xlim=` -> a number or list of two numbers specifying either the max (or min and max) value(s) to display on x-axis
	* `ylim=` -> a number or list of two numbers specifying either the max (or min and max) value(s) to display on y-axis
	* `grid=` -> a boolean that specifies whether to add grid-lines to the plot (`False` by default)
	* `figsize=` -> a list specifying the `[width and height]` of the figure
	* `color=` -> a string to specify the marker color
* Example
```Python
import pandas as pd
from matplotlib import pyplot as plt

df = pd.DataFrame({'a':[2, 3, 4, 5], 'b':[4, 9, 16, 25]})

df.plot(
    title='A vs C',
    x="c",
    y="a",
    style="*",
    color="hotpink",
    figsize=[5, 5],
    xlim=[0, 12],
    ylim=[1, 6],
    xlabel="C",
    ylabel="A"
    grid=True
    legend=False
)
plt.show()
```


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