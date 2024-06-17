See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Pandas (Working with Pandas)]]
* [[Py - statsmodels (Basics)]]
Resources:
* Documentation: [statsmodels](https://www.statsmodels.org/stable/index.html)

---
# Methods
##### `statsmodels.tsa.seasonal.seasonal_decompose()`
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