See
* [[Py - Introduction to Python]]
* [[Py - (Glossary) Built-in Functions]]
Resources
* 

---
# Tuples
## What are Tuples?
* A data structure (with an array-like structure) similar to a list
* Can contain any number of items of any data type, which are indexed by position

## Difference between Tuples and Lists
* Tuples are immutable (cannot be changed)
	* Once created cannot add or remove items
* Lists are mutable (can be changed)
* Tuples can be used as dictionary keys
```Python
# Example -- trying to change a value in a tuple

movie_info = ('Fight Club', 3999, ['thriller', 'drama', 'crime'], 139, 8.644)
movie_info[1] = 1999

print(movie_info) 
# Output: TypeError: 'tuple' object does not support item assignment 
```

## When to use Tuples?
* Use tuples when the data should not be modified anywhere in the code


---
# Working with Tuples

## Converting a List to a Tuple
* The `tuple()` function can be used to convert a list to tuple
* The `list()` function can be used to convert a tuple to a list 
```Python
# Example -- Converting a List to a Tuple

movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644]
print(tuple(movie_info)) 
# Output: ('Fight Club', 1999, ['thriller', 'drama', 'crime'], 139, 8.644)
```

## Creating Tuples
* Tuples use parentheses `()` for creation
```Python
# SYNTAX
tuple_name = (item1, item2, itemN, ...)
```

```Python
# Example -- Creating a Tuple
movie_info = ('Fight Club', 3999, ['thriller', 'drama', 'crime'], 139, 8.644)
```

## Indexing Tuples
* Tuples are indexed using square bracket notation (like lists)
```Python
# Example -- Indexing a Tuple
movie_info = ('Fight Club', 3999, ['thriller', 'drama', 'crime'], 139, 8.644)

print(movie_info) 
# Output: ('Fight Club', 3999, ['thriller', 'drama', 'crime'], 139, 8.644)

print(type(movie_info)) # Output: <class 'tuple'>
print(movie_info[2]) # Output: ['thriller', 'drama', 'crime'] 
print(movie_info[2][1]) # Output: thriller
print(len(movie_info)) # Output: 5
```

## Slicing a Tuple
* Tuples can be sliced using square bracket notation (like lists)
```Python
# Example -- Slicing a Tuple
movie_info = ('Fight Club', 3999, ['thriller', 'drama', 'crime'], 139, 8.644)

print(movie_info[1:4]) # Output: (3999, ['thriller', 'drama', 'crime'], 139)
```
