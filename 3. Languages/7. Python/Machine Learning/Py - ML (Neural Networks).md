See:
* [[Py - Introduction to Python]]
* [[Py - NumPy (Vectors)]]
* [[Py - NumPy (Matrices)]]
* [[Py - NumPy (Methods)]]
* [[Py - ML (Algorithm Analysis)]]
* [[Py - Creating Classes in Python]]
* [[Py - ML (Neural Networks)]]
Resources:
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)


---
# Neural Network Basics
* A **Stochastic Gradient Descent** can be used to train neural networks
* A **neural network** is a model that consists of many simple models (for example many linear regression models)
* In Neural Networks, each neuron, builds complex relationships between input data and output data.
	* Example: a neural network with three inputs $x_1$, $x_2$, $x_3$ and two outputs $a_1$, $a_2$:
		![[neural-network-example.png]]
		* The value at each output, or neuron, is calculated in the same way as a linear regression prediction: 
			* Here, x is a vector, x = ($x_1$, $x_2$, $x_3$).
			* Each output value has its own weights ($w_1$ and $w_2$). $$a_1 = XW_1$$ $$ a_2=XW_2$$
	* Example 2: A network has three inputs  $x_1$, $x_2$, $x_3$ two hidden variables $h_1$ and $h_2$ and one output $a$.
		![[neural-network-example-2.png]]
		* Values $h_1$ and $h_2$ are passed to the logistic function $sigma(x)$
			* $e$ -- Euler's number (approximately 2.718281828): $$sigma(x) = 1 / (1+e^-x)$$
#### Logistic Function in Neural Networks
* The logistic function in a neural network is called an **activation function**
	* The activation function is included in the neuron after the input values are multiplied by their weights, allows the neuron output to become an input for other neurons: 
		* Hidden Variable 1 is equal to input value ($X$) multiplied by a weight ($W$) $$h_1 = XW_1$$
		* Hidden Variable 2 is equal to input value ($X$) multiplied by a weight ($W$) $$h_2 = XW_2$$
		* Hidden Variables $h_1$ and $h_2$ are denoted as vector $h$. The formula for calculating neural network predictions becomes: $$a=sigma(h)W_3$$
		* Weights $W_1$ and $W_2$ are denoted as columns of Matrix $W$, the final formula becomes: $$a = sigma(xW)W_3$$

# Training of Neural Networks
* Any neural network can be written as a function from its input vector and parameters
	* $X$ -- training set features
	* $P$ -- set of all neural network parameters
	* $N(X,P)$ -- neural network function
	
* Example: Look at the following network
		![[neural-network-example-3.png]]
	* Neural Network Parameters are weights in neurons: $$P = W_1, W_2, W_3$$
	* The Neural Network Function:
		* x -- input vector with dimension p (number of features)
		* $W_1$ -- matrix with dimension $p\;x\;m$
		* $W_2$ -- matrix with dimension $m\;x\;k$
		* $W_3$ -- matrix with dimension $k\;x\;1$
		* $a$ -- model prediction (single number) $$a = N(X,P) = sigma(sigma(xW_1)W_2)W_3$$
	* The objective of Neural Network training can be described as:
		* $y$ -- training set answers (`train_target`)
		* $L(a,y)$ -- loss function (for example, MSE) $$min_p L(N(X,P),y)$$
	* The minimum of this function can be found using SGD algorithm. The neural network learning algorithm is the same as the SGD algorithm for linear regression $$∇L(N(X,P),y)$$

