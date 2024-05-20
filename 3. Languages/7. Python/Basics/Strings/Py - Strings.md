See 
* [[Py - Introduction to Python]]
* [[Py - String Methods]]
* [[Py - (Glossary) Built-in Functions]]
Resources:
* 

---
# Strings

## What is a string?
* Strings contain data in the form of text
* The data type is `string`

## Working with Strings
### Declaring strings
* Either single (`' '`) or double (`" "`) quotes
```Python
print("this is a string") # this is a string
```

### String Indexing
* Strings are made of individual characters, which can be accessed by their index (which starts are `0`)
* Indexes are used to retrieve a substring (a slice)
	* The character at the last index value is not included in the substring
	* How to remember: `length of substring = upper index - lower index
```Python
string = "Bottom of the 9th"
print(string[0]) # B

message = "Let's learn about strings!"
print(message[6]) # l
```

```Python
string = "Bottom of the 9th"
print(string[7:13]) # of the
```

### String Length
* The length of a string is equal to the number of characters it has
* The `len()` function can be used to calculate the length of a string 
```python
lullaby = "Twinkle twinkle little star, how I wonder what you are, up above the world so high, like a diamond in the sky, twinkle twinkle little star, how I wonder what you are."

print(len(lullaby)) # 166

# Empty string has a length of 0, but is of string type
print(type('')) 
print(len(''))
```

### Adding or Multiplying Strings
* Adding 2 or more strings will concatenate them
```Python
# Example

# This will throw an error; cannot added str and int
result = "Chinese is spoken by "  + 1400 + " million people worldwide" 
```
* Multiplying strings can be used to create a repeated version of the string
```Python
# Example

print(' 123ABC ' * 6)
# Output:  123ABC  123ABC  123ABC  123ABC  123ABC  123ABC
```


---
### Declaring Line breaks (`\n`)
* Newline (`\n`) is used to print information on a new line
```python
print("Max's favorite number is...\n3")
```

### Declaring Indents (`\t`)
* The tab character (`\t`) is used to indent text
```python
print("\tMax's favorite movie is:\nthe last one he watched\n\t\t:D") 
```

### Escaping Characters
* The backslash (`\`) is used to escape characters that should be included in the string, by proceeding it
```Python
print("Britney Spears once said, \"She's so lucky, she's a star\".")
```

### Including a slash in text
* The double slash (`\\`) is used to include a slash in text
```python
print('yes\\no') # yes\no
```

### Multi-line Text
* Use triple single quotes (`''' '''`) or triple double quotes (`""" """`) to spread text out across multiple lines
```python
multi_string = """This is line 1.
This is line 2.
This is line 3."""
```


---
# F - Strings

## Working with F-Strings

### Declaring F-Strings
* Preface the string with an `f` before the opening single or double quote
* The variable / expression to be included should be placed inside curly braces (`{}`)
```python
name = 'Max'
age = 23
height = 5.7

print(f"{name} is {age} years old and {height} feet tall.")
# Max is 23 years old and 5.7 feet tall.
```

```Python
name = 'Max'
age = 23
print(f"Next year, {name} will be {age + 1} years old.") # Next year, Max will be 24 years old.
```

### Formatting Numbers using F-Strings
* Numbers can be formatted to specific decimal places or percentage points
	* Formatting number using (`:.nf`)
		* `n` -- the number of decimal places to display in the number
	* Formatting percentages using (`:.n%`)
		* `n` -- the number of decimal places to display in the percentage
```python
total_price = 111
apples_total = 203
apples_bought = 98

share_bought = apples_bought / apples_total # 0.4827
apple_price =  total_price / apples_bought # 1.1326

print(f"I bought {share_bought:.0%} of the apples and paid {apple_price:.2f} per apple") # I bought 48% of the apples and paid 1.13 per apple
```

### Creating Strings of Specific Lengths
* The curly braces (`{: < n}`, `{: > n}` , `{: ^ n}`) in a formatted string can be used to create a string that is n spaces long
	* `n` -- the length of the string plus any necessary spaces.
```python
greeting = 'hi!'

# create a string 10 characters long with additonal spaces to the left
print(f"{greeting:>10}")  # '       hi!'

# create a string 10 characters long with additonal spaces to the right
print(f"{greeting:<10}")  # 'hi!       '

# create a string 10 characters long with additonal spaces to the right & left
print(f"{greeting:&10}")  # '   hi!   '
```
