See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], 
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Index vs Indexing 
- **Index**: A component of a Series or DataFrame, accessed using the `index` attribute
- **Indexing**: The process of accessing values in a Series or DataFrame using their indexes

#### The `index` Attribute
* Series and DataFrame objects in pandas always have indexes, which are stored in the `index` attribute
	* If the `index` is NOT defined when creating a DataFrame or Series, then its default `index` attribute is automatically created with default values
```Python
# Creating a Series without specifying the index

import pandas as pd

# Using the Series() class from pandas to create a Series object stored in the variable oceans using a list of ocean names
oceans = pd.Series(['Pacific', 'Atlantic', 'Indian', 'Southern', 'Arctic'])

print(oceans.index) # RangeIndex(start=0, stop=5, step=1)
print(type(oceans.index)) # <class 'pandas.core.indexes.range.RangeIndex'>
```

#### Setting the Index Values
* There are two ways to set the index values
	1. Pass the index values to the `index=` parameter when creating a DataFrame or Series
	2. Assign the index values to the `index` attribute of an existing DataFrame or Series

```Python
# Creating a Series and specifying the index after creation

import pandas as pd

# Using the Series() class from pandas to create a Series object stored in the variable oceans using a list of ocean names
oceans = pd.Series(['Pacific', 'Atlantic', 'Indian', 'Southern', 'Arctic'])
oceans.index = [1, 2, 3, 4, 5] # specifying the index after creation

print(oceans.index) # Int64Index([1, 2, 3, 4, 5], dtype='int64')
print(type(oceans.index)) # <class 'pandas.core.indexes.numeric.Int64Index'>
```

```Python
# Creating a Series and specifying the index at the point of creation
import pandas as pd 

# Using the Series() class from pandas to create a Series object stored in the variable oceans using a list of ocean names
# Specifying the index at creation using index= keyword argument
oceans = pd.Series(
	['Pacific', 'Atlantic', 'Indian', 'Southern', 'Arctic'], 
	index=[1, 2, 3, 4, 5]
)

print(oceans.index) # Int64Index([1, 2, 3, 4, 5], dtype='int64')
print(type(oceans.index)) # <class 'pandas.core.indexes.numeric.Int64Index'>
```

```Python
# Creating a Series and speciyfing string indices at point of creation

import pandas as pd

oceans = pd.Series(
	['Pacific', 'Atlantic', 'Indian', 'Southern', 'Arctic'],
	index=['A', 'B', 'C', 'D', 'E']
)

print(oceans.index) # Index(['A', 'B', 'C', 'D', 'E'], dtype='object')
print(type(oceans.index)) # <class 'pandas.core.indexes.base.Index'>
```

#### Indexing: `loc[]` vs `iloc[]`
* `loc[]` uses the index_value and col_name to retrieve elements from a DataFrame
	* Does not use 0-based indexing
* `iloc[]` uses the the index_value and col_name as **integers** to retrieve elements from a DataFrame
	* Uses 0-based indexing
#### Indexing using `loc[]`
* The `loc[]` attribute can be used to access DataFrame elements using the following syntax
```Python
# loc[] syntax
df.loc[index_value, col_name]
```
* Example
```Python
import pandas as pd

states  = ['Alabama', 'Alaska', 'Arizona', 'Arkansas']
flowers = ['Camellia', 'Forget-me-not', 'Saguaro cactus blossom', 
	'Apple blossom']
insects = ['Monarch butterfly', 'Four-spotted skimmer dragonfly', 
	'Two-tailed swallowtail', 'European honey bee']
index   = ['state 1', 'state 2', 'state 3', 'state 4']

df = pd.DataFrame({
	'state': states, 
	'flower': flowers, 
	'insect': insects
	},
	index=index
)

print(df.loc['state 4', 'insect']) # European honey bee
```

![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Untitled_17_1656572005.png)


#### Indexing using `iloc[]`
* Uses numerical integers to designate and access positions of the elements
	* `iloc[]` uses normal Python 0-indexing
* Example
```python
import pandas as pd

states  = ['Alabama', 'Alaska', 'Arizona', 'Arkansas']
flowers = ['Camellia', 'Forget-me-not', 'Saguaro cactus blossom', 
	'Apple blossom']
insects = ['Monarch butterfly', 'Four-spotted skimmer dragonfly', 
	'Two-tailed swallowtail', 'European honey bee']
index   = ['state 1', 'state 2', 'state 3', 'state 4']

df = pd.DataFrame({
	'state': states, 
	'flower': flowers, 
	'insect': insects
	},
	index=index
)

print(df.iloc[3, 2]) # European honey bee
print(df.iloc[[0, 2], 1:]) # see result below
print(df.iloc[1:, -1]) # see result 2 below
```

```
                         flower                  insect
state 1                Camellia       Monarch butterfly
state 3  Saguaro cactus blossom  Two-tailed swallowtail
```

```
state 2    Four-spotted skimmer dragonfly
state 3            Two-tailed swallowtail
state 4                European honey bee
Name: insect, dtype: object
```

#### Changing a DataFrame Index
* `set_index()` -> Takes an existing column as an argument and replaces the index with the values of the specified column
	* This will include the name on the index. 
* Example
```Python
import pandas as pd

states  = ['Alabama', 'Alaska', 'Arizona', 'Arkansas']
flowers = ['Camellia', 'Forget-me-not', 'Saguaro cactus blossom', 
	'Apple blossom']
insects = ['Monarch butterfly', 'Four-spotted skimmer dragonfly', 
	'Two-tailed swallowtail', 'European honey bee']
index = ['state 1', 'state 2', 'state 3', 'state 4']

df = pd.DataFrame({
	'state': states, 
	'flower': flowers, 
	'insect': insects
	},
	index=index
)

df = df.set_index('state')
print(df) # see below
print(df.index) # Index(['Alabama', 'Alaska', 'Arizona', 'Arkansas'], dtype='object', name='state')

df.index.name = None 
print(df) # see 2 below
```

```
                          flower                          insect
state                                                           
Alabama                 Camellia               Monarch butterfly
Alaska             Forget-me-not  Four-spotted skimmer dragonfly
Arizona   Saguaro cactus blossom          Two-tailed swallowtail
Arkansas           Apple blossom              European honey bee
```

```
                          flower                          insect
Alabama                 Camellia               Monarch butterfly
Alaska             Forget-me-not  Four-spotted skimmer dragonfly
Arizona   Saguaro cactus blossom          Two-tailed swallowtail
Arkansas           Apple blossom              European honey bee
```