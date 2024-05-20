See:
* [[Py - Introduction to Python]]
* [[Py - Python Basics]]
Resources:
* 

---
# Dynamic Typing


## What is Dynamic Typing?
* Python is Dynamically Typed -- variable types are determined and checked at runtime rather than during compilation
* **Dynamic** Typing -- runtime objects (values) have a type, as opposed to static typing where variables have a type.
* Advantageous of Dynamic Typed Languages
	* No need to explicitly declare the variable type before using it

```Python
name = "Educative"
gender = "Female"
money = 10000

print("Name is", name, "type of variable is", type(name))
print("Gender is", gender, "type of variable is", type(gender))
print("Gender is", money, "type of variable is", type(money))
```

## Dynamically Changing the Data Type
* A variable's data type can be change by changing the content
```Python
a = 3 # variable a is of integer type
a = "Hello" # variable a is now of string type (changed by changing the content of the variable)
```


# Strong Typing
#### What is Strong Typing?
* **Strong** Typing -- the type of a value doesn't change in unexpected ways.
	* A string containing only digits doesn't magically become a number. 
	* Every change of type requires an explicit conversion.
