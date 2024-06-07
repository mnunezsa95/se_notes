See:
* [[Py - Introduction to Python]]
* [[Py - NumPy (Installing & Importing Numpy)]] 
* [[Py - Pandas (Methods)]]
* [[Py - Matplotlib (Methods)]]
* [[Py - SciPy (Methods)]]
Resources:
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)


---

# NumPy Attributes
##### `np.shape`
* Returns the shape of an array or matrix
```Python
import numpy as np

A = np.array([
    [1, 2, 3], 
    [2, 3, 4]
])

print('Size:', A.shape) # Size: (2, 3) 
```

##### `numpy.matrix.T`
* Returns the transpose of a matrix
```
```

# NumPy Classes
##### `RandomState()`
* A class in the `numpy.random` module that generates a pseudo-random state number
	* Arguments
		* `seed` -- Random seed used to initialize the pseudo-random number generator
```Python
import numpy.random 

state = random.RandomState() # Creating a pseudo-random state
```

# NumPy Methods

##### `np.arange()`
* Returns evenly spaced values within a given interval
	* Arguments
		* `start` -- (default is 0); the start of interval (including this number)
		* `stop` -- (default is the end); the end of the interval (not including this number)
		* `step` -- (default is 1); spacing between values 
		* `dtype=` -- the type of the output array
		* `like=` -- references object to allow the creation of arrays which are not NumPy arrays
```Python
import numpy as np

matrix = np.array([
    [1, 2], 
    [4, -4], 
    [0, 17]
])

matrix.T
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

##### `np.exp()`
* Calculates the exponential of all elements in the input array
	* Arguments
		* `x` -- input values
		* `out=` -- a location into which the result is stored
		* `where=` -- this condition is broadcast over the input. At locations where the condition is True, the out array will be set to the ufunc result. 
```Python
import numpy as np

def logistic_transform(values):
    return 1 / (1 + np.exp(-values))
    
our_values = np.array([-20, 0, 0.5, 80, -1])
print(logistic_transform(our_values))
```


##### `np.dot()`
* Dot product of two arrays
	* Arguments
		* `a` -- first argument
		* `b` -- second argument
		* `out=` -- output argument; This must have the exact kind that would be returned if it was not used
```Python
import numpy as np

volume = np.array([0.3, 0.2, 0.25])
content = np.array([0.6, 0.7, 1])

print(np.dot(volume, content)) # 0.57
```

##### `np.argmin()`
* Returns the indices of the minimum values along an axis
	* Arguments
		* `a` -- the input array
		* `axis=` -- by default, the index is into the flattened array, otherwise along the specified axis.
		* `out=` -- If provided, the result will be inserted into this array.
		* `keepdims=` -- If this is set to `True`, the axes which are reduced are left in the result as dimensions with size one. 
```Python
taxi_distances = []
for taxi in taxis:
    taxi_vector = np.array([avenues[taxi[0]], streets[taxi[1]]])
    taxi_distances.append(distance.cityblock(address_vector, taxi_vector))

index = np.array(taxi_distances).argmin()
print(taxis[index]) # ['3rd', '76']
```


##### `np.argsort()`
* Performs an indirect sorting operation along the specified axis, utilizing the algorithm defined by the "kind" keyword. It then outputs an array of indices with the same shape as the input array, arranging them in ascending order along the designated axis.
	* Arguments
		* `a` -- the array to sort
		* `axis=` -- axis along which to sort. The default is -1 (the last axis). If None, the flattened array is used
		* `kind=` -- (default is `quicksort`); specifies the sorting algorithm to use
			* `quicksort`
			* `mergesort`
			* `heapsort`
			* `stable`
		* `order=` -- specifies which fields to compare first, second, etc
```Python
distances = []
for i in range(df_realty.shape[0]):
    value = distance.euclidean(preference_vector, df_realty.loc[i])
    distances.append(value)

best_index = np.array(distances).argsort()[1]
```

##### `np.multiply()`
* Multiply arguments element-wise.
	* Arguments
		* `x1` -- first element, must have same shape as `x2`
		* `x2` -- second element, must have same shape as `x1`
		* `out=` -- A location into which the result is stored. 
		* `where=` -- This condition is broadcast over the input.
```Python
import numpy as np

matrix1 = np.array([
    [1, 2], 
    [3, 4]])

matrix2 = np.array([
    [5, 6], 
    [7, 8]])

np.multiply(matrix1, matrix2)
```

##### `np.linalg.inv()`
* Computes the inverse of a matrix
	* Arguments
		* `matrix` -- the matrix to be inverted
```Python
a = np.array([[1., 2.], [3., 4.]])

# Invert the matrix
inverse_a = linalg.inv(a)
np.allclose(np.dot(a, inverse_a), np.eye(2)) # True
np.allclose(np.dot(inverse_a, a), np.eye(2)) # True
```