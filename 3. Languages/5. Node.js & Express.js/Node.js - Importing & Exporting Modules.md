See: [[Node - Introduction to Node.js]]

--- 

Do ES6 Modules work in Node.js
* ES6 Modules work in Node.js V8 or higher
* ES6 Modules have 'use strict' mode enabled (by default)

How to use ES6 Modules in Node.js (2 Options)
1) Add 'module' to the 'type' field of the **package.json** file
	* Can use the 'export' keyword to export variables and functions
2) Add the **.mjs** file extension when creating module files
	* Can use the 'export' keyword to export variables and functions

* Syntax: Export ES6 Modules
```js
// moduleName.mjs
export const someVariableName = someValue;
export const someFunctionName = (name) => { return someValue }; 
```

* Syntax: Importing ES6 Modules
```js
import {someVariableName, someFunctionName} from './someLocation';
```

