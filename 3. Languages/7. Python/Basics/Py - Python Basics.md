See:
* [[Py - Introduction to Python]]
* [[Py - (Glossary) Built-in Functions]]
* [[Py - (Glossary) Python Keywords]]
Resources:
* Documentation: [PEP 257 Docstring](https://peps.python.org/pep-0257/)
* Documentation: [Pandas Docstring](https://pandas.pydata.org/docs/development/contributing_docstring.html)

---

# Variables
## What is a variable?
* A variable stores a value
## Working with Variables
### Declaring a Variable
* Syntax
	* Uses the assignment operator ( `=` )
	* Variable names are case sensitive
* Rules
	* Cannot start with numbers (leads to syntax error)
	* Cannot use reserve keywords
	* Should not have capital letters
	* Words should be separated using underscores
```python
variable_name = value
```

```Python
my_name = "Marlon"
```

* Variables can be stored inside other variables
```Python
first_variable = 42
second_variable = first_variable
print(second_variable) # Output: 42
```

#### Reassigning Variables
* Variables can be assigned and reassigned
```python
person = 'Maxwell'
person = 'Max'
print(person) # Max
```


---
---
# The Python Namespace

## What is the Namespace?
* A Python namespace is a behind-the-scenes part of the code that contains the name of every available object.
* It includes Python built-in objects like the `print()` function as well as any variables or functions created in the code.


---
---
# Data Types
## Common Data Types
* In Python, every object belongs to a certain type!
* Common Data Types
	* Integers (int)
	* Floating-point numbers (float)
	* Strings (str)
	* Booleans (bool)

## Working with Data Types
### Identifying Data Types
* The `type()` function can be used to find the data type of a variable or object
```Python
# Example

language = 'Chinese'
print(type(language))
```

### Adding Different Data Types
* Adding 2 or more strings will concatenate them
* Adding only integers or only floats will result in the corresponding data types
* Adding integer & float will result in float
* Other data types cannot be added
```Python
# Can use the addition operator to add strings together
print(str3 + " " + str2 + " " + str4 + " " + str3 + " " + str1)

# This will throw an error; cannot added str and int
result = "Chinese is spoken by "  + 1400 + " million people worldwide" 
```

### Converting Data Types
* Data Types are converted in order to perform operations (Strings & numbers are not type coerced)
	* Not all objects can be converted from one type to another
* Basic functions for converting data types
	* `int()` -> transforms an object to an integer 
		* Using `int()` to transform a float will round the number down
	* `float()` -> transforms an object to a floating-point number
	* `str()` -> transforms an object to a string
```Python
ch_total_speakers = '1400' 
ch_total_speakers = int(ch_total_speakers) # covert a string to integer

share_english = '0.604'
share_english = float(share_english) # convert a string to a float

zipcode = 90210
zipcode = str(zipcode) # convert a number to a string
```

```Python
# Example

print(float('Hello, world!')) 
# Throws a ValueError; cannot convert string to float: 'Hello, world!' 
```


---
---

# Arithmetic Operations

## Arithmetic Operators
* Results can be in a variety of data types (floating-point & integer).
	* Floating-point -- decimal places
	* Integer -- a full number
* Order of operations
	1) Parentheses
	2) Exponentiation
	3) Multiplication, Division
	4) Addition, Subtraction
```Python
# Operations run in order of PEMDAS
print( (2 ** 3 + 12 / 2) / (5 * 4 - 13) )
```

| Sign | Operation      | Description                                                  |
| ---- | -------------- | ------------------------------------------------------------ |
| +    | addition       | adds two values                                              |
| -    | subtraction    | subtracts two values                                         |
| *    | multiplication | multiplys two values                                         |
| /    | division       | divides two values                                           |
| **   | exponentiation | raises a number to the the power of n                        |
| //   | floor division | divides two values and floors it to the nearest whole number |

## Working with Arithmetic Operators
```python
# summing the number of English and Russian speakers
en_ru_speakers = 1121 + 264.3

# dividing the number of native Italian speakers by the total number of Italian speakers
it_natives_share = 64.8 / 67.8

print(en_ru_speakers)
print(it_natives_share)
```

## Augmented Assignment
* Augmented assignment is a way to add values together using shorter syntax;
* Essentially takes the previous value and adds something to it and saves it to the variable
```python
items = 10
items += 5 # same as items = items + 5
items -= 5 # same as items = items - 5
items *= 3 # same as items = items * 3
items /= 5 # same as items = items / 5
```


---
---

# Conditional Statements

## What are conditional statements?
* Conditional Statements use logical expressions to allow code to make decisions based on which conditions are met.

## Conditionals
* There are three conditionals in Python:
	1) `if` 
	2) `elif`
	3) `else`
* The three are used together to make an `if-elif-else` statement
	* The first `True` condition is executed, even if, others after it are `True`
* `if-elif-else` statements can be nested

#### `if` Statement
* Only execute if the code is `True`
```Python
# SYNTAX

if expression_to_check:
	# code to execute
```

```Python
# Example

name = 'Steven'
if name == 'Carol':
    print("Hello again, Carol!")

if name == 'Steven':
    print("Welcome, Steven!") # Output: Welcome, Steven!
```

#### `else` Statement
* Execute if the `if` condition is NOT met
```python
# SYNTAX

else:
	# code to execute
```

```python
# Example

name = 'Steven'
if name == 'Carol':
    print("Hello again, Carol!")
else:
    print(f"Welcome, {name}!") # Output: Welcome, Steven!
```

#### `elif` Statement
* Executes a condition when the `if` statement is not true, but takes place before the `else` statement
```python
# SYNTAX

elif expression_to_check:
	# code to execute
```

```Python
# Example

name = 'Steven'
if name == 'Carol':
    print("Hello again, Carol!")
elif name == 'Steven':
    print("Top of the morning to you, Steven!")
else:
    print(f"Welcome, {name}!") 
```

```python
# Example

x = 50
if x < 10:
    print('low')
elif x < 500:
    print('high') # First true condition so this is executed
elif x < 100:
    print('medium')
else:
    print('mega') 
```

```python
# Example -- Nested if-elif-else statements

name = 'Carol'
age = 67
spent = 2017.03

if age >= 65:
    if spent < 100:
        discount = 0.05
    elif spent >= 100 and spent < 500:
        discount = 0.2
    elif spent >= 500 and spent < 1000:
        discount = 0.3
    else:
        discount = 0.4
else:
    if spent < 100:
        discount =0
    elif spent >= 100 and spent < 500:
        discount = 0.1
    elif spent >= 500 and spent < 1000:
        discount = 0.15
    else:
        discount = 0.2

print(f"{name} gets a {discount:.0%} discount next month") # Output: Carol gets a 40% discount next month 
```


---
---

# Logical Expressions

## What are Logical Expressions
* Expressions that return the Boolean values (`True` or `False`)

## Groups of Logical Expressions
* Comparison Operators: `==`, `!=`, `>`, `<`, `>=`, `<=`
* Logical Operators: `and`, `or`, `not`, `in`
* Predicate Functions

#### Types of Logical Expressions
```Python
print(True) # True
print(False) # False
print(5 < 3) # False
print('TripleTen' == 'tripleten') # False (two words are different)
print('TripleTen'.islower()) # False (word is NOT lowercase)
print('tripleten'.islower()) # True (word is lowercase)
```

## Comparison Operators
* Comparison Operators -- compare two values and return `True` or `False`
* Used to compare numbers & strings
	* When using ` < ` & ` > `  on strings, it checks which one comes first (in lexicographical order)

| Operator | Name                     | True Example | False Example |
| -------- | ------------------------ | ------------ | ------------- |
| >        | Greater than             | `7 > 6`      | `6 > 6`       |
| >=       | Greater than or equal to | `6 >= 6`     | `6 >= 7`      |
| <        | Less than                | `6 < 7`      | `6 < 6`       |
| <=       | Less than or equal to    | `6 <= 6`     | `7 <= 6`      |
| ==       | Equals to                | `6 == 6`     | `6 == 7`      |
| !=       | Not equal to             | `6 != 7`     | `6 != 6`      |

## Logical Operators
* Logical Operators further enhance decision making in code
* Order of Precedence for Logical Operators
	* `()` -> `not` --> `and` --> `or

| Operator | Description                                                                                                 |
| -------- | ----------------------------------------------------------------------------------------------------------- |
| `and`    | Compares two logical expressions & returns `True` if BOTH expressions are `True                             |
| `or`     | Compares two logical expressions & returns `True` if at least ONE expressions is `True`                     |
| `not`    | Returns the opposite of the expression it precedes<br>-- `True` becomes `False`<br>-- `False` becomes `True |
| `in`     | Checks an item exists in an array-like structure & returns `True` or `False                                 |

```Python
# Examples 

print(False and True) # Output: False
print(False or True) # Output: True
print(not True) # Output: False
print(not False) # Output: True
print('com' in 'www.gmail.com') # True
print('com' in 'www.usda.gov') # False
print(3 in [1, 3, 5, 7, 9]) # True
print(3 in [0, 2, 4, 6, 8])  # False
```

```Python
# Example

name = 'Steven'
age = 40
# (False or True) and False -> True and False -> False
if (name == 'Carol' or name == 'Steven') and age <= 30:
    print("Retrieving customer data...")
else:
    print("Cannot find customer data") 
```

## Predicate functions
* Predicate Functions -- functions that return Boolean values (`True` or `False`)
	* `islower()` -- returns `True` if all letter characters in a string are lowercase
	* `isdigit()` -- returns `True` if a string contains ONLY number characters
	* `isalpha()` -- returns `True` if a string contains ONLY letter characters
```Python
string_1 = '@mazing!'
string_2 = '90210'

print(string_1.islower()) # Output: True
print(string_2.islower()) # Output: False
print(string_1.isdigit()) # Output: False
print(string_2.isdigit()) # Output: True
print(string_1.isalpha()) # Output: False
print(string_2.isalpha()) # Output: False
```


---
---
# Docstrings
## What are Docstrings?
* Docstrings -- comments that describe the purpose and specifics of public modules, functions, classes, and methods. 

## Working with Docstrings
### Creating Docstrings
* Docstrings are created using a set of triple single (`''' '''`) or double quotes (`""" """`)
```python
def get_life_expectancy(hamster_obj):
        """Predicts life expectancy for a given hamster.
        
        Might produce worse accuracy for Roborovski dwarf hamster.
        """
        # unpacking features of the hamster object
    current_age = hamster_obj['current_age']
    gender = hamster_obj['gender']
    living_condition = hamster_obj['living_condition']
```


---
---

# Lexicographical Order

## What is Lexicographical Order?
* Similar to alphabetical order except that it takes letter case into account as well as other text characters like numbers and symbols.
## Priority for Lexicographical Order
* The order for Lexicographical Order (in ascending order)
	1) Special characters and symbols 
		`!, @, #, $, %, ^, &, *, (, ), [, ], {, }, =, +, -, <, >, |, \, /, ?, :, ;, ", , , ., ~,  , _`
	2) Numbers
	3) Uppercase letters (A-Z)
	4) Lowercase letters (a-z)
```Python
print(sorted('3 cats!')) # Output: [' ', '!', '3', 'a', 'c', 's', 't']
```


---
---

