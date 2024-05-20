See:
* [[Py - Introduction to Python]]
* [[Py - Numpy (Installing & Importing Numpy)]] 
Documentation
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Numpy Documentation](https://numpy.org/doc/stable/index.html)


---
# Numpy Classes
##### `RandomState()`
* A class in the `numpy.random` module that generates a pseudo-random state number
	* Arguments
		* `seed` -- Random seed used to initialize the pseudo-random number generator
```Python
import numpy.random 

state = random.RandomState() # Creating a pseudo-random state
```

# Numpy Methods

##### `np.arange()`
* Returns evenly spaced values within a given interval
	* Arguments
		* `start` -- (default is 0); the start of interval (including this number)
		* `stop` -- (default is the end); the end of the interval (not including this number)
		* `step` -- (default is 1); spacing between values 
		* `dtype=` -- the type of the output array
		* `like=` -- references object to allow the creation of arrays which are not NumPy arrays
```Python
```

##### `np.array()`
* Creates an array (vector)
	* Arguments
		* `object` -- the object to convert into an array
		* `dtype=` -- the desired data-type for the array; if left blank, numpy will try to fit it
		* `copy=` -- (default is `True`); copies the object
		* `order=` -- specifies the memory layout of the array
		* `ndmin=` -- an int specifying the min number of dimensions the array should have
		* `like=` -- references object to allow the creation of arrays which are not NumPy arrays
```Python
# Example -- Creating a numpy array from a Python list
import numpy as np

numbers1 = [2, 3] # Python List
print(numbers1) # [2, 3]

vector1 = np.array(numbers1) # Create NumPy array from list
print(vector1) # [2 3]
```

```Python
# Example -- Creating a numpy array from scratch
import numpy as np

vector2 = np.array([6, 2])
print(vector2) # [6 2]
print(len(vector2)) # 2
```

```Python
# Example -- Converting a DataFrame structure into a vector
import pandas as pd

data = pd.DataFrame([1, 7, 3]) 
print(data[0].values) # [1 7 3]
```


##### `np.var()`
* Returns the variance of the array elements, a measure of the spread of a distribution
	* `x` -- the value on which the operation is called
```Python
import numpy as np

x = [1, 2, 3, 4, 5, 6] # dataset
variance = np.var(x) # 2.9166666666666665
```

##### `np.std()` 
* Returns the standard deviation, a measure of the spread of a distribution, of the array elements
	* Arguments:
		* `x` -- the value on which the operation is called
```Python
import numpy as np

x = [1, 2, 3, 4, 5, 6] # dataset
standard_deviation = np.std(x) # 1.707825127659933
```

##### `np.sqrt()`
* Return the non-negative square-root of an array, element-wise 
	* Arguments
		* `variance` -- the variance to calculate standard deviation from
```Python
import numpy as np

variance = 2.9166666666666665 # the variance
standard_deviation = np.sqrt(variance) # # 1.707825127659933
```