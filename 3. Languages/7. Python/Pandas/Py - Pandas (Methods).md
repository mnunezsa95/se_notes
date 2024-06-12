See:
* [[Py - Introduction to Python]]
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

##### `df.index`
* Returns the indexes of the DataFrame
```Python
df = pd.DataFrame({'Name': ['Alice', 'Bob', 'Aritra'], 'Age': [25, 30, 35], 
	'Location': ['Seattle', 'New York', 'Kona']}, index=([10, 20, 30]))

df.index # Index([10, 20, 30], dtype='int64')
```

##### `df.dtype`
* Return the dtypes in the DataFrame.
```Python
df = pd.DataFrame({'float': [1.0], 'int': [1], 'datetime': 
	[pd.Timestamp('20180310')], 'string': ['foo']})

df.dtypes 
'''float              float64
   int                  int64
   datetime    datetime64[ns]
   string              object
   dtype: object
'''
```

##### `df.columns`
* Returns the column labels of the DataFrame.
```Python
df = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df.columns # Index(['A', 'B'], dtype='object')
```

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

##### `df.loc[]`
* Accesses a group of rows and columns by label(s) or a boolean array.
```Python
df = pd.DataFrame([[1, 2], [4, 5], [7, 8]],
	index=['cobra', 'viper', 'sidewinder'], columns=['max_speed', 'shield'])
df.loc['viper'] 
df.loc['cobra':'viper', 'max_speed']
df.loc[df['shield'] > 6]
```


---

# Pandas Methods

##### `pd.read_csv()`
* Reads a comma-separated values (csv) file into DataFrame.
	* Arguments
		* - `sep=` — specifies the delimiter character to use when reading the CSV file.
		- `header=` — specifies whether headers should be used (default is `infer`).
		- `names=` — sets the column names when reading data.
		- `decimal=` — sets the character to use for decimals when importing data (default is a period `.`).
		- `keep_default_na=` — indicates whether to include the default `NaN` values when parsing data. The behavior varies depending on whether `na_values` is specified:
		    - Setting to `False` — reads empty strings instead of `NaN`.
```Python
import pandas as pd

column_names = ['country', 'name', 'capacity_mw', 'latitude', 'longitude', 'primary_fuel', 'owner']

data = pd.read_csv('/datasets/gpp_modified.csv', sep='|', header=None, 
	names=column_names, decimal=',')
```

##### `read_excel()` 
* Reads an Excel file into a pandas DataFrame.
	* Arguments
		* `sheet_name=` -- specifies which sheet to use for data import (imports the first sheet by default). The sheet index or sheet name can be used in this parameter.
```Python
import pandas as pd

# Import one sheet
df = pd.read_excel('/datasets/product_reviews.xlsx', sheet_name='reviewers')

# Import multiple sheets
df = pd.read_excel('month_stats.xlsx', sheet_name=['Clients', 'Cities])
```

##### `pd.DataFrame()`
* Creates a DataFrame in Pandas
	* Arguments
		* `data=` -- a list used to create the df
		* `index=` -- index to use for resulting frame
		* `columns` -- a list used to specify the columns
		* `dtype` -- the data type to force. Only a single dtype is allowed. If `None`, infer.
		* `copy=` -- copy data from inputs
```Python
import pandas as pd # Import the pandas library

atlas = [ 
  ['France', 'Paris'],  
  ['Russia', 'Moscow'],  
  ['China', 'Beijing'],  
  ['Mexico', 'Mexico City'],  
  ['Egypt', 'Cairo'],
]
geography = ['country', 'capital'] # Prepare the column names
world_map = pd.DataFrame(data=atlas , columns=geography) # Make the DataFrame
print(world_map) # Print the DataFrame
```

##### `pd.Series()`
* Creates a Series in Pandas
	* Arguments
		* `data=` -- a list used to create the df
		* `index=` -- index to use for resulting frame
		* `columns` -- a list used to specify the columns
		* `dtype` -- the data type to force. Only a single dtype is allowed. If `None`, infer.
		* `copy=` -- copy data from inputs
```Python
import pandas as pd

# Create a Series from a list
data = [10, 20, 30, 40]
index = ['a', 'b', 'c', 'd']
series = pd.Series(data, index=index)

print(series)
```

##### `df.head()`
* Returns the first n rows
	* Arguments
		* `n` -- Number of rows to return (5 by default)
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
df.head() # Returns the first 5 rows
df.head(15) # Returns the first 15 rows
```

##### `df.tail()`
* Returns the last n rows
	* Arguments
		* `n` -- Number of rows to return (5 by default)
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
df.tail(5) # Returns the last 5 rows
df.tail(10) # Returns the last 10 rows
```

##### `df.info()`
* Print a concise summary of a DataFrame
	* Arguments
		- `verbose=` -- determines whether to print the full summary. By default, it follows the setting in `pandas.options.display.max_info_columns`.
		- `buf=` -- specifies where to send the output (default is `sys.stdout`).
		- `max_cols=` -- specifies the threshold for switching from verbose to truncated output. If the DataFrame has more than `max_cols` columns, truncated output is used. By default, it follows the setting in `pandas.options.display.max_info_columns`.
		- `memory_usage=` -- indicates whether to display the total memory usage of the DataFrame elements, including the index. By default, it follows the `pandas.options.display.memory_usage` setting.
		- `show_counts=` -- determines whether to show non-null counts. By default, this is displayed only if the DataFrame is smaller than `pandas.options.display.max_info_rows` & `pandas.options.display.max_info_columns`.
```python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
df.info()
```

##### `df.describe()`
* Generates descriptive statistics
	* Arguments
		- `percentiles=` — Specifies the percentiles to include in the output, with values ranging from 0 to 1. The default is `[.25, .5, .75]`, corresponding to the 25th, 50th, and 75th percentiles.
		    - `include=` — A whitelist of data types to include in the result.
		        - `list_of_dtypes` — A list of data types to include.
		        - `'all'` — Includes all columns from the input in the output.
		        - `None` — Includes all numeric columns in the result.
		    - `exclude=` — A blacklist of data types to omit from the result.
		        - `list_of_dtypes` — A list of data types to exclude.
		        - `'all'` — Includes all columns from the input in the output.
		        - `None` — Includes all numeric columns in the result.
```Python
s = pd.Series([1, 2, 3])
s.describe()
```

##### `df.rename()`
* Renames columns or index labels
	* Arguments
		* `mapper=` -- Dict-like or function transformations to apply to that axis’ values. 
		* `index=` -- Alternative to specifying axis (`mapper, axis=0` is equivalent to `index=mapper`).
		* `columns=` -- Alternative to specifying axis (`mapper, axis=1 `is equivalent to `columns=mapper`).
		* `axis=` -- specifies the axis to target with mapper; can be either axis name (`'index', 'columns'`) or `0, 1`
		* `copy=` -- copies underlying data
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

##### `df.isna()`
* Detects missing values
	* Arguments
		* n/a
```Python
import pandas as pd
cholera = pd.read_csv('/datasets/cholera_short.csv')

print(cholera.isna().sum())
```

##### `df.dropna()`
* Removes missing values
	* Arguments
		* `axis=` -- Determine if rows or columns which contain missing values are removed.
			* `0`, or `‘index’` : Drop rows which contain missing values.
			* `1`, or `‘columns’` : Drop columns which contain missing value.
		* `how=` -- Determine if row or column is removed from DataFrame, when we have at least one `NA` or all `NA`.
			* `'any'` --  If any `NA` values are present, drop that row or column.
			* `'all'` -- if all values are `NA`, drop that row or column.
		* `thresh=` -- require that many non-NA values.
		* `subset=` -- labels along other axis to consider, e.g. if you are dropping rows these would be a list of columns to include.
		* `inplace=` -- specifies wether to modify the DataFrame or create a new one.
		* `ignore_index=` -- if `True`, the resulting axis will be labeled 0, 1, …, n - 1.
```Python
df = pd.DataFrame({"name": ['Alfred', 'Batman', 'Catwoman'],
	"toy": [np.nan, 'Batmobile', 'Bullwhip'],
	"born": [pd.NaT, pd.Timestamp("1940-04-25"), pd.NaT]})

# Drop rows where atleast one element is missing
df.dropna()

# Drop columns where atleast one element is missing
df.dropna(axis='columns')
```

##### `df.fillna()`
* Fill `NA`/`NaN` values using the specified method
	* Arguments
		* `value=` -- value to use to fill holes
		* `axis=` -- axis along which to fill missing values (`0` for 'index', `1` for 'column')
		* `inplace=` -- if `True`, fill in-place. 
		* `limit=` -- if method is specified, this is the maximum number of consecutive NaN values to forward/backward fill.
		* `downcast=` -- a dict of item -> dtype of what to downcast if possible, or the string ‘infer’ which will try to downcast to an appropriate equal type
```Python

df = pd.DataFrame([[np.nan, 2, np.nan, 0], [3, 4, np.nan, 1], 
	[np.nan, np.nan, np.nan, np.nan], [np.nan, 3, np.nan, 4]], 
	columns=list("ABCD"))

# Fill Missing Values
values = {"A": 0, "B": 1, "C": 2, "D": 3}
df.fillna(value=values)

# Fill Missing Values
df.fillna(0)
```

##### `df.duplicated()`
* Returns a boolean Series denoting duplicate rows
	* Arguments
		- `subset=` -- Considers only specific columns for identifying duplicates; by default, it uses all columns.
		- `keep=` -- Specifies which duplicates (if any) to label.
		    - `first` -- Labels duplicates as `True` except for the first occurrence.
		    - `last` -- Labels duplicates as `True` except for the last occurrence.
		    - `False` -- Labels all duplicates as `True`.
```Python
import pandas as pd

df = pd.read_csv('/datasets/music_log.csv')
first_5_rows = df[0:5] # Extract first five rows of df
duplicates = first_5_rows.duplicated() # Produce series with duplicated()

print(duplicates) 
```

##### `df.drop_duplicate()`
* Returns a DataFrame with duplicate rows removed
	* Arguments
		* `subset=` -- Only considers certain columns for identifying duplicates, by default use all of the columns
		* `keep=` -- Determines which duplicates (if any) to keep.
			* `‘first’` -- Drops duplicates except for the first occurrence
			* `‘last’` -- Drops duplicates except for the last occurrence
			* `False` -- Drops all duplicates
		* `inplace=` -- Specifies whether to modify the DataFrame rather than creating a new one
		* `ignore_index=` -- If `True`, the resulting axis will be labeled 0, 1, …, n - 1
```Python
# Creating the initial DataFrame 'df' with columns 'brand', 'style', and 'rating'
df = pd.DataFrame({
    'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
    'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
    'rating': [4, 4, 3.5, 15, 5]
})

# Drop duplicate rows from 'df' based on all columns
df.drop_duplicates()

# Drop duplicate rows based on the 'brand' column
df.drop_duplicates(subset=['brand'])

# Drop duplicate rows based on both 'brand' and 'style' columns, and keep the last occurrence of each duplicated set
df.drop_duplicates(subset=['brand', 'style'], keep='last')
```

##### `df.reset_index()`
* Reset the index, or a level of it.
	* `level=` -- Used to only remove the given levels from the index. Removes all levels by default.
	* `drop=` -- (`False`); Resets the index to the default integer index.
	* `inplace=` -- Specifies whether to modify the DataFrame rather than creating a new one.
	* `col_level=` -- If the columns have multiple levels, determines which level the labels are inserted into. By default it is inserted into the first level.
	* `col_fill=` -- If the columns have multiple levels, determines how the other levels are named. If `None` then the index name is repeated.
	* `allow_duplicates=` -- Specifies whether or not to allow duplicate column labels to be created.

##### `Series.unique()`
* Return unique values of Series object.
```Python
series = pd.Series([2, 1, 3, 3], name='A')
series.unique() # array([2, 1, 3])
```

##### `Series.nunique()`
* Return number of unique elements in the object.
```Python
s = pd.Series([1, 3, 5, 7, 7])
s.nunique() # 4 
```

##### `Series.str.replace()`
* Replaces each occurrence of pattern/regex in the Series/Index.
	* `pat` -- the search string
	* `repl` -- the replacement string 
	* `n=` -- the number of replacements to make from start
	* `case=` -- Determines if replace is case sensitive:
		- If `True`, case sensitive (the default if pat is a string)
		- Set to `False` for case insensitive
		- Cannot be set if pat is a compiled regex.
	- `flags=` -- Regex module flags, e.g. re.IGNORECASE. Cannot be set if pat is a compiled regex.
	- `regex=` -- Determines if the passed-in pattern is a regular expression:
		- If `True`, assumes the passed-in pattern is a regular expression.
		- If `False`, treats the pattern as a literal string
		- Cannot be set to False if pat is a compiled regex or repl is a callable.

##### `Series.str.lower()`
* Converts strings in the Series/Index to lowercase
	* Arguments
		* n/a
```Python
s = pd.Series(['lower', 'CAPITALS', 'this is a sentence', 'SwApCaSe'])
s.str.lower()

'''Result 
0                 lower
1              capitals
2    this is a sentence
3              swapcase
'''
```

##### `df.value_counts()`
* Return a Series containing counts of unique values
	* Arguments
		- `normalize=` -- When set to `True`, the resulting object will include the relative frequencies of the unique values.
		- `sort=` -- Sorting by frequencies occurs if set to `True`. Data order preservation is maintained when set to `False`.
		- `ascending=` -- Specifies sorting in ascending order.
		- `bins=` -- Instead of counting values individually, groups them into half-open bins, which is particularly useful for `pd.cut`. This parameter exclusively works with numeric data.
		- `dropna=` -- If set to `True`, counts of `NaN` values are excluded.
```Python
# Use value_counts() on the source column to include None and NaN in the count
import pandas as pd
df_logs = pd.read_csv('/datasets/visit_log.csv')
df_logs['source'].value_counts(dropna=False)
```

##### `df.groupby()`
* Groups DataFrame using a mapper or by a Series of columns
	* Arguments
		* `by=` -- Specifies the condition by which to group the data.
		- `axis=` -- Specifies whether to split along rows (`0`) or columns (`1`).
	- `level=` -- If the axis is a MultiIndex (hierarchical), groups by a particular level or levels.
	- `as_index=` -- Returns the object with group labels as the index.
	    - `as_index=False` is effectively "SQL-style" grouped output.
	- `sort=` -- Sorts the group keys.
	- `group_keys=` -- When calling apply and the `by` argument produces a like-indexed result, adds group keys to the index to identify pieces.
	- `observed=` -- If `True`, only shows observed values for categorical groupers. If `False`, shows all values for categorical groupers.
	- `dropna=` -- If `True` and if group keys contain `NA` values, `NA` values together with row/column will be dropped. If `False`, `NA` values will also be treated as keys in groups.
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')
df.dropna(inplace=True)

grp = df.groupby(['platform', 'genre']) # Split the data into groups
mean_scores = grp['critic_score'].mean() # Apply function & combine the results
```

##### `df.agg()`
* Aggregate using one or more operations over the specified axis
- Arguments:
    - `func` — Function to use for aggregating the data. Acceptable combinations include:
        - function
        - string function name
        - list of functions and/or function names
        - dictionary of axis labels — functions, function names, or lists of such
    - `axis` — If `0` or `index`, applies the function to each column. If `1` or `columns`, applies the function to each row.
    - `*args` — Positional arguments to pass to `func`.
    - `**kwargs` — Keyword arguments to pass to `func`.
```Python
import pandas as pd
df = pd.read_csv('/stats/vg_sales.csv')
df.dropna(inplace=True)

# Create a dict (key = col names, values = aggregate fns)
agg_dict = {'critic_score': 'mean', 'jp_sales': 'sum'}

# Group by two platform and genre & call agg function to apply different aggregate function
grp = df.groupby(['platform', 'genre']).agg(agg_dict)
```

##### `df.query()`
* Queries the columns of a DataFrame with a boolean expression.
	* Arguments
		* `expr` -- The query string to evaluate
			* Use the `@` when referencing an external variable (list, object, etc)
		* `inplace=` -- Specifies whether to modify the DataFrame rather than creating a new one
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


##### `df.isin()`
* Determines whether each element in the DataFrame is contained in values.
	* Arguments
		* `values` -- an iterable, Series, DataFrame or dictionary containing the values to search the DataFrame
			* If `values` is a Series, it will be match on index
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

##### `pd.df.to_dict()` 
* Converts the DataFrame to a dictionary
	* Arguments (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_dict.html) for complete list)
		* `orient=` -- determines the type of the values of the dictionary.'
			* `dict`
			* `list`
			* `series`
			* `split`
		* `into=` -- the collections.abc.MutableMapping subclass used for all Mappings in the return value
		* `index=` -- specifies whether to include the index item (and index_names item if orient is ‘tight’) in the returned dictionary.
```python
df = pd.DataFrame({'col1': [1, 2], 'col2': [0.5, 0.75]}, index=['row1', 'row2'])

df.to_dict()
```


##### `pd.Series.to_excel()`
* Convert Series to {label -> value} dict or dict-like object.
	* Arguments
		* `into=` -- The collections.abc.MutableMapping subclass to use as the return object.
```python
s = pd.Series([1, 2, 3, 4])
s.to_dict() # {0: 1, 1: 2, 2: 3, 3: 4}
```


##### `pd.df.to_csv()`          `pd.Series.to_csv()` 
* Writes object to a comma-separated values (csv) file
	* Arguments (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html) for complete list)
		* `path_or_buf=` -- string, path object, or file-like object implementing a `write()` function 
		* `sep=` -- field delimiter for the output file
		* `na_rep=` -- missing data representation
		* `float_format` -- format string for floating point numbers
		* `columns=` -- columns to write
		* `header=` -- Write out the column names. If a list of string is given it is assumed to be aliases for the column names
		* `index=` -- write row names (index)
```python
df = pd.DataFrame({'name': ['Raphael', 'Donatello'], 'mask': ['red', 'purple'], 'weapon': ['sai', 'bo staff']})

df.to_csv('out.csv', index=False)  
```

##### `pd.df.to_excel()`          `pd.Series.to_excel()`
* Writes object to an Excel sheet
	* Arguments (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_excel.html) for complete list) 
		* `excel_writer` -- file path or existing ExcelWriter
		* `sheet_name=` -- name of sheet which will contain the DataFrame
		* `na_rep=` -- missing data representation
		* `float_format` -- format string for floating point numbers
		* `columns=` -- columns to write
		* `header=` -- Write out the column names. If a list of string is given it is assumed to be aliases for the column names
		* `index=` -- write row names (index)
		* `startrow` -- row to dump data frame.
		* `startcol` -- column to dump data frame.
```Python
df1 = pd.DataFrame([['a', 'b'], ['c', 'd']], index=['row 1', 'row 2'],
	columns=['col 1', 'col 2'])
	
df1.to_excel("output.xlsx")  
```


##### `pd.df.to_json()`          `pd.Series.to_json()`
* Converts the object to a JSON string 
	* Arguments (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_json.html) for complete list)
		* `path_or_buf=` -- string, path object, or file-like object implementing a `write()` function 
		* `orient=` -- indication of expected JSON string format.
```Python
from json import loads, dumps
df = pd.DataFrame(
    [["a", "b"], ["c", "d"]],
    index=["row 1", "row 2"],
    columns=["col 1", "col 2"],
)
```

##### `pd.df.to_html()`          
* Renders a DataFrame as an HTML table.
	* Arguments (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_html.html) for complete list)
		* `buf=` -- Buffer to write to. If None, the output is returned as a string.
		* `columns=` -- The subset of columns to write. Writes all columns by default.
		* `col_space=` -- The minimum width of each column in CSS length units. An int is assumed to be px units..
```Python

df = pd.DataFrame(data={'col1': [1, 2], 'col2': [4, 3]})
html_string = '''
<table border="1" class="dataframe">
	<thead>
	    <tr style="text-align: right;">
	      <th></th>
		  <th>col1</th>
	      <th>col2</th>
	    </tr>
	 </thead>
	 <tbody>
	    <tr>
		    <th>0</th>
			<td>1</td>
		    <td>4</td>
		</tr>
	    <tr>
	      <th>1</th>
	      <td>2</td>
	      <td>3</td>
	    </tr>
	</tbody>
</table>'''

assert html_string == df.to_html()
```

##### `pd.df.to_sql()`          `pd.Series.to_sql()`
* Writes records stored in a DataFrame to a SQL database.
	* Arguments (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_sql.html) for complete list)
		* `name` -- Name of the SQL table
		* `con` -- Using SQLAlchemy makes it possible to use any DB supported by that library.
		* `schema` -- Specify the schema (if supported). If `None`, use default schema.
```Python
df2 = pd.DataFrame({'name' : ['User 6', 'User 7']})
df2.to_sql(name='users', con=engine, if_exists='append')
with engine.connect() as conn:
   conn.execute(text("SELECT * FROM users")).fetchall()
```

##### `pd.df.to_stata()`
* Exports DataFrame object to Stata dta format
	* Arguments (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_stata.html) for complete list)
		* `path` -- the path/filename for the file
		* `convert_dates` -- Dictionary mapping columns containing datetime types to stata internal format to use when writing the dates.
		* `write_index=` - Write the index to Stata dataset.
```Python
df = pd.DataFrame({'animal': ['falcon', 'parrot', 'falcon', 'parrot'],
	'speed': [350, 18, 361, 15]})
df.to_stata('animals.dta')
```

##### `pd.df.to_numpy()`          `pd.Series.to_numpy()`
* Converts the DataFrame to a NumPy array.
	* Arguments
		* `dtype=` -- The dtype to pass to `numpy.asarray()`
		* `copy=` -- Whether to ensure that the returned value is not a view on another array.
		* `na_value` -- The value to use for missing values
```Python
df = pd.DataFrame({"A": [1, 2], "B": [3.0, 4.5]})
df.to_numpy()
```

##### `pd.Series.to_list()`
* Return a list of the values.
```Python
s = pd.Series([1, 2, 3])
s.to_list() # [1, 2, 3]
```

##### `pd.Series.to_markdown()`
* Prints Series in Markdown-friendly format.
	* Arguments
		* `buf=` -- Buffer to write to. If None, the output is returned as a string.
		* `mode=` -- Mode in which file is opened, “wt” by default.
		* `index=` -- add index (row)m labels
		* `storage_options=` -- Extra options that make sense for a particular storage connection, e.g. host, port, username, password, etc.

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