See 
* [[Py - Introduction to Python]] 
* [[Py - Modular Python]]
* [[Py - Installing Packages, Modules, and Libraries]]
* [[Py - Pandas (Working with DataFrames)]]
* [[Py - Pandas (Methods)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

# Renaming Columns
* Column headers can sometimes be disorganized, not accurately representing the data in their columns, and often contain unnecessary spaces.
* Using `snake_case` is preferred for naming data columns.
* The `df.rename()` function can be utilized to rename columns.
```Python
import pandas as pd

# Measurements are stored in a list of lists 
measurements = [['Sun', 146, 152], ['Moon', 0.36, 0.41], ['Mercury', 82, 217],['Venus', 38, 261], ['Mars', 56, 401], ['Jupiter', 588, 968], ['Saturn', 1195, 1660], ['Uranus', 2750, 3150], ['Neptune', 4300, 4700], ['Halley\'s comet', 6, 5400]]

# Column names are stored in the header variable
header = ['Celestial bodies ', 'MIN', 'MAX'] 

# Convert the data above into 'celestial' DataFrame
celestial = pd.DataFrame(data=measurements, columns=header)
celestial = celestial.rename(
	columns={
		'Celestial bodies ': 'celestial_bodies',
	    'MIN': 'min_distance',
	    'MAX': 'max_distance'
	}
)
```


---
# Working with Missing Values

## Introduction to Missing Values
* Missing values can arise from various factors, significantly affecting data analysis. They can be represented in different ways:
- Expected representations, automatically handled in Python:
    - `None`: A `NoneType` object in Python, which cannot be used in arithmetic operations.
    - `NaN`: Treated as a decimal (`float` type) and can be used in arithmetic operations.
- Unexpected representations, intentionally placed as missing values. Common intentional representations include:
    - `0`
    - `?`
    - `NN`
    - `n/a`

## Finding Missing Values
* `df.isna()` -- returns a boolean if a value is missing
	* Note: often combined with `sum()` to count the number of missing values
```python
import pandas as pd

cholera = pd.read_csv('/datasets/cholera_short.csv')
cholera.isna().sum() # Print number (sum) of missing values
```

```Result
region                 0
country                0
total_cases            1
imported_cases         6
deaths                 1
case_fatality_rate     1
notes                 21
dtype: int64
```


## Handling Missing Data in Datasets
#### Logic of Handling Missing Categorical (Qualitative Value)
* In datasets, missing qualitative values are often replaced with known qualitative values such as `""`, `Unknown`, `'0'`, `'None'`.
#### Logic of Handling Missing Quantitative Values
* In datasets, missing quantitative values are often replaced with the `mean` or `median`.
##### When to Use Mean vs Median?
1. **Assessment of Missing Values Size**:
    - If only a small portion of data is missing, it is acceptable to leave values missing.
    - If a larger portion of data is missing, it should be addressed.
2. **Identification of Outliers**:
    - If there are no significant outliers, use the mean.
    - If there are significant outliers, use the median.
3. **Replacement of Missing Values**:
    - Replace missing values with the calculated mean or median.

## Processing Missing Values
* Processing missing values depends on the analysis:
	1. If a column is deemed irrelevant due to its information or a high number of missing values, it might be removed.
	2. Alternatively, missing values within a specific row or column can be replaced with a designated value.
	
* Methods for Processing Missing Values
	* `fillna()` -- replaces `NaN` values in a row or column with the specified value provided as an argument.
	* `dropna()` -- eliminates rows or columns containing missing values (`None` and `NaN`) from the original DataFrame. 
		* The `axis` parameter determines whether columns or rows are removed.
```Python
import pandas as pd

cholera = pd.read_csv('/datasets/cholera_short.csv')

# Replace NaN in row 20 with the number 0, and reassign this return value to the original row
cholera.loc[20] = cholera.loc[20].fillna(0) 

# Replace NaN in the imported_cases column with "No Info"
cholera['imported_cases'] = cholera['imported_cases'].fillna('No Info')

# Remove columns that contain the python data type 'None' or 'NaN' from the df
cholera = cholera.dropna(axis='columns')
```

```python
import pandas as pd
analytics_data = pd.read_csv('/datasets/web_analytics_data.csv')

age_avg = analytics_data['age'].mean()

# Fill missing values with average
analytics_data['age'] = analytics_data['age'].fillna(age_avg)

# Create two DataFrames for `desktop` and `mobile` respectively
desktop_data = analytics_data[analytics_data['device_type'] == 'desktop']
mobile_data =  analytics_data[analytics_data['device_type'] == 'mobile']

# Find the average time for desktop and mobile
desktop_avg = desktop_data['time'].mean()
mobile_avg = mobile_data['time'].mean()

# Fill in missing values with the average time
desktop_data['time'] = desktop_data['time'].fillna(desktop_avg)
mobile_data['time'] = mobile_data['time'].fillna(mobile_avg)
```


---
# Working with Duplicate Values
## Introduction to Duplicate Values
* There are two types of duplicate values:
	* Explicit Duplicates
	* Implicit Duplicates

## Dealing with Explicit Duplicates
### Finding Duplicate Rows
* The `df.duplicated()` function creates a boolean series with the same length as the DataFrame, indicating whether each corresponding row in the DataFrame is a duplicate. 
	* By default, the first occurrence is marked as `False`, while subsequent duplicates are marked as `True`.
* The `df.value_counts()` function produces a Series that enumerates the occurrences of unique values.
	- By default, `dropna=True`. If set to `False`, it includes `None` or `NaN` values in the count.
```python
import pandas as pd

df = pd.read_csv('/datasets/music_log.csv')

# Extract first five rows of df
first_5_rows = df[0:5] 

# Produce series with duplicated()
duplicates = first_5_rows.duplicated()
print(duplicates.sum()) # Prints the number of duplicates

# Produces a dataframe containing duplicates
duplicated_first_5_rows = first_5_rows[first_5_rows.duplicated()] 
```

```Python
# Example -- Using value_counts()

# Use value_counts() on the source column to include None and NaN in the count
import pandas as pd
df_logs = pd.read_csv('/datasets/visit_log.csv')
df_logs['source'].value_counts(dropna=False)
```

```python
# Example -- Using value_counts()

import pandas as pd
stock = pd.read_csv('/datasets/phone_stock.csv')

stock['item'].value_counts()
```

### Removing Duplicate Rows
- The `drop_duplicates()` function eliminates duplicate entries from a DataFrame; Removing duplicates does not rearrange the indices to accommodate the removed index entries.
    - The `subset=` parameter focuses solely on particular columns for duplicate identification; by default, it involves all columns.
- The `reset_index()` function constructs a fresh DataFrame with renumbered indices; the indices are stored in a new column named `index`.
    - The `drop=` parameter specifies whether the original index should be discarded (no new index column created).
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
first_5_rows = df[0:5]

first_5_rows = first_5_rows.drop_duplicates() # Remove duplicates
first_5_rows = first_5_rows.reset_index(drop=True) # Call the reset_index() method and drop old index
```

![[duplicate-values.png]]

```Python
import pandas as pd
df = pd.DataFrame({'col_1': ['A', 'B', 'A', 'A'], 'col_2': [1, 2, 2, 1]})

# Drop duplicates only in column 'col_1'
df.drop_duplicates(subset='col_1')
```


## Dealing with Implicit Duplicates
### Finding Implicit Duplicates
* When identifying duplicates within string data, focus on columns and search for subtle variations in string data that result in implicit duplicates.
    - The `Series.unique()` function generates an array containing implicit duplicates within a column.
    - The `Series.nunique()` function calculates the count of implicit duplicates within a column.
```python
import pandas as pd

rating = ['date', 'name', 'points']
players = [
    ['2018.01.01',  'Rafael Nadal', 10645],
    ['2018.01.08',  'Rafael Nadal', 10600],
    ['2018.01.29',  'Rafael Nadal', 9760],
	['2018.02.19',  'Roger Federer', 10105], 
	['2018.03.05',  'Roger Federer', 10060],
	['2018.03.19',  'Roger Federerr', 9660],
	['2018.04.02',  'Rafael Nadal Parera', 8770],
	['2018.06.18',  'Roger Fedrer', 8920],
	['2018.06.25',  'Rafael Nadal Parera', 8770],
	['2018.07.16',  'Rafael Nadal Parera', 9310],
	['2018.08.13',  'Rafael Nadal Parera', 10220],
	['2018.08.20',  'Rafael Nadal Parera', 10040],
	['2018.09.10',  'Rafael Nadal Parera', 8760],
	['2018.10.08',  'Rafael Nadal Parera', 8260],
	['2018.10.15',  'Rafael Nadal Parera', 7660],
	['2018.11.05',  'Novak Djokovic', 8045],
	['2018.11.19',  'Novak Djokovic', 9045]
]
tennis = pd.DataFrame(data=players, columns=rating)

# Call the unique() method and printing the result
print(tennis['name'].unique()) 
# ['Rafael Nadal' 'Roger Federer' 'Roger Federerr' 'Rafael Nadal Parera' 'Roger Fedrer' 'Novak Djokovic']

# Call the nunique() method and printing the result
print(tennis['name'].nunique()) # 6
```

### Removing Implicit Duplicates
* When removing implicit duplicates, its important to focus on the strings within the columns that lead to implicit duplicates
* The `Series.str.replace()` method substitutes an undesired string value with a replacement string value. This function uses the `pat` and `repl` parameters to replace a string.
	- `pat` — the string(s) to be replaced (accepts a string to encompass multiple values)
	- `repl` — the string to be used as the replacement
```Python
import pandas as pd

rating = ['date', 'name', 'points']
players = [
    ['2018.01.01',  'Rafael Nadal', 10645],
    ['2018.01.08',  'Rafael Nadal', 10600],
    ['2018.01.29',  'Rafael Nadal', 9760],
	['2018.02.19',  'Roger Federer', 10105], 
	['2018.03.05',  'Roger Federer', 10060],
	['2018.03.19',  'Roger Federerr', 9660],
	['2018.04.02',  'Rafael Nadal Parera', 8770],
	['2018.06.18',  'Roger Fedrer', 8920],
	['2018.06.25',  'Rafael Nadal Parera', 8770],
	['2018.07.16',  'Rafael Nadal Parera', 9310],
	['2018.08.13',  'Rafael Nadal Parera', 10220],
	['2018.08.20',  'Rafael Nadal Parera', 10040],
	['2018.09.10',  'Rafael Nadal Parera', 8760],
	['2018.10.08',  'Rafael Nadal Parera', 8260],
	['2018.10.15',  'Rafael Nadal Parera', 7660],
	['2018.11.05',  'Novak Djokovic', 8045],
	['2018.11.19',  'Novak Djokovic', 9045]
]

# Create a DataFrame
tennis = pd.DataFrame(data=players, columns=rating)

# Use replace() to get rid of wrong versions of Federer's name
tennis['name'] = tennis['name'].replace(['Roger Federerr','Roger Fedrer'], 'Roger Federer')

print(tennis) 
```

```Result
'''
          date                 name  points
0   2018.01.01         Rafael Nadal   10645
1   2018.01.08         Rafael Nadal   10600
2   2018.01.29         Rafael Nadal    9760
3   2018.02.19        Roger Federer   10105
4   2018.03.05        Roger Federer   10060
5   2018.03.19        Roger Federer    9660
6   2018.04.02  Rafael Nadal Parera    8770
7   2018.06.18        Roger Federer    8920
8   2018.06.25  Rafael Nadal Parera    8770
9   2018.07.16  Rafael Nadal Parera    9310
10  2018.08.13  Rafael Nadal Parera   10220
11  2018.08.20  Rafael Nadal Parera   10040
12  2018.09.10  Rafael Nadal Parera    8760
13  2018.10.08  Rafael Nadal Parera    8260
14  2018.10.15  Rafael Nadal Parera    7660
15  2018.11.05       Novak Djokovic    8045
16  2018.11.19       Novak Djokovic    9045
'''
```

```python
import pandas as pd
df_stock = pd.read_csv('/datasets/phone_stock.csv')

# Generate a new column with lowercase versions; Utilize the str.lower() function to convert values
df_stock['item_lowercase'] = df_stock['item'].str.lower()

# Calculate the total count of 'apple' and 'samsung' devices in the 'count' column for each respective brand
apple_total = df_stock[df_stock['item_lowercase'] == 'apple iphone xr 64gb']['count'].sum()
samsung_total = df_stock[df_stock['item_lowercase'] == 'samsung galaxy a30 32gb']['count'].sum()

# Remove duplicates from the item_lowercase column
df_stock = df_stock.drop_duplicates(subset='item_lowercase').reset_index(drop=True)

# Update the count values for apple and samsung devices in the count column
df_stock.loc[0, 'count'] = apple_total
df_stock.loc[3, 'count'] = samsung_total
```



---
# Grouping Data
* Grouping helps provide a more detailed look at the data before moving on to searching for dependencies and similarities between different groups.
* Grouping is warranted when the data logically clusters based on specific features and when these groups are pertinent to the task at hand.
- Stages of Grouping
    1. **Split:** Divide the data into groups based on a given condition.
    2. **Apply:** Apply data aggregation techniques to each group.
    3. **Combine:** Compile and store the results from each group.

## Grouping in Pandas
- The `df.groupby()` method is used to group data.
    - Accepts the name of the column(s) to group by and returns a Series with the `DataFrameGroupBy` class.
        - Multiple grouping results in a multi-index Series with 2 or more index values for each resulting value.
- The `DataFrameGroupBy` object, resulting from grouping, is part of a data processing framework called split-apply-combine.
```Python
# Example -- Grouping 

import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df.dropna(inplace=True)

grp = df.groupby(['platform', 'genre']) # Split the data into groups
mean_scores = grp['critic_score'].mean() # Apply function & combine the results
```

```Python
# Example -- Grouping 

import pandas as pd
exoplanet = pd.read_csv("/datasets/exoplanets.csv")

# Create a new DataFrame grouped by the 'discovered' column & count the values
exoplanet.groupby('discovered').count()

# Create a new DataFrame grouped by the 'discovered' column & count the values for the 'radius' column ONLY
exo_number = exoplanet.groupby('discovered')['radius'].count()

# Create a new DataFrame grouped by the 'discovered' column & sum the values for the 'radius' column ONLY
exo_radius_sum = exoplanet.groupby('discovered')['radius'].sum()

# Find the average 
exo_radius_mean = exo_radius_sum / exo_number
```

```Python
# Example -- Group by Multiple Columns

import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df.dropna(inplace=True)

grp = df.groupby(['platform', 'genre'])
print(grp['critic_score'].mean())
```

#### Performing Multiple Functions to a Grouped Data
- The `agg()` method uses a dictionary as input where the keys are column names and the values are the aggregate functions to be applied.
```Python
# Example -- Applying multiple functions to grouped data
import pandas as pd

df = pd.read_csv('/stats/vg_sales.csv')
df.dropna(inplace=True)

# Create a dict (key = col names, values = aggregate fns)
agg_dict = {'critic_score': 'mean', 'jp_sales': 'sum'}

# Group by two platform and genre & call agg function to apply different aggregate function
grp = df.groupby(['platform', 'genre']).agg(agg_dict)
```

```Python
# Example -- Applying multiple functions to grouped data

import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

df['total_sales'] = df['na_sales'] + df['eu_sales'] + df['jp_sales']

# Group data
grp = df.groupby('genre')

# Define a dictionary to hold operations
agg_dict = {
    'total_sales': 'sum',
    'na_sales': 'mean',
    'eu_sales': 'mean',
    'jp_sales': 'mean'
}

# Apply operations
genre = grp.agg(agg_dict)
```


# Custom Filtering (Single Conditions)
* There are several ways to filter a DataFrame
	* Using built-in methods
		* `df.query()`
		* `df.isin()` 
	* Using external objects
		* Lists
		* Dictionaries
		* Series
		* DataFrames

## Using Built-in Methods to Filter Single Conditions
* The `df.query()` method uses a query string as an input to filter data 
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

# Filter where jp_sales are greater than 1, and return the 'name' and 'jp_sales' columns
df.query("jp_sales > 1")[['name', 'jp_sales']]

# Filter where only where the publisher column is equal to Nintendo and return the 'name' and 'publisher columns'
df.query("publisher == 'Nintendo'")[['name', 'publisher']].head()
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

handhelds = ['3DS', 'DS', 'GB', 'GBA', 'PSP']

# Check if the value of 'platform' is in the handhelds array and return the 'name' and 'platform' values only
df.query("platform in @handhelds")[['name', 'platform']]
```

* The `isin()` method checks if values in a column match any of the values in another array such as a list, dictionary, DataFrame or Series.
	*  If `values` is a Series, it will be match on index
	* If `values` is a dict, it will match on keys
	* If `values` is a df, it will match on both index and column labels
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

handhelds = ['3DS', 'DS', 'GB', 'GBA', 'PSP']

# Checks if the value for 'platform' is in the handheld array and returns the name and platform columsn only
df[df['platform'].isin(handhelds)][['name', 'platform']]
```

```Python
import pandas as pd

# Load the dataset
df = pd.read_csv('/datasets/vg_sales.csv')

# Define the columns to keep and the genres to exclude
columns_to_keep = ['name', 'genre']
excluded_genres = ['Shooter', 'Simulation', 'Sports', 'Strategy']

# Filter the data to retain only the rows where the genre does not start with the letter "S" and return the values for 'genre' and 'name' only
filtered_df = df[~df['genre'].isin(excluded_genres)][columns_to_keep]

print(filtered_df)
```


## Using External Objects
### Using an External List
* Useful for checking the existence of specific values within a DataFrame
* Useful for checking if specific values from a particular column are present in a list
```Python
import pandas as pd

# Define a list of values to filter the DataFrame
our_list = [2, 5, 10]

# Create a DataFrame with three columns 'a', 'b', and 'c'
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],  # Column 'a' with integer values
        'b': [5, 4, 3, 2, 1],     # Column 'b' with integer values
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],  # Column 'c' with string values
    }
)

# Print the list used for filtering
print(our_list)  # [2, 5, 10]

# Filter the DataFrame to only include rows where the values in column 'a' are in 'our_list'
print(df.query("a in @our_list")) # See result below
```

```Result
    a  b  c
0   2  5  X
2  10  3  Y
```

### Using an External Dictionary
* Useful for checking if specific values from a particular column are present in a dictionary
```Python
import pandas as pd

# Define a dictionary with some key-value pairs
our_dict = {0: 10, 3: 11, 12: 12}

# Create a DataFrame with three columns 'a', 'b', and 'c'
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],  # Column 'a' with integer values
        'b': [5, 4, 3, 2, 1],     # Column 'b' with integer values
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],  # Column 'c' with string values
    }
)

# Print the dictionary used for filtering
print(our_dict)  # {0: 10, 3: 11, 12: 12}

# Check for the presence of values from column 'a' among the dictionary values in 'our_dict'
print(df.query("a in @our_dict.values()")) # See results below
```

```
    a  b  c
2  10  3  Y
3  11  2  Y
4  12  1  Z
```

* Useful for checking if specific keys from a particular column are present in a dictionary
```Python
import pandas as pd

# Define a dictionary with specific keys and values
our_dict = {0: 10, 3: 11, 12: 12}

# Create a DataFrame with columns 'a', 'b', and 'c'
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)

# Print the dictionary
print(our_dict)  # Output: {0: 10, 3: 11, 12: 12}

# Query the DataFrame to filter rows where column 'a' has keys present in our_dict
print(df.query("a in @our_dict.keys()"))
```

### Using an External Series
* Series objects store data using index-value pairs.
	* Values are checked by default.
	* To check for an index, utilize the `index` attribute.
```Python
import pandas as pd

# Create a pandas Series named our_series with values [10, 11, 12]
our_series = pd.Series([10, 11, 12])

# Create a DataFrame df with columns 'a', 'b', and 'c'
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)

# Print the content of our_series
print(our_series)  # Output: see result below

# Query the DataFrame df to filter rows where column 'a' values are in our_series
print(df.query("a in @our_series"))  # Output: see result 2 below

# Query the DataFrame df to filter rows where column 'c' values are in our_series index
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
Empty DataFrame
Columns: [a, b, c]
Index: []
```

### Using an External DataFrame
* An external DataFrame offers two methods for data filtration:
	1. Filtering based on its `index` values
	    - This method utilizes the `index` attribute.
	2. Filtering based on values within designated columns
	    - This approach involves specifying columns using dot notation.
```Python
import pandas as pd

# Create the main DataFrame 'df' with columns 'a', 'b', and 'c'
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)

# Create our external DataFrame 'our_df' with columns 'a1', 'b1', and 'c1', and specify custom index values 'Z', 'X', 'P'
our_df = pd.DataFrame(
    {
        'a1': [2, 4, 6],
        'b1': [3, 2, 2],
        'c1': ['A', 'B', 'C'],
    },
    index=['Z', 'X', 'P']
)

# Filter 'df' based on the condition where 'c' values are found in 'our_df' index
filtered_df = df.query("c in @our_df.index")

# Print the filtered DataFrame
print(filtered_df)  # See results below
```

```Result
    a  b  c
0   2  5  X
4  12  1  Z
```

```Python
import pandas as pd

# Create the main DataFrame 'df' with columns 'a', 'b', and 'c'
df = pd.DataFrame(
    {
        'a': [2, 3, 10, 11, 12],
        'b': [5, 4, 3, 2, 1],
        'c': ['X', 'Y', 'Y', 'Y', 'Z'],
    }
)

# Create our external DataFrame 'our_df' with columns 'a1', 'b1', and 'c1', and specify custom index values 'Z', 'X', 'P'
our_df = pd.DataFrame(
    {
        'a1': [2, 4, 6],
        'b1': [3, 2, 2],
        'c1': ['A', 'B', 'C'],
    },
    index=['Z', 'X', 'P']
)

# Query 'df' to filter rows where 'a' values are found in 'our_df.b1' '@' symbol is used to reference variables from the current namespace, which allows 'our_df.b1' to be used directly in the query string
filtered_df = df.query('a in @our_df.b1')

# Print the filtered DataFrame
print(filtered_df)  # See results below
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