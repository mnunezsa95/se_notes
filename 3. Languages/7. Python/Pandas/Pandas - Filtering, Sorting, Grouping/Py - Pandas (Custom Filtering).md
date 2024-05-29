See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], 
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

----
# Custom Filtering (Single Conditions)

#### Custom Filtering using `DataFrame.query()`
* `DataFrame.query()` -> expects a string as an input to filter data
* Arguments 
	* `query` -> a string to represent how to filter data
		* When using external variables in a `query`, they MUST be prefaced with the `@` to prevent the query from treating it as a column
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

# Filtering where jp_sales are greater than 1, and returning the 'name' and 'jp_sales' columns
df.query("jp_sales > 1")[['name', 'jp_sales']]

# Filtering where only where the publisher column is equal to Nintendo and returning the 'name' and 'publisher columns'
df.query("publisher == 'Nintendo'")[['name', 'publisher']].head()
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

handhelds = ['3DS', 'DS', 'GB', 'GBA', 'PSP']

# Chcking if the value of 'platform' is in the handhelds array and returning the 'name' and 'platform' values only
df.query("platform in @handhelds")[['name', 'platform']]
```

#### Custom Filtering using `DataFrame.isin()`
* `isin()` -> Checks if values in a column match any of the values in another array such as a list or dictionary
* Arguments
	* `array` -> a list or dictionary that the will be checked 
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

handhelds = ['3DS', 'DS', 'GB', 'GBA', 'PSP']

# Checking if the value for 'platform' is in the handheld array and returning the name and platform columsn only
df[df['platform'].isin(handhelds)][['name', 'platform']]
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

cols = ['name', 'genre']
s_genres = ['Shooter', 'Simulation', 'Sports', 'Strategy']

# Using the isin() method with the given list s_genres to filter through the data, retaining only the rows where the game genre doesn't commence with the letter "S" and returning the values for 'genre' and 'name' only
df_filtered = df[~df['genre'].isin(s_genres)][cols]

print(df_filtered)
```

#### Using External List to Filter DataFrames
```Python
import pandas as pd

our_list = [2, 5, 10]
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)
print(df)
print(our_list) # [2, 5, 10]
print(df.query("a in @our_list")) # See result below
```

```Result
    a  b  c
0   2  5  X
2  10  3  Y
```

#### Using External Dictionary to Filter DataFrames
* Checking for the presence of specific values from a specific column among a dictionary
```Python
import pandas as pd

our_dict = {0: 10, 3: 11, 12: 12}
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)

print(our_dict) # {0: 10, 3: 11, 12: 12}

# Checking for the presence of values from column 'a' among the dictionary values in the 'our_dict'
print(df.query("a in @our_dict.values()")) # See results below
```

```
    a  b  c
2  10  3  Y
3  11  2  Y
4  12  1  Z
```

* Checking for the presence of specific keys from a specific column among a dictionary
```Python
import pandas as pd

our_dict = {0: 10, 3: 11, 12: 12}
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)

print(our_dict) # {0: 10, 3: 11, 12: 12}
print(df.query("a in @our_dict.keys()"))
```

#### Using External Series to Filter DataFrames
* Series objects store info as index-value pairs. 
	* Values are checked by default
	* Checking for index can be done by using the `index` attribute
```Python
import pandas as pd

our_series = pd.Series([10, 11, 12])
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)
print(our_series) # see result below
print(df.query("a in @our_series")) # see result 2 below
print(df.query("c in @our_series.index")) 
```

```Result
0    10
1    11
2    12
```

```Result 
    a  b  c
2  10  3  Y
3  11  2  Y
4  12  1  Z
```

```Result
    a  b  c
0   2  5  X
1   3  4  Y
2  10  3  Y
3  11  2  Y
```

#### Using External DataFrame to Filter DataFrames
* An external DataFrame can be used to filter data in two ways:
	1. Filter using its `index` values
		* Uses the `index` attribute
	2. Filter using values in specific columns
		* Uses dot notation to specify the column

* Example: Filter using its `index` values
```Python
import pandas as pd

df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)

our_df = pd.DataFrame(
    {
        'a1': [2, 4, 6],
        'b1': [3, 2, 2],
        'c1': ['A', 'B', 'C'],
    },
    index=['Z', 'X', 'P']
)

print(df.query("c in @our_df.index")) # See results below
```

```Result
    a  b  c
0   2  5  X
4  12  1  Z
```

* Example: Filter using values in specific columns
```Python
import pandas as pd

df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)
our_df = pd.DataFrame(
    {
        'a1': [2, 4, 6],
        'b1': [3, 2, 2],
        'c1': ['A', 'B', 'C'],
    },
    index=['Z', 'X', 'P']
)

print(df.query('a in @our_df.b1')) # See results below
```

```Result
   a  b  c
0  2  5  X
1  3  4  Y
```


---
# Custom Filtering (Multiple Conditions)

#### Filtering Multiple Conditions using Bitwise Operators
* Pandas uses bitwise operators for filtering based on Multiple Conditions
	* `&` = and
	* `|` = or
	* `~` = not
		* Precedes the condition it negates
* Syntax for Filtering Multiple Conditions
	* Each individual condition MUST be separated by parentheses
```Python
new_df = df[(df['column_1'] <op> 'condition_1') <op> (...) <op> (...)]
```
* Examples
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

# Printing a new DataFrame's first five rows, where the platform is Wii and the genre is not in the sports genre
print(df[(df['platform'] == 'Wii') & ~(df['genre'] == 'Sports')].head())

# Printing a new DataFrame where the north america sales or europe or japan sales are larger than or equal to 1 million
print(df[(df['na_sales'] >= 1) | (df['eu_sales'] >= 1) | (df['jp_sales'] >= 1)])
```


#### Filtering Multiple Conditions using `query()`
* Since the query argument is a string, traditional python logical operators OR bitwise operators can be used
	* `&` = and
	* `|` = or
	* `~` = not`
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

# Querying where platform column is Wii and genre column is NOT sports
print(df.query("platform == 'Wii' and genre != 'Sports'").head())
```

```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

q_string = str('na_sales >= 1 or eu_sales >= 1 or jp_sales >= 1')

print(df.query(q_string).head())
```


#### Example From Exercise (2 Solutions)
Solution 1:
* Sold in all 3 regions (North America, Europe, and Japan)
- The Japanese sales were greater than the combined sales from North America and Europe
- The game developer is one of the companies in the `developers` list
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

developers = ['SquareSoft', 'Enix Corporation', 'Square Enix']
cols = ['name', 'developer', 'na_sales', 'eu_sales', 'jp_sales']

# Creating a DataFrame and filtering the values of the developer column for values found in the developers list. 
df_filtered = df[df['developer'].isin(developers)] 

# Filtering the new DataFrame where sales for all three regions are NOT zero
df_filtered = df_filtered[(df_filtered['na_sales'] != 0) & (df_filtered['eu_sales'] != 0) & (df_filtered['jp_sales'] != 0)] 

# Fitering the new DataFrame where sales in japan were higher than sales in north america and europe combined
df_filtered = df_filtered[df_filtered['jp_sales'] > (df_filtered['na_sales'] + df_filtered['eu_sales'])]  

# Printing specific columns
df_filtered = df_filtered[cols]

print(df_filtered)
```

Solution 2:
* Sold in all 3 regions (North America, Europe, and Japan)
- The Japanese sales were greater than the combined sales from North America and Europe
- The game developer is one of the companies in the `developers` list
```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

developers = ['SquareSoft', 'Enix Corporation', 'Square Enix']
cols = ['name', 'developer', 'na_sales', 'eu_sales', 'jp_sales']

df_filtered = df[(df['na_sales'] != 0) & 
                 (df['eu_sales'] != 0) & 
                 (df['jp_sales'] != 0) & 
                 (df['jp_sales'] > (df['na_sales'] + df['eu_sales'])) & 
                 (df['developer'].isin(developers))]

# Select specified columns
df_filtered = df_filtered[cols]

print(df_filtered)
```

#### Replacing Values Using `where()`
* `where()` -> checks the condition, passed as an argument, for each value in the column. 
	* If the condition is true, `where()` does nothing
	* if the condition is false, `where()` replaces the current value with the new one.
* Arguments
	* `condition` -> a logical condition
	* `new_value` -> a new value to replace in the column for which the condition is false
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

df['platform'] = df['platform'].where(df['platform'] != 'NES', 'Nintendo Entertainment System')

print(df.iloc[:, :2].head())
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

df[['na_sales', 'eu_sales']] = df[['na_sales', 'eu_sales']].where((df['na_sales'] > 0) | (df['eu_sales'] > 0), None)

print(df[['name', 'na_sales', 'eu_sales']])
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

genres = ['Puzzle', 'Strategy']
df['genre'] = df['genre'].where(~df['genre'].isin(genres), "Misc")

print(df['genre'].value_counts(ascending=True))
```