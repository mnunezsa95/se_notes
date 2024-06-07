See 
* [[Py - Introduction to Python]] 
* [[Py - Modular Python]]
* [[Py - Installing Packages, Modules, and Libraries]]
* [[Py - Pandas (Methods)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
---
---

# Introduction to Pandas
* Pandas is a Python library used for working with data sets.
* It has functions for analyzing, cleaning, exploring, and manipulating data.

---
# Installing and Importing Pandas
#### Installing Pandas
```bash
pip install pandas
```
#### Importing Pandas
```python
import pandas
import pandas as pd
```

---
# Importing Data
* DataFrames can be imported using several methods (each for different types of data)
	* `read_csv()` -- reads a comma-separated values (csv) file into DataFrame.
	* `read_excel()` -- reads an Excel file into a pandas DataFrame
#### Importing CSV Data
* Reads a comma-separated values (csv) file into DataFrame.
```Python
import pandas as pd

column_names = ['country', 'name', 'capacity_mw', 'latitude', 'longitude', 'primary_fuel', 'owner']

data = pd.read_csv('/datasets/gpp_modified.csv', sep='|', header=None,             names=column_names, decimal=',')
```

```Python
import pandas as pd
df_logs = pd.read_csv('/datasets/visit_log.csv', keep_default_na=False)
```

#### Importing Excel Data
* Reads an Excel file into a pandas DataFrame.
```Python
import pandas as pd

# Import one sheet
df = pd.read_excel('/datasets/product_reviews.xlsx', sheet_name='reviewers')

# Import multiple sheets
df = pd.read_excel('month_stats.xlsx', sheet_name=['Clients', 'Cities])
```

---
# DataFrames
#### Introduction to DataFrames
* A DataFrame -- a two-dimensional pandas data structure in which each element has two coordinates: a row and a column. 
	* Rows are accessed by indices
	* Columns are accessed by their names
* A DataFrame stores both the data itself and general information about that data (in the form of attributes).
#### Creating a DataFrame
* `pd.DataFrame()` -- creates a DataFrame in Pandas
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

```Python
# Converting a Dictionary to a DataFrame
data_dict = {"students": ["Amy", "James", "Angela"], "scores": [76, 56, 65]}
new_data_frame = pandas.DataFrame(data_dict)
```

#### DataFrame Attributes
* DataFrame attributes are used to access different information
```Python
# Syntax for attributes
df.attribute_name
```
* Attributes
	* `df.index` -- returns the indexes of the DataFrame
	* `df.dtype` -- returns the dtypes of the columns in the DataFrame
	* `df.columns` -- returns a list containing column names
	* `df.shape` -- returns a tuple with the number of rows, and columns
	* `df.values` -- returns a Numpy representation of the DataFrame (as an array/vector)
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

print(df.index) # Index([10, 20, 30], dtype='int64')
print(df.dtypes) # 
print(df.columns) # (['user_id', 'artist', 'trackeName'], dtype='object')
print(df.shape) # (67963, 5)
```
#### DataFrame Methods
* DataFrames have methods that are used to get different information
* Some Methods:
	* `head()` -- Returns the first rows of the table (default is 5)
	* `tail()` -- Returns the last rows of the table (default is 5)
	* `info()` -- returns all table attributes at once
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

df.head() # Returns the first 5 rows
df.head(10) # Returns the first 10 rows
df.tail() # Returns the last 5 rows
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
df.info()
```

```Result 
### Result from calling df.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 67963 entries, 0 to 67962
Data columns (total 5 columns):
  user_id     67963 non-null object
total play    67963 non-null float64
Artist        60157 non-null object
genre         65223 non-null object
track         65368 non-null object
dtypes: float64(1), object(4)
memory usage: 2.6+ MB
```

#### Accessing Data in Columns
*  Data in columns can be accessed 
	1) Using the column name in square bracket notation
	2) Using dot notation
```python
# These two versions will retrieve the same thing
print(data["condition"])
print(data.condition)
```


---

# Series 
#### Introduction to Series
* A Series -- a dimensional Pandas array-like data structure that represents a single column from a pandas DataFrame
	* Each value in a Series is associated with an index (unique label)

#### Creating a Series
* `pd.Series()` -- creates a Series in Pandas
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

#### Indexing a Series
* Series are only indexed by an index (integer or row) and not by column name
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
artist = df['Artist'] # Get a Series from the DataFrame

# Get a cell from a Series with only one coordinate
print(artist[0]) # Marina Rei
```



#### Getting Data in Rows
* Data in rows can be accessed by using bracket notation and some unique specifier
```python
print(data[data.day == "Monday"]) # Select the row where the day is Monday
print(data[data.temp == max_value]) # Select the row where the temp is highest

monday = data[data.day == "Monday"]
print(monday.condition) # Get a specific column within a row
```


---
# Converting Data
#### Converting DataFrame
* Pandas allows for DataFrame to be converted to different objects
```python
data_dict = data.to_dict() # Convert a DataFrame to a dictionary
data_csv = data.to_csv() # Convert a DataFrame to a CSV
data_excel = data.to_excel() # Convert a DataFrame to an excel sheet 
data_json = data.to_json() # Convert a DataFrame to a JSON string
data_html = data.to_html() # Convert a DataFrame to an HTML document
data_sql = data.to_sql() # Convert a DataFrame to SQL
data_stata = data.to_stata() # Convert a DataFrame to a stata
data_numpy = data.to_numpy() # Convert a DataFrame to a stata
```

#### Converting a Series 
* Pandas allows for Series to be converted to different objects
```python
temp_list = data["temp"].to_dict() # Convert a Series to a dict
temp_list = data["temp"].to_list() # Convert a Series to a list
temp_list = data["temp"].to_csv() # Convert a Series to a csv
temp_list = data["temp"].to_excel() # Convert a Series to an excel sheet
temp_list = data["temp"].to_json() # Convert a Series to a JSON string
temp_list = data["temp"].to_sql() # Convert a Series to SQL
temp_list = data["temp"].to_markdwon() # Convert a Series to markdown
temp_list = data["temp"].to_numpy() # Convert a Series to numpy object
```


---

# Indexing
#### Introduction to Indexing
- **Index**: A component of a Series or DataFrame, accessed using the `index` attribute
- **Indexing**: The process of accessing values in a Series or DataFrame using their indexes
* Indexing is accessing a table cell or portion of a table using two coordinates: 
	* the row coordinate
	* the column coordinate

---
# Coordinate Indexing 
* There are two types of coordinate indexing 
	* Label-Based Indexing
	* Integer-Based Indexing
* Uses the row and column coordinate to access a value

##### Label-Based Indexing a DataFrame
* The `loc[row_label, column_label]` attribute is used to index a DataFrame by label
	* Allows the use of slice operator
		* The slice operator includes the end range
```Python
# Syntax
pd.loc[row_label, column_label]
```

```Python
# Retrieve data at row 4 in the genre column
df.loc[4, 'genre']
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

result = df.loc[4, 'genre'] # index one cell
result = df.loc[:, 'genre'] # index one column
result = df.loc[4, 'artist', 'genre'] # index multiple columns
result = df.loc[4, 'user_id':'genre'] # index all columns b/w two columns
result = df.loc[4] # index one row
result = df.loc[1:] # index all rows (starting at a specific one)
result = df.loc[:3] # index all rows (up to a specific one)
result = df.loc[2:5] # index multiple consecutive rows
```

##### Label-Based Indexing a Series
* The `loc[row_label]` attribute is used to index a Series by label
```Python
result = total_play.loc[7]  # index one row
result = total_play.loc[[5, 7, 10]]  # index multiple rows
result = total_play.loc[5:10]  # index multiple rows (between specific indexes)
result = total_play.loc[1:]  # index all rows (starting at a specific index)
result = total_play.loc(:3) # index all rows (up to a specific index)
```

##### Integer-Based Indexing a DataFrame
* Uses `data[row_label, column_label]` instead of `loc[]`
* Uses row indices (integers in ascending order) and column names within square brackets to access data.
	* Allows the use of slice operator
		* Slices don’t include the end of the range
```python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

result = df['genre'] # Index one column
result = df[1:] # Index all rows (starting at a specific index)
result = df[:3] # Index all rows up to and NOT including the end of range
```

Indexing Series by Coordinates (Integer-Based)
* Uses `data[row_label]` instead of `loc[]`
* Uses row indices (integers in ascending order) within square brackets to access data.
	* Allows the use of slice operator
		* Slices don’t include the end of the range
```Python
result = total_play[7] # Index one row
result = total_play[5, 7, 10] # Index multiple rows
result = total_play[5:10] # Index multiple rows (between rows, not inc end)
result = total_play[1:] # Index all rows (starting at a specific one)
result = total_play[:3] # Index all rows up to and NOT including the end of range
```


---

# Logical Indexing 
#### Introduction to Logical Indexing 
* Uses logical expressions to retrieve selected data
#### Logically Indexing a DataFrame
* Logical indexing can be used with Coordinate-Integer Indexing to retrieve specific data
```Python
import pandas as pd

info = [
    ['Chicago', 'the United States'],
    ['Boston', 'the United States'],
    ['New York City', 'the United States'],
    ['Paris', 'France'],
    ['Rome', 'Italy'],
    ['Venice', 'Italy'],
    ['Milan', 'Italy'],
    ['Madrid', 'Spain'],
    ['Barcelona', 'Spain']
]
titles = ['city', 'country']
cities_df = pd.DataFrame(data=info, columns=titles) # Create a DF

# Indexing the 'country' column where the country is "italy"
cities_of_italy = cities_df[cities_df['country'] == 'Italy']
print(cities_of_italy) 
```

* To apply multiple filtering conditions, begin by applying the first condition and saving the result.
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

# Select rows where the genre is jazz and total play ranges bewtween 80 to 130
df = df[df['total play'] >= 80] # Store first condition to a variable
df = df[df['total play'] <= 130] # Store second conditon to the same variable
df = df[df['genre'] == 'jazz'] # Store third conditon to the same variable
print(df)
```

#### Logically Indexing a Series
* A series can be logically indexed using the `loc[condition]` attribute
```python
total_play_under_ten = total_play.loc[total_play <= 10]
```


