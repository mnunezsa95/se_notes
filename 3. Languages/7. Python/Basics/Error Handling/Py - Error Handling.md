See: [[Py - Introduction to Python]], [[Py - Errors and Exceptions]]

---

## Catching an Error
* "Catching an error" means localizing the problem without terminating the whole program

#### Try-Except-Else-Finally
* `try` - executes something that might cause an exception/error
* `except` - executes if an error occurs in `try`-block (error occurs)
* `else` - executes if there were no exceptions (no errors occurred)
* `finally` - executes no matter what happens (whether except or else runs)
```python
# 'Try' to run this 
try:
	print(777 / 0)
# if an error occurs, run this block of code
except:
	print("We cannot divide by zero!")
	print("Moving on")
```

```Python
# 'Try' to run this 
try:
  im = Image.open(args.input_file)

# If file is not found, run this block of code
except FileNotFoundError: 
  print('input file not found, provide correct file name:')
  im = Image.open(input())

# If file is found but something else goes wrong, run this block of code
except Exception as error_msg: # Using an alias to capture the error message
  print(error_msg) # printing the error message
  print('Probably wrong file, try different one:')
  im = Image.open(input())
```

```Python
from PIL import Image
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('input_file', help='input file path')
parser.add_argument('output_file', help='output file path')
parser.add_argument('angle', help='desired rotation', type=int)
parser.add_argument( '-i', '--info', help='display image size', action='store_true')
args = parser.parse_args()
angle = args.angle

# Try to run this
try:
  im = Image.open(args.input_file)

# If file is not found, run this block of code
except FileNotFoundError:
  print('input file not found, provide correct file name:')
  im = Image.open(input())

# If file is found but something else goes wrong, run this block of code
except Exception:
  print('Wrong file, try different one:')
  im = Image.open(input())

# If rile is found, and no errors, run this
else:
  print("Running smoothly")

# Run this regardless of what happens
finally:
  rotated = im.rotate(angle)
  im.close()
  rotated.save(args.output_file)
```


```Python
try:  # Try out this block
  file = open("a_file.txt")
  a_dictionary = {"key": "value"}
  value = a_dictionary["key"]
except FileNotFoundError:  # If FileNotFoundError exception happens, then execute
  file = open("day_30/a_file.txt", "w")
  file.write("Something")
except KeyError as error_message:
  print(f"That key {error_message} does not exist")
else:  # Executes if there are not exceptions
  content = file.read()
  print(content)
finally: # Execute regardless of whether there were exceptions or not
  file.close()
  print("File was closed")
```

```Python
fruits = ["Apple", "Pear", "Orange"]
def make_pie(index):
  try:
    fruit = fruits[index]
  except:
    print("Fruit pie")
  else: 
    print(fruit + " pie")

make_pie(4)
```

```python
facebook_posts = [
  {"Likes": 21, "Comments": 2},
  {"Likes": 13, "Comments": 2, "Shares": 1},
  {"Likes": 33, "Comments": 8, "Shares": 3},
  {"Comments": 4, "Shares": 2},
  {"Comments": 1, "Shares": 1},
  {"Likes": 19, "Comments": 3},
]
total_likes = 0
for post in facebook_posts:
  try:
    total_likes = total_likes + post["Likes"]
  except KeyError:
    pass
    
print(total_likes)
```

#### Raising Unique Exceptions
* `raise` keyword is used to raise a unique exception
```python
height = float(input("Height: "))
weight = float(input("Weight: "))

if height > 3:
  raise ValueError("Human height should not be over 3 meters.")

bmi = weight / height**2
print(bmi)
```

