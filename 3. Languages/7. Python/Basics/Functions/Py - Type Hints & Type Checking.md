See: [[Py - Introduction to Python]], [[Py - Data Types]], [[Py - Functions]]

---

## Type Hinting
* Useful feature introduced in [PEP 484](https://peps.python.org/pep-0484/), that allows programmers to keep track of the code, but does not change the actual behavior of the Python interpreter
* Type Hinting allows for a variable's and/or an argument's data type to be declared

#### Declaring a Variable's Data Type
* To declare a data type use a colon (`:`) followed by the data type
	* Rule(s): 
		* No space before the colon
		* One space after a colon:
```Python
# Declare the data type of a variable
age: int
name: str
height: float
is_human: bool
```

#### Declaring a Function's Data Type
* To declare a data type use a colon (`:`) followed by the data type
	* Rule(s): 
		* No space before the colon
		* One space after a colon:
		* Use spaces are the `=` sign when combining with a default value
```python
def police_check(age: int):
  if age > 18:
    can_drive = True
  else:
    can_drive = False
  reutrn can_drive

print(police_check(12))
```

#### Declaring the Data Type of an Output
* To declare a data type use an arrow (`->`) followed by the data type (before the colon of the function declaration)
	* Rules:
		* Use spaces around the `->` arrow
```Python
def police_check(age: int) -> bool:
  if age > 18:
    can_drive = True
  else:
    can_drive = False
  reutrn can_drive

print(police_check(12))
```

```Python
# Specifying that:
## the 'text' arg should be of the string type
## the 'sep' arg should be of the string type and has a deafult value of " "
## the function will return a list
def list_of_words(text: str, sep: str = " ") -> list:
    return text.split(sep)
```


---

## Type Checking
* Type Hints are not enforced by Python, but there are tools for performing type checking:
	* [mypy](https://mypy-lang.org/): a tool used for type checking
#### Using the `mypy` tool
* Install `mypy`
```bash
pip install mypy
```
* Run the tool 
```bash
mypy list_of_words.py
```