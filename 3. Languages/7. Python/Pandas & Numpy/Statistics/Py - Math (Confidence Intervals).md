See:
* [[DS - What is Data Science?]]
* [[Py - Introduction to Python]]
* [[ML - Machine Learning in Business]]
Resources
* 


---

## Calculating the Confidence Interval
* ##### `t.interval()`
* Returns the upper and lower percentile for a confidence interval calculation
	* Arguments
		* `alpha` -- the level of significance (threshold) 
		* `df` -- the degrees of freedom (calculated as n - 1)
			* `n` -- number of samples
		* `loc` -- average distribution equal to the mean estimate
		* `scale` -- the standard error of distribution equal to the standard error estimate
```Python
import pandas as pd
from scipy import stats as st

sample = pd.Series([
    439, 518, 452, 505, 493, 470, 498, 442, 497,  423, 524, 442, 459, 452, 463, 
    488, 497, 500, 476, 501, 456, 425, 438, 435, 516, 453, 505, 441, 477, 469, 
    497, 502, 442, 449, 465, 429, 442, 472, 466, 431, 490, 475, 447, 435, 482, 
    434, 525, 510, 494, 493, 495, 499, 455, 464, 509, 432, 476, 438, 512, 423, 
    428, 499, 492, 493, 467, 493, 468, 420, 513, 427])

print('Mean:', sample.mean())
n = len(sample)

confidence_interval = st.t.interval(0.95, n-1, sample.mean(), sample.sem())

print('95% confidence interval:', confidence_interval)
```

```Result
Mean: 470.5285714285714
95% confidence interval: (463.357753651609, 477.6993892055338)
```