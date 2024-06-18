See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Pandas (Working with Pandas)]]
* [[Py - Pandas (Methods)]]
* [[Py - statsmodels (Basics)]]
* [[Py - pmdarima (Basics)]]
* [[Py - statsmodels (Methods)]]
* [[Py - pmdarima (Methods)]]
Resources:
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* Documentation: [statsmodels](https://www.statsmodels.org/stable/index.html)
* Documentation: [pmdarima](https://alkaline-ml.com/pmdarima/)
* Documentation: [Tsfresh](https://tsfresh.readthedocs.io/en/v0.1.2/#)
* Documentation: [Prophet](https://facebook.github.io/prophet/)
* Documentation: [Kats](https://facebookresearch.github.io/Kats/)
* Documentation: [LSTM](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) 
* GitHub: [pmdarima](https://github.com/alkaline-ml/pmdarima)
* Article: [Partial Autocorrelation Function](https://arauto.readthedocs.io/en/latest/how_to_choose_terms.html#estimating-ar-terms)
* Blog Post: [ARIMA & SARIMA: Real-World Time Series Forecasting](https://neptune.ai/blog/arima-sarima-real-world-time-series-forecasting-guide)
* User Guide: [Time Series Analysis](https://www.statsmodels.org/stable/user-guide.html#time-series-analysis)
* User Guide: [pmdarima - ARIMA estimators for Python](https://alkaline-ml.com/pmdarima/)
	* Examples - [pmdarima use examples](https://alkaline-ml.com/pmdarima/auto_examples/index.html)
* Article: [11 Classical Time Series Forecasting Methods in Python (Cheat Sheet)](https://machinelearningmastery.com/time-series-forecasting-methods-in-python-cheat-sheet/)


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


# Time Series Forecasting
## Intro to Time Series Forecasting
* **Time Series Forecasting** -- the process of developing a model which predicts the future values of a time series based on previous data.
* **Forecast Horizon** -- the length of time into the future for which the forecast is prepared
* If the values of either a time series or the function `x(t)` (where t = time) are numbers, then it is a regression task for the time series. 
* If the values of either a time series or the function `x(t)` (where t = time) are categories, it will be a classification task.

## The Train and Test Sets in Time Series Forecasting
* The train and test sets cannot be mixed and the training set data must precede the test set data
* The `train_test_split()` function has a `shuffle=` parameter which can be set to false to prevent the mixing of the train and test sets
		![[train-test-set-time-series.png]]

```Python
# Example 
import pandas as pd
from sklearn.model_selection import train_test_split

data = pd.Series([0.1, 0.5, 2.3, 1.2, 1.5])
train, test = train_test_split(data, shuffle=False, test_size=0.2)
print('Training set:')
print(train)
print('Test set:')
print(test)
```

```Result
Training set:
0    0.1
1    0.5
2    2.3
3    1.2
dtype: float64

Test set:
4    1.5
dtype: float64
```

```Python
# Example 
import pandas as pd
from sklearn.model_selection import train_test_split

data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)
data.sort_index(inplace=True)
data = data.resample('1D').sum()

train, test = train_test_split(data, shuffle=False, test_size=0.20)

print(train.index.min(), train.index.max())
print(test.index.min(), test.index.max())
```

# Forecast Accuracy
- The _MAE_ metric is suitable for evaluating models in tasks due to its straightforward interpretability.

## Forecasting Without Training
- There are two common methods for forecasting time series without training:
    1. Predicting all values of the test sample with the same number (a constant). 
	    * For the _MAE_ metric, this number corresponds to the median.
    2. Predicting the new value $x(t)$ using the previous value in the series, denoted as $x(t−1)$. 
	    * This approach is independent of the metric used.
        - It's important to note that the most recent value from the training data can serve as the initial value for the test data.
```Python
# Example -- Method #1

import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error

data = pd.read_csv('/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0])

data.sort_index(inplace=True)
data = data.resample('1D').sum()

train, test = train_test_split(data, shuffle=False, test_size=0.2)

print('Median daily power consumption:', test['PJME_MW'].median())

# Create an array of ones with the same shape as the `test` DataFrame. The shape of `test` determines the dimensions of the array. 

# Calculate the median of the `PJME_MW` column in the `train` DataFrame.
# Multiply the two values
pred_median = np.ones(test.shape) * train['PJME_MW'].median()
print('MAE:', mean_absolute_error(test, pred_median))
```

```Result
Median daily power consumption: 723141.0
MAE: 96625.08333333333
```

```Python
# Example -- Method #2

import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error

data = pd.read_csv('/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0])

data.sort_index(inplace=True)
data = data.resample('1D').sum()

train, test = train_test_split(data, shuffle=False, test_size=0.2)

print('Median daily power consumption:', test['PJME_MW'].median())

# Shift the `test` data one time step forward to create a lagged version of the data where each value is moved to the next row.
pred_previous = test.shift()

# Set the first element of `pred_previous` to the last element of the `train` data to initialize the first value of the shifted series with the last value from the training set, ensuring continuity between the training and test sets.
pred_previous.iloc[0] = train.iloc[-1]
print('MAE:', mean_absolute_error(test, pred_previous))
```

```Result
Median daily power consumption: 723141.0
MAE: 44941.65924092409
```

# Creating Features in Time Series

## Types of Features in Time Series
* There are different types of features:
	* Calendar Features
	* Lag Features
	* Rolling Mean

### Calendar Features
- Trends and seasonality are often associated with specific dates.
- The `datetime64` type in pandas holds the required information; the only task left is to display it in separate columns.
```Python
# Example
data = pd.read_csv('energy_consumption.csv', index_col=[0], parse_dates=[0])
data.sort_index(inplace=True)
data = data.resample('1D').sum()

# This feature contains years as numeric values
data['year'] = data.index.year

# This feature contains weekdays as numeric values
data['dayofweek'] = data.index.dayofweek

print(data.head(10))
```

```Result
             PJME_MW  year  dayofweek
Datetime                             
2002-01-01  714857.0  2002          1
2002-01-02  822277.0  2002          2
2002-01-03  828285.0  2002          3
2002-01-04  809171.0  2002          4
...
```

### Lag Features
- The preceding values in the time series can indicate whether the function `x(t)` will increase or decrease. 
- Lag values can be obtained using the `shift()` function
```Python
data['lag_1'] = data['PJME_MW'].shift(1)
data['lag_2'] = data['PJME_MW'].shift(2)
data['lag_3'] = data['PJME_MW'].shift(3)

print(data.head(10))
```

```Result
             PJME_MW     lag_1     lag_2     lag_3
Datetime                                          
2002-01-01  714857.0       NaN       NaN       NaN
2002-01-02  822277.0  714857.0       NaN       NaN
2002-01-03  828285.0  822277.0  714857.0       NaN
2002-01-04  809171.0  828285.0  822277.0  714857.0
2002-01-05  729723.0  809171.0  828285.0  822277.0
2002-01-06  727766.0  729723.0  809171.0  828285.0
...
```

### Rolling Mean
* The rolling mean feature sets the general trend of the time series
```Python
# Example -- Calculate the rolling mean
data['rolling_mean'] = data['PJME_MW'].rolling(5).mean()
```

```Result
             PJME_MW  rolling_mean
Datetime                          
2002-01-01  714857.0           NaN
2002-01-02  822277.0           NaN
2002-01-03  828285.0           NaN
2002-01-04  809171.0           NaN
2002-01-05  729723.0      780862.6
2002-01-06  727766.0      783444.4
2002-01-07  800012.0      778991.4
```

## Calculating Features
- Rolling mean at time $t$ includes the current value $x(t)$
- Current value $x(t)$ belongs to the target, not the features
- Use lag features to exclude the current value in feature engineering

```Python
# Example -- Creating a custom function to engineer features in time series

import pandas as pd
import numpy as np


data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)
data.sort_index(inplace=True)
data = data.resample('1D').sum()

def make_features(data, max_lag):
    data['year'] = data.index.year
    data['month'] = data.index.month
    data['day'] = data.index.day
    data['dayofweek'] = data.index.dayofweek
    
	# Calculate the lag values
    for lag in range(1, max_lag+1):
        data[f'lag_{lag}'] = data['PJME_MW'].shift(lag)
        
	# Calculate the rolling average and add it as a 'rolling_mean' feature. 
	# The current value of a row cannot be used to calculate the moving average.
    data['rolling_mean'] = 
	    data['PJME_MW'].shift().rolling(rolling_mean_size).mean()

make_features(data, 4)
print(data.head())
```

# Model Training
* It is impossible to get the features for the first values of the training set because there's no previous data.
* Remove values that are `NaN` from the train dataset

```Python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error


data = pd.read_csv(
    '/datasets/energy_consumption.csv', index_col=[0], parse_dates=[0]
)
data.sort_index(inplace=True)
data = data.resample('1D').sum()

# Function to create features
def make_features(data, max_lag, rolling_mean_size):
    data['year'] = data.index.year
    data['month'] = data.index.month
    data['day'] = data.index.day
    data['dayofweek'] = data.index.dayofweek

    for lag in range(1, max_lag + 1):
        data['lag_{}'.format(lag)] = data['PJME_MW'].shift(lag)

    data['rolling_mean'] = (
        data['PJME_MW'].shift().rolling(rolling_mean_size).mean()
    )

# Create features
make_features(data, 6, 10)

# Split the data
train, test = train_test_split(data, shuffle=False, test_size=0.2)

# Drop n/a values
train = train.dropna()

# Declare features and target
features_train = train.drop(['PJME_MW'], axis=1)
target_train = train['PJME_MW']
features_test = test.drop(['PJME_MW'], axis=1)
target_test = test['PJME_MW']

# Create, train and predict with model
model = LinearRegression()
model.fit(features_train, target_train)
pred_train = model.predict(features_train)
pred_test = model.predict(features_test)

# Evaluate accruacy
print("MAE for the training set:", mean_absolute_error(pred_train, target_train))
print("MAE for the test set: ", mean_absolute_error(pred_test, target_test))
```

# Autoregression (AR) Model
## The Autoregressive Model
* **Autoregressive (AR) Model** -- a model that uses linear combinations of past values to predict future values.
* Autoregressive models uses lagged variables as inputs (similar to Linear Regression)
* Autoregressive models assume that past observations correlate with future values.
	* Only lags with a strong correlation should be taken into consideration.

## Autoregressive Function
* Execute the autocorrelation function (ACF) to reveal strong relationships between lagged values in a time series:
	- Interpreting the results:
	    - Each spike in the ACF plot represents the strength and direction of correlation for a given lag.
	    - The blue area indicates the 95% confidence interval.
	    - Spikes outside the blue area signify lags with statistically significant correlations.
		![[autocorrelation-function-example.png]]
```Python
import pandas as pd
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split
from statsmodels.graphics.tsaplots import plot_acf

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Plot ACF
lags_to_check = 50
acf = plot_acf(x=train, lags=lags_to_check)

plt.xlabel("Lags")
plt.ylabel("ACF")
plt.show()
```


* Run the partial autocorrelation function (PACF), which which displays partial relationships between lagged values of a time series
		![[partial-autocorrelation-function-example.png]]
```Python
# Example -- Finding partial relationship using PAFC

import pandas as pd
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split
from statsmodels.graphics.tsaplots import plot_pacf

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Plot PACF
lags_to_check = 50
pacf = plot_pacf(x=train, lags=lags_to_check) 
```


* The PACF can be analyzed either manually or using a function:
	- Manual observation:
	    - Count the spikes in the PACF plot from left to right until encountering a spike that does not exceed the Confidence Interval (ignore the first spike at lag 0)
	- Using the `statsmodels.tsa.ar_model.ar_select_order()` function, which employs complex calculations based on the [Information Criterion](https://otexts.com/fpp2/arima-estimation.html)
```Python
# Example -- Using the ar_select_order() function to analyze PACF

import pandas as pd
from sklearn.model_selection import train_test_split
from statsmodels.tsa.ar_model import AutoReg, ar_select_order

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Find optimal number of lags
mod = ar_select_order(endog=train, maxlag=30)
ar_order = mod.ar_lags
print("Lags that define the AR model order:", ar_order)

# Create AR model and fit it using the training set
ar_model = AutoReg(train, lags=ar_order)
ar_model = ar_model.fit()
```

## ACF vs PACF
- The Autocorrelation Function (ACF) captures both direct and indirect types of correlation.
- The Partial Autocorrelation Function (PACF) reveals the direct correlation between two observations.
    - It shows the direct correlation of the $kth$​ lag while removing the influence of all shorter lag terms (indirect correlation).


## Building an Autoregressive (AR) Model
Steps:
* Import the data 
* Split the data 
* Execute the `ar_select_order()` function to determine the optimal number of lags and save the output to a variable:
	* Use the `endog=` parameter to specify the dataset to analyze.
	* Use the `max_lag=` parameter to define the maximum number of lags to consider.
		* Setting this value too low might cause the model to overlook important lag features.
		* Setting this value too high can increase the model's runtime.
* Extract the optimal AR model order using the `ar_lags` attribute from the results of `ar_select_order()`, and store this in a variable.
* Instantiate the `AutoReg()` class, passing the data and the optimal number of lags obtained in the previous step to the `lags=` parameter.
- Train the model using the `fit()` method.
- Predict using the `predict()` method:
	- Set the `start=` and `end=` parameters to define the future time period for prediction.
		- Typically, use `start=len(train)` and `end=len(train) + len(test) - 1`.
```Python
# Example -- Building an Autoregressive (AR) Model
import pandas as pd
from sklearn.model_selection import train_test_split
from statsmodels.tsa.ar_model import AutoReg, ar_select_order
from sklearn.metrics import mean_absolute_error

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Find optimal number of lags
mod = ar_select_order(endog=train, maxlag=30)
ar_order = mod.ar_lags
print("Lags that define the AR model order:", ar_order)

# Create AR model and fit it using the training set
ar_model = AutoReg(train, lags=ar_order, seasonal=True)
ar_model = ar_model.fit()

# Make predictions
start_value = len(train)
end_value = len(train) + len(test) - 1
ar_pred = ar_model.predict(start=start_value, end=end_value, dynamic=False)

# Plot results
plt.plot(ar_pred, color='blue', label='pred')
plt.plot(test, color='red', label='test')
plt.legend(loc="upper left")
plt.xticks(rotation=90)
plt.show()

# Evaluate model
ar_mae_value = mean_absolute_error(test, ar_pred)
print(ar_mae_value.round(3)) # 625.14
```

```Result
Lags that define the AR model order: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```


# Moving Average (MA) Model
## Residuals and the MA Model
* The accuracy of future forecasts can be improved by accounting for how far away predictions were from the actual values
* The **Moving Average (MA) Model** uses past residuals to predict future values
	![[moving-average-residuals.png]]

* The **Moving Average (MA) Model** also has order (similar to AR Models)
	* The order can be determined manually by examining the PACF plot
		* The order for an MA Model is equal to the number of spikes that exceed the confidence intervals in the ACF plot (ignore the first spike at lag 0)
	* The order can also be determined using the `arma_order_select_ic()` function from the `statsmodels.tsa.stattools` module.
		* This function uses an automated way of determining the model order based on the Information Criteria
```Python
import pandas as pd
from statsmodels.tsa.arima.model import ARIMA
from statsmodels.tsa.stattools import arma_order_select_ic
from sklearn.model_selection import train_test_split

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Find optimal order for MA model
res = arma_order_select_ic(y=train, max_ar=0, max_ma=10)
ma_order = res.bic_min_order[1]
print("Output of the arma_order_select_ic() function is:", res.bic_min_order)
```

## Building a Moving Average (MA) Model
Steps:
- Import the data.
- Split the data.
- Determine the best order for the MA model using `arma_order_select_ic()` and save the output to a variable:
    - `y=` -- the training dataset.
    - `max_ma=` -- the maximum number of lags to consider for the MA model.
        - Setting this value too low might cause the model to overlook important lag features.
        - Setting this value too high can increase the model's runtime.
    - `max_ar=` -- the maximum number of lags to consider for the AR model; set to 0 if the model should be strictly MA.
- Extract the MA model order using the `bic_min_order` attribute from the result of `arma_order_select_ic()` and store it in a variable:
    - The first element in the tuple is the best AR model order.
    - The second element is the best MA model order.
- Create an instance of the `ARIMA()` class:
    - Pass the training set to the `endog=` parameter.
    - Pass the variables obtained above to the `order=` parameter.
- Train the model using the `fit()` method.
- Predict using the `predict()` method:
    - Set the `start=` and `end=` parameters to define the future time period for prediction.
        - Typically, use `start=len(train)` and `end=len(train) + len(test) - 1`.
```Python
# Example -- Building a Moving Average (MA) Model

import pandas as pd
from statsmodels.tsa.arima.model import ARIMA
from sklearn.model_selection import train_test_split
from statsmodels.tsa.stattools import arma_order_select_ic
from sklearn.metrics import mean_absolute_error

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Find optimal order for MA model
res = arma_order_select_ic(y=train, max_ar=0, max_ma=10)
ma_order = res.bic_min_order[1]
print("Output of the arma_order_select_ic() function is:", res.bic_min_order)

# Create and fit MA model
ma_model = ARIMA(train, order=(0, 0, ma_order))
ma_model = ma_model.fit()

# Make predictions
start_value = len(train)
end_value = len(train) + len(test) - 1
ma_pred = ma_model.predict(start=start_value, end=end_value, dynamic=False)

# Plot results
plt.plot(ma_pred, color="blue", label="pred")
plt.plot(test, color="red", label="test")
plt.legend(loc="upper left")
plt.xticks(rotation=90)
plt.show()

# Calculate MAE of predictions
ma_mae_value = mean_absolute_error(test, ma_pred)
print(ma_mae_value) # 4761.75810998995
```

# Autoregressive Moving Average (ARMA) Model
* Sometimes the **Moving Average (MA)** Modal and **Autoregressive Model (AR)** Model are not great alone at forecasting
* These two can be combined into one model called the **Autoregressive Moving Average (ARMA)**

## The Autoregressive Moving Average (ARMA) Model
- When working with the ARMA model, two orders must be set:
    - One for Autoregressive, denoted by ppp
    - One for Moving Average, denoted by qqq
- A key assumption of the ARMA model is that the time series data is stationary.
    - Conduct an augmented Dickey-Fuller (adfuller) unit root test to check for stationarity:
        - Interpreting the result:
            - $p<0.05$ -- The dataset is very likely stationary.
            - $p>0.05$ -- The dataset is very likely non-stationary.

## Building an Autoregressive Moving Average (ARMA) Model
Steps
- Import the data.
- Split the data.
- Check for stationarity using the `adfuller()` function.
- Set the model orders:
    - `ar_order` ($p$) -- sets the order for the autoregressive part.
    - `differencing_term` ($d$) -- specifies the differencing term.
    - `ma_order` ($q$) -- sets the order for the moving average part.
- Create an instance of the `ARIMA()` class:
    - Pass the training set to the `endog=` parameter.
    - Pass the orders obtained above to the `order=` parameter.
- Train the model using the `fit()` method.
- Predict using the `predict()` method:
    - Set the `start=` and `end=` parameters to define the future time period for prediction.
        - Typically, use `start=len(train)` and `end=len(train) + len(test) - 1`.

```Python
# Example -- Building an Autoregressive Moving Average (ARMA) Model 

import pandas as pd
from statsmodels.tsa.arima.model import ARIMA
from sklearn.model_selection import train_test_split

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Plot the data to check for stationarity
data.plot()
plt.show()

# Run the adfuller test to check for stationarity
df_stationarityTest = adfuller(train, autolag='AIC')
print("P-value: ", df_stationarityTest[1])

# Create and fit ARMA model
arma_model = ARIMA(train, order=(5, 0, 3))
arma_model = arma_model.fit()
```


# Autoregressive Integrated Moving Average (ARIMA) Model

## The Autoregressive Integrated Moving Average (ARIMA) Model
* The **Autoregressive Integrated Moving Average (ARIMA)** model includes differencing, which subtracts the previous observation at time $t−1$ from the current observation at time $t$.
	- Differencing converts a non-stationary time series into a stationary one.
	    - This enables the ARMA components of the model to make more accurate predictions for time series with trends and seasonality.

## Building an Autoregressive Integrated Moving Average (ARIMA) Model
Steps: 
- Import the data.
- Split the data.
- Set the model orders:
    - `ar_order` ($p$) -- sets the order for the autoregressive part.
    - `differencing_term` ($d$) -- specifies the differencing term.
	    - This must be set to a non-zero number for differencing to occur
    - `ma_order` ($q$) -- sets the order for the moving average part.
- Create an instance of the `ARIMA()` class:
    - Pass the training set to the `endog=` parameter.
    - Pass the orders obtained above to the `order=` parameter.
- Train the model using the `fit()` method.

```Python
# Example -- Building an Autoregressive Integrated Moving Average (ARIMA) Model

import pandas as pd
from sklearn.model_selection import train_test_split
from statsmodels.tsa.arima.model import ARIMA

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Set model p, d, and q model orders
ar_order = 1
diff_order = 1
ma_order = 1
arima_full_order = (ar_order, diff_order, ma_order)

# Create and fit ARIMA model
arima_model = ARIMA(train, order=arima_full_order)
arima_model = arima_model.fit()
```

# Seasonality in Models
* Use the `seasonal_decompose()` function from the `statsmodels.tsa.seasonal` module to get a more rigorous consideration of seasonality
	* Plotting the decomposition, will return 4 graphs:
		* original time series
		* trend
		* seasonal
		* residuals
* The seasonal graph will help identify whether or no the data is cyclical, meaning that seasonality does exist and is repeated consistently over the whole dataset
* 
```Python
import pandas as pd
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split
from statsmodels.tsa.seasonal import seasonal_decompose

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Separate time series into its components and plot each one
decomposition = seasonal_decompose(train)
decomposition.plot()
plt.show()

# Plot seasonal for a period of 3 years
N = 3
months_per_year = 12
months_in_period = N * months_per_year

decomposition.seasonal[0:months_in_period].plot()
plt.show()
```


# Seasonal Autoregressive Integrated Moving Average (SARIMA) Model
## The SARIMA Model
- The SARIMA model is effective for time series data that exhibit clear seasonal patterns.
- Implemented using the `SARIMAX()` class in the `tsa.statespace.sarimax` module of the `statsmodels` library.

# Seasonal Autoregressive Integrated Moving Average with Exogenous Factors (SARIMAX) Model
## The SARIMAX Model
- The SARIMAX model extends the SARIMA model by incorporating exogenous factors.
- Also implemented using the `SARIMAX()` class in the `tsa.statespace.sarimax` module of the `statsmodels` library.


# Simple Model Selection in Python
- The `pmdarima` library in Python automates the selection of the best forecasting model and parameters for a given dataset.
- Key functions to focus on:
    - The `auto_arima()` function
        - The `auto_arima()` function operates similarly to creating a class and calling `fit()` in sklearn
        - It helps identify the optimal ARIMA-like model for the univariate time series by determining:
            - The best model
            - The optimal set of model parameters
        - The output of `auto_arima()` can be stored in a variable, allowing access to other methods such as:
            - `predict()` -- generates forecasts using the model
            - `summary()` -- provides a comprehensive overview of the model
            - `get_params()` -- retrieves the parameters used in the model

## Working with the pmdarima library
Steps:
- Import the dataset
- Divide the data into training and test sets
- Utilize the `auto_arima()` function for model training and fitting
    - The `seasonal=` parameter can be adjusted to account for seasonality
    - The `m=` parameter specifies the number of periods per season
    - The `scoring=` parameter indicates the key metric to be minimized
- Make predictions with the `predict()` method
- Assess the model's performance
- Visualize the outcomes
    - Introduce a new column in the DataFrame to store predictions for each time point in the series
        - For the training set, this can be `NaN`
        - For the test set, this will contain the model's predictions
    - Generate a plot of the results
```Python
# Example -- Using the auto_arima() function

#====================== Building the model ======================#
import pandas as pd
from sklearn.model_selection import train_test_split
from pmdarima import auto_arima

# Read data and split into training and test sets
data = pd.read_csv('/datasets/Alcohol_Sales.csv', index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Find optimal model for our data
model = auto_arima(train, seasonal=True, m=12, scoring='mae')

# Make predictions
predictions = model.predict(len(test))

# Evaluate the model predictions
auto_arima_mae = mean_absolute_error(test, predictions)
print(auto_arima_mae) # 583.9691551216356

# Get info about the model (print version)
model.summary()

# Get info about the model (access to the keys and values)
parameters = model.get_params()
for key, value in parameters.items():
    print(f"{key}: {value}")


#====================== Visualize Data ======================#
# Create a new column to store predictions
x = np.zeros(len(data))

# Fill training set points with NaN
x[:len(train)] = np.nan 

# Fill test set points with model predictions
x[len(train):] = predictions

# Add new column to dataframe
data['predicted_sales'] = x 

# Rename the original column
data.rename(columns={'beer_sales': 'actual_sales'}, inplace=True)

# Print the data
print(data)

# Plot the results
data.plot()
data[len(train):].plot()
plt.show()
```

```Result
#================ Result from calling print(data)
            actual_sales  predicted_sales
DATE                                     
1992-01-01          3459              NaN
1992-02-01          3458              NaN
1992-03-01          4002              NaN
1992-04-01          4564              NaN
1992-05-01          4221              NaN
...                  ...              ...
2018-09-01         12396     12002.517213
2018-10-01         13914     13170.224995
2018-11-01         14174     12743.396852
2018-12-01         15504     14394.768817
2019-01-01         10718     10306.996180

#================ Result from calling get_params()
maxiter: 50
method: lbfgs
order: (3, 1, 1)
out_of_sample_size: 0
scoring: mae
scoring_args: {}
seasonal_order: (2, 1, 2, 12)
start_params: None
suppress_warnings: True
trend: None
with_intercept: False
```
	![[auto-arima-print-example.png]]


# Additional Libraries
Here are a few more libraries that help with time series data:
- [Tsfresh](https://tsfresh.readthedocs.io/en/v0.1.2/#) is excellent for generating features from time series data.
- [Prophet](https://facebook.github.io/prophet/) is a robust forecasting library that handles outliers and missing data well.
- [Sktime](https://www.sktime.org/en/stable/) extends scikit-learn with time series algorithms and provides tools compatible with sklearn.
- [kats](https://facebookresearch.github.io/Kats/) is an all-in-one library for time series analysis in Python, offering tools for feature engineering, analysis, and forecasting.
- [LSTM](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) can be used for time series predictions. Unlike ARIMA, LSTMs do not require parameters (`p`, `d`, and `q`); instead, they have their own set of hyperparameters that need to be tuned.

