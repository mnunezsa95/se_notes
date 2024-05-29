See [[Py - Introduction to Python]], [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---

#### What are Missing Values?
* Missing values can occur due to a number of reasons but often can impact the data analysis

#### How are Missing Values represented?
* Expected way -> done automatically with Python
	* `None` -> a `NoneType` object in Python
		* Cannot be used in arithmetic operations
	* `NaN` --> treated as a decimal (`float` type)
		* Can be used in arithmetic operations
* Unexpected way -> intentional placement of missing values. Common intentional missing values include:
	* `0`
	* `?`
	* `NN`
	* `n/a`

#### Finding Missing Values
* `isna()` -> returns a boolean if a value is missing
	* Note: often combined with `sum()` to count the number of missing values
* Example
```python
import pandas as pd

cholera = pd.read_csv('/datasets/cholera_short.csv')
cholera.isna().sum() # print number (sum) of missing values
```
* `value_counts()` -> Return a Series containing counts of unique values.
	* `dropna=` -> set to `True` by default. If set to `False` it will include `None` or `NaN` values in the count
* Example
```Python
# using value_counts() on the source column to include None and NaN in the count
import pandas as pd
df_logs = pd.read_csv('/datasets/visit_log.csv')
df_logs['source'].value_counts(dropna=False)
```

#### Processing Missing Values
See [[DS - Dealing with Missing Values]]
* How to process missing values will depend on our analysis
	1) An entire column could be removed if deemed useless if information is irrelevant to our analysis or number of missing values is large
	2) We can replace all missing values in a particular row or column with a specific value if we choose to do so.
* `fillna()` ->  returns a copy of the original row (column), where all NaN values will be replaced with the value passed as an argument
	* args:
		* `value` --> the value to be used for replacing missing values (`NaN`)
* `dropna()` -> returns a copy of the original DataFrame with the removal of rows (or columns) with missing values (`None`and `NaN`, Python missing value types). 
	* args:
		* `axis` -> specifies if columns should be deleted instead of rows
```Python
import pandas as pd

cholera = pd.read_csv('/datasets/cholera_short.csv')

# replacing NaN in row 20 with the number 0, and reassigning this return value to the original row
cholera.loc[20] = cholera.loc[20].fillna(0) 

# replacing NaN in the imported_cases column with "No Info" and reassigning this return value to the original column
cholera['imported_cases'] = cholera['imported_cases'].fillna('No Info')

# removing columns that contain the python data type 'None' or 'NaN' from the DataFrame and reassinging it back to the DataFrame
cholera = cholera.dropna(axis='columns')
```

```python
import pandas as pd
analytics_data = pd.read_csv('/datasets/web_analytics_data.csv')

age_avg = analytics_data['age'].mean()
analytics_data['age'] = analytics_data['age'].fillna(age_avg)

# Creating two DataFrames for `desktop` and `mobile` respectively
desktop_data = analytics_data[analytics_data['device_type'] == 'desktop']
mobile_data =  analytics_data[analytics_data['device_type'] == 'mobile']

# Finding the average time for desktop and mobile
desktop_avg = desktop_data['time'].mean()
mobile_avg = mobile_data['time'].mean()

# Fill in missing values with the average time
desktop_data['time'] = desktop_data['time'].fillna(desktop_avg)
mobile_data['time'] = mobile_data['time'].fillna(mobile_avg)

```