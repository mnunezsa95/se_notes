See: [[Node - Introduction to Node.js]]

--- 
##### Importing Node.js Modules
* Node.js modules are imported via the **require()** method (see [[Node.js - Methods]])
```js
const md5 = require('md5'); 
const http = require('http'); 
```

##### Creating & Importing Custom Modules
* ES6 Modules are imported differently (see [[Node.js - Importing & Exporting Modules]])
* Module code is written in separate file and imported where needed
	* Modules have the .js extension (can be omitted)
	* Use lowercase to write modules
* Syntax: Importing costume modules
```js
// Import
const utils = require('./utils');
const someFunction = utils.someFunction;
const someVariable = utils.someVariable;

// Import via Destructuring
const { someFunction, someVariable } = require('./utils');
```

##### Exporting Node.js Modules
* The **module.exports** object is used to export Node.js modules
	* Assign variables and functions to be exported to this object (as a property)
* Custom modules do NOT have 'use strict' enabled
* Syntax: module.exports
```js
// someFile.js
'use strict'
module.exports.someFunction = () => { //someFunction is property of exports obj
	// body of the function
}

module.exports.someVariable = someValue // someVariable is property of exports obj
```
* Syntax: module.exports
```js
const someFunction = () => {
	// body of the function
}

const someVariable = someValue;

module.exports = {
	someVariable,
	someFunction
}
```

##### Importing NPM Packages
* NPM packages are also imported via the **require()** method (see [[Node.js - Methods]])

