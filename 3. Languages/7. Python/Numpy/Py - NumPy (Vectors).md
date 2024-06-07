See: 
* [[Py - Introduction to Python]]
* [[Py - NumPy (Methods)]]
* [[Py - Pandas (Methods)]]
* [[Py - Matplotlib (Methods)]]
* [[Py - SciPy (Methods)]]
Resources:
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [Matplotlib](https://matplotlib.org/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)

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


# Creating Multidimensional Vectors
* Multidimensional vectors are vectors with more than 2-dimensions
* Multidimensional vectors -- useful in identifying how closely related different observations are to one another
```Python
# Example -- Multidimensional Vector
vector1 = np.array([1, 2, 3, 4])
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
- When performing an operation with a number and a vector, each element in the array undergoes the same operation, resulting in a new array of identical size.
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


# Calculating the Mean Value of Vectors
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


# Creating Vectorized Functions
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


# Vectorizing Metrics
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


# Calculating the Dot Product
* Dot Product -- the product of two or more vectors. The result of a dot product operation is a scalar value
	* The dot product of vectors $a$ and $b$ is denoted by ⟨ $a$, $b$ ⟩ or $a⋅b$
	* Can be calculated using `np.dot()` or the matrix multiplication operator, which is denoted by `@`
```Python
import numpy as np

volume = np.array([0.3, 0.2, 0.25])
content = np.array([0.6, 0.7, 1])

print(np.dot(volume, content)) # 0.57
print(volume @ content) # 0.57
```

```Python
# Example -- Calculating the dot product of a vector & itself; returns the same value as using pythagorean theorem

import numpy as np

a = np.array([5, 6])

# Use the dot product
print(np.dot(a, a) ** 0.5) # 7.810249675906654
```

```Python
# Example -- Calculate dot product
import numpy as np
import pandas as pd

store1_price = [209.9, 119.9, 53.9, 31.9, 19.9, 109.9, 59.99, 22.9, 81.11, 32.9]
store1_quantity = [19, 11, 8, 15, 23, 7, 14, 9, 10, 4]

store2_price = [209.9, 124.9, 42.9, 27.9, 23.9, 109.9, 49.9, 24.9, 89.9, 32.9]
store2_quantity = [10, 16, 20, 9, 18, 12, 10, 11, 18, 22]

models = ['Apple AirPods Pro', 'Apple AirPods MV7N2RU/A', 'JBL Tune 120TWS', 
'JBL TUNE 500BT', 'JBL JR300BT', 'Huawei Freebuds 3','Philips TWS SHB2505',
'Sony WH-CH500', 'Sony WF-SP700N', 'Sony WI-XB400']

items1 = pd.DataFrame({'Price':store1_price, 'Quantity':store1_quantity}, 
	index=models)
items2 = pd.DataFrame({'Price':store2_price, 'Quantity':store2_quantity}, 
	index=models)

items1_price = items1['Price'].values 
items1_quantity = items1['Quantity'].values 

items2_price = items2['Price'].values
items2_quantity = items2['Quantity'].values

# Calculating dot product
items1_value = items1_price @ items1_quantity
items2_value = items2_price @ items2_quantity

total_value = items1_value + items2_value
print('Total value of the items of the two stores:', total_value, 'USD')
# Total value of the items of the two stores: 19502.760000000002 USD
```


# Calculating Euclidean Distance
* Euclidean Distance	is used across many machine learning algorithms as the default distance metric
* Euclidean Distance -- the shortest distance between two vectors ($a$) and ($b$) on a plane
	* Calculating the Euclidean Distance of 2-Dimensional Vectors
		* $d_2(a, b)$ -- $d$ carries the subscript 2 to indicate the vector coordinates are raised to the second power
		* Formula: $$ d_2 (a, b) = sqrt((b-a) * (b-a)) = sqrt((x_2 -x_1)^2 + (y_2 - y_1)^2) $$
		
	* Calculating the Euclidean Distance of Multidimensional Vectors
		* Formula: $$d_2(a,b) = sqrt((x_1 - y_1)^2 + (x_2 - y_2)^2 + ... + (x_n - y_n)) = sqrt (sum_(i=1)^n(x_I - y_i)^2) $$
		
* Calculating Euclidean Distance with NumPy
	* Use `np.dot()` to calculate distance
```Python
# Example -- Using NumPy to calculate the euclidean distance between a = (5,6) and b = (1,3)

import numpy as np

a = np.array([5, 6])
b = np.array([1, 3])

d = np.dot(b - a, b - a) ** 0.5
print('Distance between a and b is', d) # Distance betweeen a and b is 5.0
```

* Calculating Euclidean Distance with SciPy
	* Use `scipy.spatial.distance.euclidean()` to calculate distance
```Python
# Example -- Using SciPy to calculate the euclidean distance between a = (5,6) and b = (1,3)

import numpy as np
from scipy.spatial import distance

a = np.array([5, 6])
b = np.array([1, 3])
d = distance.euclidean(a, b)
print('Distance between a and b is', d) # Distance betweeen a and b is 5.0
```

```Python
# Example -- Calculate euclidean distance of 2D vectors using euclidean() fn
import numpy as np
import pandas as pd
from scipy.spatial import distance

x_axis = np.array([0., 0.18078584, 9.32526599, 17.09628721, 4.69820241, 11.57529305, 11.31769349, 14.63378951])

y_axis  = np.array([0.0, 7.03050245, 9.06193657, 0.1718145, 5.1383203, 0.11069032, 3.27703365, 5.36870287])

deliveries = np.array([5, 7, 4, 3, 5, 2, 1, 1])

town = ['Willowford', 'Otter Creek', 'Springfield', 'Arlingport', 'Spadewood',
'Goldvale', 'Bison Flats', 'Bison Hills']

data = pd.DataFrame(
    {
        'x_coordinates_km': x_axis,
        'y_coordinates_km': y_axis,
        'Deliveries': deliveries,
    },
    index=town,
)

vectors = data[['x_coordinates_km', 'y_coordinates_km']].values

distances = []
for town_from in range(len(town)):
    row = []
    for town_to in range(len(town)):
        value = distance.euclidean(vectors[town_from], vectors[town_to])
        row.append(value)
    distances.append(row)

deliveries_in_week = []
for i in range(len(distances)):
    value = 2 * np.dot(np.array(distances[i]), deliveries)
    deliveries_in_week.append(value)

deliveries_in_week_df = pd.DataFrame(
    {'Distance': deliveries_in_week}, index=town
)

print(deliveries_in_week_df)
print('Warehouse town:', deliveries_in_week_df['Distance'].idxmin())
```

```Python
# Example -- Calculate euclidean distance of multi-dimensional vectors
import numpy as np
from scipy.spatial import distance

a = np.array([4, 2, 3, 0, 5])
b = np.array([1, 0, 3, 2, 6])

# Calculate euclidean manually 
d = np.dot(b - a, b - a)**0.5
print(d) # 4.242640687119285

# Calculate with the euclidean function
e = distance.euclidean(a, b)
print(e) # 4.242640687119285
```

```Python
# Example -- Calculate manhattan distance of multi-dimensional vectors

import pandas as pd
from scipy.spatial import distance

columns = ['bedrooms', 'total area', 'kitchen', 'living area', 'floor', 'total floors']
realty = [[1, 38.5, 6.9, 18.9, 3, 5], [1, 38.0, 8.5, 19.2, 9, 17], 
		  [1, 34.7, 10.3, 19.8, 1, 9], [1, 45.9, 11.1, 17.5, 11, 23], 
		  [1, 42.4, 10.0, 19.9, 6, 14],[1, 46.0, 10.2, 20.5, 3, 12], ..., 
		  [3, 69.3, 8.5, 39.3, 4, 9], [3, 89.8, 11.2, 58.2, 24, 25]]

df_realty = pd.DataFrame(realty, columns=columns)

vector_first = df_realty.loc[3].values
vector_second = df_realty.loc[11].values

print('Euclidean distance:', distance.euclidean(vector_second, vector_first))
# Euclidean distance: 42.73417835877976
```


# Calculating Manhattan Distance
* Manhattan Distance (or city-block distance) -- the sum of the absolute difference of all the points' coordinates.
	* Calculating Manhattan Distance for 2-dimensional vectors
		* Manhattan Distance between points $a=(x_i, y_i)$ and $b=(x_2, y_2)$ 
			* $d_1​(a,b)$ -- $d$ carries the subscript 1 to indicate that the vector coordinates are raised to the first power
		* Formula: $$ d_1(a, b) = |x_1 - x_2| + |y_1 - y_2| $$
	* Calculating Manhattan Distance of Multidimensional Vectors
		* Formula: $$d_1(a,b)= |x_1 - y_1| + |x_2 - y_2| + ... + |x_n - y_n| = sum^n_(i=1) | x_i = y_i|$$
```Python
# Example -- Using Manhattan Distance (city-block distance)
import numpy as np

def manhattan_distance(first, second):
    return np.abs(first - second).sum()

first = np.array([3, 11])
second = np.array([1, 6])

print(manhattan_distance(first, second))
```

* Calculating Manhattan Distance with SciPy
	* Use `scipy.spatial.distance.cityblock()` to calculate distance
```Python
# Example -- Calculate manhattan distance of 2D vectors using cityblock() fn
import numpy as np
import pandas as pd
from scipy.spatial import distance

avenues = pd.Series([0, 153, 307, 524], index=['Park', 'Lexington', '3rd', '2nd'])
streets = pd.Series([0, 81, 159, 240, 324], index=['76', '75', '74', '73', '72'])

address = ['Lexington', '74']
taxis = [
    ['Park', '72'],
    ['2nd', '75'],
    ['3rd', '76'],
]

address_vector = np.array([avenues[address[0]], streets[address[1]]])

taxi_distances = []
for taxi in taxis:
    taxi_vector = np.array([avenues[taxi[0]], streets[taxi[1]]])
    taxi_distances.append(distance.cityblock(address_vector, taxi_vector))

index = np.array(taxi_distances).argmin()
print(taxis[index]) # ['3rd', '76']
```

```Python
# Example -- Calculate manhattan distance of multi-dimensional vectors

import numpy as np
from scipy.spatial import distance

a = np.array([4, 2, 3, 0, 5])
b = np.array([1, 0, 3, 2, 6])

# Calculate manhattan manually
d = np.abs(b - a).sum()
print(d) # 8

# Calculate with manhattan function
e = distance.cityblock(a, b)
print(e) # 8
```

```Python
# Example -- Calculate manhattan distance of multi-dimensional vectors

import pandas as pd
import numpy as np
from scipy.spatial import distance

columns = ['bedrooms', 'total area', 'kitchen', 'living area', 'floor', 'total floors']
realty = [[1, 38.5, 6.9, 18.9, 3, 5], [1, 38.0, 8.5, 19.2, 9, 17], 
		  [1, 34.7, 10.3, 19.8, 1, 9], [1, 45.9, 11.1, 17.5, 11, 23], 
		  [1, 42.4, 10.0, 19.9, 6, 14],[1, 46.0, 10.2, 20.5, 3, 12], ..., 
		  [3, 69.3, 8.5, 39.3, 4, 9], [3, 89.8, 11.2, 58.2, 24, 25]]

df_realty = pd.DataFrame(realty, columns=columns)

vector_first = df_realty.loc[3].values
vector_second = df_realty.loc[11].values

print('Manhattan distance:', distance.cityblock(vector_second, vector_first))
# Manhattan distance: 71.7
```


# The K-Nearest Neighbors Algorithm
* The K-Nearest Neighbors Algorithm(KNN) -- a distance-based machine learning algorithm that can be used for performing both classification and regression tasks.
* How the KNN algorithm works
	* **Step 1:** Choose the number ($k$) of neighbors to analyze.
	* **Step 2:** Compute the distance between the new observation and other points in the dataset. 
		* The default distance metric is Euclidean, but alternatives like Manhattan, Minkowski, or Hamming distances can be used.
	* **Step 3:** Arrange the distances from closest to farthest and identify the nearest $k$ neighbors.
	* **Step 4:** Assign the new observation to the class with the majority among its $k$ nearest neighbors.
		![[knn-algorithm.png]]
		
```Python
# Example -- Create a KNN algorithm

import pandas as pd
import numpy as np
from scipy.spatial import distance

columns = ['bedrooms', 'total area', 'kitchen', 'living area', 'floor', 'total floors']
df_train = pd.DataFrame(
	[
		[1, 38.5, 6.9, 18.9, 3, 5], [1, 38.0, 8.5, 19.2, 9, 17], ..., 
		[3, 69.3, 8.5, 39.3, 4, 9], [3, 89.8, 11.2, 58.2, 24, 25],
	],
	columns=columns)

def nearest_neighbor_predict(train_features, train_target, new_features):
    distances = [] # placeholder for distances
    
    # Loop through all rows of train_features
    for i in range(train_features.shape[0]): 
	    # Grab the current row from train_features as an array (not list)
        vector = train_features.loc[i].values
        # Find distances between current row from train_features & new_features
        value = distance.euclidean(new_features, vector)
		# Add the distance to distances list
        distances.append(value)
        
	# Get index with the lowest value
    best_index = np.array(distances).argmin()
    
    # Get the value at best_index from the target series
    answer = train_target.loc[best_index]
    return answer
    

train_features = df_train.drop('bedrooms', axis=1)
train_target = df_train['bedrooms']
new_apartment = np.array([72, 14, 39, 8, 16])
pred = nearest_neighbor_predict(train_features, train_target, new_apartment)

print(pred) # 2.0
```