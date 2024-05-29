See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### Importing Data (CSV)
* DataFrames can be imported using several methods (each for different types of data)
* `read_csv()`
	* `sep=` -> specifies the delimiter character to use when reading the csv file
	* `header=` -> specifies if headers should be used or not (by default it is `infer`)
	* `names=` -> sets the names of the headers when reading data
	* `decimal=` -> sets the decimal character that should be used when importing data (by default this is a period `.`)
	* `keep_default_na=` -> Specifies whether or not to include the default `NaN` values when parsing the data. Depending on whether `na_values` is passed in, the behavior is different
		* Setting to `False` -> will read values as empty strings instead of `NaN`
* Example(s)
```python
df = pd.read_csv('/datasets/music_log.csv')
```

```Python
import pandas as pd

column_names = ['country', 'name', 'capacity_mw', 'latitude', 'longitude', 'primary_fuel', 'owner']

data = pd.read_csv('/datasets/gpp_modified.csv', sep='|', header=None,             names=column_names, decimal=',')
```

```Python
import pandas as pd
df_logs = pd.read_csv('/datasets/visit_log.csv', keep_default_na=False)
```
#### Importing Data (Excel)
* `read_excel()` 
	* `sheet_name=` -> specifies which sheet to use for data import (imports the first sheet by default). The sheet index or sheet name can be used in this parameter.
* Examples
```Python
import pandas as pd

df = pd.read_excel('/datasets/product_reviews.xlsx', sheet_name='reviewers')
df = pd.read_excel('/datasets/product_reviews.xlsx', sheet_name=2)
```

```Python
import pandas as pd

# Using a list to import multiple sheets
df = pd.read_excel('month_stats.xlsx', sheet_name=['Clients', 'Cities])
```

#### Converting DataFrame to other Data Types
* Pandas allows for DataFrame to be converted to different objects
	* See documentation for methods
```python
data_dict = data.to_dict() # converting a DataFrame to a dictionary
```

#### Converting a Series to another Data Type
* Pandas allows for DataFrame to be converted to different objects
	* See documentation for methods
```python
temp_list = data["temp"].to_list() # converting the temp series to a list
```

#### Creating a DataFrame from scratch
* The `DataFrame()` method converts objects in Python to DataFrames in Pandas
```Python
# Converting a Dictionary to a DataFrame
data_dict = {"students": ["Amy", "James", "Angela"], "scores": [76, 56, 65]}
new_data_frame = pandas.DataFrame(data_dict)
```
* The `to_csv()` method converts DataFrame can be saved as a CSV file
```Python
new_data_frame.to_csv("new_data.csv")
```