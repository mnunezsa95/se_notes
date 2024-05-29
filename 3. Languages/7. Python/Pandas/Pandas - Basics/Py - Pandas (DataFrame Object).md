See [[Py - Introduction to Python]],  [[Py - Pandas (Data Structures)]], [[Py - Pandas (Series Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### What is a DataFrame
* A DataFrame is a two-dimensional pandas data structure in which each element has two coordinates: a row and a column. 
	* Rows are accessed by indices
	* Columns are accessed by their names
* A DataFrame can be thought of as a dictionary of lists

#### Creating a DataFrame
* `DataFrame()` -> creates a data frame in Python
* Arguments
	* `data` -> a list used to create the data 
	* `columns` -> a list used to specify the columns
* Example
```Python
import pandas as pd # importing the pandas library

atlas = [ # preparing the data 
  ['France', 'Paris'],  
  ['Russia', 'Moscow'],  
  ['China', 'Beijing'],  
  ['Mexico', 'Mexico City'],  
  ['Egypt', 'Cairo'],
]
geography = ['country', 'capital'] # preparing the column names

world_map = pd.DataFrame(data=atlas , columns=geography) # making a DataFrame

print(world_map) # printing the DataFrame
```

#### Getting Data in Columns
* Data in columns can be accessed using the column name using square bracket notation or dot notation
```python
# These two will retrieve the same thing
print(data["condition"])
print(data.condition)
```

#### DataFrame Attributes
* A DataFrame stores both the data itself and general information about that data (in the form of attributes).
	* Attributes are invoked using dot notation
* Syntax: DataFrame Attribute
```python
df.attribute
```
* Attributes in Pandas
	* `index` -> access the index 
	* `dtype` ->  stores the data type of the columns
	* `columns` -> stores a list containing column names (each name is `object` (`string`) type)
	* `shape` -> stores a tuple with two elements (number of rows, number of columns)

* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

print(df.dtypes)
print(df.columns) # (['user_id', 'artist', 'trackeName'], dtype='object')
print(df.shape) # (67963, 5)
```

#### Data Types
* A DataFrame can contain columns of different data types
	* Pandas has its own data types (corresponding to certain data types in Python)
![image](https://practicum-content.s3.amazonaws.com/resources/3._Getting_an_Overview_of_Your_Data_2_1697204153.png)

![image](https://practicum-content.s3.amazonaws.com/resources/3._Getting_an_Overview_of_Your_Data_1_1697204148.png)


#### DataFrame Methods
* DataFrames have methods that are used to get different information
* Some Methods:
	* `head()` -> returns the first rows of the table (default is 5)
		* Args: 
			* number -> specifies the number of rows to return
	* `tail()` -> returns the last rows of the table (default is 5)
		* Args: 
			* number -> specifies the number of rows to return
	* `info()` -> returns all table attributes at once
* Examples
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

df.head() # returns the first 5 rows
df.head(10) # returns the first 10 rows
df.tail() # returns the last 5 rows
```

```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
df.info()
```

```
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

