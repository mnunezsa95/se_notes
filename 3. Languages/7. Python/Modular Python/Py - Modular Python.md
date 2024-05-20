See: [[Py - Introduction to Python]], [[Py - Installing Packages, Modules, and Libraries]], [[Py - Modules, Packages and Libraries]]

---

#### Using Modules 
* Create a file with the `.py` extension
* Import the created file into a different file using the `import` keyword

```Python
# module.py
def foo():
  print('Running foo')

print("Hi! I'm a module")
```

```python
# myscript.py
import module
print("Running the main program")
```

#### Accessing imports
* When a module is imported, its namespace (along with its attributes) becomes available
	* Attributes are accessed using dot notation

```Python
# module.py
import re

def check_email(string: str):
  if re.match('[.\w]+@\w+[.]\w+', string):
    print('correct')
  else:
    print('check email address')

def check_age(age: int):
  if age >= 50:
    print('access granted')
  else:
    print("you're just too young")
```

```Python
# myscript.py
import module

email = input()
module.check_email(email) # the check_email() function is an attribute of the 'module' file, so we can access using dot notation
```

## Ways to Import
* Basic import
* Single Import (from...import)
* Alias import 
* Import everything
```Python
# Basic import
import module

# Single import
from module_name import thing_in_module

# Alias import
import module_name as alias_name # alias_name can be everything

# Import everything (unpacks all attributes into the current namespace)
from module import *

```

#### Check if main
* An entry-point `if` block can be used to  prevent code from running when being imported
* The  `__name__` variable for the main script is always given the string value `'__main__'`, while the `__name__` variable for modules imported by the main script are given string values that are simply the module name.
```Python
# module_1.py

def useful_function():
  print('working')

if __name__ == "__main__":
  print("testing function...")
  useful_function()
```

```Python 
# module_2.py
import module_1 # importing module_1

def double_check():
  print('Twice now:')
  module_1.useful_function()
  module_1.useful_function()

if __name__ == "__main__":
  print("testing function...")
  double_check()
```
* If we run `module_2.py `as our main script, then `module_2.py` has `'__main__'` as its `__name__` value and `module_1.py `has `'module_1' `as its `__name__` value:


