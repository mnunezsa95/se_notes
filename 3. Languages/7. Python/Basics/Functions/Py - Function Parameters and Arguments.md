See: [[Py - Introduction to Python]], [[Py - Functions]]

---
## Parameters vs Arguments (the differences)
* **Parameters** are the names of the temporary variables that we pass to a function as input
* **Arguments** are the actual values that we give to those parameters when we call the function after it’s been created.

---
#### Combining Keyword & Positional Arguments
* **When combining positional and keyword arguments, ALL positional arguments must be placed first**
```Python
def division(numerator, denominator): 
  result = numerator / denominator 
  print(result) 

division(numerator=10, 2)
```

```Python
def trip_price(dist_miles, mpg, price, loc_from, loc_to):
    total_price = dist_miles * price / mpg
    print(f'A trip from {loc_from} to {loc_to} will cost ${total_price:.2f}')

trip_price(409, 35, loc_from='Boston', loc_to='New York', price=5.1)
# A trip from Boston to New York will cost $59.60
```

#### Positional Arguments
* Positional arguments are arguments passed in order to the parameters when calling the function
* When calling a function defined with positional arguments, the argument values must be passed in the exact same order as when declared to prevent errors or unwanted results
```Python
def greet(name, birth_country, current_city):
  print(f"My name is {name}.")
  print(f"I am from {birth_country}.")
  print(f"I live in {current_city}.")

# calling the function with positional arguments
greet("Marlon", "Costa Rica", "Boston")
```

```Python
def trip_price(dist_miles, mpg, price, loc_from, loc_to):
    total_price = dist_miles * price / mpg
    print(f'A trip from {loc_from} to {loc_to} will cost ${total_price:.2f}')

trip_price(409, 35, 5.1, 'A', 'B') # A trip from A to B will cost $59.60
```

#### Keyword Arguments
* Keyword arguments are arguments assigned to the parameter name when calling the function
* When calling a function using keyword arguments, the arguments' names and values must be passed in. This allows the arguments to be passed in any order
```Python
def greet_with_keyword_arguments(name, birth_country, current_city):
  print(f"My name is {name}.")
  print(f"I am from {birth_country}.")
  print(f"I live in {current_city}.")

# calling the function with keyword arguments
greet(current_city="Boston", name="Harper", birth_country="USA")
```

```Python
def trip_price(dist_miles, mpg, price, loc_from, loc_to):
    total_price = dist_miles * price / mpg
    print(f'A trip from {loc_from} to {loc_to} will cost ${total_price:.2f}')

trip_price(dist_miles=409, loc_from='A', loc_to='B', mpg=35, price=5.1)
# A trip from A to B will cost $59.60
```

#### Default Arguments
* Default parameter values can be declared in the function using an `=` sign
* Default parameters must be placed at the end of the function definition
* The default values will be used if the function is called without passing in arguments
```Python 
def foo(a, b=4, c=6):
  print(a, b, c)

foo(1) # 1, 4, 6
```

```Python
def foo(a, b=4, c=6):
  print(a, b, c)

foo(20, c=6) # 20, 4, 6
```

```Python
# Adding default values for arguments 
def greet_with_keyword_arguments(name="Marlon", birth_country="Costa Rica", current_city="Boston"):
  print(f"My name is {name}.")
  print(f"I am from {birth_country}.")
  print(f"I live in {current_city}.")

greet(current_city="Philadelphia") # Changing the value of a default value
```

```Python
# Default parameters must be placed at the end of the function definition
def trip_price(dist_miles, mpg, price, loc_from='A', loc_to='B'):
    total_price = dist_miles * price / mpg
    print(f'A trip from {loc_from} to {loc_to} will cost ${total_price:.2f}')

trip_price(409, 35, price=3.8) # A trip from A to B will cost $44.41
```

#### Unlimited Positional Arguments (`*args`)
* `*args` is passed into the function's parameter to allow for unlimited positional arguments
	* The asterisk (`*`) tells python to accept any number of args
	* `*args` is of type 'tuple'
	* `*args` can be accessed using bracket notation (since `*args` is a tuple)
```Python
def add(*args): # the asterisk (*) tells python to accept any number of args
  for n in args:
    sum = 0
    for n in args:
      sum += n
    return sum
    
print(add(1, 2, 3, 4)) # 10
```

#### Unlimited Keyword Arguments (`**kwargs`)
* `**kwargs` is passed into the function's parameter to allow for unlimited keyword arguments
* `**kwargs` is of type 'dict'
* `**kwargs` can be accessed using bracket notation (since *args is a dict)
```python
def calculate(**kwargs):
  print(kwargs)
  for key, value in kwargs.items():
    print(key)
    print(value)
  print(kwargs["add"])

calculate(add=3, multiply=5)
```