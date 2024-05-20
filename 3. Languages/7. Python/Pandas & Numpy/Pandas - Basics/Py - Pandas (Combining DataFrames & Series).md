See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Grouping Data)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

# Concatenating DataFrames or Series
* Concatenating DataFrames preserves the total amount of data
	* Example: Combining a DataFrame having two columns and three rows with another DataFrame that has the same two columns and five rows results in a DataFrame with two columns and eight rows.

#### Concatenating DataFrames or Series Objects with `concat()`
* `pandas.concat()` -> Concatenate pandas objects along a particular axis (see [documentation](https://pandas.pydata.org/docs/dev/reference/api/pandas.concat.html))
	* To concatenate rows from separate DataFrames, set `axis='index'` in `concat()` 
	* Integers can be used for the `index=` argument, where `index=0` will concatenate row-wise and `index=1` will concatenate column-wise
	* Arguments
		* `objs` -> an iterable or mapping of Series or DataFrame objects
		* `axis=` -> The axis to concatenate along.
			* `'columns'` / `1` 
			* `'index'`/ `0` (default)
* Example: 
```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')

mean_score = df.groupby('publisher')['critic_score'].mean()

df['total_sales'] = df['na_sales'] + df['eu_sales'] + df['jp_sales']

num_sales = df.groupby('publisher')['total_sales'].sum()

df_concat = pd.concat([mean_score, num_sales], axis='columns')
df_concat.columns = ['avg_critic_score', 'total_sales']
```

* Example: Concatenating Rows from separate DataFrames
	* To concatenate rows from separate DataFrames, set `axis='index'` in `concat()` 
```Python
import pandas as pd
df = pd.read_csv('/datasets/vg_sales.csv')

rpgs = df[df['genre'] == 'Role-Playing']
platformers = df[df['genre'] == 'Platform']

df_concat = pd.concat([rpgs, platformers])
df_concat[['name', 'genre']]
```

* Example
```Python
import pandas as pd

df = pd.read_csv('/datasets/vg_sales.csv')
df['total_sales'] = df['na_sales'] + df['eu_sales'] + df['jp_sales']

total_sales = df.groupby('platform')['total_sales'].sum()
num_pubs = df.groupby('platform')['publisher'].nunique()

platforms = pd.concat([total_sales, num_pubs], axis=1)
platforms.columns = ['total_sales', 'num_publishers']
```


---
# Merging and Joining DataFrames & Series
#### Types of Merges
* `Inner Merge` --> only values present in both DataFrames are kept
* `Outer Merge` --> _all_ the values in the specified column are kept from both original DataFrames, but the merged DataFrame has missing values where there isn’t a match.
* `Left Merge` --> all the values from the left DataFrame (the one we call `merge()` on) are present in the merged DataFrame. Values from the right DataFrame (the one we pass as input to `merge()`) are only kept for values that match the specified column in the left DataFrame.
* `Right Merge` --> all the values from the right DataFrame (the one we call `merge()` on) are present in the merged DataFrame. Values from the left DataFrame (the one we pass as input to `merge()`) are only kept for values that match the specified column in the left DataFrame.

#### Concatenating DataFrames or Series Objects with `merge()`
* `merge()` -> combines entries (see [documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html))
	* The result contains only values common to both DataFrames
	* Arguments
		* `on=` -> the name of the column on which merging will take place
		* `how=` -> specifies how the merging will be done
			* `inner` -> use intersection of keys from both frames (default)
			* `outer` -> use union of keys from both frames
			* `left` -> use only keys from left frame
			* `right` -> use only keys from right frame
		* `suffixes=` -> A list (of 2) where each element is optionally a string indicating the suffix to add to overlapping column names in left and right respectively
		* `left_on=` -> Column or index level names to join on in the left DataFrame
		* `right_on` -> Column or index level names to join on in the right DataFrame
* `drop()` -> Drop specified labels from rows or columns.
	* Arguments
		* `labels`  -> a string or list of strings specifying the labels to be dropped
		* `axis=` -> designates if a row or column should be removed
			
* Example: Inner Merge
```Python
# Inner Merge

import pandas as pd

first_pupil_df = pd.DataFrame(
  { 
    'author': ['Alcott', 'Fitzgerald', 'Steinbeck', 'Twain', 'Hemingway'],
    'title': ['Little Women', 'The Great Gatsby', 'Of Mice and Men',
			  'The Adventures of Tom Sawyer', 'The Old Man and the Sea'],
  }
)
second_pupil_df = pd.DataFrame(
  {
    'author': ['Steinbeck', 'Twain', 'Hemingway', 'Salinger', 'Hawthorne'],
    'title': ['East of Eden', 'The Adventures of Huckleberry Finn',
			 'For Whom the Bell Tolls', 'The Catcher in the Rye',
			 'The Scarlett Letter'
			 ],
  }
)

# Inner Merging entries on the 'author' column
both_pupils = first_pupil_df.merge(second_pupil_df, on='author', suffixes=['_1st_student', '_2nd_student'])

# Result: contains only those authors who are present in both original DataFrames
```

* Example: Outer Merge
```Python
# Outer Merge

import pandas as pd

first_pupil_df = pd.DataFrame(
  { 
    'author': ['Alcott', 'Fitzgerald', 'Steinbeck', 'Twain', 'Hemingway'],
    'title': ['Little Women', 'The Great Gatsby', 'Of Mice and Men',
			  'The Adventures of Tom Sawyer', 'The Old Man and the Sea'],
  }
)
second_pupil_df = pd.DataFrame(
  {
    'author': ['Steinbeck', 'Twain', 'Hemingway', 'Salinger', 'Hawthorne'],
    'title': ['East of Eden', 'The Adventures of Huckleberry Finn',
			 'For Whom the Bell Tolls', 'The Catcher in the Rye',
			 'The Scarlett Letter'
			 ],
  }
)

# Outer Merging entries on the 'author' column
both_pupils = first_pupil_df.merge(second_pupil_df, on='author', how='outer')

# The result will have NaN for title_x for index 5 because 'Salinger' is not available in in the first_pupil_df
```

* Example: Left Merge
```Python
# Left Merge

import pandas as pd

first_pupil_df = pd.DataFrame(
  { 
    'author': ['Alcott', 'Fitzgerald', 'Steinbeck', 'Twain', 'Hemingway'],
    'title': ['Little Women', 'The Great Gatsby', 'Of Mice and Men',
			  'The Adventures of Tom Sawyer', 'The Old Man and the Sea'],
  }
)
second_pupil_df = pd.DataFrame(
  {
    'author': ['Steinbeck', 'Twain', 'Hemingway', 'Salinger', 'Hawthorne'],
    'title': ['East of Eden', 'The Adventures of Huckleberry Finn',
			 'For Whom the Bell Tolls', 'The Catcher in the Rye',
			 'The Scarlett Letter'
			 ],
  }
)

# Left Merging entries on the 'author' column
both_pupils = first_pupil_df.merge(second_pupil_df, on='author', how='left')

# Result: All authors and titles from the first student are in the merged DataFrame, but the rows with 'Salinger' and 'Hawthorne' from the second student are not because those authors do not occur in the first student’s DataFrame
```

* Example: Using the `left_on=` and `right_on=` parameters
```Python
# Left Merge

import pandas as pd

first_pupil_df = pd.DataFrame(
  { 
    'authors': ['Alcott', 'Fitzgerald', 'Steinbeck', 'Twain', 'Hemingway'],
    'title': ['Little Women', 'The Great Gatsby', 'Of Mice and Men',
			  'The Adventures of Tom Sawyer', 'The Old Man and the Sea'],
  }
)
second_pupil_df = pd.DataFrame(
  {
    'author': ['Steinbeck', 'Twain', 'Hemingway', 'Salinger', 'Hawthorne'],
    'title': ['East of Eden', 'The Adventures of Huckleberry Finn',
			 'For Whom the Bell Tolls', 'The Catcher in the Rye',
			 'The Scarlett Letter'
			 ],
  }
)

both_pupils = first_pupil_df.merge(second_pupil_df, left_on='authors', right_on='author')
both_pupils.drop('author', axis='columns')
```