See [[Node - Introduction to Node.js]], [[Node.js - Importing & Exporting Modules]], [[package.json and package-lock.json]], [[JS - Async & Await]]

---

There are two ways to import modules in Node.js
1. `require()`
2. `import`

#### `require()`
* `require()` is synchronous -> will pause execution until module is loaded
```JS
const fs = require("fs"); 
```
* Pros:
	* Easy to use & widely supported
	* Synchronous loading -> useful for ensuring modules are loaded before execution continues
* Cons
	* No static analysis -> the dependencies are loaded at runtime, making it difficult to for tools to analyze and optimize code
	* No tree shaking -> All the code from a module is included (even when only part is needed)

#### `import`
* `import` -> Must specify the `.mjs` file extension or use `"type": "module"` in `package.json`
* `import` is asynchronous 
* `import` works with `async/await` 
```JS
import fs from 'fs';
```
* Pros:
	* Static Analysis -> Tools can analyze the code and perform optimizations like tree shaking to remove unused code
	* Support for ES6 Features -> Allows use of modern JS features (like `import`, `export`, `await`)
* Cons:
	* Compatibility -> Older Node.js version may not support ES Modules (might need transpilers like Babel)
	* Asynchronous Loading -> Can be a bit challenging


#### When to use each
* Use `require()` when maintaining older Node.js applications or need to work in an environment where ES modules are not supported
* Use `import` when building a new project or working on the front-end