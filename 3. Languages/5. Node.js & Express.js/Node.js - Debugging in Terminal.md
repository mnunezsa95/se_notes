See: [[Node - Introduction to Node.js]]

--- 

How to debug Node.js programs?
* 3 Ways
	1) In the Terminal
	2) In the browser (requires additional setup)
	3) In vsCode (see [[Node.js - Debugging in vsCode]])
### Starting up a Node.js Program
* Running a node program when NOT in the file
```bash
node path/to/fileName.js 
```
* Running a node program when INSIDE the file
```bash
node fileName.js 
```

### Starting up a Node.js Program to Debug
* Running a node program to debug when NOT in the file
```bash
node inspect path/to/fileName.js
```
* Running a node program to debug when INSIDE the file
```bash
node inspect fileName.js
```

### Commands for Moving in Terminal - Debug Mode
| step name | keyboard shortcut | action                                             |
| --------- | ----------------- | -------------------------------------------------- |
| const     | c                 | continue execution                                 |
| next      | n                 | step next --> used to go line by line              |
| step      | s                 | Step in --> used to step in into a block of code   |
| out       | o                 | Step out --> used to step out of a block of code   |
| pause     | pause             | Pause on running code (like pause btn in DevTools) |


### Methods / Command for Debugging in the Terminal
* **watch()** --> used to watch a variable change overtime 
* **.exit** --> used to exit the debugger entirely
