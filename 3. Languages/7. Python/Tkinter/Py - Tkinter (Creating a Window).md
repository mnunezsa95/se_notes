See [[Py - Introduction to Python]], [[Py - Tkinter (Getting Started)]]

Documentation:
* [Tkinter Official Python Documentation](https://docs.python.org/3/library/tk.html)
* [The Packer Function](https://docs.python.org/3/library/tkinter.html#the-packer)
* [The Tkinter Packer Command](https://tcl.tk/man/tcl8.6/TkCmd/pack.htm) 

---
#### Creating a window in Tkinter
* Import Tkinter
* Create an instance of the `Tk` class
* Call the `mainloop()` function of the `tk` class (should be at end of code)
* There are different functions for working with a window such as:
	* `title()`
	* `minsize()`
```Python
import tkinter
window = tkinter.Tk()
window.title("My First GUI Program")
window.minsize(width=500, height=300)

window.mainloop()
```
