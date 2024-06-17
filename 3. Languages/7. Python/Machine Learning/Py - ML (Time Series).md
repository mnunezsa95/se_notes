See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Pandas (Working with Pandas)]]
* [[Py - Pandas (Methods)]]
* [[Py - statsmodels (Basics)]]
* [[Py - statsmodels (Methods)]]
Resources:
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)

----

# What is Time Series?
- Time series are sequences of numbers arranged along a time axis. For example:
    - a company’s stock price at the beginning of each trading day
    - the daily sales volume of an online store
    - the number of online players per hour
- In time series, the intervals between values are consistent, such as 
	- a day
	- an hour
	- ten minutes
	- etc
- Working with Time Series in Python
	- The dates in time series can be indicated in slices
```Python
import pandas as pd

data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)
data.sort_index(inplace=True)

# Slicing data for Jan-Jun 2018
data = data['2018-01':'2018-06']
data.plot()
```


# Resampling Time Series Data
## Resampling
* **Resampling**  -- changing the interval with the values of the series. 
* Resampling is done in two steps:
	1) Choose the new interval length; the values from the existing interval are grouped.
	2) In each group, the aggregated value of the series is calculated. It can be median, mean, maximum or minimum.
* Resampling Visual Example:
		![[resampling-visual-example.png]]
		
* Resampling in Python
	* The `df.resample()` method is used to resample the index based on a specific rule
		* This method groups data similar to the `df.groupby()` method, so it can use aggregate functions `mean()`, `sum()`, `max()`, etc
```Python
import pandas as pd

# Set index to the datetime col; parse the dates in col 1
data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)

# Sort the index (time series)
data.sort_index(inplace=True)

# Resample the data by year, and find average
data = data.resample('1Y').mean()

# Plot the data
data.plot()
```

```Python
import pandas as pd

# Set index to the datetime col; parse the dates in col 1
data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)

# Sort the index (time series)
data.sort_index(inplace=True)

# Slice data for Jan-June 2018, resample by 1 day and find the sum for each day
data = data['2018-01':'2018-06'].resample('1D').sum()

# Plot the data
data.plot()
```

# The Rolling Mean in Time Series
## Rolling Mean
* **Rolling Mean (moving average)** -- a method of smoothing the data in a time series, by reducing fluctuations 
	* Involves finding the values least susceptible to fluctuations (the arithmetic mean)
* How Rolling Mean works:
	* The window size (interval for averaging) is selected experimentally
		* The larger the interval, the stronger the smoothing
		* The window starts to 'roll' from the beginning to the end of the time series
		* The mean is calculated at each point
* Finding the rolling mean
	* The `df.rolling()` method is used to create a rolling window, with the specified size.
```Python
# Example -- Finding the Rolling mean with window size 7
data.rolling(7).mean()
```

```Python
import pandas as pd

# Set index to the datetime col; parse the dates in col 1
data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)

# Sort the index (time series)
data.sort_index(inplace=True)

# Slice data for Jan-June 2018, resample by 1 day and find the sum for each day
data = data['2018-01':'2018-06'].resample('1D').sum()

# Slice data for Jan-June 2018, find the rolling avg for each day with a window size of 10
data['rolling_mean'] = data['2018-01':'2018-06'].rolling(10).mean()

# Plot the data
data.plot()
```

# Trends and Seasonality
* Trends and seasonality depend on the scale of the data.
	* Must have data for enough time to observe trends and seasonality
## Trends
* **Trend** -- a smooth change of the mean value of a series without repeating patterns
* Example:
	* Annual increase of sales of airline tickets
## Seasonality
* **Seasonality** -- cyclical repeating patterns in a time series
* Example:
	* The growth of airline ticket sales each summer

## Working with Trends & Seasonality 
* The time-series analysis (**tsa.seasonal**) module of the statsmodels library has functions for dealing with trends & seasonality 
	* `seasonal.decompose()` -- takes a time series and returns an instance of the `**DecomposeResult**` class. It contains three attributes:
		* `trend` -- the trend component
		* `seasonal` -- the seasonal component
		* `resid` -- the residuals (noise)
```Python
# Import the seasonal_decompose() function from tsa.seasonal module of the statsmodels library
from statsmodels.tsa.seasonal import seasonal_decompose

# Call the seasonal_decompose() function
decomposed = seasonal_decompose(df)

# Create a figure with a size 8x8
plt.figure(figsize=(8, 8))

# Create subsplot & plot the trend
plt.subplot(311)
decomposed.trend.plot(ax=plt.gca())
plt.title('Trend')

# Create subplot & plot the seasonality
plt.subplot(312)
decomposed.seasonal.plot(ax=plt.gca())
plt.title('Seasonality')

# Create subplot & plot the residuals
plt.subplot(313)
decomposed.resid.plot(ax=plt.gca())
plt.title('Residuals')

# plt.subplot(x,y,z) says that the images make a table of x rows and y columns. z is the place of the current image.
# plt.subplot(311) says 3 rows, 1 column, first image. 

# Fit subplots into the area
plt.tight_layout()

print(decomposed.trend[4:6] + decomposed.seasonal[4:6] + decomposed.resid[4:6])
print(df[4:6])
```

```Result
2020-09-03     9.0
2020-09-04    11.0
Freq: D, dtype: float64

             0
2020-09-03   9
2020-09-04  11
```

![[trends-seasonality-residuals-example.png]]

```Python
import pandas as pd
from statsmodels.tsa.seasonal import seasonal_decompose
import matplotlib.pyplot as plt

data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)
data.sort_index(inplace=True)
data = data['2018-01':'2018-06'].resample('1D').sum()

# Decompose the data
decomposed = seasonal_decompose(data)

# To display the graph correctly, specify its axes ax equal to plt.gca() (gca = get current axis)

plt.figure(figsize=(6, 8))
plt.subplot(311)
decomposed.trend.plot(ax=plt.gca())
plt.title('Trend')
plt.subplot(312)
decomposed.seasonal.plot(ax=plt.gca())
plt.title('Seasonality')
plt.subplot(313)
decomposed.resid.plot(ax=plt.gca())
plt.title('Residuals')
plt.tight_layout()
```

# Stationary vs Non-Stationary Series

## Non-stationary Stochastic Process
- A **Non-Stationary Stochastic Process** is a process where:
    - Random variations and distributions change over time
    - Mean and variance values are not constant and shift over time
- Example
	- The graph is NOT stationary because the mean value changes
		![[non-stationary-series-1.png]]​
	*  The graph is NOT stationary the standard deviation changes 
		![[non-stationary-series-2.png]]

## Stationary Stochastic Process
- A stationary stochastic process is defined by a distribution that remains unchanged over time.
- Example:
    - Periodic fluctuations in values
	    ![[stationary-series-1.png]]


# Converting a Series to Stationary

## Time Series Differences
* A time series can be made stationary by finding the ***time series differences***
* **Time Series Differences** -- a sequence of differences between neighboring elements of a time series 
	* The previous value is subtracted from the next one

## Finding the Time Series Differences
* Steps:
	1) Compute shifted data
		* `shift()` -- finds the difference of time series by shifting all values one step forward along the time axis
			* The last value of the series is lost because there is no place to shift it to
	2) Find the differences between shifted data and original data 
```Python
data = pd.Series([0.5, 0.7, 2.4, 3.2])

print(data)
print(data.shift(fill_value=0))
print(data-data.shift())
```

```Result
0    0.5
1    0.7
2    2.4
3    3.2
dtype: float64

0    0.0
1    0.5
2    0.7
3    2.4
dtype: float64

0    NaN
1    0.2
2    1.7
3    0.8
dtype: float64
```

```Python
# Example 
import pandas as pd

data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)
data.sort_index(inplace=True)
data = data['2018-01':'2018-06'].resample('1D').sum()
data -= data.shift()
data['mean'] = data['PJME_MW'].rolling(15).mean()
data['std'] = data['PJME_MW'].rolling(15).std()
data.plot()
```
	![[shift-time-series-to-stationary.png]]

