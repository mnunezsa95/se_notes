See 
* [[Py - Introduction to Python]]
* [[Py - List Methods]]
Resources:
* 

---
# Lists 

## What are lists?
* Lists are one of the four main data types in Python
* Lists are used to store multiple items in a single variable.

## Characteristics of a List
* Ordered: They contain elements or items that are sequentially arranged according to their specific insertion order.
* Zero-based: They allow you to access their elements by indices that start from zero.
* Mutable: They support in-place mutations or changes to their contained elements.
* Heterogeneous: They can store objects of different types.
* Growable and dynamic: They can grow or shrink dynamically, which means that they support the addition, insertion, and removal of elements.
* Nestable: They can contain other lists, so you can have lists of lists.
* Iterable: They support iteration, so you can traverse them using a loop or comprehension while you perform operations on each of their elements.
* Sliceable: They support slicing operations, meaning that you can extract a series of elements from them.
* Combinable: They support concatenation operations, so you can combine two or more lists using the concatenation operators.
* Copyable: They allow you to make copies of their content using various techniques.

## Basic Properties of Lists
* Lists allow us to store a collection of values within a single data structure
* Lists are of the `'list'` type
* Lists items are called elements or values
* Lists can contain items with different types, and items of any data type are allowed to be in a list — even other lists:


---
# Working with Lists
## Creating Lists
* Created using a name and setting it equal to square brackets `[ ]`
* List values are separated by commas
```Python
# List syntax
list_name = [value_1, value_2, value_3, ...]
```

```Python
# Example
favorite_films = ['The Graduate', 'Reservoir Dogs', 'Fear and Loathing in Las Vegas']

print(favorite_films) # prints the list 
print(type(favorite_films)) # Output: <class 'list'>
print(len(favorite_films)) # Output: 3
```

```Python
# Example -- Lists with various data types
my_list = ['<3', 77, 3.89, True, False, ['sub', 'list', 0.2]]

print(my_list)
print(len(my_list)) 
```

## Indexing Lists
* Values in a list are indexed (indexing begins at 0)
```Python
# Example 
movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644]

print(movie_info[0]) # Output: Flight Club
print(type(movie_info[0])) # Output: <class 'str'>
print(type(movie_info[2][0])) # Output: thriller
```

## Negative Indexing
* Can index from the end of the list (starting with -1) to traverse the list backwards
```Python
movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644]

print(movie_info[-1]) # Output: 8.644
print(movie_info[-2]) # Output: 139
```

## Slicing lists
* When a list is sliced, it returns another list
```Python
# Example -- Slicing from betweem two specific indices
movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644]

print(movie_info[2:4]) # Output: [['thriller', 'drama', 'crime'], 139, 8.644]]
print(type(movie_info[2:4])) # Output: <class 'list'>
```
``
```Python
# Example -- Slicing from beginning up to a specific index
movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644]

print(movie_info[:3]) # Output: ['Fight Club', 1999, ['thriller', 'drama', 'crime']] 
```

```Python
# Example -- Slicing from a specific index to the end of the list
movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644]

print(movie_info[2:]) # Output: [['thriller', 'drama', 'crime'], 139, 8.644] 
```

```Python
piano_keys = ["a", "b", "c", "d", "e", "f", "g"]
piano_keys[2:5]  # Slicing list from position 2-5
piano_keys[2:]  # Slicing list from position 2 to the end
piano_keys[2:5:2]  # Slicing list from position 2 to 5, skipping every 2
piano_keys[::2]  # Slicing list from begining to end, skipping every 2
piano_keys[::-1]  # Slicing list from the end to beginning (reverses the list)
```

Replacing Items in a List
* Items can be replaced by accessing the index and editing the value
```Python
movie_info = ['Fight Club', 2999, ['thriller', 'drama', 'crime'], 139, 8.644]
movie_info[1] = 1999

print(movie_info) 
# ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644] 
```

## Adding Items to a List 
* Items can be added to the end of a list using the `append()` method
```Python
count = [1, 2, 3, 4, 5, 6]

count.append(7)
print(count) # Output: [1, 2, 3, 4, 5, 6, 7]
```

* Items can be added at a specific index using the `insert()` method 
```Python
dark_knight_movie = ['The Dark Knight', 'USA']
dark_knight_movie.insert(1, ['fantasy', 'action', 'thriller'])

print(dark_knight_movie) 
# ['The Dark Knight', ['fantasy', 'action', 'thriller'], 'USA']
```

## Removing Items from a List
* Items can be removed from a list using the `pop()` method
```Python
movies = ['Matrix', 'Matrix 2', 'Matrix 3']
movies.pop()
print(movies) # Output: ['Matrix', 'Matrix 2'] 
```

```Python
movies = ['Matrix', 'Matrix 2', 'Matrix 3']
movies.pop(1)
print(movies) # Output: ['Matrix', 'Matrix 3'] 
```

## Sorting Items in a List
* Items in a list can be sorted lexicographically using the `sorted()` function, which returns a new sorted list 
```python
years = [1994, 1972, 2008, 1993, 2003, 1994, 1966, 1999, 1962, 1997]
years_sorted = sorted(years)

print(years_sorted) 
# [1962, 1966, 1972, 1993, 1994, 1994, 1997, 1999, 2003, 2008] 

print(sorted(years, reverse=True)) 
# [2008, 2003, 1999, 1997, 1994, 1994, 1993, 1972, 1966, 1962] 
```

* Items in a list can be sorted lexicographically using the `sort()` method 
	* `Sort()` does not return a new list (object), which changes the list it was called on
```python
years = [1994, 1972, 2008, 1993, 2003, 1994, 1966, 1999, 1962, 1997]
years.sort()

print(years) # [1962, 1966, 1972, 1993, 1994, 1994, 1997, 1999, 2003, 2008] 
```


---

# List Comprehension
## What is List Comprehension?
* A way of creating a list in python from scratch or from other lists

### Using List Comprehension
* Using list comprehension to create a new list
```Python
# SYNTAX

new_list = [new_item for item in list]
## new_list is the name of the new list
## new_item is the expression
## item is the name assigned to each item in list
#$ list is the old list
```

```Python
# Example

numbers = [1, 2, 3]
new_list = [n + 1 for n in numbers] # [2, 3, 4]
```

```Python
# Example

name = "Harper"
letters_list = [letter for letter in name] # ["H", "a", "r", "p", "e", "r"]
```

```Python
# Example

range_list = [number * 2 for number in range(1, 5)] # [2, 4, 5, 8]
```

```Python
# Example

numbers2 = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
squared_numbers = [num**2 for num in numbers2]
```

```Python
# Example

names = ['Steven', 'Carol', 'Yuna', 'Greg']
name_lengths = [len(name) for name in names] # [6, 5, 4, 4]
```

```Python
# Example

year = [2023 for i in range(100)]
print(f"First five elements: {year[:5]}") # First five elements: [2023, 2023, 2023, 2023, 2023]
```

```Python
# Example

names = ['Steven', 'Carol', 'Yuna', 'Greg']
welcome = [f"Welcome, {name}!" for name in names]

for i in range(len(welcome)):
  print(welcome[i]) 
  # Welcome, Steven! Welcome, Carol! Welcome, Yuna! Welcome, Greg!
```

### Using List Comprehension & Conditionals
* Conditional statements can be used in list comprehension
```Python
# Syntax
new_list = [new_item for item in list if test]

## new_list is the name of the new list
## new_item is the expression
## item is the name assigned to each item in list
## list is the old list
## if test will only execute expression if the test is passed
```

```Python
# Example

names = ["Alex", "Beth", "Caroline", "Dave", "Eleanor", "Freddie"]
short_names = [name for name in names if len(name) < 5] 
# ["Alex", "Beth", "Dave"]

long_names = [name.upper() for name in names if len(name) > 5]
# ['CAROLINE', 'ELEANOR', 'FREDDIE']
```

```Python
# Example

numbers3 = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
even_nums = [num for num in numbers3 if num % 2 == 0] # [2, 8, 34]
```

```Python
# Example
list_1 = ["3", "6", "5", "8", "33", "12", "7", "4", "72", "2", "42", "13"]
list_2 = ["3", "6", "13", "5", "7", "89", "12", "3", "33", "34", "1", "344"]

common_numbers = [int(num) for num in list_1 if num in list_2]
# [3, 6, 5, 33, 12, 7, 13]
```