See 
* [[Py - Introduction to Python]]
Resources:
* Documentation: [datetime](https://docs.python.org/3/library/datetime.html)

---
# Datetime Module

## What is the `datetime` module?
* The `datetime` module supplies classes for manipulating dates and times.
* While date and time arithmetic is supported, the focus of the implementation is on efficient attribute extraction for output formatting and manipulation.

---
# Getting Started
## Importing `datetime` module
```python
import datetime as dt
```


---
# Working with the `datetime` Module

## Working with current date
* Some attributes/methods return a number; python counts from 0
```python
now = dt.datetime.now() # Retrieves current date/time
year = now.year # Accesses the year attribute
month = now.month # Accesses the month attribute

day_of_week = now.weekday() # Returns the day of week (as a number); python is 0-based so 0 is Monday and 6 is Sunday
```

## Working with a unique date
* When creating a date, only `year`, `month`, and `day` are REQUIRED, all others are optional
```Python
date_of_birth = dt.datetime(year=1995, month=10, day=31) 
```