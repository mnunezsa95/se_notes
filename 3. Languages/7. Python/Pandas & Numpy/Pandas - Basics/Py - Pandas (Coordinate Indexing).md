See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Indexing DataFrame by Coordinates (Label-based)
* `loc[row_label, col_label]` attribute is used to index a DataFrame and retrieve info from the DataFrame
* Examples:
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

result = df.loc[4, 'genre'] # indexing one cell
result = df.loc[:, 'genre'] # indexing one column
result = df.loc[4, 'artist', 'genre'] # indexing multiple columns
result = df.loc[4, 'user_id':'genre'] # indexing all columns b/w two columns
result = df.loc[4] # indexing one row
result = df.loc[1:] # indexing all rows (starting at a specific one)
result = df.loc[:3] # indexing all rows (up to a specific one)
result = df.loc[2:5] # indexing multiple consecutive rows
```

#### Indexing Series by Coordinates (Label-Based)
* `loc[row_label]` attribute is used to index a Series and retrieve info from the Series
* Examples
```Python
result = total_play.loc[7]  # indexing one row
result = total_play.loc[[5, 7, 10]]  # indexing multiple rows
result = total_play.loc[5:10]  # indexing multiple rows (b/w specific rows)
result = total_play.loc[1:]  # indexing all rows (starting at a specific one)
result = total_play.loc(:3) # indexing all rows (up to a specific one)
```


#### Indexing DataFrames by Coordinates (Integer-based)
* Uses row indices (integers in asc order) and column names in square brackets to access data
	* Slices don’t include the end of the range
	* You can’t address a single cell or row
```python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

result = df['genre'] # indexing one column
result = df[1:] # indexing all rows (starting at a specific one)
result = df[:3] # indexing all rows up to and NOT including the end of range
```

#### Indexing Series by Coordinates (Integer-Based)
* Use row indices ONLY to access data
	* Slices don’t include the end of the range
```Python
result = total_play[7] # indexing one row
result = total_play[5, 7, 10] # indexing multiple rows
result = total_play[5:10] # indexing multiple rows (b/w rows, not inc end)
result = total_play[1:] # indexing all rows (starting at a specific one)
result = total_play[:3] # indexing all rows up to and NOT including the end of range
```