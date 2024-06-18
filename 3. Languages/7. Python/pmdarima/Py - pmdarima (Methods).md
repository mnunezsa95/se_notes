See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Pandas (Working with Pandas)]]
* [[Py - statsmodels (Basics)]]
* [[Py - pmdarima (Basics)]]
Resources:
* Documentation: [pmdarima](https://alkaline-ml.com/pmdarima/)
* Documentation: [statsmodels](https://www.statsmodels.org/stable/index.html)


---

# Methods

##### `auto_arima()`
* The auto-ARIMA process seeks to identify the most optimal parameters for an ARIMA model, settling on a single fitted ARIMA model.
	* Arguments 
		* `y` -- The time-series to which to fit the `ARIMA` estimator. 
			* This may either be a Pandas `Series` object (statsmodels can internally use the dates in the index), or a numpy array.
		* `X=` -- (`None`); An optional 2-d array of exogenous variables. If provided, these variables are used as additional features in the regression operation.
		* `seasonal=` (`True`);  Whether to fit a seasonal ARIMA. 
			* If `seasonal` is `True` and `m` == 1, `seasonal` will be set to `False`.
		* `scoring=` -- (`'mse'`); If performing validation (i.e., if out_of_sample_size > 0), the metric to use for scoring the out-of-sample data.
			* `'mse'`
			* `'mae'`
		* `m` -- (`1`); The period for seasonal differencing, `m` refers to the number of periods in each season.
```Python
# Example -- Using the auto_arima() function

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
```
