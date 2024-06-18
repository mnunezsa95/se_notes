See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Pandas (Working with Pandas)]]
* [[Py - statsmodels (Basics)]]
Resources:
* Documentation: [statsmodels](https://www.statsmodels.org/stable/index.html)

---
# Methods
##### `tsa.seasonal.seasonal_decompose()`
* Computes seasonal decomposition using moving averages.
	* Arguments
		* `x` -- Time series
			* If 2d, individual series are in columns. x must contain 2 complete cycles.
		* `model=` -- (`'additive'`); Type of seasonal component.
			* `'additive`
			* `'multiplicative'`
		* `filt=` -- (`None`); The filter coefficients for filtering out the seasonal component. The concrete moving average method used in filtering is determined by two_sided.
		* `period=` -- (`None`); Period of the series. Must be used if x is not a pandas object or if the index of x does not have a frequency. Overrides default periodicity of x if x is a pandas object with a timeseries index.
		* `two_sided=` -- (`True`); The moving average method used in filtering. 
			* If `True` (default), a centered moving average is computed using the filt. 
			* If `False`, the filter coefficients are for past values only.
		* `extrapolate_trend=` -- (`0`); If set to > 0, the trend resulting from the convolution is linear least-squares extrapolated on both ends (or the single one if two_sided is False) considering this many (+1) closest points. If set to ‘freq’, use freq closest points.

##### `graphics.tsaplots.plot_acf()`
* Plots the autocorrelation function
* Plots lags on the horizontal and the correlations on vertical axis.
	* Arguments (see complete list in [documentation](https://www.statsmodels.org/stable/generated/statsmodels.graphics.tsaplots.plot_acf.html))
		* `x` -- the array of time-series values
		* `ax` -- (`None`); 
			* If given, this subplot is used to plot in instead of a new figure being created.
		* `lags=` -- (`None`); An int or array of lag values, used on horizontal axis. Uses `np.arange(lags)` when lags is an int. If not provided, `lags=np.arange(len(corr))` is used.
		* `alpha=` -- If a number is given, the confidence intervals for the given level are returned.
		* `use_vlines=` -- (`True`); 
			* If `True`, vertical lines and markers are plotted. 
			* If `False`, only markers are plotted. The default marker is `‘o’`; it can be overridden with a `marker` kwarg.
```Python
import pandas as pd
from matplotlib import pyplot as plt
from sklearn.model_selection import train_test_split

# Read in the data
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])

# Split data into training and test sets
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Plot ACF
lags_to_check = 50
acf = plot_acf(x=train, lags=lags_to_check)

plt.xlabel("Lags")
plt.ylabel("ACF")
plt.show()
```

##### `graphics.tsaplots.plot_pacf()`
* Plot the partial autocorrelation function
	* Arguments (see complete list in [documentation](https://www.statsmodels.org/dev/generated/statsmodels.graphics.tsaplots.plot_pacf.html))
		* `x` -- the array of time-series values
		* `ax` -- (`None`); 
			* If given, this subplot is used to plot in instead of a new figure being created.
		* `lags=` -- (`None`); An int or array of lag values, used on horizontal axis. Uses `np.arange(lags)` when lags is an int. If not provided, `lags=np.arange(len(corr))` is used.
		* `alpha=` -- If a number is given, the confidence intervals for the given level are returned.
		* `use_vlines=` -- (`True`); 
			* If `True`, vertical lines and markers are plotted. 
			* If `False`, only markers are plotted. The default marker is `‘o’`; it can be overridden with a `marker` kwarg.
		* `method=` -- Specifies which method for the calculations to use:
			- `“ywm”` or `“ywmle”` : Yule-Walker without adjustment. Default.
			- `“yw”` or `“ywadjusted”` : Yule-Walker with sample-size adjustment in denominator for acovf. Default.
			- `“ols”` : regression of time series on lags of it and on constant.
			- `“ols-inefficient”` : regression of time series on lags using a single common sample to estimate all PACF coefficients.
			- `“ols-adjusted” `: regression of time series on lags with a bias adjustment.
			- `“ld”` or `“ldadjusted”` : Levinson-Durbin recursion with bias correction.
			- `“ldb”` or `“ldbiased”` : Levinson-Durbin recursion without bias correction.
```Python
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

##### `tsa.ar_model.ar_select_order()`
* Finds the ideal autoregressive AR-X(p) model order selection.
	* Arguments (see complete list in [documentation](https://www.statsmodels.org/stable/generated/statsmodels.tsa.ar_model.ar_select_order.htmll))
		* `endog=` -- The dataset working as the independent variable
		* `max_lag=` -- The maximum lag to consider
		* `ic=` -- (`bic`); The information criterion to use in the select
			* `'aic'`
			* `'hqic'`
			* `'bic'`
		* `glob=` -- (`False`); Flag indicating where to use a global search across all combinations of lags. 
		* `seasonal=` --  (`False`); Flag indicating whether to include seasonal dummies in the model. 
				* If seasonal is `True` and trend includes `‘c’`, then the first period is excluded from the seasonal terms.
		* `trend=` -- (`'c'`); The trend to include in the model:
			* `'n'` -- no trend
			* `'c'` -- constant trend only
			* `'t'` -- time trend only
			* `'ct'` -- constant and time trend
		* `exog` -- (`None`); Exogenous variables to include in the model.
```Python
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


##### `tsa.stattools.arma_order_select_ic()`
* Compute information criteria for many ARMA models.
	* Arguments
		* `y` -- The dataset containing the time-series data (
		* `max_ar=` -- (`4`); Maximum number of AR lags to use.
		* `max_ma=` -- (`2`); Maximum number of MA lags to use.
		* `ic=` -- (`'bic'`); Information criteria to report. Either a single string or a list of different criteria is possible.
		* `trend=` -- (`'c'`); The trend to use when fitting the ARMA models.
		* `model_kw=` -- (`None`); Keyword arguments to be passed to the `ARMA` model.
		* `fit_kw=` -- (`None`); Keyword arguments to be passed to `ARMA.fit`.
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

# Create and fit MA model
ma_model = ARIMA(train, order=(0, 0, ma_order))
ma_model = ma_model.fit()
```


##### `tsa.stattools.adfuller()`
* Performs an Augmented Dickey-Fuller unit root test.
* The Augmented Dickey-Fuller test can be used to test for a unit root in a univariate process in the presence of serial correlation.
	* Arguments
		* `x` -- The dataset to test
		* `maxlag=` -- (`None`); Maximum lag which is included in test, default value of $12*((nobs)/100)^(1/4)$ is used when `None`.
		* `regression=` -- (`'c'`); Constant and trend order to include in regression.
			- `“c”` -- constant only
			- `“ct”` -- constant and trend.
			- `“ctt”` -- constant, and linear and quadratic trend.
			- `“n”` -- no constant, no trend.
		- `autolag=` -- (`'AIC'`); Method to use when automatically determining the lag length among the values 0, 1, …, `maxlag`.
			- If `“AIC”` or `“BIC”`, then the number of lags is chosen to minimize the corresponding information criterion.
			- `“t-stat”` based choice of `maxlag`. Starts with `maxlag` and drops a lag until the t-statistic on the last lag length is significant using a 5%-sized test.
			- If `None`, then the number of included lags is set to `maxlag`.
		- `store=` -- (`False`); If `True`, then a result instance is returned additionally to the adf statistic.
		- `regresults` -- (`False`); If `True`, the full regression results are returned.
```Python
import pandas as pd
from sklearn.model_selection import train_test_split
from statsmodels.tsa.stattools import adfuller

# Read data and split into training and test sets
data = pd.read_csv("/datasets/Alcohol_Sales.csv", index_col=[0], parse_dates=[0])
train, test = train_test_split(data, shuffle=False, test_size=0.15)

# Run the adfuller test to check for stationarity
df_stationarityTest = adfuller(train, autolag='AIC')
print("P-value: ", df_stationarityTest[1]) # P-value:  0.9843301428483437
```

# Classes
##### `tsa.ar_model.AutoReg()`
* Creates an Autoregressive AR-X(p) model
* Estimate an AR-X model using Conditional Maximum Likelihood (OLS)
	* Hyperparameters (see complete list in [documentation](https://www.statsmodels.org/stable/generated/statsmodels.tsa.ar_model.AutoReg.html))
		* `endog=` -- The dataset working as the independent variable
		* `lags=` -- The number of lags to include in the model if an integer or the list of lag indices to include
		* `glob=` -- (`False`); Flag indicating where to use a global search across all combinations of lags. 
		* `seasonal=` --  (`False`); Flag indicating whether to include seasonal dummies in the model. 
				* If seasonal is `True` and trend includes `‘c’`, then the first period is excluded from the seasonal terms.
		* `trend=` -- (`'c'`); The trend to include in the model:
			* `'n'` -- no trend
			* `'c'` -- constant trend only
			* `'t'` -- time trend only
			* `'ct'` -- constant and time trend
		* `exog` -- (`None`); Exogenous variables to include in the model.
```Python
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

##### `tsa.arima.model.ARIMA()`
* Creates an Autoregressive Integrated Moving Average (ARIMA) model
	* Hyperparameters (see complete list in [documentation](https://www.statsmodels.org/dev/generated/statsmodels.tsa.arima.model.ARIMA.html#statsmodels.tsa.arima.model.ARIMA))
		* `endog` -- The observed time-series process $y$
		* `exog=` -- An array of exogenous regressors
		* `order=` -- (`(0,0,0)`); A tuple containing the `(p,d,q)` order of the model for the autoregressive, differences, and moving average components. 
			* `d` is always an integer
			* `p` and `q` may be integers or lists of integers
		* `seasonal_order=` (`(0,0,0,0)`); The `(P,D,Q,s)` order of the seasonal component of the model for the AR parameters, differences, MA parameters, and periodicity. 
			* `D` and `s` are always integers
			* `P` and `Q` may be integers or lists of positive integers.
		* `trend=` -- (`None`); The trend to include in the model:
			* `'n'` -- no trend
			* `'c'` -- constant trend only
			* `'t'` -- time trend only
			* `'ct'` -- constant and time trend
		* `enforce_stationarity=` -- Whether or not to require the autoregressive parameters to correspond to a stationarity process.
		* `enforce_invertibility=` -- Whether or not to require the moving average parameters to correspond to an invertible process.
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

# Create and fit MA model
ma_model = ARIMA(train, order=(0, 0, ma_order))
ma_model = ma_model.fit()
```


##### `statespace.sarimax.SARIMAX()`
* Seasonal AutoRegressive Integrated Moving Average with eXogenous regressors model
	* Hyperparameters (see complete list in [documentation](https://www.statsmodels.org/dev/generated/statsmodels.tsa.statespace.sarimax.SARIMAX.html))
		* `endog` --  The observed time-series process $y$
		* `exog=` -- (`None`); Array of exogenous regressors, shaped $nobs x k$.
		* `order=` -- (`(1, 0, 0)`); A tuple containing the `(p,d,q)` order of the model for the autoregressive, differences, and moving average components. 
			* `d` is always an integer
			* `p` and `q` may be integers or lists of integers
		* `seasonal_order=` -- (`(0, 0, 0, 0)`); The `(P,D,Q,s)` order of the seasonal component of the model for the AR parameters, differences, MA parameters, and periodicity. 
			* `D` and `s` are always integers
			* `P` and `Q` may be integers or lists of positive integers.
		* `trend=` -- (`None`); The trend to include in the model:
			* `'n'` -- no trend
			* `'c'` -- constant trend only
			* `'t'` -- time trend only
			* `'ct'` -- constant and time trend
		* `measurement_error=` -- (`False`); Whether or not to assume the endogenous observations `endog` were measured with error.
		* `time_varying_regression=` -- Used when an explanatory variables, exog, are provided to select whether or not coefficients on the exogenous regressors are allowed to vary over time.