See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Processing Missing Values)]], [[Py - Pandas (Processing Duplicate Values)]], [[Py - Pandas (Grouping Data)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Sorting Data
* `sort_values()` -> sorts the data (the table as a whole, or groups of rows within it) by a given column
	* Args
		* `by=` -> the column name the data will be sorted by
			* If calling `sort_values()` on a series, there will be no `by=` parameter
		* `ascending=` -> dictates the sorting order (by default set to True); to sort data in descending, set to false

```Python
import pandas as pd
exoplanet = pd.read_csv("/datasets/exoplanets.csv")

# sorting DataFrame by 'radius' column in ascending order
print(exoplanet.sort_values(by='radius').head(10))

# sorting the 'radius' column and printing the first 10 values
print(exoplanet['radius'].sort_values().head(10))

# logically indexing planets that have a radius smaller than earth
# and indexing only planets discovered in the year 2014
exo_small_14 = exoplanet[exoplanet['radius'] < 1] 
exo_small_14 = exo_small_14[exo_small_14['discovered'] == 2014]

# sort by radius in descending order & reassigning result to a variable
exo_small_14 = exo_small_14.sort_values(by='radius', ascending=False)
```
