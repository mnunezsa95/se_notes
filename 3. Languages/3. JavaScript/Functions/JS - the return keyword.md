See [[JS - Introduction to JavaScript]], [[JS - What are Functions?]]

---

# Return values
* EVERY function has a return value
	* If not explicitly stated, the return value is `undefined` (see [[JS - null, undefined, and NaN]])
	* Can be explicitly stated using the `return` keyword
* Can be used with all function types (see [[JS - Arrow Functions]], [[JS - Function Expressions]], [[JS - Function Declarations]])

### The return keyword
* Stops and returns the specified line of code, which can be used outside the function
	* Nothing after the `return` declaration will execute

### Example
* Example 1: No return value
```js
// this function will return 'undefined' since it does not explicitly have a return statement
function calculateArea(length, width) {
	console.log(length * width); 
}

calculateArea(10, 5); 
```

Example 2: using a return value
```js
// this function will return the result of length * width since it does explicitly have a return statement; this value can be used elsewhere if saved to a variable
function calculateArea(length, width) {
	console.log(length * width); 
	return length * width;
}

let area = calculateArea(10, 5); // return value is saved here!
```

