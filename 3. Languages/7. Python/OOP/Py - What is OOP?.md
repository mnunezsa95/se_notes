See [[Py - Introduction to Python]]

## What is Object Oriented Programming?
* OOP is a coding paradigm
* Allows for complex tasks / code to be separated into separate modules
* Allows modules to become reusable
* Allows code to become scalable

#### What is a Class?
* Classes -- blueprints for creating instances
#### What is an instance?
*  Objects created from the same class are considered to be different instances of the class
	* Instances have state independent of the class
* All instances of the same class have the same set of attributes and methods.
```Python
import CarBlueprint

# These are different instances of the the CarBlueprint() class. Each one of these could have their own state
audi = CarBlueprint()
mercedes_benz = CarBlueprint() 
ferarri = CarBlueprint()
```

#### What makes up an object?
* Attributes & methods make up an object
	* Attributes (things an object has) -> a variable attached to particular object
	* Method (things an object can do) -> a function attached to a particular object
* Classes can be used to generate several instances of an object

### Creating an instance of a class
* Classes use PascalCase for naming
```Python
car = CarBlueprint()  # CarBlueprint() is the class; car will be the object modeled after the class
car.speed  # accessing an attribute from car object inherited from CarBlueprint()
car.stop() # accessing an method from car object inherited from CarBlueprint()
```


