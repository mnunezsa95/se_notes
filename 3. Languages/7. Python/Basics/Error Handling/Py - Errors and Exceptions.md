See: [[Py - Introduction to Python]], [[Py - Error Handling]]
Resources:
* Documentation: [Built-in Exceptions](https://docs.python.org/3/library/exceptions.html#Exception)

---
# How to Read Errors
* Errors in Python are called `traceback` messages. 
	* `Traceback` means a program is written and checked every step of the way. If something doesn't work, an error is produced.
* Long traceback messages means that Python performed alot of functions before encountering an error
![](https://lh7-us.googleusercontent.com/_sAAJUmqZTbK7eyzIa0L3Jvfu3QM7LoxL68rDfXH2gvcLB87QgSu0njyWhS1qVu-c_U3dwNYvZsQBQS9XHaimy_lCF92FpDRbyP_ZQ2AtOJNdLl3OzC_HdOZBOfYjJ0SMpBsmx3BGSLLuDsFv8ycf9s)

## Errors & Exceptions
* Errors and exceptions can lead to unexpected behavior or even stop a program from executing.
* Errors -- thrown when an operation or code cannot be executed
* Exceptions -- conditions that interrupts the normal flow of the program
	* All exceptions are under the generic `Exception` object type, but each specific type of exception is its own unique object

## Reasons for Errors
* Many different reasons
* Three most common reasons:
	1) Improper syntax
	2) Forbidden operations
	3) Reference to invalid variables (namespace errors)
* Errors will STOP the execution of the code at that point

# Types of Errors
#### SyntaxError
* A parentheses, colon or comma was forgotten.
```Python
2_name = 'Mary'
print(2_name) # SyntaxError -- variables cannot start with a number
```

#### IndentationError
* There's an incorrect number of indentations
```Python
for name in names:
          print(name) # IndentationError
```

#### NameError
* A variable is referenced before its been declared or assigned a value
* A variable that is not declared is referenced (caused by typos)
```Python
apple_price = 1.25
banana_price = 0.99

print("Total price:", apple_price + banana_price + kiwi_price) 
# NameError -- kiwi_price is not defined
```

#### IndexError
* An element that is not in the list or dictionary is referenced
```python
list = [1, 2, 3, 4]
print(list[5]) # IndexError -- there is no position 5 in the list
```

#### TypeError
```Python
numbers = 'one two three four' + 5
print(numbers) # TypeError -- cannot add string and number
```

#### ZeroDivisionError
```python
print(777 / 0) # throws an error; cannot divide by 0
```


