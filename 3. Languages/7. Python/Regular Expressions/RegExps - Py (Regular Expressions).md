See: 
* [[RegExps - Introduction to Regular Expressions]]
* [[Py - Introduction to Python]]
Resources
* [regex101: Regular Expression Test Site](https://regex101.com/)
* [TripleTen: Regex Practice Exercises (PDF)](https://practicum-content.s3.us-west-1.amazonaws.com/data-scientist-eng/moved_practicum_Regular_Expression_Practice.pdf)
* [RegexOne: Regular Expression Interactive Exercises](https://regexone.com/)
* [Python Documentation: Regular Expressions](https://docs.python.org/3/howto/regex.html#regex-howto)
* [Learn Regex (GitHub Repo) - Introduction to Regular Expressions](https://github.com/ziishaned/learn-regex)
* [Regexr: Regular Expression Testing Tool](https://regexr.com/)
* [Debuggex: Python Regex Cheatsheet](https://www.debuggex.com/cheatsheet/regex/python)

---
# Regular Expression in Python

## Importing `re` Module
* The `re` module is used to work with regular expressions
```python
# Importing the re module
import re 
```

## How Regular Expressions Work
* Requires two steps:
	1) Creation of the regular expression pattern 
	2) Passing the pattern into the methods of the `re` module
		* Methods are used to 'search', 'replace', 'remove' symbols.

## Basic Regular Expression Patterns
| Regular Expression | Description                                | Example            | Explanation              |
| ------------------ | ------------------------------------------ | ------------------ | ------------------------ |
| `[]`               | Single character contained within brackets | `[a-]`             | a or -                   |
| `[^...]`           | Negation                                   | `[^a]`             | any character except 'a' |
| `-`                | Range                                      | `[0-9]`            | Any digit from 0 to 9    |
| `.`                | Any single character except a newline      | `a.`               | as, a1, a_               |
| `\d`               | Any digit                                  | `a\d &#124;a[0-9]` | a1, a2, a3               |
| `\w`               | Any letter, digit, or _                    | `a\w`              | a_, a1, ab               |
| `[A-z]`            | Any letter                                 | `a[A-z]`           | ab                       |
| `?`                | 0 or 1 instance                            | `a?`               | a or nothing             |
| `+`                | 1 or more instances                        | `a+`               | a or aa or aaa           |
| `*`                | 0 or more instances                        | `a*`               | nothing or a, or aa      |
| `^`                | Start of string                            | `^a`               | a1234, abcd              |
| `$`                | End of string                              | `a$`               | 1a, ba                   |
* Searching for special characters in Regular Expressions requires us to escape the character using a backslash
```Python
# Searching for a + in the string
regexp = '\+' 
```

#### Examples
* Writing a regular expression that checks whether the string begins with a number, and if it does, matches the number.
```Python
# [0-9] will match numbers 0-9 
# + will match continuous instances
# ^ will match if it starts with this format
regexp = '^[0-9]+'
```

## Regular Expressions in Python
* The most common tasks for analysts include:
	* Finding a substring within a string
	* Breaking strings into substrings
	* Replacing parts of a string with other strings

### `re` Methods for Regular Expressions


#### `search()`
* `search(pattern, string)` -- searches for a `pattern` in a `string`, and returns a `match`-type object.
	* The `match` object includes:
		* `span` -- a parameter that defines the range of indices matching the pattern
		* `match` -- a parameter that indicates the value of the substring
	* Arguments
		* `pattern` -- the pattern using to search
		* `string` -- the string searching in
```Python
import re

string='"General Slocum" 15 June 1904 East River human factor'
print(re.search('\w+', string)) # <re.Match object; span=(1, 8), match='General'>
```

* `group()` -- returns just the substring that matches the criteria
```Python
import re

string = '"General Slocum" 15 June 1904 East River human factor'
print(re.search('\w+', string).group()) # 'General'
```

```python
import re 

string = '"General Slocum" 15 June 1904 East River human factor'
print(re.match('"[A-z ]+"', string).group()) # "General Slocum"
```

#### `split()`
* `split(pattern, string)` -- breaks up a `string` at points where the `pattern` occurs
	* Arguments
		* `pattern` -- the pattern using to search
		* `string` -- the string searching in
		* `maxsplit=` -- limits the number of times the string is divided
```Python
import re

string = '"General Slocum" 15 June 1904 East River human factor'
# splits the string where +1 consecutive numbers occur
print(re.split('\d+', string)) 

# ['"General Slocum" ', ' June ', ' East River human factor']
```

```python
import re

string = '"General Slocum" 15 June 1904 East River human factor'
# splits the string where +1 consecutive numbers occur, 1x max
print(re.split('\d+', string, maxsplit = 1))

# ['"General Slocum" ', ' June 1904 East River human factor']
```

#### `sub()` 
* `sub(pattern, repl, string)` -- searches for the pattern substring within a string and replaces it with the `repl` (i.e. replace) substring.
	* Arguments
		* `pattern` -- the pattern using to search
		* `repl` -- the replacement string to be used
		* `string` -- the string searching in
```python
import re

string = '"General Slocum" 15 June 1904 East River human factor'
# Replace any 1+ consecutive digits with empty string
print(re.sub('\d+', '', string)) 
# "General Slocum" June East River human factor'
```

#### `findall()`
* `findall(pattern, string)` -- returns a list of all substrings in a `string` that match the `pattern`.
	* Arguments
		* `pattern` -- the pattern using to search
		* `string` -- the string searching in
```python
import re

tion = "Arrived at the station in total frustration"
# finds all words that have tion consecutively at the end
print(re.findall(' [A-z]+tion', string)) # ['station', 'frustration']
```

```python
import re

string = 'sixty-seven drops of rain'

# finds all words with format xx-xx
print(re.findall('\w+-\w+', string)) # ['sixty-seven']
```

* When combined with the `len()` function, the `findall()` function will return the number of occurrences
```Python
import re

string = 'sixty-seven drops of rain'
print(len(re.findall('\w+', string))) # 5
```

## Examples
1. Write a regular expression to find the `<title> </title>` tags and their contents. Print the result as follows: `<title>Tag text</title>`
```Python
import requests
import re

URL = 'https://store.data-analyst.praktikum-services.ru/en/'
req_text = requests.get(URL).text
print(re.search('<title>[A-z ]+</title>', req_text).group())
```

2. Write a regular expression that outputs all product names that include the word "Butter" (note the capital letter). "Butter" may come in the middle of the name. So there might be 0 or more letters or spaces before "Butter" and there might be some letters or spaces after.
```Python
import requests
import re

URL = 'https://store.data-analyst.praktikum-services.ru/en/'
req_text = requests.get(URL).text
print(re.findall('[A-z ]*Butter[A-z ]*', req_text))
```

3. Write a regular expression to find all product names containing the word "Horizon" (a brand). It only appears at the beginning of a name. Do not include the weight, just the product name. Product names may contain letters, digits, spaces, hyphens, and percent signs.
```python
import requests
import re

URL = 'https://store.data-analyst.praktikum-services.ru/en/'
req_text = requests.get(URL).text
found_products = re.findall('Horizon[ \w\-%]+', req_text)
print(len(found_products))
print(found_products)
```