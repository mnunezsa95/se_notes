See [[Py - Introduction to Python]], [[Py - Pandas (Sample Space Probability)]], [[Py - Numpy (Probability Distributions and Value Intervals)]], 
Documentation
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Numpy Documentation](https://numpy.org/doc/stable/index.html)
* [SciPy Documentation](https://docs.scipy.org/doc/scipy/reference/stats.html)

---

#### Combinations
* Combinations can be solved using the combination formula: (see [[DS - The Binomial Distribution]])
	![](https://lh7-us.googleusercontent.com/nFl43y9V1-t_NtKii4Y11eFGilzW2oRB49RgwSwJxmQMy2zd6sA-cDskjSr36EJGMl7UQtb4GG15apKOXQ61L-AUWm_A5k_M1cSvLOJ_ktE19nXzakqbnXKOurf2ul4u-_K594W69V6VIZEE6Oj-d9w)
* In Python, this can be solved using the factorial function of the math library
```Python
from math import factorial

c = factorial(14)/(factorial(3)*factorial(11))
print(c) # 364.0
```

#### Binomial Distribution
* Conditions for a random variable to have a binomial distribution
	* A finite, fixed number of trials (`n`) are conducted
	* Every trial is a simple binomial experiment experiment with exactly two outcomes
	* The trials are independent of each other
	* The probability of success (`p`) is the same for all `n` trials
* Formula:
$$ C^k_n p^k(1-p)^n-^k$$
* Example
	* Given: n = 5, p = 0.5
```Python
from matplotlib import pyplot as plt
from math import factorial

n = 5
p = 0.5

distr = []
for k in range(0, n + 1):
  choose = factorial(n)/(factorial(k) * factorial(n-k))
  prob = choose * p**k * (1-p) ** (n-k)
  distr.append(prob)

plt.bar(range(0, n+1), distr)
```

#### Example from Exercise: Binomial Distribution
```Python
from matplotlib import pyplot as plt
from math import factorial

p = .20
n = 30

distr = []

for k in range(0 , n + 1):
    c = factorial(n) / (factorial(k) * factorial(n-k))
    distr.append(c * p**k * (1-p)**(n-k))

plt.bar(range(0, n+1), distr)
```