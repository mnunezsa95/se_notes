See [[Py - Introduction to Python]], [[Py - Tkinter (Getting Started)]], [[Py - Tkinter (Creating a Window)]]
Documentation:
* [Tkinter Official Python Documentation](https://docs.python.org/3/library/tk.html)
* [TKinter Commands](https://tcl.tk/man/tcl8.6/TkCmd/contents.htm)

#### Creating a label in Tkinter
* Create an instance of the `Label()` class from the tkinter module
* Use the `pack()` to pack the label.
	* There are many arguments that can be passed into the pack function
```Python
### Creating a label
my_label = tkinter.Label(text="I am a label", font=("Arial", 24, "bold", "italic"))
my_label.pack(side="left")
```

#### Creating a Button in Tkinter
* Create an instance of the `Button()` class from the tkinter module
* Use the `pack()` method to pack the button
```Python
def button_clicked(): # callback function
  new_text = input.get()
  my_label["text"] = new_text # accessing & changing the text property

# command tells button to listen for the callback function
button = tkinter.Button(text="Click Me", command=button_clicked)
button.pack()
```

#### Creating a Label
* Create an instance of the `Input()` class from the tkinter module
* Use the `pack()` method to pack the input
```Python
input = tkinter.Entry(width=10) 
input.pack()
input.get() # Returns the input as a string
```