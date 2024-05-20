See [[Py - What is OOP?]], [[Py - Introduction to Python]], [[Py - Functions]]

#### Creating classes with unlimited `**kwargs`
* The `get()` method will get a property if it exists, or return none if it doesn't
```python
class Car:
  def __init(self, **kwargs):
    self.make = kwargs.get("make")
    self.model = kwargs.get("model")
    self.color = kwargs.get("color")
    self.color = kwargs.get("seats")

my_car = Car(make="Nissan", model="GT-R")
print(my_car.model)
```