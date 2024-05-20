See [[Py - Introduction to Python]], [[Py - Tkinter (Getting Started)]], [[Py - Tkinter (Creating a Window)]]
Documentation:
* [Tkinter Official Python Documentation](https://docs.python.org/3/library/tk.html)
* [TKinter Commands](https://tcl.tk/man/tcl8.6/TkCmd/contents.htm)

#### `pack()`
* Packs each of the widgets next to each other
* By Default
	* Starts from top
	* Packs every widget below (can be changed with side parameter)
```Python
my_label = tkinter.Label(text="I am a label", font=("Arial", 24, "bold", "italic"))
my_label.config(text="New Text")
my_label.pack(side="left")
```

#### `place()`
* Places a widget with precise positioning (x, y)
* Downside of place()
	* It is too specific 
```python
my_label = tkinter.Label(text="I am a label", font=("Arial", 24, "bold", "italic"))
my_label.config(text="New Text")
my_label.pack(x="100", y="200")
```

#### `grid()`
* Creates a grid (rows, columns) across the window
* Places a widget at a specific row & column
* Relative to other widgets 
	* Best to start with widget you want at top and work down
```Python
button.grid(column=1, row=1)
label.grid(column=2, row=2)
```


#### Using multiple Layout Managers
* `grid()` & `pack()` in the same project (have to choose one or the other)