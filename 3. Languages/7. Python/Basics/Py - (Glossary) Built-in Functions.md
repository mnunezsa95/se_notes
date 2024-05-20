See
* [[Py - Introduction to Python]]
* [[Py - Functions]]
* [[Py - Data Types]]
* [[Py - Strings]]
Resources:
* [Python-Builtin Function](https://docs.python.org/3/library/functions.html)

---
##### `print()`
* Prints out a value/prompt to the console
	* Arguments
		1) `value` -- the value to be printed (can take strings, numbers, etc data types) 
			* values are separated by commas
```Python
print(value1, value2, ...)
```

```python
# Example
print('The print() function is used to output data on the screen.')
metric = 34
print('metric:', metric) # metric: 34
```

##### `type()`
* Gets the data type of a value 
	* Arguments
		1) `value` -- the value for which the data type is to be identified
```Python
type(value)
```

```python
# Example
language = 'Chinese'
print(type(language))

website_share = 0.017
print(type(website_share))

native_speakers = 908.7
print(type(native_speakers))
```

##### `int()`
* Transforms an object to an integer 
	* Arguments
		1) `value` -- the value to be converted
```Python
int(value)
```

```Python
# Example
ru_website_share = 0.061
sites = 10000000
ru_sites = sites * ru_website_share
ru_sites = int(ru_sites)
```

##### `float()` 
 * Transforms an object to a floating-point number 
	* Arguments
		1) `value` -- the value to be converted
```Python
float(value)
```

```Python
# Example
ch_native_speakers = '908.7'
ch_native_speakers = float(ch_native_speakers) 
```

##### `str()`
 * Transforms an object to a string
	 * Arguments
		1) `value` -- the value to be converted
```Python
float(value)
```

```Python
# Example
ch_native_speakers = 908.7
ch_native_speakers = str(ch_native_speakers) # '908.7'
```

##### `len()`
* Returns the length of a string
	* Arguments
		1) `value` -- a string or list for which the length will be calculated
```python
len(value)
```

```python
# Example
lullaby = "Twinkle twinkle little star, how I wonder what you are, up above the world so high, like a diamond in the sky, twinkle twinkle little star, how I wonder what you are."

print(len(lullaby)) # Output: 166
```

##### `range()`
* Creates a range of numbers varying from `a` to `b` (not including b)
	* Arguments
		1) `a` -- the starting number for the range
		2) `b` -- the ending number for the range
		3) `step` -- change the step value when ranging from `a` to `b`
```python
range(a, b, step)
```

```python
for number in range(1, 10):
  print(number) # 1, 2, 3, 4, 5, 6, 7, 8, 9
```

##### `list()`
* Converts a tuple or string into a list
	* Arguments
		1) `iterable` -- the string or tuple to be converted
```python
list(tuple)
list(str)
```

```python
# Example

# Converting a list to a tuple
movie_info = ('Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644)
print(list(movie_info)) 
  # ('Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644)
```

##### `tuple()`
* Converts a list or string into a tuple
	* Arguments
		1) `iterable` -- the string or list to be converted
```python
tuple(list)
tuple(str)
```

```python
# Example

# Converting a tuple to a list
movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644]
print(tuple(movie_info)) 
  # ('Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644)
```

##### `input()`
* Allows user input
	* Arguments
		1) `prompt` -- the prompt for user input
```python
input(prompt)
```

```python
input("What is your name ")
print("Hello " + input("What is your name? ") + "!")
```

##### `round()`
* Rounds a number to only two decimals (by default); number of decimal places can be changed
	* Arguments
		1) `value` -- the value to be rounded
		2) `digits` -- the number of decimal places to round
```python
round(value, digits)
```

```python
print(round(8 / 3, 2)) # Output: 2.67
print(round(8 / 3, 4)) # Output: 2.6667
```