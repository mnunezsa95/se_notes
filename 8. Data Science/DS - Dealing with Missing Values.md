See [[DS - What is Data Science?]]

---
#### Handling Missing Categorical (Qualitative Value)
* In datasets, missing qualitative values are often replaced with known qualitative values such as `""`, `Unknown`, `'0'`, `'None`

#### Handling Missing Quantitative Values
* In datasets, missing quantitative values are often replaced with the `mean` or `median`
	* `mean` -> the average (sum_of_values / num_of_values)
	* `median` -> the middle number
* When to use `mean` vs `median`?
	* Step 1: Determine the size of missing values
		* If only a small portion of data is missing (it is okay to leave values missing)
		* If a larger portion of data is missing then it should be dealt with
	* Step 2: Determine whether data has significant outliers
		* If there are no significant outliers, use the mean
		* If there are significant outliers, use the median
	* Step 3: Replace missing values with the mean or median 


