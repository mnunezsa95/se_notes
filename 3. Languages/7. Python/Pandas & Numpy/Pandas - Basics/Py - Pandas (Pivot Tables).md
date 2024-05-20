See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], 
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### Pivot Tables
* Pivoting is a neat process that transforms a DataFrame into a new one by converting selected columns into new columns based on their values. 
#### Pivot Tables in Pandas
* `pivot_table()` --> Create a spreadsheet-style pivot table as a DataFrame (see [documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot_table.html))
	* Returns a DataFrame of the `DataFrame` class
	* Arguments
		* `index` -> the column whose values become the index in the pivot table
		* `columns=` -> the column whose values become columns in the pivot table
		* `values=` -> the column whose values are to be aggregated in the pivot table
		* `aggfunc=` -> the aggregate function to apply to values in each row-column group
* Example
```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df.dropna(inplace=True)

pivot_data = df.pivot_table(index='genre', columns='platform', values='eu_sales', aggfunc='sum')

print(pivot_data)
print(type(pivot_data))
```

```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df = df[df['year_of_release'] >= 2000]

df.user_score = pd.to_numeric(df.user_score, errors='coerce')

df_pivot = df.pivot_table(index='genre', columns='year_of_release', values="user_score", aggfunc='mean')

print(df_pivot)
```