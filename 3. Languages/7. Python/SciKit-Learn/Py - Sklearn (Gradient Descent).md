See:
* 
Resources:
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)

---
# Loss Function Minimization

* Formula: 
	* $y$ -- the number of correct answers
	* $a$ -- the number of predictions
$$w = arg\;min_w\;L(y,a)$$

* Mean Squared Error (MSE) or Quadratic Loss Function
	* Square the difference between number of correct answers and predictions
	* Formula: $$ L(y,a) = sum^n_(i=1)(a_i - y_i)^2 $$
* Absolute Loss Function (MAE) 
	* Less sensitive to outliers
	* Formula: $$L(y,a) = sum^n_(i=1)|a_i - y_i|$$
* Negative Logarithmic Likelihood (Logistic Loss Function) 
	* Adds up the logarithms of probabilities depending on the observation
	* Can be used instead of accuracy because it has a derivative 
	* The Loss function relies on algorithm parameters.
	- Is a vector-valued function, taking a vector as input and producing a scalar output.
	* Fromula: 
		* $a_i$ -- the probability of class 1 for observation with index $i$
			* The value of $a_i$ should be as high as possible for a positive class observation, The value of $a_i$ should be as low as possible for a negative class observation.
$$L(y, a) = - \sum_{i=1}^{n} \left\{ \begin{array}{c} \displaystyle \log_{10} a_i \;\text{ if } y_i = 1 \\[1ex] \displaystyle (\log_{10}(1 - a_i) \; \text{ if } y_i = 0 \end{array} \right.$$
```Python
from math import log10

result = -1 * (log10(1 - 0.2) + log10(1 - 0.4) + log10(0.6) + log10(0.8) + log10(1 - 0.1))

print(result)
```

# Function Gradient
* The gradient of a vector-valued function is a vector consisting of derivatives of the answer for each argument.
* The gradient shows the direction in which the function increases the fastest
	* Formula: 
		* $(∂f)/(∂x_i)$ -- the partial derivative of the function $f$ for the argument $x_i$
$$∇f(x) = ((∂f)/(∂x_i), (∂f)/(∂x_2), ..., (∂f)/(∂x_n))$$
* The negative gradient shows the direction in which the function decreases the fastest
	* Formula:
$$-∇f(x)$$

##### Examples:
* Example: The function gradient for one argument is the derivative:
$$f(x)=(x-5)^2$$
$$∇f(x) = ∇(x^2 -10x+25) = 2x-10$$
* Example: The function gradient of a three-argument function:
$$f(x,y,z)= x^2 + 2y^2 + 10yz - 5z$$
$$(∂f(x,y,z))/(∂x) = (∂x^2)/(∂x) + (∂(2y^2))/(∂x) + (∂(10yz))/(∂x) - (∂(5z))/((∂x)) = 2x + 0 + 0 +0$$
$$(∂f(x,y,z))/(∂x) =  0 + 4y + 10z +10$$
$$(∂f(x,y,z))/(∂x) = 0 + 0 + 10y - 5$$
$$∇f(x,y,z) = 2x,4y+10z, 10y-5$$
* Example: The function gradient of a two-argument function:
$$f(x,y)=2x^2 + 3y-5x +20$$
$$(∂f(x,y))/(∂x) = (∂(2x^2))/(∂x) + (∂(3y))/(∂x) - (∂(5x))/(∂x) = 4x + 0 - 5 + 0$$
$$(∂f(x,y))/(∂y) = (∂(2x^2))/(∂y) + (∂(3y))/(∂y) - (∂(5x))/(∂y) + 20 = 0 + 3 + 0 +0 $$
$$∇f(x,y) = 4x-5, 3$$

* Example: Find the gradient of a three-argument function:
$$f(x,y,z)= 3x^2 + 2y^2 + 3xy - 3z$$
$$(∂f(x,y,z))/(∂x) = (∂(3x^2))/(∂x) + (∂(2y^2))/(∂x) + (∂(5xy))/(∂x) - (3z)/(∂x) = 6x + 0 + 3y + 0$$
$$(∂f(x,y,z))/(∂y) = (∂(3x^2))/(∂y) + (∂(2y^2))/(∂y) + (∂(5xy))/(∂y) - (3z)/(∂y) = 0 + 4y + 3x + 0$$
$$(∂f(x,y,z))/(∂z) = (∂(3x^2))/(∂z) + (∂(2y^2))/(∂z) + (∂(5xy))/(∂x) - (3z)/(∂z) = 0 + 0 - 0 -3$$
$$∇f(x,y,z) = (6x+3y, 4y+3x, -3)$$

# Gradient Descent
* **Gradient descent** is an iterative method used to pinpoint the minimum of a loss function. This approach involves consistently moving in the direction opposite to the gradient, gradually moving closer to the minimum value.
	- The process of the gradient descent algorithm can be likened to a continuous descent towards the bottom, achieved through repetitive actions.
	- Reaching the minimum in a single iteration is challenging, as the negative gradient vector guides the descent towards decreasing values rather than directly pinpointing the precise minimum point of the loss function.
	
- How to Perform a Gradient Descent
	- Select the **initial value** for the argument (vector _x_), denoted as x⁰.
	- Incorporate the negative gradient scaled by the gradient descent magnitude, represented by $mu$.
	    - The parameter μ regulates the magnitude of the gradient descent step.
	        - When $mu$ is small, the descent progresses through numerous steps, with each bringing the solution closer to the minimum of the loss function.
	        - Conversely, if $mu$ is large, there's a risk of overshooting the minimum.
$$X^1 - X^0 + mu*(-∇f(x))$$
	- Iterate to derive the argument values for subsequent steps. 
		- The number of iterations is denoted by $t$.
	- Scale the negative gradient by the step size and add the resulting product to the previous point.
	$$x^t=x^(t-1)-mu*∇f(x^(t-1))$$
* The gradient descent is complete when:
	* The algorithm completes the required number of iterations
	* The value of $x$ stops changing

##### Examples
* Example 1: Calculate the x value and the loss function value after four iterations of gradient descent.
	* $u$ = 0.4
	* $x^0$ = 0 
	* $t$ = 4
$$f(x) = (x-10)^2$$

	* Find the Derivative of $f(x)$: $$f'(x) = 2(x-10)$$

	* Iteration 0: 
		* Set Initial Value:$$x^0 = 0 $$
		* Calculate Iteration: $$f'(x) - 2(0-10) = -20$$
		* Update Rule: $$x^1 = x^0 - mu * f'(x^0) = 0 -0.4*(-20) = 0 + 8 = 8$$
		* Loss Function Value: $$f(x^1) = (8-10)^2 = 4$$
	* Iteration 1:
		* Set Initial Value:$$x^1=8$$
		* Calculate Iteration: $$f'(x^1)=2(8−10)=−4$$
		* Update Rule: $$x^2=x^1−u⋅f'(x^1)=8−0.4*(−4)=8+1.6=9.6$$
		* Loss Function Value: $$f(x^2)=(9.6−10)^2=0.64$$
	* Iteration 2: 
		* Set Initial Value: $$x^2=9.6$$
		- Calculate Iteration: $$f'(x^2)=2(9.6−10)=−0.8$$
		- Update Rule: $$x^3=x^2−u⋅f'(x^2)=9.6−0.4×(−0.8)=9.6+0.32=9.92$$
		- Loss Function Value: $$f(x^3)=(9.92−10)^2=0.032$$
	- Iteration 3: 
		- Set Initial Value: $$x^3=9.92$$
		- Calculate Iteration: $$f'(x^3)=2(9.92−10)=−0.16$$
		- Update Rule: $$x^4=x^3−u⋅f'(x^3)=9.92−0.4×(−0.16)=9.92+0.064=9.984$$
		- Loss Function Value: $$f(x^4)=(9.984−10)^2=0.00256$$
	- Result
	$$x=9.984, f(x)=0.000256$$
	