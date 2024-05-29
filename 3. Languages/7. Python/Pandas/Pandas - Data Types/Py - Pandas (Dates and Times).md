See 
* Python: [[Py - Introduction to Python]]
* Pandas: [[Py - Pandas (Data Structures)]], [[Py - Pandas (DataFrame Object)]], [[Py - Pandas (Series Object)]], [[Py - Pandas (Data Types)]]
Documentation
* [Installing Pandas](https://pandas.pydata.org/docs/getting_started/install.html)
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Pandas API reference](https://pandas.pydata.org/docs/reference/index.html)

---
#### Dates and Times
* Different parts of the world have different date formats
	* day/month/year
	* month/day/year

#### Dates and Times - Data Type
* `datetime` = A python data type for dates and times
* `Timestamp` = A pandas data type for dates and times (equivalent to Python's `datetime` data type)

#### Converting to datetime
* `to_datetime()` -> converts dates from a string data type to the datetime data type
	* `format=` -> takes a string that specifies how dates are to be formatted using the formatting codes designated by `%`
		* `%d` — day of the month (01 to 31)
		- `%m` — month (01 to 12)
		- `%Y` — four-digit year (2019)
		- `%y` — two-digit year (19)
		- `%H` — hour in 24-hour format
		- `%I` — hour in 12-hour format
		- `%M` — minutes (00 to 59)
		- `%S` — seconds (00 to 59)
- Example
```Python
import pandas as pd

string_date = '2010-12-17T12:38:00Z'
datetime_date = pd.to_datetime(string_date, format='%Y-%m-%dT%H:%M:%SZ')

print(type(string_date)) # <class 'str'>
print(type(datetime_date)) # <class 'pandas._libs.tslibs.timestamps.Timestamp'>
print(datetime_date) # 2010-12-17 12:38:00

df['InvoiceDate'] = datetime_date
```

```Python
import pandas as pd
position = pd.read_csv('/datasets/position.csv')

position["timestamp"] = pd.to_datetime(position['timestamp'], format='%Y-%m-%dT%H:%M:%S')
print(position.head(5))
```

#### Working with Datetime Attributes
* If a column in a DataFrame is of the `timestamp` data type, it can be accessed using different attributes
	* `day` -> returns the numerical day of the month
	* `year` -> returns the numerical year
	* `month` -> returns the numerical month
	* See more: [Time/date components](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#time-date-components)
```Python
import pandas as pd
df = pd.read_csv('/datasets/OnlineRetail.csv')

df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'], format='%Y-%m-%dT%H:%M:%SZ')

# Getting the data type of the 'InvoiceDate' column's first entry
print(type(df['InvoiceDate'][0]))

# Accessing the day using the day attribute
print(df['InvoiceDate'][0].day) # 1
```

#### What is the Accessor Object? (`.dt`)
* Datetime attributes cannot be directly called on a Series, but the series does NOT have these attributes
	* Need to use the **accessor object** to access attributes for an entire column of datetime data
```Python
import pandas as pd 
df = pd.read_csv('/datasets/OnlineRetail.csv')

df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'], format='%Y-%m-%dT%H:%M:%SZ')

# Creating a new column in the DF and setting it equal to the day of the month for each entry
df['day'] = df['InvoiceDate'].dt.day
print(df.sample(5, random_state=42))
```

#### Working with Time Zones
* `.dt.tz_localize()` -> Assigns a timezone to a datetime column, making the data 'aware' of timezone
* `.dt.tz_convert()` -> Converts a time-zone aware column to a different timezone
	* See list of [timezones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List)
```Python
import pandas as pd 

df = pd.read_csv('/datasets/OnlineRetail.csv')
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'], format='%Y-%m-%dT%H:%M:%SZ')

# 
df['InvoiceDate'] = df['InvoiceDate'].dt.tz_localize('UTC')
df['InvoiceDate_NYC'] = df['InvoiceDate'].dt.tz_convert('America/New_York')
print(df['InvoiceDate'].sample(5, random_state=42))
```

```Python
import pandas as pd

position = pd.read_csv('/datasets/position.csv')
position['timestamp'] = pd.to_datetime(position['timestamp'], format='%Y-%m-%dT%H:%M:%S')
position['ts_toronto'] = position['timestamp'].dt.tz_localize('America/Toronto')

position['ts_brisbane'] = position['ts_toronto'].dt.tz_convert('Australia/Brisbane')

```