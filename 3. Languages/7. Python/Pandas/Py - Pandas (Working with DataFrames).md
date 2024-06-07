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



# Obtain Value Counts
* `df.value_counts()` -- Returns a Series containing counts of unique values.
	* `dropna=` -- set to `True` by default. If set to `False` it will include `None` or `NaN` values in the count
```Python
# Use value_counts() on the source column to include None and NaN in the count
import pandas as pd
df_logs = pd.read_csv('/datasets/visit_log.csv')
df_logs['source'].value_counts(dropna=False)
```