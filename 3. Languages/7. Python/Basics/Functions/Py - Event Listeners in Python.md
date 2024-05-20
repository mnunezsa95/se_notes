See [[Py - Introduction to Python]], [[Py - Functions]]

#### What are event listeners?
* Event listeners are functions that 'listen' for an event to happen in order to trigger a callback function

```Python
def move_forwards(): # a function
  turtle.forward(30)

screen.onkey(move_forwards, "space") # onkey() is an event listener that takes an object as an input and a key

# move_forwards() is executed when "space" is clicked
```