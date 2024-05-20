See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Processing Missing Values)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### Looking for duplicate rows
* `duplicated()` -> returns a boolean series with the same length as the DataFrame, where each item indicates whether or not the corresponding DataFrame row is a duplicate
	* By default, first occurrence is set to `False` and subsequent duplicates are set to `True`
```python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
first_5_rows = df[0:5] # extracting first five rows of df
duplicates = first_5_rows.duplicated() # producing series with duplicated()
print(duplicates.sum()) # prints the number of duplicates

# producing a dataframe containing duplicates
duplicated_first_5_rows = first_5_rows[first_5_rows.duplicated()] 
```
* `value_counts()` -> Return a Series containing counts of unique values.
	* `dropna=` -> set to `True` by default. If set to `False` it will include `None` or `NaN` values in the count
```python
import pandas as pd
stock = pd.read_csv('/datasets/phone_stock.csv')
stock['item'].value_counts()
```

#### Removing duplicate rows
* `drop_duplicate()` -> removes duplicates from a DataFrame; Dropping the duplicates does not re-arrange the indices to account for the removed index
	* `subset=` -> Only consider certain columns for identifying duplicates, by default use all of the columns.
* `reset_index()` -> creates a new DataFrame with the indices re-numbered; the indices are located in a new column called `index`
	* Args
		* `drop=` --> used to specify if the original index should be removed (does not create a new index column)
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')
first_5_rows = df[0:5]

first_5_rows = first_5_rows.drop_duplicates() # removing duplicates
first_5_rows = first_5_rows.reset_index(drop=True) # calling the reset_index() method and dropping old index
```

![image](https://practicum-content.s3.amazonaws.com/resources/8._Processing_Duplicate_Values1_1698934393.png)

```Python
import pandas as pd
df = pd.DataFrame({'col_1': ['A', 'B', 'A', 'A'], 'col_2': [1, 2, 2, 1]})

# dropping duplicates only in column 'col_1'
df.drop_duplicates(subset='col_1')
```

#### Looking for implicit duplicates of a string type
* When looking for string-type duplicates, we should work with columns
* `unique()` -> returns an array with implicit duplicates in a column
* `nunique()` -> returns a number of implicit duplicates in a column
```python
import pandas as pd

rating = ['date', 'name', 'points']
players = [
    ['2018.01.01',  'Rafael Nadal', 10645],
    ['2018.01.08',  'Rafael Nadal', 10600],
    ['2018.01.29',  'Rafael Nadal', 9760],
	['2018.02.19',  'Roger Federer', 10105], 
	['2018.03.05',  'Roger Federer', 10060],
	['2018.03.19',  'Roger Federerr', 9660],
	['2018.04.02',  'Rafael Nadal Parera', 8770],
	['2018.06.18',  'Roger Fedrer', 8920],
	['2018.06.25',  'Rafael Nadal Parera', 8770],
	['2018.07.16',  'Rafael Nadal Parera', 9310],
	['2018.08.13',  'Rafael Nadal Parera', 10220],
	['2018.08.20',  'Rafael Nadal Parera', 10040],
	['2018.09.10',  'Rafael Nadal Parera', 8760],
	['2018.10.08',  'Rafael Nadal Parera', 8260],
	['2018.10.15',  'Rafael Nadal Parera', 7660],
	['2018.11.05',  'Novak Djokovic', 8045],
	['2018.11.19',  'Novak Djokovic', 9045]
]
tennis = pd.DataFrame(data=players, columns=rating)

# calling the unique() method and printing the result
print(tennis['name'].unique()) # ['Rafael Nadal' 'Roger Federer' 'Roger Federerr' 'Rafael Nadal Parera' 'Roger Fedrer' 'Novak Djokovic']

# calling the nunique() method and printing the result
print(tennis['name'].nunique()) # 6
```

#### Removing implicit duplicates of string type
* `replace()` --> replaces an unwanted string value with a replacement string values
	* Args
		* to_replace -> `string` to be replace (can use a string to include several values)
		* replace_with -> the string to be used as the replacement
```Python
import pandas as pd

rating = ['date', 'name', 'points']
players = [
    ['2018.01.01',  'Rafael Nadal', 10645],
    ['2018.01.08',  'Rafael Nadal', 10600],
    ['2018.01.29',  'Rafael Nadal', 9760],
	['2018.02.19',  'Roger Federer', 10105], 
	['2018.03.05',  'Roger Federer', 10060],
	['2018.03.19',  'Roger Federerr', 9660],
	['2018.04.02',  'Rafael Nadal Parera', 8770],
	['2018.06.18',  'Roger Fedrer', 8920],
	['2018.06.25',  'Rafael Nadal Parera', 8770],
	['2018.07.16',  'Rafael Nadal Parera', 9310],
	['2018.08.13',  'Rafael Nadal Parera', 10220],
	['2018.08.20',  'Rafael Nadal Parera', 10040],
	['2018.09.10',  'Rafael Nadal Parera', 8760],
	['2018.10.08',  'Rafael Nadal Parera', 8260],
	['2018.10.15',  'Rafael Nadal Parera', 7660],
	['2018.11.05',  'Novak Djokovic', 8045],
	['2018.11.19',  'Novak Djokovic', 9045]
]
tennis = pd.DataFrame(data=players, columns=rating)

# using replace() to get rid of wrong versions of Federer's name
tennis['name'] = tennis['name'].replace(['Roger Federerr','Roger Fedrer'], 'Roger Federer')

print(tennis) 

'''
          date                 name  points
0   2018.01.01         Rafael Nadal   10645
1   2018.01.08         Rafael Nadal   10600
2   2018.01.29         Rafael Nadal    9760
3   2018.02.19        Roger Federer   10105
4   2018.03.05        Roger Federer   10060
5   2018.03.19        Roger Federer    9660
6   2018.04.02  Rafael Nadal Parera    8770
7   2018.06.18        Roger Federer    8920
8   2018.06.25  Rafael Nadal Parera    8770
9   2018.07.16  Rafael Nadal Parera    9310
10  2018.08.13  Rafael Nadal Parera   10220
11  2018.08.20  Rafael Nadal Parera   10040
12  2018.09.10  Rafael Nadal Parera    8760
13  2018.10.08  Rafael Nadal Parera    8260
14  2018.10.15  Rafael Nadal Parera    7660
15  2018.11.05       Novak Djokovic    8045
16  2018.11.19       Novak Djokovic    9045
'''
```

* `str.lower()` -> lowercases an entire string
	* Useful when implicit duplicates appear due to capitalization 
```python
import pandas as pd
df_stock = pd.read_csv('/datasets/phone_stock.csv')

# creating a new column with the lowercase versions
df_stock['item_lowercase'] = df_stock['item'].str.lower()

# getting sum of 'apple' and 'samsung' numbers in the 'count' column for apple and samsung respectively
apple = df_stock[df_stock['item_lowercase'] == 'apple iphone xr 64gb']['count'].sum()
samsung = df_stock[df_stock['item_lowercase'] == 'samsung galaxy a30 32gb']['count'].sum()

# dropping duplicates in the item_lowercase column
df_stock = df_stock.drop_duplicates(subset='item_lowercase').reset_index(drop=True)

# updating the value of apple and samsung phones in the count column
df_stock.loc[0, 'count'] = apple
df_stock.loc[3, 'count'] = samsung
```