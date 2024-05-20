See: 
* [[Py - Introduction to Python]]
* [[Py - Numpy (Methods)]]
Resources

---
# Creating Vectors
* Any numerical data can be represented as a **vector**
* Vector -- an ordered set of numerical data in mathematics
	* Vector operations include any operations that can be performed with numbers
	* Vector operations are faster (in Python)
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
import numpy as np
import pandas as pd

ratings_values = [[68,18], [81,19], [81,22], [15,75], [75,15], [17,72], [24,75], [21,91], [76, 6], [12,74], [18,83], [20,62], [21,82], [21,79], [84,15], [73,16], [88,25], [78,23], [32, 81], [77, 35]]
ratings = pd.DataFrame(ratings_values, columns=['Price', 'Quality'])

price = ratings['Price'].values # Create a vector of all values
quality = ratings['Quality'].values # Creat a vector of all values
visitors_count = len(ratings['Quality'].values) # Find length of vector
visitor4 = ratings.loc[4].values # Find the 5th vector
vector_list = list(ratings.values) # Convert array into a list of vectors
```