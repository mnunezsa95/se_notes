See
* [[Py - Introduction to Python]]
* [[Py - Python Lists]]
* [[Py - List Comprehension]]

---
#### `append()`
* Adds a new item to the end of a list; changes the original list
	* Arguments
		1) `value` -- the value to append (add to end of list)
```python
# SYNTAX
list_name.append(value)
```

```Python
# Example

dk_info = ['The Dark Knight', "fantasy, action, thriller", 152]
rating = 8.917
dk_info.append(rating)
print(dk_info) # Output: ['The Dark Knight', 'fantasy, action, thriller', 152, 8.917]
```

#### `extend()`
* Extends the list by appending all the items from the iterable
	* Arguments
		1) `list` -- the list to be appended
```python
# SYNTAX
list_name.extend(list)
```

```Python
# Example
states_of_america = ["Delaware", "Pennsylvania", "New Jersey", "Georgia", ...]
states_of_america.extend(["Pennyland", "Harperland"])

print(states_of_america) # Output: Delaware, Pennsylvania, New Jersey, Georgia, Pennyland, Harperland
```

#### `insert()`
* Adds a new item a specific index
	* Arguments
		1) `index` -- the location at which the value should be added
		2) `value` -- the value to be inserted
```Python
# SYNTAX
list_name.insert(index, value)
```

```python
# Example
dk_info = ['The Dark Knight', "fantasy, action, thriller", 152, 8.917]
year = 2008

# inserting the year at position 1 in the list
dk_info.insert(1, year) # Output: ['The Dark Knight', 2008, 'fantasy, action, thriller', 152, 8.917]
```

#### `pop()`
* Removes an item from a list
	* By Default, the last item is removed; an index can be specified to overwrite this behavior
	* Arguments
		1) `index` -- optional; location of the value to remove
```python
# SYNTAX
list_name.pop(index)
```

```Python
# Example
movies = ['Matrix', 'Matrix 2', 'Matrix 3']
deleted_movie =  movies.pop(1)

print(movies) # Output: ['Matrix', 'Matrix 3']
print(deleted_movie) # Output: Martix 2
```

#### `sorted()`
* Sorts a list lexicographically; returns a new sorted list; By default, the function sorts in ascending order, which can be overwritten using `reverse=true` argument
	* Arguments
		1) `list` -- the list to be sorted
		2) `reverse=True` -- a named argument used to reverse the sort order
```Python
# SYNTAX
sorted(list, reverse=True)
```

```Python
# Example
years = [1994, 1972, 2008, 1993, 2003, 1994, 1966, 1999, 1962, 1997]
years_sorted = sorted(years)

print(years) # Output: [1994, 1972, 2008, 1993, 2003, 1994, 1966, 1999, 1962, 1997]
print(years_sorted) # Output: [1962, 1966, 1972, 1993, 1994, 1994, 1997, 1999, 2003, 2008] 
print(sorted(years, reverse=True)) # Output: [2008, 2003, 1999, 1997, 1994, 1994, 1993, 1972, 1966, 1962] 
```

#### `sort()`
* Sorts a list lexicographically; does NOT return a new list (modifies existing one)
	* Arguments
		1) `reverse=True` -- a named argument used to reverse the sort order
```Python
# SYNTAX
list_name.sort(reverse=True)
```

```Python
# Example
years = [1994, 1972, 2008, 1993, 2003, 1994, 1966, 1999, 1962, 1997]

years.sort(reverse=True)
print(years) # Output: [2008, 2003, 1999, 1997, 1994, 1994, 1993, 1972, 1966, 1962] 
```

#### `split()`
* Splits a string into a list; By default, `split()` will split words at a space, which can be overwritten by specifying the separator
	* Arguments
		1) `separator` -- determines how to split the string
```python
# SYNTAX
list_name.split(separator)
```

```Python
# Example
phrase = 'Cuckoo builds a nest!'
words = phrase.split()
print(words) # Output: ['Cuckoo', 'builds', 'a', 'nest!'] 

phrase = 'The * stars * are * out * tonight'
words = phrase.split(' *')
print(words) # Output: ['The', ' stars', ' are', ' out', ' tonight'] 
```

#### `index()`
* Returns a zero-based index in the list of the first item whose value is equal to _x_. Raises a [`ValueError`](https://docs.python.org/3/library/exceptions.html#ValueError "ValueError") if there is no such item.
	* Arguments
		1) `value` -- the value for which we want to find the index
		2) `start` -- (optional) the starting index
		3) `end` -- (optional) the ending index
```python
# SYNTAX
list_name.index(value)
```

```Python
# Example
position = "B3"
letter = position[0].lower()
abc = ["a", "b", "c"]
print(abc.index(letter)) # Output: 1 
# Returns 1 because the index of "B" is 1 on the abc list
```
