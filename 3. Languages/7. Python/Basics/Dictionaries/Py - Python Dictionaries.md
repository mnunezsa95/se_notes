See 
* [[Py - Introduction to Python]]
* [[Py - Dictionary Methods]]
Resources


---
# What are Dictionaries?
* Dictionaries store and process data when it’s convenient for each value to be accessed by name rather than index position
* Dictionaries can be used to create tables and import/export data from text files or databases.

## Dictionaries: What are key-value pairs?
* Dictionaries use key-value pairs to store information
* Rules for Keys
	* Must be an immutable data type (stings, booleans, integers, floats, tuples) 
* Rules for Values
	* Can be of any data type 


---
# Working with Dictionaries
## Creating Dictionaries
* Two ways to create a dictionary
	1) Using dictionary syntax (`{}`)
	2) Using the `dict()` function
		* Pass in key-value pairs as arguments 
```Python
laptops = {
  'lenovo': 399.99, 
  'apple': 749.99, 
  'hp': 349.99, 
  'dell': 599.99
} 

print(type(laptops)) # <class 'dict'>
print(len(laptops)) # 4
```

```Python
laptops = dict(lenovo=399.99, apple=749.99, hp=349.99, dell=599.99)
```

## Accessing Dictionary Values
* Dictionary values can be accessed using bracket (`[]`) notation and the key name
	* If key does not exist, python throws a "KeyError"
```python
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99} print(laptops['dell'])
```

* Retrieve a specified key from a dictionary using the `get()` method
```Python
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99}
print(laptops.get('lenovo', -1)) # 399.99
print(laptops.get('acer', -1)) # -1
```

* Access the keys and values of a dictionary using the `items()` method 
	* The first tuple consists of the keys
	* The second tuple consists of the values
```python
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99}

print(laptops.items()) 
# dict_items([('lenovo', 399.99), ('apple', 749.99), ('hp', 349.99), ('dell', 599.99)])

print(type(laptops.items())) # <class 'dict_items'>

# Converting to a list
print(list(laptops.items())) 
# [('lenovo', 399.99), ('apple', 749.99), ('hp', 349.99), ('dell', 599.99)]
```

* Access the keys of a dictionary using the `keys()` method
```Python
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99}

print(laptops.keys()) # dict_keys(['lenovo', 'apple', 'hp', 'dell'])
print(type(laptops.keys())) # <class 'dict_keys'>
```

* Access the values of a dictionary using the `values()` method
```Python
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99}

print(laptops.values()) # dict_values([399.99, 749.99, 349.99, 599.99])
print(type(laptops.values())) # <class 'dict_values'>
```


---
# Modifying Dictionaries

## Updating dictionary values
* Dictionary values can be updated using bracket notation to access the entry and modify its value
```Python
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99} laptops['dell'] = 499.99
print(laptops) # {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 499.99}
```

## Adding new items to a dictionary
* New items can be added to a dictionary by using bracket notation
```python
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99}
laptops['acer'] = 472.99

print(laptops)  # {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99, 'acer': 472.99}
print(len(laptops)) # 5
```

## Removing items
* Removing an item from a dictionary using the `pop()` method
```python
# Example
laptops = {'lenovo': 399.99, 'apple': 749.99, 'hp': 349.99, 'dell': 599.99}
removed_value = laptops.pop('apple')

print(laptops) # {'lenovo': 399.99, 'hp': 349.99, 'dell': 599.99}
print(len(laptops)) # 3
print(removed_value) # 749.99
```

```Python
# Example
coffee_stocks = {'SBUX': 120.29, 'DKNN': 106.48, 'BROS': 76.25}
dnkn_price = coffee_stocks.pop("DKNN")

coffee_stocks["DNKN"] = dnkn_price
print(coffee_stocks)
```


---

# Dictionary Comprehension

## What is Dictionary Comprehension?
* Dictionary comprehension is a method for transforming one dictionary into another dictionary. 
* During this transformation, items within the original dictionary can be conditionally included in the new dictionary, and each item can be transformed as needed.

#### Using Dictionary Comprehension
```Python
# Syntax

new_dict = {new_key:new_value for item in list}
new_dict = {new_key:new_value for (key,value) in dict.items()}
new_dict = {new_key:new_value for (key,value) in dict.items() if test}

# new_dict is the name of the new dict
# new_key:new_value are the new values to be used in the dict
# key,value are key values to be grabbed from the existing dict
# list/dict.items() is the name of the old list / old dictionary
```

```Python
# Example

names2 = ["Alex", "Beth", "Caroline", "Dave", "Eleanor", "Freddie"]
students_scores = {student: random.randint(1, 100) for student in names2}

passed_students = {
  student: score for (student, score) in students_scores.items() if score >= 60
}
```

```Python
# Example

sentence = "What is the Airspeed Velocity of an Unladen Swallow?"
len_of_words = {word: len(word) for word in sentence.split()}

# {'What': 4, 'is': 2, 'the': 3, 'Airspeed': 8, 'Velocity': 8, 'of': 2, 'an': 2, 'Unladen': 7, 'Swallow?': 8}
```

```Python
# Example

weather_c = { "Monday": 12, "Tuesday": 14, "Wednesday": 15, "Thursday": 14,        "Friday": 21, "Saturday": 22, "Sunday": 24,
}
weather_f = {day: (temp * 9 / 5) + 32 for (day, temp) in weather_c.items()}

# {'Monday': 53.6, 'Tuesday': 57.2, 'Wednesday': 59.0, 'Thursday': 57.2, 'Friday': 69.8, 'Saturday': 71.6, 'Sunday': 75.2}
```