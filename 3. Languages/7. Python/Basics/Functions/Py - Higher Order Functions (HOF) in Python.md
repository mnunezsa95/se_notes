See [[Py - Introduction to Python]], [[Py - Functions]]

#### What are higher order functions?
* HOFs are functions that work with other functions
	1) Take other functions as inputs
	2) Return another function

```Python
def move_forwards(): # a function
  turtle.forward(30)

screen.onkey(move_forwards, "space") # onkey() is an event listener that takes an object as an input and a key
```

```Python
# Functions
def move_forwards():
  tim.forward(10)

def move_backwards():
  tim.backward(10)

def turn_left():
  tim.left(10)

def turn_right():
  tim.right(10)

def clear_drawing():
  tim.clear()
  tim.penup()
  tim.home()
  tim.pendown()

# HOFs
screen.listen()
screen.onkey(move_forwards, "w")
screen.onkey(move_backwards, "s")
screen.onkey(turn_left, "a")
screen.onkey(turn_right, "d")
screen.onkey(clear_drawing, "c")
screen.exitonclick()
```