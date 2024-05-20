See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], 
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Creating New Columns Based on Values in Other Columns
Column Transforms using Arithmetic Operators
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

# Creating a new col and adding the three sales columns
df['total_sales'] = df['na_sales'] + df['eu_sales'] + df['jp_sales']

# Creating a new col and adding the share of total sales from the EU
df['eu_sales_share'] = df['eu_sales'] / df['total_sales']
```

```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')
df['average_score'] = (df['user_score'] * 10 + df['critic_score']) / 2
print(df['average_score'].head())
```

Generating Boolean Columns
* `Boolean` columns can be created using comparison operators (`==`, `<`, `>=`)
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

# Creating a new col and adding True or False, based on condition
df['is_nintendo'] = df['publisher'] == 'Nintendo'
```

---
# Category Columns

#### Designating Categorical Column
* If a string column is categorical, they should be treated as such by adding the `categorical` data type
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

# Casting the entire platform column as `categorical` data type
df['platform'] = df['platform'].astype('category')
```

#### Creating Category Columns with `apply()`
* Python functions can be created to help categorize data 
```Python
def era_group(year):
    """ 
    The function returns the era group for games according to the year of
    release, using the following rules:
      —'retro'   for year < 2000
      —'modern'  for 2000 <= year < 2010
      —'recent'  for year >= 2010
      —'unknown' for missing year values (NaN)
    """
    if year < 2000:
      return 'retro'
    elif year < 2010:
      return 'modern'
    elif year >= 2010:
      return 'recent'
    else:
      return 'unknown'
```
* `apply()` --> takes values from a DataFrame column and applies a function to each value in the column
	* Arguments
		* `function` -> the function to be applied
		* `axis=` -> specifies if the `function` argument should take in column or row values 
			* `0`  -> Columns (default)
			* `1` -> Rows 
	* Example
```Python
import pandas as pd
import numpy as np
df = pd.read_csv('vg_sales.csv')

# Creating a new col 'era_group' and setting it equal to the era_group function applied to each value of the 'year_of_release' col
df['era_group'] = df['year_of_release'].apply(era_group)
```

* Example: Using `apply()`
```Python
import pandas as pd
import numpy as np

df = pd.read_csv('/datasets/vg_sales.csv')

def score_group(score):
    if score < 60:
        return 'low'
    elif score < 80:
        return 'medium'
    elif score >= 80:
        return 'high'
    else:
        return 'no score'

df['score_group'] = df['critic_score'].apply(score_group)

print(df.groupby('score_group')['na_sales'].sum())
```

#### Creating Categories with Row Functions
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

# Dropping rows with missing values
df.dropna(inplace=True)

# Defining the Row function
def era_sales_group(row):
    """
    The function returns a category for games according to the year of release 
    and total sales, using the following rules:
      —'retro'   for year < 2000 and total sales < $1 million
      —'modern'  for 2000 <= year < 2010 and total sales < $1 million
      —'recent'  for year >= 2010 and total sales < $1 million
      —'classic' for year < 2010 and total sales >= $1 million
      —'big hit' for year >= 2010 and total sales >= $1 million
    """
    # Defining variables based on input
    year = row['year_of_release']
    na_sales = row['na_sales']
    eu_sales = row['eu_sales']
    jp_sales = row['jp_sales']
    
    total_sales = na_sales + eu_sales + jp_sales
    
    # Making conditionals based on variables
    if year < 2000:
        if total_sales < 1:
            return 'retro'
        else:
            return 'classic'
    if year < 2010:
        if total_sales < 1:
            return 'modern'
        else:
            return 'classic'
    if year >= 2010:
        if total_sales < 1:
            return 'recent'
        else:
            return 'big hit'

# Using the function based on rows
df['game_category'] = df.apply(era_sales_group, axis=1)

# Seeing our results
print(df['game_category'].value_counts())
```

```Python
# Testing the row function with a made up row
cols = ['year_of_release', 'na_sales', 'eu_sales', 'jp_sales']

row_1 = pd.Series([1989, 0, 0, 0.6], index=cols) # expect 'retro'
row_2 = pd.Series([1989, 1, 2, 0], index=cols)   # expect 'classic'
row_3 = pd.Series([2006, 0.3, 0, 0], index=cols) # expect 'modern'
row_4 = pd.Series([2020, 0, 0.4, 0], index=cols) # expect 'recent'
row_5 = pd.Series([2020, 1, 1, 1], index=cols)   # expect 'big hit'

rows = [row_1, row_2, row_3, row_4, row_5]

for row in rows:
    print(era_sales_group(row))
```

* Example
```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

df.dropna(inplace=True)

def avg_score_group(row):
    critic_score = row['critic_score']
    user_score = row['user_score']
    avg_score = (critic_score + user_score * 10) / 2
    
    if avg_score < 60:
        return 'low'
    if avg_score < 80:
        return 'medium'
    if avg_score >= 80:
        return 'high'

# create the test input rows here
row_1 = pd.Series([66, 3.6], index=["critic_score", "user_score"])
row_2 = pd.Series([72, 8.1], index=["critic_score", "user_score"])
row_3 = pd.Series([99, 9.4], index=["critic_score", "user_score"])
   
# print results of calling the function with the test inputs in order
print(avg_score_group(row_1))
print(avg_score_group(row_2))
print(avg_score_group(row_3))

# applying the function
df['score_group'] = df.apply(avg_score_group, axis=1)
```