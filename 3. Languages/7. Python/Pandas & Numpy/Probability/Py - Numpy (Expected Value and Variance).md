See [[Py - Introduction to Python]], [[Py - Pandas (Sample Space Probability)]], [[Py - Numpy (Probability Distributions and Value Intervals)]], [[Py - Math (Confidence Intervals)]]
Documentation
* [Pandas Documentation](https://pandas.pydata.org/docs/)
* [Numpy Documentation](https://numpy.org/doc/stable/index.html)

---

#### Example: Finding the Expected Value
* The probability distribution of a random variable:
![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved__5_1_1582790399.jpg)

* Transform the table to a dictionary
```Python
x_probs = {
    '3': 0.1,
    '4': 0.2,
    '5': 0.2,
    '7': 0.3,
    '11': 0.1,
    '16': 0.05,
    '18': 0.05    
}
# E(X): For each dictionary element, we calculate the product of the probability and the value of the random variable (the integer representation of the dictionary key), then add it all up:

expectation = 0
for x_i in x_probs: 
  expectation += int(x_i) * x_probs[x_i]

print(expectation) # 7.000000000000001
```


#### Example: Finding the Variance
```Python
x_probs = {
    '3': 0.1,
    '4': 0.2,
    '5': 0.2,
    '7': 0.3,
    '11': 0.1,
    '16': 0.05,
    '18': 0.05    
}

expected = 0
expected_of_square = 0
square_of_expected = 0

# E(X) - expected value
for x_i in x_probs:
    expected += int(x_i) * x_probs[x_i]

# E(X^2) - expected value of squared random variable
for x_i in x_probs:
    expected_of_square += int(x_i) * int(x_i) * x_probs[x_i]

# E(X)^2 - square of expected value
square_of_expected = expected ** 2

variance = expected_of_square - square_of_expected

print(variance) # 15.899999999999991
```

```Python
import numpy as np

weight_probs = {
    '2': 0.25,
    '3': 0.50,
    '5': 0.25
}

expectation = sum(int(x_i) * weight_probs[x_i] for x_i in weight_probs)
expected_squared = expectation ** 2
expected_of_square = sum(int(x_i) * int(x_i) * weight_probs[x_i] for x_i in weight_probs)

variance = expected_of_square - expected_squared

print('Expected value:', expectation)
print('Variance:', variance)
```