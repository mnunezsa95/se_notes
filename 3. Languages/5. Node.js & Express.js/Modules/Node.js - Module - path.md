--[Node.js Documentation - the path Module](https://nodejs.org/api/path.html)--
### What is the path Module?
* The path module provides utilities for working with file and directory paths
* Allows us to add together folder names to create a path
* Often used in tandem with the fs module (see [[Node.js - Module - fs]])

### Using the path Module
* Import the path module into the module that needs to be accessed
* Use the path module variables and one of the following to create paths
	1) the path.join() method (see [[Node.js - Methods]])
	2) concatenation 
	3) template literal notation 
* Path module variables:
	* _____filename --> stores the module's file path
	* _____dirname --> stores the module's directory path
* Example:
```js
const fs = require('fs')
const file = require('path')

module.exports.readFile = () => {
	const filepath = path.join(__dirname, 'file.txt'); // joining path segments
	const file = fs.readFile(filepath, {encoding: 'utf8'}, (err, data) => {
		console.log(data)
	})
}
``` 
