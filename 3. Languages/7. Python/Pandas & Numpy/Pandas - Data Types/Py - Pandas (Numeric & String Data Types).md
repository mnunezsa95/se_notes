See 
* Python: [[Py - Introduction to Python]]
* Pandas: [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Data Types)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### Understanding Numeric Types
* In Pandas, numeric data types are followed by suffix value (`64`, `32`, `16`).
	* These values refer to the bit size of the integers in memory.
		* Higher bit size types can hold more digits than lower bit types

#### Converting Strings to Numbers
* `to_numeric()` -> Converts argument to a numeric type
	* By default, can’t convert strings with non-numeric or decimal characters into a number.
	* Arguments
		* `arg` -> the value to be converted
		* `errors=` -> determines what to do if it encounters an invalid value
			* `'raise'` -> default argument, whereby invalid values generate errors, blocking conversion to numbers for the entire column
			* `'coerce'` -> invalid values are replaced with `NaN`
			* `'ignore'` -> invalid values are simply ignored and left unchanged
* Example
```Python
import pandas as pd
d = {'col1': ['1.0', '2.0'], 'col2': ['3', '4']}
df = pd.DataFrame(data=d)

df['col2'] = df['col2'].astype('int')

df['col1'] = pd.to_numeric(df['col1'])
```

