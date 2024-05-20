See 
* [[Py - Introduction to Python]]
* [[Py - Strings]]
Resources:
* [Python String Methods](https://www.w3schools.com/python/python_ref_string.asp)

---
# String Methods


##### `capitalize()`
* Converts the first character in the entire string to upper case and converts the rest to lowercase
	* Arguments
		1) None
```Python
string.capitalize()
```

```Python
txt = "hello, and welcome to my world."  
x = txt.capitalize()
print(x) # Hello, and welcome to my world.
```

```Python
txt = "python is FUN!"
x = txt.capitalize()
print(x) # Python is fun!
```

##### `casefold()`
* Converts the first character to lower case
	* Arguments
		1) None
```Python
string.casefold()
```

```Python
txt = "hello, And Welcome To My World!"  
x = txt.casefold()  
print(x) # hello, and welcome to my world.
```

##### `center()`
* Returns a centered string of a specified length 
	* Arguments
		1) `length` -- the length of the returned string
		2) `character` -- the character to fill the missing space on each side. Default is " "
```Python
string.center(length, character)
```

```Python
txt = "banana"  
x = txt.center(20, "0")  
print(x) # OOOOOOObananaOOOOOOO
```

##### `count()`
* Returns the number of times a specified value appears in the string.
	* Arguments
		1) `value` -- a string specifying the string to value to search for
		2) `start` -- an integer specifying the position to start the search (default is 0)
		3) `end` -- an integer specifying the position to end the search (default is end of str)
```Python
string.count(value, start, end)
```

```Python
txt = "I love apples, apple are my favorite fruit"
x = txt.count("apple")
print(x) # 2
```

```Python
txt = "I love apples, apple are my favorite fruit"
x = txt.count("apple", 10, 24)
print(x) # 1
```

##### `encode()`
* Encodes and returns a string, using the specified encoding. If no encoding is specified, UTF-8 will be used.
	* Arguments
		1) `encoding=` -- a String specifying the encoding to use. Default is UTF-8
		2) `errors=` -- a String specifying the error method. Legal values are:
			* `backslashreplace` -- uses a backslash instead of the character that could not be encoded
			* `ignore` -- ignores the characters that cannot be encoded
			* `namereplace` -- replaces the character with a text explaining the character
			* `strict` -- Default, raises an error on failure
			* `replace` -- replaces the character with a question mark
			* `xmlcharrefreplace` -- replaces the character with an xml character
```Python
string.encode(encoding=encoding, errors=errors)
```

```Python
txt = "My name is Ståle"

print(txt.encode(encoding="ascii",errors="backslashreplace")) 
# b'My name is St\\xe5le'  

print(txt.encode(encoding="ascii",errors="ignore"))
# b'My name is Stle'  

print(txt.encode(encoding="ascii",errors="namereplace"))
# b'My name is St\\N{LATIN SMALL LETTER A WITH RING ABOVE}le'  

print(txt.encode(encoding="ascii",errors="replace"))
# b'My name is St?le'

print(txt.encode(encoding="ascii",errors="xmlcharrefreplace"))
# b'My name is Ståle'
```

##### `endswith()`
* Returns `True` if the string ends with the specified value, otherwise False.
	* Arguments
		4) `value` -- (Required); the value to check if the string ends with
		5) `start` -- (Optional); an Integer specifying at which position to start the search
		6) `end`	-- (Optional); an Integer specifying at which position to end the search
```Python
string.endswith(value, start, end)
```

```Python
txt = "Hello, welcome to my world."
x = txt.endswith("my world.")
print(x) # True
```

```Python
txt = "Hello, welcome to my world."
x = txt.endswith("my world.", 5, 11)
print(x) # False
```

##### `expandtabs()`
* Sets the tab size to the specified number of whitespaces
	* Arguments
		1) `tabsize` -- (Default is 8); a number specifying the tabsize
```Python
string.expandtabs(tabsize)
```

```Python
txt = "H\te\tl\tl\to"

print(txt) # H       e       l       l       o  
print(txt.expandtabs()) # H       e       l       l       o  
print(txt.expandtabs(2)) # H e l l o 
print(txt.expandtabs(4)) # H   e   l   l   o  
print(txt.expandtabs(10)) # H         e         l         l         o
```

##### `find()`
* Searches the string for a specified value and returns the position (index) of the first occurrence where it was found; returns -1 if the value is not found
	* Arguments
		1) `value` -- (required); the value to search for
		2) `start` -- (Default is 0); where to start the search
		3) `end` -- (Default is the end of string); where to end the search
```Python
string.find(value, start, end)
```

```Python
txt = "Hello, welcome to my world."
x = txt.find("e")
print(x) # 1
```

```Python
txt = "Hello, welcome to my world."
x = txt.find("e", 5, 10)
print(x) # 8
```

```Python
txt = "Hello, welcome to my world."
print(txt.find("q")) # -1
```

##### `format()`
* Formats the specified value(s) and insert them inside the string's placeholder (identified using named indexes, numbered indexes, or empty placeholders)
	* Arguments
		1) `value` -- one or more values (of any data type) that should be formatted and inserted in the string (separated by commas)
		
* Formatting Type -- Formats the result (placed inside placeholders)
	* `:<` -- Left aligns the result (within the available space)
	* `:>` -- Right aligns the result (within the available space)
	* `:^` -- Center aligns the result (within the available space)
	* `:=` -- Places the sign to the left most position
	* `:+` -- Use a plus sign to indicate if the result is positive or negative
	* `:-` -- Use a minus sign for negative values only
	* `:`  -- Use a space to insert an extra space before positive numbers (and a minus sign before negative numbers)
	* `:,` -- Use a comma as a thousand separator
	* `:_` -- Use a underscore as a thousand separator
	* `:b` -- Binary format
	* `:c` -- Converts the value into the corresponding unicode character
	* `:d` -- Decimal format
	* `:e` -- Scientific format, with a lower case e
	* `:E` -- Scientific format, with an upper case E
	* `:f` -- Fix point number format
	* `:F` -- Fix point number format, in uppercase format (show inf and nan as INF and NAN)
	* `:g` -- General format
	* `:G` -- General format (using a upper case E for scientific notations)
	* `:o` -- Octal format
	* `:x` -- Hex format, lower case
	* `:X` -- Hex format, upper case
	* `:n` -- Number format
	* `:%` -- Percentage format
```python
string.format(value1, value2, valueN...)
```

```python
total_italian = 64.9
native_italian = 61.6
share_native = native_italian / total_italian

message = "The share of Italian speakers that are native speakers is {:.2f}".format(share_native)
print(message) 
```

```Python
# Named indexes:
txt1 = "My name is {fname}, I'm {age}".format(fname = "John", age = 36)
print(txt1) # My name is John, I'm 36

# Numbered indexes:
txt2 = "My name is {0}, I'm {1}".format("John", 36)
print(txt2) # My name is John, I'm 36

# Empty placeholders:
txt3 = "My name is {}, I'm {}".format("John", 36)
print(txt3) # My name is John, I'm 36
```

##### `format_map()`
* Formats specified values in a string
	* Arguments
		1) 
```Python
string.format_map()
```

```Python

```

##### `index()`
* Searches the string for a specified value and returns the position (index) of the first occurrence where it was found; returns an error if the value is not found
	* Arguments
		1) `value` -- (required); the value to search for
		2) `start` -- (Default is 0); where to start the search
		3) `end`	-- (Default is the end of string); where to end the search
```Python
string.index(value, start, end)
```

```Python
txt = "Hello, welcome to my world."
x = txt.index("e")
print(x) # 1
```

```Python
txt = "Hello, welcome to my world."
x = txt.index("e", 5, 10)
print(x) # 8
```

```Python
txt = "Hello, welcome to my world."
print(txt.index("q")) 

# Traceback (most recent call last):  
	# File "demo_ref_string_find_vs_index.py", line 4 in <module>  
	    # print(txt.index("q"))  
# ValueError: substring not found 
```

##### `isalnum()`
* Returns `True` if all the characters are alphanumeric, meaning alphabet letter (a-z) and numbers (0-9)
	* Arguments: none
```Python
string.isalnum()
```

```Python
txt = "Company 12"
x = txt.isalnum()
print(x) # False
```

##### `isalpha()`
* Returns `True` if all the characters are alphabet letters (a-z).
	* Arguments: none
```Python
string.isalpha()
```

```Python
string_1 = '@mazing!'
string_2 = '90210'
string_3 = "CompanyX"

print(string_1.isalpha()) # False
print(string_2.isalpha()) # False
print(string_3.isalpha()) # True
```

##### `isascii()`
* Returns `True` if all the characters are ascii characters (a-z).
	* Arguments: none
```Python
string.isascii()
```

```Python
txt = "Company123"
x = txt.isascii()
print(x) # True

```

##### `isdecimal()`
* Returns `True` if all characters in the string are decimals (0-9)
	* Arguments: none
```Python
string.isdecimal()
```

```Python
txt = "1234"
x = txt.isdecimal()
print(x) # True
```

```Python
a = "\u0030" # Unicode for 0
b = "\u0047" # Unicode for G

print(a.isdecimal()) # True
print(b.isdecimal()) # False
```

##### `isdigit()`
* Returns `True` if all characters in the string are digits, otherwise `False`
	* Arguments: none
```Python
string.isdigit()
```

```Python
string_1 = '@mazing!'
string_2 = '90210'
string_3 = '50800'
print(string_1.isdigit()) # False
print(string_2.isdigit()) # True
print(string_3.isdigit()) # True
```

```Python
a = "\u0030" # Unicode for 0
b = "\u00B2" # Unicode for ²

print(a.isdigit()) # True
print(b.isdigit()) # True
```

##### `isidentifier()`
* Returns `True` if the string is an identifier, otherwise `False`
	* Arguments: none
* What is considered a valid identifier
	* Only contains alphanumeric letters (a-z) and (0-9), or underscores (`_`)
	* Does not start with a number
	* Does not contain any spaces
```Python
string.isidentifier()
```

```Python
a = "MyFolder"
b = "Demo002"
c = "2bring"
d = "my demo"

print(a.isidentifier()) # True
print(b.isidentifier()) # True
print(c.isidentifier()) # False
print(d.isidentifier()) # False
```

##### `islower()`
* Returns `True` if all characters in the string are lowercase, otherwise `False`
	* Arguments: none
```Python
string.islower()
```

```Python
a = "Hello world!"
b = "hello 123"
c = "mynameisPeter"

print(a.islower()) # False
print(b.islower()) # True
print(c.islower()) # False
```

##### `isnumeric()`
* Returns `True` if all the characters are numeric (0-9), otherwise `False`. 
	* Arguments: none
```Python
string.isnumeric()
```

```Python
txt = "565543"
x = txt.isnumeric()
print(x) # True
```

```Python
a = "\u0030" # Unicode for 0
b = "\u00B2" # Unicode for ²
c = "10km2"
d = "-1"
e = "1.5"

print(a.isnumeric()) # True
print(b.isnumeric()) # True
print(c.isnumeric()) # False
print(d.isnumeric()) # False
print(e.isnumeric()) # False
```

##### `isprintable()`
* Returns `True` if all characters in the string are printable, otherwise `False`.
	* Arguments: none
* What are non-printable characters?
	* Carriage return
	* Line feed
```Python
string.isprintable()
```

```Python
txt = "Hello! Are you #1?"
x = txt.isprintable()
print(x) # True
```

```python
txt = "Hello!\nAre you #1?"
x = txt.isprintable()
print(x) # False
```

##### `isspace()`
* Returns `True` if all characters in the string are whitespaces
	* Arguments
		1) 
```Python
string.isspace()
```

```Python

```

##### `istitle()`
* Returns `True` if the string follows the rules of a title
	* Arguments
		1) 
```Python
string.istitle()
```

```Python

```

##### `isupper()`
* Returns `True` if all characters in the string are upper case
	* Arguments
		* None
```Python
string.isupper()
```

```Python
string_1 = 'ABCDE'
string_2 = 'ABDCde'
print(string_1.isupper()) # True
print(string_2.isupper()) # False
```

##### `join()`
* Converts the elements of an iterable into a string
	* Arguments
		1) `iterable` -- any iterable object where the values are strings
```python
"".join(iterable)
```

```Python
words = ['Max\'s', 'favorite', 'film', 'is', 'The', 'Graduate.']
phrase = ' '.join(words) # forms a string from the elements, separated by spaces
print(phrase) # Max's favorite film is The Graduate. 

movie_info = ['Fight Club', 1999, ['thriller', 'drama', 'crime'], 139]
genre = ', '.join(movie_info[2])
movie_info[2] = genre
print(movie_info) # ['Fight Club', 1999, 'thriller, drama, crime', 139]
```

##### `ljust()`
* Returns a left justified version of the string
	* Arguments
		* 
```Python
string.ljust()
```

```Python

```

##### `lower()`
* Converts a string into lower case
	* Arguments
		* None
```Python
string.lower()
```

```Python
shopping_list = 'APPLES, oranges, Lettuce'
print(shopping_list.lower()) # apples, oranges, lettuce
```

##### `lstrip()`
* Returns a left trim version of the string (removes whitespace from the left side of the string)
	* Arguments
		* none
```Python
string.lstrip()
```

```Python
column_name = "     purchase date          "
print(column_name.lstrip()) # purchase date           
```

##### `maketrans()`
* Returns a translation table to be used in translations
	* Arguments
		* 
```Python
string.maketrans()
```

```Python

```

##### `partition()`
* Returns a tuple where the string is parted into three parts
	* Arguments
		* 
```Python
string.partition()
```

```Python

```

##### `replace()`
* Returns a string where a specified value is replaced with a specified value
	* Arguments
		1) `substring` -- The substring we want to be replaced
		2) `new_string` -- The string we want to replace it with
```Python
string.replace(substring, new_string)
```

```Python
# Replacing substring
shopping_list = 'canola oli, olive oil, avocado oil, peanut oli'
print(shopping_list.replace(' oli', ' oil')) # replacing oli with oil; 
# canola oil, olive oil, avocado oil, peanut oil 

# Removing substring without replacing
user_ids = "_151234_, _792051_, _955247_" 
user_ids = user_ids.replace('_', '')
print(user_ids) # 151234, 792051, 955247 
```


##### `rfind()`
* Searches the string for a specified value and returns the last position of where it was found
	* Arguments
		* 
```Python
string.rfind()
```

```Python

```

##### `rindex()`
* Searches the string for a specified value and returns the last position of where it was found
	* Arguments
		* 
```Python
string.rindex()
```

```Python

```

##### `rjust()`
* Returns a right justified version of the string
	* Arguments
		* 
```Python
string.rjust()
```

```Python

```

##### `rpartition()`
* Returns a tuple where the string is parted into three parts
	* Arguments
		* 
```Python
string.rpartition()
```

```Python

```

##### `rsplit()`
* Splits the string at the specified separator, and returns a list
	* Arguments
		* 
```Python
string.rsplit()
```

```Python

```

##### `rstrip()`
* Returns a right trim version of the string (removes whitespace from the right side of the string)
	* Arguments
		* 
```Python
string.rstrip()
```

```Python
column_name = "     purchase date          "
print(column_name.rstrip()) # Output: purchase date     
```

##### `split()`
* Splits the string at the specified separator, and returns a list
	* Arguments
		* 
```Python
string.split()
```

```Python

```

##### `splitlines()`
* Splits the string at line breaks and returns a list
	* Arguments
		* 
```Python
string.splitlines()
```

```Python

```

##### `startswith()`
* Returns true if the string starts with the specified value
	* Arguments
		* 
```Python
string.startswith()
```

```Python

```

##### `strip()`
* Returns a trimmed version of the string (removes whitespace from both sides of the string, while preserving whitespace between characters)
	* Arguments
		* none
```Python
string.strip()
```

```Python
column_name = "     purchase date          "
print(column_name.strip()) # purchase date
print(len(column_name.strip())) # 13
```

##### `swapcase()`
* Swaps cases, lower case becomes upper case and vice versa
	* Arguments
		* 
```Python
string.swapcase()
```

```Python

```

##### `title()`
* Converts the first character of each word to upper case
	* Arguments
		* 
```Python
string.title()
```

```Python

```

##### `translate()`
* Returns a translated string
	* Arguments
		* 
```Python
string.translate()
```

```Python

```

##### `upper()`
* Converts a string into upper case
	* Arguments
		* none
```Python
string.upper()
```

```Python
message = "Hi, my name is Max!"

print(message)
print(message.upper()) # HI, MY NAME IS MAX! 

message = message.upper() 
```

##### `zfill()`
* Fills the string with a specified number of 0 values at the beginning
	* Arguments
		* 
```Python
string.zfill()
```

```Python

```


