See [[Py - Introduction to Python]], [[Py - Tkinter (Getting Started)]], [[Py - Tkinter (Creating a Window)]]
Documentation:
* [Tkinter Official Python Documentation](https://docs.python.org/3/library/tk.html)
* [TKinter Commands](https://tcl.tk/man/tcl8.6/TkCmd/contents.htm)

#### Creating a Textbox
* Create an instance of the `Text()` class from the tkinter module
* Use the `pack()` to pack the label.
	* There are many arguments that can be passed into the pack function
```Python
text = Text(height=5, width=30)
text.focus() # Puts cursor in textbox.
text.insert(END, "Example of multi-line text entry.") # Adds some text to begin with.
print(text.get("1.0", END)) # Get's current value in textbox at line 1, character 0
text.pack()
```


#### Creating a Spinbox
* Create an instance of the `Spinbox()` class from the tkinter module
* Use the `pack()` to pack the label.
	* There are many arguments that can be passed into the pack function
```Python
def spinbox_used():
  print(spinbox.get()) # gets the current value in spinbox.

spinbox = Spinbox(from_=0, to=10, width=5, command=spinbox_used)
spinbox.pack()
```

#### Creating a Scale
* Create an instance of the `Scale()` class from the tkinter module
* Use the `pack()` to pack the label.
	* There are many arguments that can be passed into the pack function
```Python
def scale_used(value): # Called with current scale value.
  print(value)

scale = Scale(from_=0, to=100, command=scale_used)
scale.pack()
```

#### Creating a Checkbutton
* Create an instance of the `Checkbutton()` class from the tkinter module
* Use the `pack()` to pack the label.
	* There are many arguments that can be passed into the pack function
```Python
def checkbutton_used():
  print(checked_state.get()) # Prints 1 if On button checked, otherwise 0.

checked_state = IntVar() # variable to hold on to checked state, 0 is off, 1 is on.
checkbutton = Checkbutton( text="Is On?", variable=checked_state, command=checkbutton_used)
checked_state.get()
checkbutton.pack()
```


#### Creating a Radiobutton
* Create an instance of the `Radiobutton()` class from the tkinter module
* Use the `pack()` to pack the label.
	* There are many arguments that can be passed into the pack function
```Python
def radio_used():
  print(radio_state.get())

radio_state = IntVar() # Variable to hold on to which radio button value is checked.

radiobutton1 = Radiobutton(text="Option1", value=1, variable=radio_state, command=radio_used)

radiobutton2 = Radiobutton(text="Option2", value=2, variable=radio_state, command=radio_used)

radiobutton1.pack()
radiobutton2.pack()
```

#### Creating a Listbox
* Create an instance of the `Listbox()` class from the tkinter module
* Use the `pack()` to pack the label.
	* There are many arguments that can be passed into the pack function
```Python
def listbox_used(event):
  print(listbox.get(listbox.curselection())) # Gets current selection from listbox

listbox = Listbox(height=4)
fruits = ["Apple", "Pear", "Orange", "Banana"]
for item in fruits:
  listbox.insert(fruits.index(item), item)

listbox.bind("<<ListboxSelect>>", listbox_used)
listbox.pack()
```