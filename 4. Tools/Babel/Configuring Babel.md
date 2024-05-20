Resources
* [Babel: Documentation](https://babeljs.io/)

### What is babeljs?
* Babel is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments (see [[Bundling with Parcel]])
	* Transform syntax
	* Polyfill features that are missing in your target environment (through a third-party polyfill such as core-js)
	* Source code transformations (codemods)

### Pollyfiling 
* Newer additions to the JavaScript language will need to be pollyfilled
	* Pollyfiling will make them usable in older browsers 
* core-js is a popular library for polyfilling

### Installing babel
* Install babel as a development dependency
```bash
npm install --save-dev
```

### Installing & Importing core-js
* For polyfilling, install **core-js**
```bash
npm install core-js
```

* Import core-js
```js
// Importing everything from core-js
import 'core-js/stable';

// Importing specific pollyfillers
import 'core-js/stable/array/find';
import 'core-js/stable/promise;
```