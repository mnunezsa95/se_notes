See 
* Python: [[Py - Introduction to Python]]
* Pandas: [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Data Types)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### Casting to a Specific Data Type
* The `astype()` method in pandas exists on both DataFrames and Series allows you to cast (or convert) between data types
* `astype()` -> casts a Series or DataFrame as a specified data type
	* `data_type` -> The data type to cast as

#### Casting a DataFrame
* Example
```Python
import pandas as pd
d = {'col1': [1.0, 2.0], 'col2': [3, 4]}

# Creating a DataFrame from 'd' which contains strings, integers and floats
df = pd.DataFrame(data=d) 
df_str_dtype = df.astype('str') # Converting all values in the DF to string
```

#### Casting a Series
* Example
```Python
import pandas as pd
d = {'col1': [1.0, 2.0], 'col2': [3, 4]}

# Creating a DataFrame from 'd' which contains strings, integers and floats
df = pd.DataFrame(data=d)
df['col1'] = df['col1'].astype('int') # Casting all values in `col1` Series to integer
```

#### Checking for Safety before Casting
* Sometimes, we need to check if a column contains a mix of numeric data types, before converting so that we don't lost value data

#### Using `array_equal()` from `Numpy`
* `array_equal()` -> returns `True` if two arrays have the same shape and elements and `False` otherwise
* Arguments
	* `array` -> a list for comparison
	* `array` -> a list for comparison
* Example
```Python
import numpy as np
import pandas as pd

d = {'col1': [1.0, 2.0, 3.0, 4.0], 'col2': [5.0, 6.01, 7.0, 8.0]}
df = pd.DataFrame(data=d)

# check if converting 'col1' is safe.
np.array_equal(df['col1'], df['col1'].astype('int')) # True

# check if converting 'col2' is safe
np.array_equal(df['col2'], df['col2'].astype('int')) # False

# Now we know that we can’t convert `'col2'` from `float` to `int` without losing some of our data.
```