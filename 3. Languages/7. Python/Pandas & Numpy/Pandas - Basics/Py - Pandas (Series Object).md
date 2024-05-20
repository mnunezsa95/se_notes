See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### What is a Series?
* A series object represents a single row from a pandas DataFrame (entire table)
* A series is one-dimensional
	* Accessed by index values ONLY

#### Indexing a Series
* A series in pandas can be compared to a list (data retrieve by index)
* Series are indexed by an integer (not by column name)
* Example
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
artist = df['Artist'] # getting a Series object from the DataFrame

# getting a cell from a Series with only one coordinate
print(artist[0]) # Marina Rei
```

#### Getting Data in Rows
* Data in rows can be accessed by using bracket notation and some unique specifier
```python
print(data[data.day == "Monday"]) # Selecting the row where the day is Monday
print(data[data.temp == max_value]) # Selecting the row where the temp is highest

monday = data[data.day == "Monday"]
print(monday.condition) # Getting a specific column within a row
```