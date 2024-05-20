See [[Py - Introduction to Python]]

#### What are for Loops?
* Loops are useful for executing a piece of code over and over again

#### The `for loop`
* Syntax
	* Starts w/ the keyword `for`
	* Declares a loop variable (can be named anything)
		* ONLY exists within the execution of the loop
	* Uses the `in` keyword
	* Followed by the item/list to be looped
	* Ends in a colon (`:`)
```Python
for loop_variable in item_or_list:
	# code to execute
```

#### What can be looped?
* The `for loop` can loop over items in a list or dictionary or tuple, characters in a string, and more.
```Python
# Looping over a list
film_genres = ['SCIFI', 'drama', 'Thriller', 'comedy', 'Action']

for genre in film_genres:
    print(genre) # Output: SCIFI drama Thriller comedy Action
```

# Loop Techniques

#### The `range()` function
* Used to perform a set of actions/instructions a number of times, rather than looping through items (see [[Py - (Glossary) Built-in Functions]])
	* Produces a set of consecutive whole numbers from 0 up to, but not including `n`
		* Two numbers can be used to start at a different number
```python
for i in range(n):  # n is a number
	# code to execute

for i in range(n, e):  # n is a number to start; e is a number to end
	# code to execute
```

```Python
# a list
film_genres = ['SCIFI', 'drama', 'Thriller', 'comedy', 'Action']

# looping through the length of the list
for i in range(len(film_genres)):
    film_genres[i] = film_genres[i].lower() # reassigning each item at position i

print(f"Processed data: {film_genres}")  # printing finished product
# Output: Processed data: ['scifi', 'drama', 'thriller', 'comedy', 'action'] 
```

#### Initialization
* Initialization = creating a variable that will change throughout the loop life-cycle
```Python
score_dict = {'quiz 1': 61, 'exam 1': 99, 'quiz 2': 72, 'exam 2': 87, 'quiz 3': 80, 'exam 3': 95}

# initialize the list
scores = []

for score in score_dict.values():
    scores.append(score)
    
print(scores) # Output: [61, 99, 72, 87, 80, 95] 

# initialize the sum
total = 0

for score in scores:
    total = total + score

print(f"Average score: {total / len(scores):.1f}") # Output: Average score: 82.3
```

#### Counters
* Used to keep track of how many times something happens over all of the loop iterations
* How it works:
	* Initialize the counter outside of the loop and then increment it within the loop
```Python
scores = [61, 99, 72, 87, 80, 95] 

# initialize the sum and counter
total = 0
k = 0

for score in scores:
    k = k + 1
    total = total + score

print(f"The loop executed {k} times.") 
```