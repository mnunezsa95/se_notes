See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Coordinate Indexing)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

----
#### What is Logical Indexing
* Using logical expressions to retrieve selected data

#### Logical (Boolean) Indexing
* Logical indexing can be used with Coordinate-Integer Indexing to retrieve specific data
* Example
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
cities_df = pd.DataFrame(data=info, columns=titles) # creating a DF

# Indexing the 'country' column where the country is "italy"
cities_of_italy = cities_df[cities_df['country'] == 'Italy']
print(cities_of_italy)
```

* To apply several filtering conditions, start by applying the first condition and storing the result
```Python
import pandas as pd
df = pd.read_csv('/datasets/music_log.csv')

# selecting rows where the genre is jazz and total play ranges b/w 80 to 130
df = df[df['total play'] >= 80] # store first condition to a variable
df = df[df['total play'] <= 130] # store second conditon to the same variable
df = df[df['genre'] == 'jazz'] # store third conditon to the same variable
print(df)
```

* Logically indexing a Series
```python
total_play_under_ten = total_play.loc[total_play <= 10]
```