Defining Customer Errors
* Extend Error object --> to include additional info for handling errors
	* Specify the desired info as a property of a specific error instance
* Example: 
```js
class ValidationError extends Error {  // extend Error class
	constructor(message) {  // use constructor
		super(message); // import message from parent (Error class)
		this.name = "ValidationError";  // set error name
		this.statusCode = 400; // set error statusCode
	} 
}

// throwing custom error
throw new ValidationError('A validation error occured')
```