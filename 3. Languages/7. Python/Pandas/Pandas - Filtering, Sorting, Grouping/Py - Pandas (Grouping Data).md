See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Processing Missing Values)]], [[Py - Pandas (Processing Duplicate Values)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Grouping Data
* Grouping helps provide us with a more detailed look at the data before moving on to searching for the dependencies and similarities between different groups.

#### When to Group?
* Grouping is justified when the data falls logically into groups based on certain features, and when the groups are relevant to the task at hand.
#### Stages of Grouping
1) Split: Splitting the data into groups by a given condition
2) Apply: Apply data aggregating techniques to each group
3) Combine: Store the different results stored

---
#### Understanding Grouping in Pandas
* The `DataFrameGroubBy` object (results from grouping) is part of a data processing framework called split-apply-combine:
	1. split the data into groups
	2. apply a statistical aggregation function to each group
	3. combine the results for each group
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')
df.dropna(inplace=True)

grp = df.groupby(['platform', 'genre']) # Split the data into groups
mean_scores = grp['critic_score'].mean() # Apply a fn & Combine the results
```

#### Using `groupby()` to Group in Pandas
* `groupby()` --> takes in the name of column(s) that should be grouped and returns an object (Series) of the `DataFrameGroupBy` class
	* Changes the row index of the data to the keys being grouped
	* Can be used to group by multiple columns
		* Multiple Grouping Result is a multi-index Series with 2+ index values for each resulting value
	* Arguments
		* `column` -> a string or list of strings that specify the column(s) to group data by

* Example: Single Grouping 
```Python
import pandas as pd
exoplanet = pd.read_csv("/datasets/exoplanets.csv")

# Creating a new DataFrame grouped by the 'discovered' col & counting the values
exoplanet.groupby('discovered').count()

# Creating a new DataFrame grouped by the 'discovered' col & counting the values for the 'radius' col ONLY
exo_number = exoplanet.groupby('discovered')['radius'].count()

# Creating a new DataFrame grouped by the 'discovered' col & summing the values for the 'radius' col ONLY
exo_radius_sum = exoplanet.groupby('discovered')['radius'].sum()

# Finding the average 
exo_radius_mean = exo_radius_sum / exo_number
```

* Example: Multiple Grouping 
```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df.dropna(inplace=True)

grp = df.groupby(['platform', 'genre'])
print(grp['critic_score'].mean())
```

#### Using `agg()` to Perform Multiple Functions to a Group in Pandas
* `agg()` -> uses a dictionary as input where the keys are column names & values are the aggregate function to be applied
	* Arguments
		* `dict` -> a dictionary of key-value pairs (key = column, value = aggregate fn)
* Example
```Python
import pandas as pd
df = pd.read_csv('/stats/vg_sales.csv')
df.dropna(inplace=True)

# Creating a dict (key = col names, values = aggregate fns)
agg_dict = {'critic_score': 'mean', 'jp_sales': 'sum'}

# Grouping by two platform and genre & calling agg fn to apply diff aggregate fns
grp = df.groupby(['platform', 'genre']).agg(agg_dict)
```

* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

df['total_sales'] = df['na_sales'] + df['eu_sales'] + df['jp_sales']
grp = df.groupby('genre')
agg_dict = {
    'total_sales': 'sum',
    'na_sales': 'mean',
    'eu_sales': 'mean',
    'jp_sales': 'mean'
}

genre = grp.agg(agg_dict)
```