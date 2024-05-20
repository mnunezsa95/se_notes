See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]], [[Py - Numpy (Installing & Importing Numpy)]] [[Py - Pandas (Sample Space Probability)]]
Documentation
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Numpy Documentation](https://numpy.org/doc/stable/index.html)

---
#### Creating a Probability Distribution Table in Python
* Create an array a numpy array object
* Calculate the number of times each outcome occurs (the numerator when calculating probabilities).  
* Example
```Python
import numpy as np 

spots = np.array( # Create an array with the possible ouctomes
  [
    [2, 3, 4, 5, 6, 7], 
    [3, 4, 5, 6, 7, 8], 
    [4, 5, 6, 7, 8, 9], 
    [5, 6, 7, 8, 9, 10], 
    [6, 7, 8, 9, 10, 11], 
    [7, 8, 9, 10, 11, 12] 
  ] 
)

spot_counts = {} # The keys of the dictionary will represent each unique outcome (the total number of spots), and the values will indicate the number of times each outcome can occur.

for i in range(0, 6):
  for j in range(0, 6):
    if spots[i][j] not in spot_counts.keys():
      spot_counts[spots[i][j]] = 1
    else:
      spot_counts[spots[i][j]] += 1

print(spot_counts) 
# {2: 1, 3: 2, 4: 3, 5: 4, 6: 5, 7: 6, 8: 5, 9: 4, 10: 3, 11: 2, 12: 1}

spot_probs = {}
for k in spot_counts:
  spot_probs[k] = spot_counts[k]/36

print(spot_probs)

'''{
 2: 0.027777777777777776,
 3: 0.05555555555555555,
 4: 0.08333333333333333,
 5: 0.1111111111111111,
 6: 0.1388888888888889,
 7: 0.16666666666666666,
 8: 0.1388888888888889,
 9: 0.1111111111111111,
 10: 0.08333333333333333,
 11: 0.05555555555555555,
 12: 0.027777777777777776}
'''
```

#### Graphing Probability Distribution Table
* `ndarray.reshape()` -> Gives a new shape to an array without changing its data (see [documentation](https://numpy.org/doc/stable/reference/generated/numpy.reshape.html#numpy.reshape))
* Example
```Python
import pandas as pd 

pd.Series(spots.reshape(36)).hist(density=True,bins=11)
```