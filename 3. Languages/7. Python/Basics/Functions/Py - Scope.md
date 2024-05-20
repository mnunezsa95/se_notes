See: [[Py - Introduction to Python]], [[Py - Functions]]

---
## What is scope?
* Scope -- the context in which a variable or function is created
* A variable or function is only available from inside the region it is created.

## Understanding Scope (analogy)
* Scope is like a tree in your yard vs a tree on a sidewalk
	* The tree in your yard is accessible by ONLY you
	* The tree on the sidewalk is accessible by anyone

## What is the namespace?
* Anything assigned to a variable has a namespace
	* Each namespace is valid in certain scopes

#### Local Scope
* Local scope exists within a function
* If a variable is referred to inside a function, the interpreter will first look for the variable inside the function definition (Local Scope)
```Python
def drink_potion():
  potion_strength = 2 # 'potion_strength' only exists within the drink_potion fn
  print(potion_strength)

drink_potion() # 2 because the variable was found in local scope
print(potion_strength) # NameError b/c potion_strength is not available (only accessible inside the fn)
```

```Python
# Local Scope -- when calling the fn, it looks for variables inside the local scope first
product_price = 12.0
product_qty = 5

def total_price():
    product_price = 11.0
    product_qty = 4
    print(f'Total price: {product_price * product_qty}')

total_price() # Total price: 44.0
```

#### Global Scope
* Global scope exists within all functions
* If a variable is referred to inside a function, and it was NOT found in the local scope, it searches for it in the Global Scope (outside the function definition)
```Python
player_health = 10 # a globally-scoped variable

def drink_potion2():
  potion_strength = 2 
  print(player_health)  # 10 because it can access global variables

drink_potion2()
```

```Python
# Global Scope -- the variables referenced in the function are NOT in local scope, so interpreter searches the global scope

product_price = 12.0
product_qty = 5

def total_price():
    print(f'Total price: {product_price * product_qty}')

total_price() # Total price: 60.0
```

#### Block Scope
* Python DOES NOT have block scope
* Variables created inside an if statement or loop can be accessed externally
```Python
nemies2 = ["zombie", "skeleton", "alien"]
game_level = 3
if game_level < 5:
  new_enemy = enemies2[0]  # create new_enemy variable inside the if statement

print(new_enemy)  # new_enemy is printed bc Python DOES NOT have block scope
```

### Built-in Scope
* If a variable is referred to inside a function, and not found in the Local or Global scope, the interpreter will look for the variable in Python's built-in scope
```Python
# -- Built-in Scpope -- the variables referenced in the function are NOT in the local or global scope; also not in the built-in scope

product_price = 12.0
product_qty = 5

def total_price():
    print(f'Total price: {price * qty}')

total_price() # NameError: name 'price' is not defined
```

## Python Constants & Global Scope
* Global constants are variables declared that will NEVER change
* Naming convention for global constants
	* All uppercase
	* Separate words w/ underscores (`_`)
```Python
PI = 3.14159
URL = "https://www.google.com"
TWITTER_HANDLE = "#yu_angela"
```

### Modifying a Global Variable
* SHOULD TRY to avoid modifying variables in the global scope
* Two ways to modify:
	1) Using `global` keyword
		* `global` keyword will force the function to look at global scope for the variable
	2) Using return statements
		* Return statements can be used to overwrite the previous value
```Python
enemies = 1 # a global variable
def increase_enemies():
  global enemies  # the 'global' flag designates the fn to look at global scope
  enemies += 1  # changing the global variable
  print(f"enemies inside function: {enemies}")  # prints "2"

increase_enemies()
print(f"enemies outside function: {enemies2}") # prints "1"
```

```Python
enemies = 1 # a global variable
def increase_enemies():
  return enemies + 1 # returning the global variable with a change

enemies3 = increase_enemies() # assigning the return of the function to enemies
```