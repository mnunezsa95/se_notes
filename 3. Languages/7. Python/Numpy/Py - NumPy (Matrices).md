See: 
* [[Py - Introduction to Python]]
* [[Py - NumPy (Vectors)]]
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
# Matrices
#### What is a Matrix?
* **Matrix** -- a rectangular table or two-dimensional array that consists of $m$ rows and $n$ columns (the size is written as: 𝑚 × 𝑛).
* A matrix is a collection of vectors all of the same length.
#### Denoting Matrices
* **Matrices** are denoted by uppercase Latin letters (e.g. 𝐴)
* **Matrices**' elements are denoted lowercase with a double index (e.g. $a_(ij)$), where $i$ is the row number & $j$ is the column number

#### Example: Denoting Matrices 
* Matrix 𝐴 contains 2 rows & 3 columns. Its elements are: $𝑎_(11)$=1, $𝑎_(12)$=2, $𝑎_(13)$=3,  $𝑎_(21)$=2 , $𝑎_(22)$=3, and $𝑎_(23)$=4
	![[denoting-matrices.png]]

# Creating a Matrix
* Matrices are created 3 different ways:
	1) Using `np.array()` method, specifying arrays of the same length
	2) Using `np.array()` method, on a list of vectors (arrays)
	3) Using `df.values` attribute from the pandas DataFrame object
```Python
# Example -- Using np.array() method, specifying arrays of the same length
import numpy as np

# Create a matrix
matrix = np.array([
    [1, 2, 3], 
    [4, 5, 6],
    [7, 8, 9]
])
print(matrix)
```

```Result
[[1 2 3]
 [4 5 6]
 [7 8 9]]
```

```Python
# Example -- Using np.array() method, on a list of vectors (arrays)

import numpy as np

vector1 = np.array([1, 2, 3])
vector2 = np.array([-1, -2, -3])
list_of_vectors = [vector1, vector2]

# Create a matrix from a list of vectors
matrix_from_vectors = np.array(list_of_vectors)

print(matrix_from_vectors)
```

```Result
[[ 1  2  3]
 [-1 -2 -3]]
```

```Python
# Example -- Using np.values attribute from the pandas DataFrame object
import pandas as pd

df = pd.DataFrame({'a': [120, 60, 75], 'b': [42, 50, 90]})
matrix = df.values
print(df)
print(matrix)
```

```Result
     a   b
0  120  42
1   60  50
2   75  90

[[120  42]
[ 60  50]
[ 75  90]]
```

```Python
# Example -- Using np.values attribute from the pandas DataFrame object
import numpy as np
import pandas as pd

monday_df = pd.DataFrame({
	'Minutes': [10, 3, 15, 27, 7], 
	'Messages': [2, 5, 3, 0, 1], 
	'Megabytes': [72, 111, 50, 76, 85]})
 
monday = monday_df.values
```
# Accessing a Matrix Element
* Matrices are accessed using bracket notation `[i, j]` where $i$ is the row number (0-indexed) and $j$ is the column number (0-indexed)
```Python
import numpy as np

A = np.array([
    [1, 2, 3], 
    [2, 3, 4]
])

print(A[1, 2]) # 4
```

# Accessing a Matrix Row or Column
* Matrix rows are accessed using bracket notation `[i, :]`, where $i$ is the row number
* Matrix columns are accessed using bracket notation `[:, j]` where $j$ is the column number
```Python
import numpy as np

matrix = np.array([
    [1, 2, 3], 
    [4, 5, 6],
    [7, 8, 9],
    [10,11,12]
])

print(matrix[0, :]) # [1 2 3]
print(matrix[:, 2]) # [ 3 6 9 12]
```

```Python
import numpy as np
import pandas as pd

monday_df = pd.DataFrame({
	'Minutes': [10, 3, 15, 27, 7], 
	'Messages': [2, 5, 3, 0, 1], 
	'Megabytes': [72, 111, 50, 76, 85]})

monday = monday_df.values

# Select data for the fourth client
print(monday[3, :])

# Select how much data each client used
print(monday[:, 2])
```


# Matrix Operations
- Matrices can be added, subtracted, or multiplied. Division is not possible with a matrix
    - Operations are done element-by-element.
        - Matrices must be the same size.
        - The result is a matrix of the same size.
- When performing an operation with a number and a matrix, each element in the array undergoes the same operation, resulting in a new array of identical size.
	![[matrix-operations-example.png]]

```Python
# Example -- Adding two matrices
import numpy as np

matrix1 = np.array([
    [1, 2], 
    [3, 4]
])

matrix2 = np.array([
    [5, 6], 
    [7, 8]
])

print(matrix1 + matrix2) 
```

```Result
[[ 6  8]
 [10 12]]
```

```Python
# Example -- Subtracting two matrices

import numpy as np

matrix1 = np.array([
    [5, 10], 
    [1, 20]
])

matrix2 = np.array([
    [1, 3], 
    [3, 10]
])

print(matrix1 - matrix2)
```

```Result
[[ 4  7]
 [-2 10]]
```

```Python
# Example -- Multiplying two matrices
import numpy as np

matrix1 = np.array([
    [1, 2], 
    [3, 4]])

matrix2 = np.array([
    [5, 6], 
    [7, 8]])

print(np.multiply(matrix1, matrix2)) 
```

```Result
[[ 5 12]
 [21 32]]
```

```Python
# Example -- Adding, subtracting and multiplying a matrix and number
import numpy as np

matrix = np.array([
    [1, 2], 
    [3, 4]])

print(matrix * 2)
print(matrix + 2)
print(matrix - 2)
```

```Result
[[2 4]
 [6 8]]
 
[[3 4]
 [5 6]]
 
[[-1  0]
 [ 1  2]]
```

```Python
# Example -- Using Matrix Operations

import numpy as np
import pandas as pd

services = ['Minutes', 'Messages', 'Megabytes']

monday = np.array([
    [10, 2, 72],
    [3, 5, 111],
    [15, 3, 50],
    [27, 0, 76],
    [7, 1, 85]])

tuesday = np.array([
    [33, 0, 108],
    [21, 5, 70],
    [15, 2, 15],
    [29, 6, 34],
    [2, 1, 146]])

wednesday = np.array([
    [16, 0, 20],
    [23, 5, 34],
    [5, 0, 159],
    [35, 1, 74],
    [5, 0, 15]])

thursday = np.array([
    [25, 1, 53],
    [15, 0, 26],
    [10, 0, 73],
    [18, 1, 24],
    [2, 2, 24]])

friday = np.array([
    [32, 0, 33],
    [4, 0, 135],
    [2, 2, 21],
    [18, 5, 56],
    [27, 2, 21]])

saturday = np.array([
    [28, 0, 123],
    [16, 5, 165],
    [10, 1, 12],
    [42, 4, 80],
    [18, 2, 20]])

sunday = np.array([
    [30, 4, 243],
    [18, 2, 23],
    [12, 2, 18],
    [23, 0, 65],
    [34, 0, 90]])

weekly = monday + tuesday + wednesday + thursday + friday + saturday + sunday

print('In a week')
print(pd.DataFrame(weekly, columns=services))

forecast = (weekly * 30.4) / 7

print('Forecast for a month')
print(pd.DataFrame(forecast, dtype=int, columns=services))
```

```Result
In a week
   Minutes  Messages  Megabytes
0      174         7        652
1      100        22        564
2       69        10        348
3      192        17        409
4       95         8        401

Forecast for a month
   Minutes  Messages  Megabytes
0      755        30       2831
1      434        95       2449
2      299        43       1511
3      833        73       1776
4      412        34       1741
```


# Matrix-Vector Multiplication
- **Matrix-Vector Multiplication**
	- **Procedure for the operation:**
		- Compute the dot product of each row of the matrix and the vector.
			- Make sure each row of the matrix is the same length as the vector.
	  - The result of matrix-vector multiplication is a **Vector**.
	![[matrix-times-vector-1.png]]
	
	![[matrix-times-vector-2.png]]
* Example
	* Matrix $𝐴$ with size _n×m_ ($n$ rows by $m$ columns) is multiplied by Vector _b_ of length 𝑛. 
		* The product will be a new vector 𝑐⃗ = 𝐴𝑏⃗. 
	* The result is an 𝑛-dimensional vector where each value is equal to the dot product of a row of the matrix and 𝑏⃗
		![[matrix-times-vector-3.png]]
	
* Matrix-Vector Multiplication in Python
	* Use the `np.dot()` function which works as a standalone function or method of a matrix
```Python
import numpy as np
    
matrix = np.array([
    [1, 2, 3], 
    [4, 5, 6]])

vector = np.array([7, 8, 9])

# Standalone function - takes two arguments
print(np.dot(matrix, vector))

# Method of the matrix - only needs one argument
print(matrix.dot(vector))
```

```Result
[ 50 122]
[ 50 122]
```

```Python
import numpy as np
import pandas as pd

services = ['Minutes', 'Messages', 'Megabytes']
packs_names = ['"Behind the wheel"', '"On the subway"']
packs = np.array([
	[20, 5], 
	[2, 5], 
	[500, 1000]
])

clients_packs = np.array([[1, 2], [2, 3], [4, 1], [2, 3], [5, 0]])

print("Client's package")
print(pd.DataFrame(clients_packs[1], index=packs_names, columns=['']))

# Grabbing the second client
client_vector = clients_packs[1]

# Calculating the second client's usage for minutes, messages and internet
client_services = packs.dot(client_vector)

print('Minutes, Messages, Megabytes')
print(client_services)
```

```Result
Minutes, Messages, Megabytes
[  55   19 4000]
```


# Matrix-Matrix Multiplication
- **Matrix-Matrix Multiplication**
	- **Procedure for the operation:**
		- Compute the dot product of a row in the first matrix and a column in the second matrix.
	  - Make sure the first matrix's number of columns must match the second matrix's number of rows.
	  - The result of matrix-matrix multiplication is a **Matrix**.
		![[matrix-matrix-multiplication.png]]
* Matrix-Matrix Multiplication in Python
	* Use the `np.dot()` function which works as a standalone function or method of a matrix
```Python
# Example -- Matrix-Matrix Multiplication

import numpy as np

# Number of columns in first matrix = number of rows in second matrix
A = np.array([
    [1, 2, 3], 
    [-1, -2, -3]])

B = np.array([
    [1, 0], 
    [0, 1],
    [1, 1]])

# Standalone function - takes two arguments
print(np.dot(A, B)) 

# Method of the matrix - only needs one argument
print(A.dot(B)) 

# Using the @ operator
print(A @ B)

# Multiplying in different order produces a different result
print(B @ A)
```

```Result
# All three produce same result

[[ 4  5]
 [-4 -5]]
 
[[ 4  5]
 [-4 -5]]
 
[[ 4  5]
 [-4 -5]]

-----

# Multiplying in different order produces a different result
[[ 1  2  3]
 [-1 -2 -3]
 [ 0  0  0]]
```

* Multiplying a Matrix by itself is only possible when it is a square (3 x 3)
```Python
# Example -- Multiplying a matrix by itself
square_matrix = np.array([
    [1, 2, 3], 
    [-1, -2, -3],
    [0, 0, 0]])

print(square_matrix @ square_matrix)


# Example -- Multiplying a matrix by itself (not a square)
matrix = np.array([
    [1, 2, 3], 
    [-1, -2, -3]])

print(matrix @ matrix)
```

```Result
[[-1 -2 -3]
 [ 1  2  3]
 [ 0  0  0]]


---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
... in <module>
      3     [-1, -2, -3]])
      4 
----> 5 print(matrix @ matrix)

ValueError: matmul: Input operand 1 has a mismatch in its core dimension 0, with gufunc signature (n?,k),(k,m?)->(n?,m?) (size 2 is different from 3)
```

```Python
import numpy as np
import pandas as pd

months_1 = ['February', 'March']
months_2 = ['June', 'July', 'August']

costs = np.array([
    [700, 50] # honeymoon_suite, regular
])

bookings_1 = np.array([
    [3, 4], # number of bookings for honeymoon suites in February & March
    [17, 26] # number of bookings for regular rooms in February & March
])

bookings_2 = np.array([
    [8, 9, 11], # number of bookings for honeymoon suites in June, July & August
    [21, 26, 30] # number of bookings for regular rooms in June, July & August
])

print(pd.DataFrame((costs @ bookings_1), columns=months_1))
print('----------------------')
print(pd.DataFrame((costs @ bookings_2), columns=months_2))
```

```Result
   February  March
0      2950   4100
----------------------
   June  July  August
0  6650  7600    9200
```

```Python
# Example
import numpy as np
import pandas as pd

services = ['Minutes', 'Messages', 'Megabytes']
packs_names = ['"Behind the wheel', '"On the subway"']
packs = np.array([
    [20, 5],
    [2, 5],
    [500, 1000]])

clients_packs = np.array([
    [1, 2],
    [2, 3],
    [4, 1],
    [2, 3],
    [5, 0]])

print('Packages')
print(pd.DataFrame(clients_packs, columns=packs_names))
print()

clients_services = np.dot(clients_packs, packs.T)

print('Minutes, Messages and Megabytes')
print(pd.DataFrame(clients_services, columns=services))
print()
```

```Python
import numpy  as np
import pandas as pd

materials_names = ['Board', 'Pipe', 'Screws']
venues_names = ['Coffee shop', 'Diner', 'Restaurant']

manufacture = np.array([
    [0.2, 1.2, 8],    # chair materials
    [0.5, 0.8, 6],    # bench materials
    [0.8, 1.6, 8]])   # table materials

furniture = np.array([
    [12, 0, 3],   # Coffee shop order (chair, bench, table)
    [40, 2, 10],  # Diner order
    [60, 6, 18]]) # Restaurant order

venues_materials = furniture @ manufacture
print('By the venue')
print(pd.DataFrame(venues_materials, index=venues_names, columns=materials_names))

venues = [18, 12, 7]
total_materials = venues_materials.T @ venues
print('Total')
print(pd.DataFrame([total_materials], index=[''], columns=materials_names))
```

```Result
By the venue
             Board   Pipe  Screws
Coffee shop    4.8   19.2   120.0
Diner         17.0   65.6   412.0
Restaurant    29.4  105.6   660.0

Total
  Board    Pipe   Screws
  496.2  1872.0  11724.0
```


# Transposing a Matrix
* **Transpose** -- flipping the matrix over its main diagonal (running from the upper left to the lower right); in other words, swapping the rows and columns.
  * Converts a matrix of size \( m x n \) to \( n \x m \).
  * The transposed matrix is denoted by the superscript \( T \).
	![[transposed-matrix.png]]
* Why is transposing useful?
  * It can change the dimensions of the matrix to better suit the needs of analysis.
* Transposing in Python
	* Use the `.T` attribute on the matrix to transpose it
```Python
# Example -- Transposing a Matrix

import numpy as np

matrix = np.array([
    [1, 2], 
    [4, -4], 
    [0, 17]
])

print('Original matrix')
print(matrix)
print('Transposed matrix')
print(matrix.T)

# Attempt to multiply original matrix by vector; throws an error due to size differences
vector = [2, 1, -1]
print(np.dot(matrix, vector)) 

# Attempt to multiply tranposed matrix by vector
print(np.dot(matrix.T, vector))
```

```Result
Original matrix
[[ 1  2]
 [ 4 -4]
 [ 0 17]]
 
Transposed matrix
[[ 1  4  0]
 [ 2 -4 17]]



# Throws an error because sizes are not the same
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
... in <module>
      1 vector = [2, 1, -1]
----> 2 print(np.dot(matrix, vector))

ValueError: shapes (3,2) and (3,) not aligned: 2 (dim 1) != 3 (dim 0)



# Works because size of the matrix and width of vector are equal
[  6 -17]
```

```Python
# Example -- Transpose a matrix to use dot multiplication

import numpy  as np
import pandas as pd

materials_names = ['Board', 'Pipe', 'Screws']

manufacture = np.array([
    [0.2, 1.2, 8],
    [0.5, 0.8, 6],
    [0.8, 1.6, 8]
])

furniture = [60, 4, 16]
materials = np.dot(manufacture.T, np.array(furniture))

print(pd.DataFrame([materials], index=[''], columns=materials_names))
```

```Result
  Board   Pipe  Screws
   26.8  100.8   632.0
```