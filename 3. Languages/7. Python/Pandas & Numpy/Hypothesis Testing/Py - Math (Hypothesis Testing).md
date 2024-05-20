See [[Py - Introduction to Python]], [[Py - Math (Normal Distribution)]]
Documentation
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Numpy Documentation](https://numpy.org/doc/stable/index.html)
* [SciPy Documentation](https://docs.scipy.org/doc/scipy/reference/stats.html)


---

# Hypothesis Testing
* Important to determine if the T-Distribution in a dataset is close to normal because **scipy** library makes it normal automatically
* There are three methods for conducting hypothesis test
	* `ttest_1samp()` -- Two-Tailed or One-Tailed Hypothesis Tests
	* `ttest_ind()` -- A hypothesis that tests of the means of the two statistical populations are equal based on samples
	* `ttest_rel()` --  A Hypothesis that tests that the means of two populations are equal for dependent (paired) samples

----
## Two-Tailed Hypothesis Test
* The `scipy.stats.ttest_1samp (array, popmean)` method is used to test hypothesis of the sort "the mean of the population equal x."
	* `ttest` -- signifies t-test
	* `1samp` -- works with one sample and compares it to a given mean
##### `ttest_1samp()`
* Calculates the difference statistic between `popmean` and the sample mean from the `array`.
* Provides the two-sided statistical significance (Two-Sided Hypothesis Test), indicating the probability of the entire population mean deviating from the proposed value by at least as much as observed in the sample (either increasing or decreasing).
	* Arguments:
		* `array` -> an array containing the sample
		* `popmean` -> the proposed mean being tested for
		
* Example 1: Two-Tailed Hypothesis
```Python
from scipy import stats as st
import numpy as np
import pandas as pd

time_on_site = pd.read_csv('user_time.csv')

interested_value = 120 # 2 hours (120 minutes)
alpha = 0.05  # critical statistical significance

results = st.ttest_1samp(time_on_site, interested_value)
print('p-value: ', results.pvalue) 

if results.pvalue < alpha:
	print('We reject the null hypothesis')
else:
	print("We can't reject the null hypothesis")
```

```
p-value:  [0.27702871]
We can't reject the null hypothesis
```

* Example 2: Two-Tailed Hypothesis
```python
from scipy import stats as st
import pandas as pd

scooters = pd.Series([15, 31, 10, 21, 21, 32, 30, 25, 21, 28, 25, 32, 38, 18, 33, 24, 26, 40, 24, 37, 20, 36, 28, 38, 24, 35, 33, 21, 29, 26, 13, 25, 34, 38, 23, 37, 31, 28, 32, 24, 25, 13, 38, 34, 48, 19, 20, 22, 38, 28, 31, 18, 21, 24])

optimal_value = 30
alpha = 0.05
results = st.ttest_1samp(scooters, optimal_value)

print('p-value: ', results.pvalue)

if results.pvalue < alpha:
  print('We reject the null hypothesis')
else:
  print("We can't reject the null hypothesis")
```

```
p-value:  0.00033528259973700795
We reject the null hypothesis
```

## One-Tailed Hypothesis Test
* There’s no special method for one-sided tests in Python, only two-tailed tests
* Conduct a One-Tailed Hypothesis
	* Conduct a **Two-Sided Test** one 
	* Divide the p-value by 2 which returns the one-sided statistical significance
* Analysis a One-Sided Test
	* **One-Sided test to the Left** -- reject the hypothesis only if the sample mean is significantly less than the predicted value
	* **One-sided Test to the Right** -- reject the hypothesis only if the sample mean is significantly more than the predicted value
*  Example 3: One-Tailed Hypothesis
```Python
from scipy import stats as st
import pandas as pd

screens = pd.Series([4, 2, 4, 5, 5, 4, 2, 3, 3, 5, 2, 5, 2, 2, 2, 3, 3, 4, 8, 3, 4, 3, 5, 5, 4, 2, 5, 2, 3, 7, 5, 5, 6,  5, 3, 4, 3, 6, 3, 4, 4, 3, 5, 4, 4, 8, 4, 7, 4, 5, 5, 3, 4, 6, 7, 2, 3, 6, 5, 6, 4, 4, 3, 4, 6, 4, 4, 6, 2, 6, 5, 3])

prev_screens_value = 4.867
alpha = 0.05  # Critical statistical significance level
results = st.ttest_1samp(screens, prev_screens_value)

# One-sided test: p-value will be halved
print('p-value: ', results.pvalue / 2)

# One-sided test to the left: reject the hypothesis only if the sample mean is significantly less than the predicted value
if (results.pvalue / 2 < alpha) and (screens.mean() < prev_screens_value):
    print("We reject the null hypothesis")
else:
    print("We can't reject the null hypothesis")
```

```
p-value:  1.3358596895543794e-06
We reject the null hypothesis
```


## Equality of Two Population Means (Hypothesis Test)
* The `scipy.stats.ttest_ind(array1, array2, equal_var)` tests a hypothesis of the means of the two statistical populations are equal based on samples
##### `ttest_ind()`
* Calculates the T-test for the means of two independent samples of scores.
* Tests the null hypothesis that the means of these two independent samples are identical (have equal average values).
* Assumes by default that the populations from which the samples are drawn have identical variances.
	* Arguments
		* `array1` -- array of samples
		* `array2` -- array of samples
		* `equal_var=` -- specifies whether or not the variances of the populations should be considered equal
			* `True` -- (default) means the variances are considered equal
				* Used when samples are taken from populations with similar parameters
			* `False` -- the variances are not considered equal

* Example 1: 
	* There are two data sets: The amount spent on purchases made in one month by visitors coming from two different channels. You have a random sample of 30 purchases from each channel.
```Python
from scipy import stats as st
import numpy as np

sample_1 = [3071, 3636, 3454, 3151, 2185, 3259, 1727, 2263, 2015, 2582, 4815,
			633, 3186, 887, 2028, 3589, 2564, 1422, 1785, 3180, 1770, 2716]
sample_2 = [1211, 1228, 2157, 3699, 600, 1898, 1688, 1420, 5048, 3007, 509,
			3777, 5583, 3949, 121, 1674, 4300, 1338, 3066, 3562, 1010, 2311]

alpha = 0.05  # critical statistical significance level

# if the p-value is less than alpha, we reject the hypothesis
results = st.ttest_ind(sample_1, sample_2)
print('p-value: ', results.pvalue)
```

```
p-value:  0.1912450522572209
We can't reject the null hypothesis

The p-value tells us that although the average amounts for the two channels are different, there is a 20% probability of randomly getting a difference that size or larger. This probability is clearly too high to conclude that there is a significant difference between the average amounts spent.
```

* Example 2: 
	* We have two data sets: The visit depth for the website from different groups of users for summer and autumn months. Test the hypothesis that the visit depths for the websites are equal. For instance, maybe in the summer visitors don't get as deep into the content, which would be something to consider when planning an ad campaign for the summer months. Let the significance level be 0.05.
```Python
from scipy import stats as st
import numpy as np

pages_per_session_autumn = [7.1, 7.3, 9.8, 7.3, 6.4, 10.5, 8.7, 17.5, 3.3, 15.5, 
16.2, 0.4, 8.3, 8.1, 3.0, 6.1, 4.4, 18.8, 14.7, 16.4, 13.6, 4.4, 7.4, 12.4, 3.9, 13.6, 8.8, 8.1, 13.6, 12.2]

pages_per_session_summer = [12.1, 24.3, 6.4, 19.9, 19.7, 12.5, 17.6, 5.0, 22.4, 
13.5, 10.8, 23.4, 9.4, 3.7, 2.5, 19.8, 4.8, 29.0, 1.7, 28.6, 16.7, 14.2, 10.6, 18.2, 14.7, 23.8, 15.9, 16.2, 12.1, 14.5]

alpha = 0.05

results = st.ttest_ind(pages_per_session_autumn, pages_per_session_summer, equal_var=False)

print('p-value:', results.pvalue)

if results.pvalue < alpha:
    print("We reject the null hypothesis")
else:
    print("We can't reject the null hypothesis")
```


## Equality of the Means of Paired Samples (Hypothesis Test)
* The method `scipy.stats.ttest_rel()` -- tests the hypothesis that the means of two populations are equal for dependent (paired) samples
	* Used when working with ONE statistical population to know if changes have an effect on the population's mean
	* 'Paired samples' -- measuring a variable for the same units
##### `ttest_rel()`
* Calculates the t-test on TWO RELATED samples of scores, a and b. 
* This is a test for the null hypothesis that two related or repeated samples have identical average (expected) values.
	* Arguments
		* `before` -> arrays with data from before
		* `after` -> arrays with data from after

* Example1: 
	* We have two data sets: package weight, in grams, before changing the method of calculating shipping, and the weight after (for the same repeat customers). We'll test the hypothesis that the package weight didn’t change, even though the method for calculating shipping did.
```Python
from scipy import stats as st
import numpy as np

before = [157, 114, 152, 355, 155, 513, 299, 268, 164, 320, 192, 262, 506, 240, 
		  364, 179, 246, 427, 187, 431, 320, 193, 313, 347, 312, 92, 177, 225]

after = [282, 220, 162, 226, 296, 479, 248, 322, 298, 418, 552, 246, 251, 404, 
		 368, 484, 358, 264, 359, 410, 382, 350, 406, 416, 438, 364, 283, 314]

alpha = 0.05  # critical statistical significance level
results = st.ttest_rel(before, after)

print('p-value: ', results.pvalue)

if results.pvalue < alpha:
    print("We reject the null hypothesis")
else:
    print("We can't reject the null hypothesis")
```

```
p-value:  0.005825972457958989
We reject the null hypothesis

# The data provides sufficient evidence, given the significance level we selected, to reject the null hypothesis. Therefore, we can conclude that there's been in a change in package weights.
```

* Example 2:
```Python
from scipy import stats as st
import numpy as np
import pandas as pd

bullets_before = [821, 1164, 598, 854, 455, 1220, 161, 1400, 479, 215, 564, 159, 
				  920, 173, 276, 444, 273, 711, 291, 880, 892, 712, 16, 476]

bullets_after = [904, 220, 676, 459, 299, 659, 1698, 1120, 514, 1086, 1499, 
				 1262, 829, 476, 1149, 996, 1247, 1117, 1324, 532, 1458, 898]

print('mean before:', pd.Series(bullets_before).mean())
print('mean after:', pd.Series(bullets_after).mean())

alpha = 0.05

results = st.ttest_rel(
    bullets_before, 
    bullets_after)

print('p-value:', results.pvalue / 2)

if 
  results.pvalue / 2 < alpha and 
  pd.Series(bullets_after).mean() > pd.Series(bullets_before).mean():
    print("We reject the null hypothesis")
else:
    print("We can't reject the null hypothesis")
```