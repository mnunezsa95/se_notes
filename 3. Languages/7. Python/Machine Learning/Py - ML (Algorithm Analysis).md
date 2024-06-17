See:
* [[Py - Introduction to Python]]
* [[ML - Machine Learning Basics]]
* [[Py - Sklearn (Models & Model Comparison)]]
* [[ML - Supervised Learning]]
Resources
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)

---
# Computational Complexity
* Definitions
	* Computational Complexity (Asymptotic Running Time) -- the amount of resources required to run the algorithm
	* Algorithm Running Time -- the length of time it takes for it to run as a function, measured by number of operations (not seconds)
	* Real Running Time -- The running time on a given computer
	
* Determining Algorithm Run Time
	* Algorithm Run Time is affected by:
		* Arguments
		* Number of operations
* Complexities
	* Linear Complexity 
		* Example:
			* $T(n) = 4n+ 3$      $-->$     $T(n) ~ n$
	* Quadratic Complexity 
		* Example:
			* $T(n) = 5n^2 + 3n - 1$      $-->$     $T(n) ~ n^2$
	* Cubic Complexity
		* Example:
			* $T(n) = 10n^3 - 2n^2$      $-->$     $T(n) ~ n^3$
	* Constant Complexity -- Computational Complexity does not depend on $n$
		* Example:
			* $T(n) = 10$      $-->$     $T(n) ~ 1$
			
```Python
def increase(elements):
    n = len(elements)     # 2 operations
    for i in range(n):    # 1 operation + 2 operations * n
        elements[i] += 1  # 2 operations (for every value of i)

# T(n) = 2 + 1 + n * (2 + 2) = 4n + 3
```


# Linear Regression Training Time
#### Understanding Linear Regression Training Time
* The Linear Regression Training Objective
	* Fromula: $$ w = \text{argmin}(MSE(Xw, y)) $$
* Weight Calculation
	* Formula: $$w = (X^TX)^-1X^Ty$$
* Definitions:
	* $n$ = number of observations
	* $p$ = number of features
* Knowns
	* Size of Matrix X --> $n\;x\;p$
	* Size of Vector Y --> $n$
	* Computational Complexity is defined as $T(n,p)$
		* Depends on two parameters $n$ and $p$


#### Calculating Linear Regression Training Time
* Step 1: Multiply Matrix X, by its transpose 
	* Complexity: $T(n,p) ~ np^2$
```Python
# Multiply Matrix X, by its transpose 

X.T.dot(X)
```

* Step 2: Find the inverse of the Matrix 
	* Complexity: $T(n,p) ~ p^3$
	
* Step 3: Multiply the Inverse Matrix by the Transpose of Matrix X
	* Complexity: $T(n, p) ~np^2$
	
* Step 4: Multiply the result by Vector y
	* Complexity : $T(n,p) ~ np$

* Step 5: Compute the Result $$T(n,p) ~ np^2 + p^3 +np^2 + np$$ $$ T(n,p) ~ np^2$$

# Direct & Iterative Methods
#### Direct Methods
* Direct Methods -- methods that help find a precise solution using a given formula or algorithm
	* Direct methods' computational complexity is independent of the data
	* Performs the same matrix operations regardless of data

#### Iterative Methods
* Iterative Methods -- methods that help find an approximate solution (not precise) using a formula or algorithm
	* Iterative methods' computation complexity is dependent on the number of steps (and amount of data)
	
* Bisect Method -- a method used to find the roots of a polynomial equation
	* The Bisect Method is an example of an iterative method
	* Works for any continuous function
	* Process
		* Repeats the following steps while the right value minus left value is greater than the margin of error:
			* Checks if $f(a)$ or $f(b)$ equal zero
				* If yes, the solution was found
			* Find the middle segment using: $c = (a + b) / 2$
			* Compares the sign of $f(c)$ with the signs of $f(a)$ and $f(b)$
				* If $f(c)$ and $f(a)$ have opposite signs, the root lies within the interval $[a,c]$. The algorithm will analyze this segment in the next iteration.
				- If $f(c)$ and $f(b)$ have opposite signs, the root is within the interval $[b,c]$. The algorithm will analyze this segment in the next iteration.
				- Since $f(a)$ and $f(b)$ have different signs, there are no other possibilities.
```Python 
# Bisect Method

import math

def bisect(function, left, right, error):
    while right - left > error:
        if function(left) == 0:
            return left
        if function(right) == 0:
            return right
            
        middle = (left + right) / 2
	        
        if function(left) * function(middle) < 0:
            right = middle
        else:
            left = middle
    return left


def f1(x):
    return x ** 3 - x ** 2 - 2 * x


def f2(x):
    return (x + 1) * math.log10(x) - x ** 0.75


print(bisect(f1, 1, 4, 0.000001))
print(bisect(f2, 1, 4, 0.000001))
```

- Finding the Roots by hand
	- Process: Using Quadratic Formula
		- Identify the formula:
			- $ax^2 + bx + c = 0$
		- Identify the coefficients for $a$, $b$, and $c$
		- Calculate the discriminate 
			- $D = sqrt(b^2 - 4ac)$ 
		- Compute the roots
			- $x1 = (-b +- D)/(2a)$
				- If $D >0$, the quadratic has two roots
				- If $D =0$, the quadratic has one root
				- If $D <0$,  the quadratic has zero roots
	* Example
		$2x^2 + 3x -2 = 0$     $-->$     $a = 2,  b=3, c=-2$   
		$sqrt(D) = b^2 - 4ac = 3^2 - 4(2)(-2) = 9 + 16 = sqrt(25) = 5$
		$(-b+-D)/(2a)$     $-->$     $(-3+-5)/(2(2)) = 0, 0.5, -2$
		