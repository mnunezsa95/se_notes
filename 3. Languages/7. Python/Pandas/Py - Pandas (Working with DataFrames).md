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
Missing values can arise from various factors, significantly affecting data analysis. They can be represented in different ways:
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
* There are two types of duplicate values:
	* Explicit Duplicates
	* Implicit Duplicates

## Finding Duplicate Rows
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

## Removing Duplicate Rows
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

## Finding Implicit Duplicates
* When identifying duplicates within string data, focus on columns and search for subtle variations in string data that result in implicit duplicates.
    - The `pd.unique()` function generates an array containing implicit duplicates within a column.
    - The `pd.nunique()` function calculates the count of implicit duplicates within a column.
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

## Removing Implicit Duplicates
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