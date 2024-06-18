See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Pandas (Working with Pandas)]]
* [[Py - statsmodels (Basics)]]
Resources:
* Documentation: [pmdarima](https://alkaline-ml.com/pmdarima/)
* Documentation: [statsmodels](https://www.statsmodels.org/stable/index.html)


---
# Introduction to pmdarima
* Pmdarima (originally `pyramid-arima`, for the anagram of 'py' + 'arima') is a statistical library designed to fill the void in Python's time series analysis capabilities. This includes:
	- The equivalent of R's [`auto.arima`](https://www.rdocumentation.org/packages/forecast/versions/7.3/topics/auto.arima) functionality
	- A collection of statistical tests of stationarity and seasonality
	- Time series utilities, such as differencing and inverse differencing
	- Numerous endogenous and exogenous transformers and featurizers, including Box-Cox and Fourier transformations
	- Seasonal time series decompositions
	- Cross-validation utilities
	- A rich collection of built-in time series datasets for prototyping and examples
	- Scikit-learn-esque pipelines to consolidate your estimators and promote productionization
- Pmdarima wraps [statsmodels](https://github.com/statsmodels/statsmodels/blob/master/statsmodels) under the hood, but is designed with an interface that's familiar to users coming from a scikit-learn background.

# Installing statsmodels
* Statsmodels can be installed with anaconda or pip
```bash
conda config --add channels conda-forge
conda config --set channel_priority strict
conda install pmdarima
```

```bash
pip install pmdarima
```

# Importing statsmodels
```Python
import pmdarima as pm
```