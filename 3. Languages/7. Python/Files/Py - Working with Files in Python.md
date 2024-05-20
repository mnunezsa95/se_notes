See: 
* [[Py - Introduction to Python]]
* [[Py - Relative vs Absolute File Paths]]
Resources: 
* Documentation: [The open() Method](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)
* Documentation: [CSV Library](https://docs.python.org/3/whatsnew/3.12.html#csv) 

---
# Reading from Files
* Python has a built-in method `open()` that can open any file. This method defaults to read-only mode.
* When working with files, it is important close files when done to prevent them from occupying memory

#### Working with Files
* `open()` -- opens the specified file;
	* Arguments
		1) filename --> name of file (including the ext)
		2) `mode=` --> how to open file
			* `w` = write (opens a new empty file to be written to)
				* If the file does not exist, it is automatically created
				* Can overwrite contents of an existing file, 
			* `a` = append (opens a new or existing file and appends text to it)
			* `r` = read
* `close()` -- closes the specified file
```Python
# Opening a file
f = open('my_file.txt')

print(f) # <_io.TextIOWrapper name='my_file.txt' mode='r' encoding='cp1252'> 
print(type(f)) # <class '_io.TextIOWrapper'>

# Closing the file
f.close()
```

```Python
# Python will automatically create this file
file = open("day_24/my_file.txt", mode="w")
```

```Python
# Opening the file
f = open('my_file.txt')

# Printing the contents of the file
for line in f:
    print(line.rstrip()) # Removes unncessary whitepace at end of a string

# Closing the file
f.close()
```

* `read()` -- reads the specified file as a single string
* `readlines()` -- creates a list of strings, with each element in the list being a line from the file
```Python
# Opening the file
f = open('my_file.txt')

# Reading & printing the lines form the file as a single string
print(f.read())

# Closing the file
f.close()
```

```Python
# Opening the file
f = open('my_file.txt')

# Reading & printing the list of strings
print(f.readlines())

# Closing the file
f.close()
```

* `write()` -- writes to the file on which it is called
	* Arguments
		* string_to_write --> the string indicating what will be written
```Python
from datetime import datetime

now = datetime.now() # get the current time

f = open('my_journal.txt', mode='a')
f.write(\n) # write a new line
f.write(str(now)) # write the timestampe
f.write("Today...")
```

* `writelines()` -- writes a list of strings, in order, to the file on which it is called 
	* Arguments:
		* list_of_strings -- the list of strings to write into the file
```Python
# A list of strings
## Each string ending in \n puts it on a new line
titles = ['Future Planet\n', 'Solutions for a sustainable world\n'] 

# Opening the file
f = open('my_journal.txt', mode='a')

# Writing to the file
f.writelines(titles)
```

## Working with Files using a `with`-block
* Using the `with` block is better as it closes the file when the block ends
#### Opening Files using '`with`'
```Python
# opening the file with an alias of f
with open('my_file.txt') as f:
    for line in f.readlines(): # iterating through the list of strings   
        print(line.rstrip()) # printing each line removing excess whitespace
```

```Python
# opening the file with an alias of 'file' in write mode
with open('my_journal.txt', mode='w') as file:
  file.write('\nNew Text.')
```

```Python
from datetime import datetime # Importing the datetime library

now = datetime.now() # get the current time

# Opening a file in append mode with an alias of f
with open('my_journal.txt', 'a') as f:
	# Writing to the file
    f.write('\n')     # begin with a new line
    f.write(str(now)) # timestamp
    f.write('\n\n')   # insert blank line
    f.write(' ')      # empty space
    f.write(input())  # type journal entry
    f.write('\n\n')   # end with a blank line
```

```Python
# A list of strings
## Each string ending in \n puts it on a new line
titles = ['Future Planet\n', 'Solutions for a sustainable world\n']

# Opening a file in write mode with alias f
with open('output.txt', 'w') as f:
    f.writelines(titles) # writing to the file
```


---
---
# Compressing Files
#### What are Archives?
* Archives are widely used to compress files or pack related files together

#### The `zipfile` Library
* Used to create ZIP files
* This module provides tools to create, read, write, append, and list a ZIP file
* When archiving, text is encoded in bytes.
	* When reading files from an archive, they must be decoded

#### Working with Archives (ZIP Files)
* `printdir()` -- prints a list of the archive's contents
```Python
# Importing the zipfile package
from zipfile import ZipFile

# Opening a file and writing to it
with open("info.txt", "w") as f:
    f.write('some data')

# Opening a file and appending to it
with open("logs.txt", "a") as f:
    f.write('new_log')

# Opening a ZIP Archive called 'archive.zip'
with ZipFile("archive.zip", mode="w") as archive:
    # adding the info.txt file to it
    archive.write("info.txt") 
    archive.write("logs.txt")
    # printing the archive directory
	archive.printdir()     
```

#### Decoding a File from an Archive
```Python
# Opening an archive
with ZipFile("archive.zip") as archive:
    # opening a file in the archive
    with archive.open("logs.txt") as f:
	    # Decoding and printing the file as one string
        print(f.read().decode())
```


---
---

# Working with JSON Formatted Data

#### What is JSON?
* JSON format is an object data structure, similar to Python Dictionaries or JavaScript Objects

#### The `json` Library 
* Python has a built-in `JSON` library to read, write and parse `.json` files
* The `dump`/`load` convention is used to save/read when working with file paths, while `dumps`/`loads` is applied when dealing with data inside Python. 

#### Working with JSON data
* `json.dumps()` -- Converts data from Python format into a JSON format
	* Arguments
		1) `data` -- the data to be converted to JSON
* `json.dump()` -- adds (or writes) to a specified JSON file
	* Arguments:
		1) `data` -- the data to be written
		2) `file` -- the file to where data will be written
		3) `indent` (optional) --> sets the indent
* `json.loads()` -- converts strings that are in the JSON format 
	* Arguments
		1) `data` -- the data to be converted in Python
* `json.load()` -- loads data from a specified JSON file
	* Arguments
		1) `data_file` --> the data file to be open
* `jsonFile.update()` -- updates an existing json data file
	* Arguments
		1) `data` -- the data to be updated

```Python
# JSON string
x = '{"name": "General Slocum", "date": "June 15, 1904"}'

y = json.loads(x) # Converting the JSON string into a Python format
print('Name : {0}, date : {1}'.format(y['name'], y['date']))

# Name : General Slocum, date : June 15, 1904
```

```Python
# Converting the variable y into a JSON object
out = json.dumps(y)
print(out) # [{"name": "General Slocum", "date": "June 15, 1904"}, 
```

```Python
# Working with JSON data from an external API
import json
import requests

# fetch data from the internet
data = requests.get('https://dummyjson.com/products/1')
text = data.text # use the main part of the response

# parse the request's outputs
print(json.loads(text))
```

```Python
import json
data = dict(id=12, status='active', user_name='Rachel')

# Printing to the data variable as a json object
print(json.dumps(data)) # {"id": 12, "status": "active", "user_name": "Rachel"}

# Creating a json file called output in write mode with an alias 'f'
with open ('output.json', 'w') as f:
	# Adding the data to the file 
    json.dump(data, f)
```

```Python
# Import requests & json libraries
import json
import requests

# fetch data from the internet
response = requests.get('https://dummyjson.com/products/')
text = response.text

# parse the request's outputs and apply JSON formatting
products = json.loads(text)['products']

items = []
brand = 'Samsung'

# add items with the desired brand to the list
for entry in products:
    if entry['brand'] == brand:
        items.append(entry)

# create json file with item info
with open(brand + '_items.json', 'w') as f:
    json.dump(items, f)
```


---
---

# Working with YAML Formatted Data

#### What is YAML?
* YAML -- a format suited for transmitting configuration settings and has specific formatting, including Python-style indentation
* YAML is a superset of JSON 
	* JSON is proper YAML
	* YAML is more human-readable
* YAML supports comments (using the `#`)
* YAML supports several documents in one file (divided by `--`)
* 

#### The `yaml` Library
* Python has a built-in `yaml` library to read, write and parse yaml data

#### Working with yaml data
* `dump` -- adds (or writes) to a specified yaml file
* `yaml.load()` -- loads the data 
	* Arguments
		* `file` -- the file to be loaded
		* `Loader=` -- the loader to be used
			* Use: `Loader=yaml.FullLoader`
```python
# Import the yaml library
import yaml

# An array of dictionaries
data = [{'user_id': '1', 'age': 34}, {'user_id': '2', 'age': 37}]

# Printing the data as a yaml object
print(yaml.dump(data)) 

# Printing the list as a yaml object
var = [22, 23, 'root']
print(yaml.dump(var))
```

```
# Output

- age: 34
  user_id: '1'
- age: 37
  user_id: '2'

- 22
- 23
- root
```


```yaml
# YAML File

%YAML 1.2 # yaml version
---
user:
  first_name: Noel
  last_name: Williams
  dob: 1970-01-01
  employed: true
  pets:
    - cat
    - dog
    - goat
```

```Python
# Opening the user.yaml file as f
with open('user.yaml') as f:
	# Loading the data 
    data = yaml.load(f, Loader=yaml.FullLoader) # Saving the info to 'data'
    print(type(data))
    
	# Accessing the data variable (yaml data) and printing the list of pets
    pets = data['user']['pets']
    print(sorted(pets))  # ['cat', 'dog', 'goat']
```


---
---
# Working with CSV Formatted Data
#### What is CSV (Comma Separated Values)?
* A document type that stores tabular data using comma-separated values
#### The `csv` Library
* Python has a built-in `csv` library with methods for working with CSV files
#### Importing csv
```python
import csv
```

#### Reading CSV data
* `csv.reader()` --> Return a [reader object](https://docs.python.org/3/library/csv.html#reader-objects) that will process lines from the given csvfile.
* Arguments
	1) `csvfile` --> the name of the csv file
	2) `dialect`
	3) `fmtparams` 
```python
with open("day_25/weather_data.csv") as data_file:
  data = csv.reader(data_file)
  temperatures = []
  for row in data:
    if row[1] != "temp":
      temperatures.append(row[1])
  print(temperature)
```