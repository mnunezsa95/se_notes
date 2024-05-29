See [[Py - Introduction to Python]], [[Py - Pandas (Sample Space Probability)]], [[Py - Numpy (Probability Distributions and Value Intervals)]]
Documentation
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Numpy Documentation](https://numpy.org/doc/stable/index.html)
* [SciPy Documentation](https://docs.scipy.org/doc/scipy/reference/stats.html)

---

#### What is the SciPy Package?
* SciPy.Stats is a large number of probability distributions, summary and frequency statistics, correlation functions and statistical tests, masked statistics, kernel density estimation, quasi-Monte Carlo functionality, and more.
* Relevant Methods: Both work with the normal distribution if the mean and variance are known
	* `st.norm()` -> normal continuous random variable
	* `norm.cdf()` -> cumulative distribution function
	* `norm.ppf()` -> percent point function

#### Finding Probability Using the Normal Distribution
* `norm.cdf()` -> gives the probability of the interval to the left of the value **when the value along the X axis is known**.
* `norm.ppf()` -> gives the value along the X axis **when the probability of the interval to the left of the value is known**.

#### Example: using `norm.cdf()`
* Example 1: We know the X axis value and want to know the probability of the interval to the left.
```Python
from scipy import stats as st

# normal distribution with an expected value (mean) of 1000 and a standard deviation of 100
distr = st.norm(1000, 100)
x = 1000

result = distr.cdf(x)  # calculate probability of getting the value x
print(result) # 0.5
```

```Python
# Can get the same result using a one-liner
result = st.norm(1000, 100).cdf(1000)
```

* Example 2: What the probability of falling between 900 and 1100?
```Python
from scipy import stats as st

distr = st.norm(1000, 100) 
x1 = 900
x2 = 1100
result = distr.cdf(x2) - distr.cdf(x1)

print(result) # 0.6826894921370859
```

#### Example: using `norm.ppf()`
* Example 1: We can see that the value 1100 should be greater than approximately 50% + 34.1% = 84.1% of values
```Python
from scipy import stats as st

distr = st.norm(1000, 100) 
p1 = 0.841
result = distr.ppf(p1)

print(result) # 1099.8576270615658
```

#### Normal Approximation to the Binomial Distribution
* If the number of trials is high enough, the binomial distribution can be modeled by the normal distribution
	* Then these binomial distribution parameters (expected value and variance) can be taken as the mean and variance of a normal distribution, which will be fairly close to the binomial.
		* The expected value (mean) os: $n ⋅ p$
		* The variance is $n⋅ p ⋅ (1 - p)$
* Example
```Python
from matplotlib import pyplot as plt
from math import factorial
from scipy.stats import norm

# binomial distribution with n **= 50 and p = 0.8
p = 0.8
n = 50

binom = []
for k in range(0, n+1):
	c = float(factorial(n)) / (factorial(k) * factorial(n-k))
	prob = c * p ** k * (1-p) ** (n-k)
	binom.append(prob)

# normal distribution with n **= 50 and p = 0.8
mu = n * p # Expected Value
var = n * p * (1 - p) # variance
sigma = var ** 0.5 # standard deviation

x = range(0, n + 1)
norm = norm.pdf(x, mu, sigma)

plt.bar(range(25, n + 1), binom[25:], alpha=0.3)
plt.plot(range(25, n + 1), norm[25:], 'g-')
plt.show()
```

* Example
```Python
from scipy import stats as st
import math as mt

binom_n = 5000
binom_p = 0.15

clicks = 715

mu = binom_n * binom_p
sigma = mt.sqrt(binom_n * binom_p * (1 - binom_p))

p_clicks = st.norm(mu, sigma).cdf(clicks)
print(p_clicks) # .08284191945650154
```