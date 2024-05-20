See [[Py - Introduction to Python]], [[Py - What is OOP?]]

#### Creating a Class
* Classes are capitalized and use pascal case (letter of each word is capitalized)
* Classes are made up of methods and attributes
* Classes have an `__init__()` function that runs when the class is created
* The `self` keyword is used to refer to the instance of the class being created
```python
# SYNTAX

class ClassName:
  def __init__(self):
    # Code to run when the class is initialized
  # Methods for the class
```

```Python
# Creating an instance of the class
object_name = ClassName
```

#### Adding Properties to a Class
* `__init__(self)` is used to add initial variables to the class constructor 
* `__init__(self, param_1, param_2)` takes in as many parameters as needed (after `self`)
```Python
# User Class
class User:
  # Defining the __init__ function & initial properties
  def __init__(self, user_id, username):
    self.id = user_id  # setting user_id parameter to the ide of the object
    self.username = username
    self.followers = 0 # adding a default value (can be changed later)

# This user_1 object will have the id & username attibute
user_1 = User("001", "Harper") 
print(user_2.username) # Harper
```
* Whenever an object is created from a class, the `__init__(self)` function will run

#### Adding Methods to a Class
```Python
class User:
  def __init__(self, user_id, username):
    self.id = user_id  # setting user_id parameter to the ide of the object
	self.username = username
	self.followers = 0  # creating a follower attribute (with a default value)
	self.following = 0
	
	# methods always have a 'self' param (identifies which object called it) 
    def follow(self, user): 
     user.followers += 1  # increasing the other account's followers count 
     self.following += 1  # increasing our own following count

# Creating instances of the user class
user_1 = User("001", "Harper") 
user_2 = User("002", "Penny")  

# Calling the follow() method of user_1
user_1.follow(user_2)
```

## Class & Static Methods:
#### Adding Static Methods to a Class
* Static Methods -- do not interact with an instance directly and do not use the `self` keyword
* Creating a static method
	1) Use the `@staticmethod` decorator
	2) Create the method
#### Adding Class Methods to a Class
* Class Methods -- take a class object instead of an instance as the first argument, and can be used to implement alternative ways of creating instances.
* Creating a Class Method
	1) Use the `@classmethod` decorator
	2) Create the method
```Python
class Stock:
    def __init__(self, ticker, amount, price):
        self.ticker = ticker
        self.amount = amount
        self.price = price
        self.total = self.price * self.amount
        
    def buy(self, quantity):
        self.amount += quantity
        self.total = self.amount * self.price
		
    # Creating a Static Method
	@staticmethod
	def show_current_price(ticker):
		current = # fetch price from online
		print(current)
	
	# Creating a Class Method
	@classmethod
    def from_string(cls, string):
        ticker, amount, price = string.split()
        return cls(ticker, int(amount), float(price))
```

```Python
stock.show_current_price('ABC')
abc = stock.from_string('ABC 10 1.5')
```


#### Example
```python
# Defining the Knight class
class Knight:
    def __init__(self, name):
        self.health = 100
        self.damage = 25
        self.knowledge = 20
        self.name = name
        
    # Methods for the Knight class
	def heal(self):
        self.health += 20
    def learn(self):
        self.knowledge += 5


# Creating two instances of the Knight class
arthur = Knight('Arthur')
richard = Knight('Richard')

# Calling the heal() and learn() methods on the arthur instance
arthur.heal() # adds 20 to health
arthur.learn() # adds 5 to knowledge

# Accessing the attributes
print(arthur.health) # 120
print(arthur.damage) # 25
print(arthur.knowledge) # 35
print(arthur.name) # Arthur

# Chaning the value of the health attribute on the aruthur instance of the class. Will not change the Richard instance
arthur.health = 150 

# Accessing the __dict__ attribute:
print(aruthur.__dict__) # {'health': 150, 'damage': 25, 'knowledge': 20, 'name': 'Arthur'}
```

