See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Processing Missing Values)]], [[Py - Pandas (Processing Duplicate Values)]], [[Py - Pandas (Grouping Data)]], [[Py - Pandas (Sorting Data)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### Statistical Methods in Pandas
* Pandas has methods for working with data and getting statistical analysis such as `min()`, `max()`, `mean()`, `median()`
	* See documentation for methods
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log_upd_en.csv')

df['total_play_seconds'].max() # finding the maximum value in the 'total_play_seconds' column

df_drop_skip = df[df['total_play_seconds'] > 30] df_drop_skip['total_play_seconds'].min() # finding the minimum value that is greater than 30

df_drop_skip['total_play_seconds'].mean() # finding the mean of the 'total_play_seconds' that is larger than 30

df_stat['total_play_seconds'].median() # finding the median of the 'total_play_seconds' column 
```

#### The `info()` Method
* Prints out general information about the DataFrame; information cannot be accessed directly because this method does not return anything
	* Number of rows (`RangeIndex: x entries`)
	* Number of columns (`total x columns`)
	* The name of each column (`Column`)
	* Number of values in each column that are not missing (`Non-Null Count`)
	* The data type of each column (`Dtype`)
```python
data = pd.read_csv('/datasets/gpp_modified.csv') 
data.info()
n_rows, n_cols = data.shape # unpacking the values returned by the shape attribute
```

#### The `describe()` Method
* `describe()` -> can be called on a Series or DataFrame and returns a Series or DataFrame with summary statistics 
* Arguments:
	* `include=` -> accepts a string or list of strings that specifies the data type of the columns to be included in the result
		* `object` = columns with strings
		* `all`= will include all columns
* Only processes numeric columns, but can be called on a Series that isn’t numeric.
* Provides the following:
	* `count`
	* `max`
	* `min`
	* `mean`
	* `25%`: The first quartile 
	* `50%`: The second quartile (median)
	* `75%`: The third quartile 
	* `std` -> (standard deviation) & quartiles
```python
# Calling the describe() method on a Series
import pandas as pd
df = pd.read_csv('/datasets/music_log_upd_en.csv')
df_drop_skip = df[df['total_play_seconds'] > 30]

print(df_drop_skip.describe())
```
``
```
       total_play_seconds
count        24809.000000
mean           199.765577
std            128.989293
min             30.004000
25%            115.371000
50%            196.336000
75%            253.278912
max           4133.616327
```

* Example: Calling the `describe()` method on a non-numeric Series
	* `'count'`: The number of non-null values
	* `'unique'`: The number of unique values
	* `'top'`: The value that occurs most frequently (users of the app prefer pop the most!)
	* `'freq'`: The number of times the most frequent value occurs
```Python
# Calling the describe() method on a non-numeric Series
import pandas as pd
df = pd.read_csv('/datasets/music_log_upd_en.csv')
df_drop_skip = df[df['total_play_seconds'] > 30]

print(df_drop_skip['genre_name'].describe())
```

```
count     24809
unique     1354
top         Pop
freq       2620
Name: genre_name, dtype: object
```

```Python
# using the inlcude parameter in the describe method

data = pd.read_csv('/datasets/gpp_modified.csv', sep='|', header=None,             names=column_names, decimal=',')

data.describe(include='object')
```

#### `sample()`
* Works like `head()` and `tail()` but selects random rows from the DataFrame rather than consecutive rows from the beginning or end of the DataFrame.
	* Preserves the index values from the original DataFrame
* Arguments
	* `number` -> the number of samples to return from the DataFrame
	* `random_state=` -> sets the random_state of the method (useful for when you want to get the same result with every execution)
* Example
```python
data = pd.read_csv('/datasets/gpp_modified.csv') 
data.sample(5)
data.sample(5, random_state=1369)