See: 
* [[Py - Introduction to Python]]
* [[Py - NumPy (Methods)]]
* [[Py - Pandas (Methods)]]
* [[Py - Matplotlib (Methods)]]
Resources
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)

---

##### `scipy.spatial.distance.euclidean()`
* Computes the Euclidean distance between two 1-D arrays
	* Arguments
		* `u` -- an array-like structure specifying the input array.
		* `v` -- an array-like structure specifying the input array.
		* `w=` -- an optional array-like structure specifying the  weights for each value in `u` and `v`. 
			* Default is `None`, which gives each value a weight of 1.0
```Python
import numpy as np
from scipy.spatial import distance

a = np.array([5, 6])
b = np.array([1, 3])
d = distance.euclidean(a, b)
print('Distance between a and b is', d) # Distance betweeen a and b is 5.0
```


##### `scipy.spatial.distance.cityblock()`
* Computes the City Block (Manhattan) distance
	* Arguments
		* `u` -- an array-like structure specifying the input array.
		* `v` -- an array-like structure specifying the input array.
		* `w=` -- an optional array-like structure specifying the  weights for each value in `u` and `v`. 
			* Default is `None`, which gives each value a weight of 1.0
```Python
import numpy as np

def manhattan_distance(first, second):
    return np.abs(first - second).sum()

first = np.array([3, 11])
second = np.array([1, 6])

print(manhattan_distance(first, second))
```
