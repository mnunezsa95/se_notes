See [[Py - What is OOP?]], [[Py - Creating Classes in Python]]

#### What is Inheritance?
* Inheritance allows classes in python to inherit methods and attributes from other classes

#### Creating a Class that uses Inheritance
* Create the class, and pass in the class it will inherit from as an input
* Inside the constructor either
	1) Inherit the parent's constructor
	2) Calls the `super()` method on the `__init__()`
```Python
# SYNTAX

# Option 1: Inheriting the parent's constructor
class NameOfClass(ClassToInheritFrom):
  def __init__(self, ...):
	ClassToInheritFrom.__init__(self, ...)

# Option 2: Calling the super() method on the __init__() method
class NameOfClass(ClassToInheritFrom):
  def __init__(self, ...):
    super().__init__() 
```


```Python
# Parent Class Attributes and Methods
class Character:
    def __init__(self, name):
        self.name = name
        self.health = 100
    
    def heal(self, value:int=20):
        self.health += value
    
    def learn(self, value:int=20):
        self.knowledge += value
        
# Child Class inherits parent's attributes, but has some unique ones too
class Knight(Character):
    def __init__(self, name):
        Character.__init__(self, name) # Option 1: Inherit Parent's Constructor
        self.damage = 25
        self.knowledge = 20

# Child Class inherits parent's attributes, but has some unique ones too
class Peasant(Character):
    def __init__(self, name):
        super().__init__(name) # Option 2: Calling super
        self.damage = 10
        self.knowledge = 36


arthur = Knight('Arthur')
arthur.heal() # default value is used
arthur.learn(100) # custom value
print(arthur.__dict__)
```

#### Example:
```Python 
# Creating the parent class
class Animal:
  def __init__(self):
    self.num_eyes = 2
    
  def breathe(self):
    print("Inhale, exhale.")

# Creating a child class to inherit from parent
class Fish(Animal): # Inheriting from Animal class
  def __init__(self):
    super().__init__() # call super() on the init method
    
  def breathe(self): # Taking the existing method from the parent class
    super().breathe() # calling everything from parent's breathe() method
    print("doing this underwater") # add more to breathe() method of child
    
  def swim(self):
    print("Moving in water")


# Creating an instance of Fish() class
nemo = Fish()
nemo.swim()

# Instance of Fish() has access to all properties and methods of parent class
nemo.breathe()
print(nemo.num_eyes)
```