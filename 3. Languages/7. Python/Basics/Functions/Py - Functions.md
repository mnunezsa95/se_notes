See: [[Py - Introduction to Python]], [[Py - (Glossary) Built-in Functions]]
Resources: [Python-Builtin Function](https://docs.python.org/3/library/functions.html)

---
#### What is a function?
* A function is a subprogram built into Python or created within a program for a specific task.
* Functions can take in **parameters**
	* A value that we pass to a function, it is input information for the function.

#### Creating a function
* `def` is a keyword used to define a function
* Functions should be named
* Parentheses are used to pass in inputs
* Colon is used to end the definition
```Python
def my_function():
  print("Hello")
  print("Bye")
```

#### Calling the function
* Functions must be invoked in order to run
```Python
my_function() # calling the function
```


---
#### The `return` statement
* The `return` keyword is used to return some output from the function
* A function can have any number of `return` statements, but ONLY one can be executed
* When more than one variable is listed after the `return` statement, a tuple is received including the values
	* The tuple can be unpacked using the following notation
```python
tuple_var_1, tuple_var_2,... = function(arg1, arg2)
```
* Example
```Python
def categorize_sales(sales, dates): 
  categories = {} 
  for i in range(len(sales)): 
    amount = sales[i] 
    date = dates[i] 
    if amount < 2000: 
      categories[date] = 'low' 
    elif amount < 6000: 
      categories[date] = 'medium' 
    else: categories[date] = 'high' 
  avg_sales = sum(sales) / len(sales) 
  return categories, avg_sales 

sales = [9412, 1778, 2987, 2512, 3999, 7655, 11003] 
dates = ['2022-10-02', '2022-10-03', '2022-10-04', '2022-10-05', '2022-10-06', '2022-10-07', '2022-10-08']

weekly_sales, avg = categorize_sales(sales, dates)
print(f"Tuple with two items:\n{output}") 
print(f"First item from tuple:\n{output[0]}") 
print(f"Second item from tuple:\n{output[1]}")
```
