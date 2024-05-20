--[Node.js Documentation - the fs Module](https://nodejs.org/api/fs.html)--
### What is the **fs** Module?
* Allows for access and manipulation of the file system
* Has many methods for working with file systems (see [[Node.js - Methods]] for details) 
	* fs.readFile()
	* fs.readdir()
	* fs.mkdir()
	* fs.writeFile()
	* fs.unlink()

### Using Promises in the fs Module
* The fs module supports promises
* How to use fs promises?
	* Import the 'promises' property of the fs module
* When using promises with fs module method --> no need for callbacks
	* If successful --> promises are resolved
	* if unsuccessful --> promises are rejected
		* use **catch()** blocks to handle errors
```js
const fsPromises = require('fs').promises; // import promises property of the fs module

fsPromises.readFile('data.json', { encoding: 'utf8' }) // no callback needed
	.then((data) => {  // hanlde data w/ promises
		console.log(data); 
	}) 
	.catch(err => {  // handle errors (in case Promise is rejected)
		console.log(err); 
	});
```

### Using Paths in fs Module Methods
* Using relative paths is NOT ideal
	* Hard to maintain as project grows 
	* Easy to make errors
* Use the dynamic routes
	* Identify where the module we want to access is located
	* Add the **path** module for working with directories and file paths (see [[Node.js - Module - path]])
	