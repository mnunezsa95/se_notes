## Exporting & Importing Statements
* Export and Import statements are used to work with modules (see [[JS - What are Modules?]], [[JS - Loading & Using Modules]])
- Exporting = making variables and functions of a module available for other files
	- To export a function or a variable add the export statement
- Importing = making variables and functions from one module work in another
	- To import a function or a variable add use the import statement  

### Exporting
* Two types of exports
	* Named export --> exports several functions, variables, etc from a module
		* On declaration
		* After declaration
		* Rename on export
	* Default export --> exports a single value returned from a module
		* default

* Exporting on declaration --> exporting when declared or written
	* Use the **export** statement at the beginning of the variable
```js
export function giveMeSomeInternet() {
	return "Hello! Yes, this is internet.";
}
```

* Exporting after declaration --> exporting after declared or written
	* Use curly brackets `{ }` and export statement at the end of file
```js
const array = [1, 2, 3, 4];
const arrSquared = arr.map(item => item * item);

// export a list
export { array, arrSquared }; 
```

* Renaming the export --> exporting and renaming during export
```js
const array = [1, 2, 3, 4];
const arrSquared = arr.map(item => item * item);

// Rename at export
export { array as arr, arrSquared as sq }; 
```

* Default export --> used when only need to export one entity 
	* Uses the `default` keyword after the `export` statement; 
		* Names given to the variables or functions don't matter when imported
	* Usually used for classes or for one function
```js
export default function renderItems() {
  // function code
} 

export default class {
	constructor() { }
}

export default [12, 22, 31]; 
```

---
### Importing
* Three types of imports
	* Named import --> imports several functions, variables, etc from a module
		* Import
		* Rename on import
	* Import all --> imports all variables and functions exported from a file
	* Import default --> imports ONLY the one default exported variable from the file

* Named imports
	* Use `import` statement & curly braces `{ }` at the beginning of a file
```js
import { array, arrSquared } from "./data.js"

console.log(array); // [1, 2, 3]
console.log(arrSquared); // [1, 4, 9] 
```

* Rename on import --> change the name when importing
```js
// index.js
import { array as arr, arrSquared as sq } from "./data.js"

console.log(arr); // [1, 2, 3]
console.log(sq); // [1, 4, 9] 
```

* Import all --> imports all variables and functions exported from a file
	* NOT Recommend --> can lead to bugs & difficult to refractor
```js
// index.js
import * as data from "./data.js";

// Everything that has been exported from the data.js file will be imported 
console.log(data.array); // [1, 2, 3]
console.log(data.arrSquared); // [1, 4, 9] 
```

* Default import
	* Curly braces `{ }` are NOT needed with default imports
	* The item MUST be named at import
```js
import renderItems from "./render-items.js";
import Song from "./song.js";
import someArr from "./data.js";
```


---

# Summary: Imports & Exports

| Syntax                           | Explanation                                              |
| -------------------------------- | -------------------------------------------------------- |
| `export const array = [1, 2, 3]` | export on declaration                                    |
| `export { dog, cat }`            | export multiple entities separate from their declaration |
| `export default data`            | export a single variable, function, or class.            |

| Syntax                                    | Explanation                                         |
| ----------------------------------------- | --------------------------------------------------- |
| `import { array } from "./data.js" `      | import using a feature's original name              |
| `import *                          `      | import all exports.                                 |
| `import { array as arr } from "./data.js` | rename feature on import                            |
| `import data from "./data.js”`            | import of a default export (no curly braces needed) |
