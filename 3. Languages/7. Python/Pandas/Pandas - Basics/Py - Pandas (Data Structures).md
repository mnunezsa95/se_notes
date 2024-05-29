See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### The two data structures in Pandas
* Pandas has two data structures
	1) Series -> a column (single column in a DataFrame)
		* One dimensional 
	2) DataFrame -> a table (the combination of all Series)
		* Two dimensional
* Several series will make up a DataFrame
![image](https://practicum-content.s3.amazonaws.com/resources/5._The_Series_Object_1697205106.png)
* Example
```Python
print(type(data))  # A DataFrame (entire table)
print(type(data[temp]))  # A series (a row)
```

#### DataFrame vs Series
* A DataFrame in pandas can be compared to a dictionary of lists
	* To retrieve data from a table, an index and column must be specified
* A series in pandas can be compared to a list
	* To retrieve data from a list, an index must be specified

