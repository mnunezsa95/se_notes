See: 
* [[Py - Introduction to Python]]
* [[Py - Numpy (Methods)]]
* [[Py - Matplotlib (Methods)]]
Resources
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)

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

# Representing Vectors
* Vectors are represented by a point or an arrow that connects the origin and the point
	* Arrows show direction and magnitude
	* Points do not show either
```Python
# Example -- Plotting vectors on a graph

import numpy as np
import matplotlib.pyplot as plt

vector1 = np.array([2, 3])
vector2 = np.array([6, 2])

plt.figure(figsize=(10, 10))
plt.axis([0, 7, 0, 7])
plt.plot([vector1[0], vector2[0]], [vector1[1], vector2[1]], 'ro')
plt.grid(True)
plt.show()
```
	![[plotting-vector-point.png]]
```Python
import matplotlib.pyplot as plt

ratings_values = [[68,18], [81,19], [81,22], [15,75], [75,15], [17,72], [24,75], [21,91], [76, 6], [12,74], [18,83], [20,62], [21,82], [21,79], [84,15], [73,16], [88,25], [78,23], [32, 81], [77, 35]]

ratings = pd.DataFrame(ratings_values, columns=['Price', 'Quality'])
plt.figure(figsize=(3.5,3.5))
plt.axis([0, 100, 0, 100])
price = ratings['Price'].values
quality = ratings['Quality'].values
plt.plot(price, quality, 'ro')
plt.xlabel('Price')
plt.ylabel('Quality')
plt.grid(True)
plt.show()
```
	![[plotting-vector-arrow2.png]]


```Python
# Example -- Plotting vectors on a graph (as an arrow)

import numpy as np
import matplotlib.pyplot as plt

vector1 = np.array([2, 3])
vector2 = np.array([6, 2])

plt.figure(figsize=(10, 10))
plt.axis([0, 7, 0, 7]) # Define the axis points

# Arrow from origin to vector1[0] (2) to vector1[1] (3)
plt.arrow(0, 0, vector1[0], vector1[1], head_width=0.3, 
		  length_includes_head="True", color='b')

# Arrow from origin to vector1[0] (6) to vector1[1] (2)
plt.arrow(0, 0, vector2[0], vector2[1], head_width=0.3,
		  length_includes_head="True", color='g')
plt.plot(0, 0, 'ro')
plt.grid(True)
plt.show()
```
	![[plotting-vector-arrow.png]]


# Adding and Subtracting Vectors
* Vectors of the same size can be added or subtracted
* When adding or subtracting vectors, the operation is performed for each element of the vectors
	![[table-adding-subtracting-vectors.png]]

```Python
import numpy as np
import matplotlib.pyplot as plt

# Adding Vectors
vector1 = np.array([2, 3])
vector2 = np.array([6, 2])
sum_of_vectors = vector1 + vector2
print(sum_of_vectors) # [8, 5] -- x1 + y1 + x2 + y2

# Subtracting Vectors
difference_of_vectors = vector2 - vector1
print(difference_of_vectors) # [4 -1] 

# Plotting Vectors
vector1 = np.array([2, 3])
vector2 = np.array([6, 2])
sum_of_vectors = vector1 + vector2
subtraction = vector2 - vector1

plt.figure(figsize=(10.2, 10))
plt.axis([0, 8.4, -2, 6])

arrow1 = plt.arrow(0, 0, vector1[0], vector1[1], head_width=0.3, 
	length_includes_head="True", color='b')
	
arrow2 = plt.arrow(0, 0, vector2[0], vector2[1], head_width=0.3, 
	length_includes_head="True", color='g')
	
arrow3 = plt.arrow(0, 0, sum_of_vectors[0], sum_of_vectors[1], head_width=0.3,
	length_includes_head="True", color='r')
	
arrow4 = plt.arrow(0, 0, subtraction[0], subtraction[1], head_width=0.3,
	length_includes_head="True", color='m')
	
plt.plot(0, 0, 'ro')
plt.legend(
	[arrow1, arrow2, arrow2, arrow3],
	['vector1', 'vector2', 'sum_of_vectors', 'subtraction'],
	loc='upper left'
)
plt.grid(True)
plt.show()
```
	
	![[plotting-addition-subtraction-vectors.png]]

* Plotting a vector going in a negative direction
```Python
import numpy as np
import matplotlib.pyplot as plt

vector1 = np.array([2, 3])
vector2 = np.array([6, 2])
sum_of_vectors = vector1 + vector2
subtraction = vector2 - vector1

plt.figure(figsize=(10.2, 10))
plt.axis([0, 8.4, -2, 6])

arrow1 = plt.arrow(0, 0, vector1[0], vector1[1], head_width=0.3, 
	length_includes_head="True", color='b')
	
arrow2 = plt.arrow(0, 0, vector2[0], vector2[1], head_width=0.3, 
	length_includes_head="True", color='g')
	
arrow4 = plt.arrow(0, 0, subtraction[0], subtraction[1], head_width=0.3,
	length_includes_head="True", color='m')
	
# Plotting vector in negative direction
arrow1new = plt.arrow(vector2[0], vector2[1], -vector1[0], -vector1[1],
	head_width=0.3, length_includes_head="True", color='b')
	
plt.plot(0, 0, 'ro')
plt.legend(
    [arrow1, arrow2, arrow4],
    ['vector1', 'vector2', 'subtraction'],
    loc='upper left'
)
plt.grid(True)
plt.show()
```
	
	![[plotting-vector-negative-direction.png]]

* Example: Vector Addition
```Python
import numpy as np
import pandas as pd

# Data
quantity_1 = [25, 63, 80, 91, 81, 55, 14, 76, 33, 71]
quantity_2 = [82, 24, 92, 48, 32, 45, 4, 34, 12, 1]
models = ['Silicone case for iPhone 8', 'Leather case for iPhone 8',
		  'Silicone case for iPhone XS', 'Leather case for iPhone XS',
		  'Silicone case for iPhone XS Max', 'Leather case for iPhone XS Max',
		  'Silicone case for iPhone 11', 'Leather case for iPhone 11',
		  'Silicone case for iPhone 11 Pro', 'Leather case for iPhone 11 Pro'
	]
	
# Create DataFrames
stocks_1 = pd.DataFrame({'Quantity' : quantity_1}, index=models)
stocks_2 = pd.DataFrame({'Quantity' : quantity_2}, index=models)

# Create vectors
vector_of_quantity_1 = stocks_1['Quantity'].values
vector_of_quantity_2 = stocks_2['Quantity'].values

# Add vectors
vector_of_quantity_united = vector_of_quantity_1 + vector_of_quantity_2

# Create result DataFrame
stocks_united = pd.DataFrame({'Quantity':vector_of_quantity_united},index=models)
print(stocks_united)
```

# Multiplying Vectors by a Scalar
* Vectors can be multiplied by a Scalar
* When multiplying vectors by a scalar, each coordinate of the vector is multiplied by the same number
	* If the number is negative, all coordinates also change their signs
* When multiplying by a positive number:
	* Vectors in a plane maintain their direction,
	* Arrows change length
* When multiplying by a negative number
	* Vectors flip in in the opposite direction
	* Arrows change length
		![[table-multiplying-vectors.png]]
```Python
# Example -- Multiplying by positive number
import numpy as np

vector1 = np.array([2, 3])
vector3 = 2 * vector1
print(vector3) # [4, 6]
```

* Performing an operation with a number and an array, each item in the array undergoes the same operation, creating a new array of the same size.
```Python
import numpy as np

array2 = np.array([1, 2, 3, 4])
array2_plus_10 = array2 + 10
array2_minus_10 = array2 - 10
array2_div_10 = array2 / 10
print('Sum: ', array2_plus_10) # Sum: [11 12 13 14]
print('Difference: ', array2_minus_10) # Difference: [-9 -8 -7 -6]
print('Quotient: ', array2_div_10) # Quotient:  [0.1 0.2 0.3 0.4]
```

```Python
# Example -- Multiplying by negative number
import numpy as np

vector1 = np.array([2, 3])
vector4 = -1 * vector1
print(vector4) # [-2 -3]
```

```Python
# Example
import numpy as np
import matplotlib.pyplot as plt

vector1 = np.array([2, 3])
vector3 = 2 * vector1
vector4 = -1 * vector1

plt.figure(figsize=(10.2, 10))
plt.axis([-4, 6, -4, 6])

arrow1 = plt.arrow(0, 0, vector1[0], vector1[1], head_width=0.3,
	length_includes_head="True", color='b')
	
arrow3 = plt.arrow(0, 0, vector3[0], vector3[1], head_width=0.3,
	length_includes_head="True", color='g')
	
arrow4 = plt.arrow(0, 0, vector4[0], vector4[1], head_width=0.3,
	length_includes_head="True", color='m')
	
plt.plot(0, 0, 'ro')
plt.legend(
    [arrow1, arrow3, arrow4],
    ['vector1', 'vector3', 'vector4'],
    loc='upper left',
)
plt.grid(True)
plt.show()
```

```Python
# Example

import numpy as np
import pandas as pd

quantity_1 = [25, 63, 80, 91, 81, 55, 14, 76, 33, 71]
models = ['Silicone case for iPhone 8', 'Leather case for iPhone 8',
		  'Silicone case for iPhone XS', 'Leather case for iPhone XS',
		  'Silicone case for iPhone XS Max', 'Leather case for iPhone XS Max',
		  'Silicone case for iPhone 11', 'Leather case for iPhone 11',
		  'Silicone case for iPhone 11 Pro', 'Leather case for iPhone 11 Pro',
	]
	
stocks_1 = pd.DataFrame({'Quantity': quantity_1}, index=models)
quantity_2 = [82, 24, 92, 48, 32, 45, 4, 34, 12, 1]
stocks_2 = pd.DataFrame({'Quantity': quantity_2}, index=models)

vector_of_quantity_1 = stocks_1['Quantity'].values
vector_of_quantity_2 = stocks_2['Quantity'].values
vector_of_quantity_united = vector_of_quantity_1 + vector_of_quantity_2

stocks_united = pd.DataFrame({'Qty':vector_of_quantity_united}, index=models)
stocks_united['Price'] = [30, 21, 32, 22, 18, 17, 38, 12, 23, 29]
price_united = stocks_united['Price'].values

# Multiplying the price
price_discount_10 = price_united * 0.9
stocks_united['10% discount prise'] = price_discount_10.astype(int)

# Dividing the price
price_no_discount =  price_discount_10 * 1.10
stocks_united['10% raise price'] = price_no_discount.astype(int)
print(stocks_united)
```

# Mean Value of Vectors
* The Mean Value of Vectors represents the average for a set of data points stored in a vector
* Calculating Mean Value of Vectors
	* Formula: $$bara = 1/n (a_1 + a_2 + ... + a_n)$$
```Python
import numpy as np

# Create vectors
vector1 = np.array([2, 3])
vector2 = np.array([6, 2])

# Calculate the mean
vector_mean = 0.5 * (vector1 + vector2)
print(vector_mean) # [4, 2.5]
```

```Python
import numpy as np
import matplotlib.pyplot as plt

vector1 = np.array([2, 3])
vector2 = np.array([6, 2])
vector_mean = 0.5 * (vector1 + vector2)

plt.figure(figsize=(10, 10))
plt.axis([0, 8.4, -1, 6])
arrow1 = plt.arrow(0, 0, vector1[0], vector1[1], head_width=0.3, 
	length_includes_head="True", color='b')
	
arrow2 = plt.arrow(0, 0, vector2[0], vector2[1], head_width=0.3,
	length_includes_head="True", color='g')
	
arrow_sum = plt.arrow(0, 0, vector1[0] + vector2[0], vector1[1] + vector2[1],
	head_width=0.3, length_includes_head="True", color='r')
	
arrow_mean = plt.arrow(0, 0, vector_mean[0], vector_mean[1], head_width=0.3,
	length_includes_head="True", color='m')
	
plt.plot(vector1[0], vector1[1], 'ro')
plt.plot(vector2[0], vector2[1], 'ro')
plt.plot(vector_mean[0], vector_mean[1], 'ro')
plt.legend(
    [arrow1, arrow2, arrow_sum, arrow_mean],
    ['vector1', 'vector2', 'vector1+vector2', 'vector_mean'],
    loc='upper left',
)
plt.grid(True)
plt.show()
```
	
	![[plotting-mean-vector.png]]


* Example 1:
```Python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

ratings_values = [[68,18], [81,19], [81,22], [15,75], [75,15], [17,72], [24,75], [21,91], [76, 6], [12,74], [18,83], [20,62], [21,82], [21,79], [84,15], [73,16], [88,25], [78,23], [32, 81], [77, 35]]
ratings = pd.DataFrame(ratings_values, columns=['Price', 'Quality'])

price = ratings['Price'].values
sum_prices = sum(price)
average_price_rat = sum(price) / len(price)

quality = ratings['Quality'].values
average_quality_rat = sum(quality) / len(quality)
average_rat = np.array([average_price_rat, average_quality_rat])

plt.figure(figsize=(7, 7))
plt.axis([0, 100, 0, 100])
plt.plot(average_rat[0], average_rat[1], 'mo', markersize=15)
plt.plot(price, quality, 'ro')
plt.xlabel('Price')
plt.ylabel('Quality')
plt.grid(True)
plt.title('Distribution of ratings and mean value for the whole sample')
plt.show()
```
	
	![[plotting-mean-value-example1.png]]

* Example 2:
```Python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

ratings_values = [[68,18], [81,19], [81,22], [15,75], [75,15], [17,72], [24,75], [21,91], [76, 6], [12,74], [18,83], [20,62], [21,82], [21,79], [84,15], [73,16], [88,25], [78,23], [32, 81], [77, 35]]

ratings = pd.DataFrame(ratings_values, columns=['Price', 'Quality'])
price = ratings['Price'].values
quality = ratings['Quality'].values

clients_1 = []
clients_2 = []
for client in list(ratings.values):
    if client[0] < 40 and client[1] > 60:
        clients_1.append(client)
    else:
        clients_2.append(client)

average_client_1 = sum(clients_1)/len(clients_1)
average_client_2 = sum(clients_2)/len(clients_2)

plt.figure(figsize=(7, 7))
plt.axis([0, 100, 0, 100])

plt.plot(average_client_1[0], average_client_1[1], 'bo', markersize=15)
plt.plot(average_client_2[0], average_client_2[1], 'go', markersize=15)
plt.plot(price, quality, 'ro')
plt.xlabel('Price')
plt.ylabel('Quality')
plt.grid(True)
plt.title('Distribution of ratings and mean value for each group')
plt.show()
```
	
	![[plotting-mean-value-example2.png]]


# Vectorized Functions
* Vectorized Functions -- Functions that are written using vectors (arrays)
	* Vectorized functions are FASTER than using loops & lists
* Creating vectorized functions 
	* Define the function & parameters
	* Call the function
```Python
import numpy as np

# Define Function
def min_max_scale(values):
	return (values - min(values)) / (max(values) - min(values))

# Pass in the values
our_values = np.array([-20, 0, 0.5, 80, -1]) 
print(min_max_scale(our_values)) # [0.    0.2   0.205 1.    0.19 ]
```

```Python
import numpy as np

# Define function 
    return 1 / (1 + np.exp(-values))

# Pass in the values
our_values = np.array([-20, 0, 0.5, 80, -1])
print(logistic_transform(our_values))
```

# Vectorization of Metrics
* Metric functions can be created to calculate metrics
	* These metric functions offer the benefit of being more efficient and quicker compared to other pre-existing functions.
* For example, functions can be manually created to calculate the following:
	* MSE
	* RMSE 
	* Etc
```Python
# Example -- Create MSE functions using sum() and mean()

import numpy as np

# Store the target and predictions as numpy arrays
target = np.array([0.9, 1.2, 1.4, 1.5, 1.9, 2.0])
predictions = np.array([1.0, 1.2, 1.4, 1.6, 1.8, 2.0])

# Create a metric function for MSE
def mse1(target, predictions):
    n = target.size
    return ((target - predictions) ** 2).sum() / n

# Create a metric function for MSE
def mse2(target, predictions):
    return ((target - predictions) ** 2).mean()

print(mse1(target, predictions), mse2(target, predictions)) 
# 0.0049999999999999975 0.0049999999999999975
```

```Python
# Example -- Create the MSE function

import numpy as np

# Create a metric function for MSE
def mae(target, predictions):
    return np.abs((target - predictions)).mean()

# Store the target and predictions as numpy arrays
target = np.array([0.9, 1.2, 1.4, 1.5, 1.9, 2.0])
predictions = np.array([1.0, 1.2, 1.4, 1.6, 1.8, 2.0])

# Call the function
print(mae(target, predictions)) # 0.04999999999999999
```

```Python
# Example -- Create the RMSE function

import numpy as np

# Create a metric function for RMSE
def rmse(target, predictions):
    return (((target - predictions) ** 2).mean()) ** 0.5

# Store the target and predictions as numpy arrays
target = np.array([0.9, 1.2, 1.4, 1.5, 1.9, 2.0])
predictions = np.array([1.0, 1.2, 1.4, 1.6, 1.8, 2.0])

# Call the function
print(rmse(target, predictions)) # 0.07071067811865474
```