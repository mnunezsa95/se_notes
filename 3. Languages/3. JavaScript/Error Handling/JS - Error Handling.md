### Asynchronous Code

##### Async / Await Functions
- async / await --> allows for async code to be written in a sync style (tells JS where to 'wait' for the result of a promise before proceeding with rest of code)
    - async --> a keyword placed before a function
        - allows the function to return a promise
    - await --> a keyword used to make JavaScript pause until a promise (from async) is settled
        - allows for the code to pause and wait for the promise from async

- Example
```js
// Moved the code returning the promise with an error to an external
function function returnPromiseError() {
	return Promise.reject(new Error("Something went wrong..."));
}

(async function testAsyncAwaitError() {
	try {
		console.log("Function execution started");
		await returnPromiseError(); // wait till returnPromiseError() is executed
	} catch (err) {
		console.error(`${err.name} with the message ${err.message} has occured, 
		but we've handled it`);
	}
	console.log("Function execution completed successfully");
})();
```

---

##### The .catch() Handler / Method

- .catch()
    - catches and handles error from code that comes before it
    - catch() methods can be chained, but only one is executed (most specific --> least specific)

- Example
```js
function returnPromiseError() {
	return Promise.reject(new Error("Error. Something went wrong..."));
}

(function testPromiseRejectHandler() {
	returnPromiseError();
	.catch((err) => {
		console.error(`Error ${err.name} with the message ${err.message} has 
		occurred while executing the code, but we've handled it`);
	});
})();
```

##### Using console.error()
- console.error() w/ Express:
    - console.error() --> identifying issues that might occur w/ server
        - connection errors
        - unexpected behavior
        - errors related to specific routes
        - errors related to middleware functions

---

### Error Handling in callbacks
- Callback functions
    - Errors in callback functions --> handled different
        - Result of function --> returned to callback function as two arguments
            1. error object (if error occurs)
            2. the result of operation

*  Errors in callbacks
    - Errors do not cause application catches and can go unnoticed
	    - use if statement to help

* Example: 
```js
const fs = require('fs'); function writeTextToFile(filename, text) { fs.writeFile(filename, text, function (err, res) { 
	if (err) {  // check that the error object is not empty 
		console.error(`An error has occurred while writing the file: 
		${err.message}`); 
		return;  // end the function execution if an error occurs 
	} 
	console.log(`fs.writeFile has ended with the following result: ${res}`); 
	}) 
} 
writeTextToFile('', 'sometext');
```

### Error Handling in Mongoose
* Errors in **findById()** and **findOne()** --> pass 'null' to the .then() handler
	*  **.orFail()** --> used to handle errors
		* throws a 'DocumentNotFoundError'
		* can throw a custom error ()

* Example:  Using Default orFail() method
```js
Card.find({ title: "nonexistant card" }) 
	.orFail() // throws a DocumentNotFoundError 
	.then((cardData) => { res.send(cardData); // skipped bc an error was thrown 
	}) .catch((error) => { 
	// this runs so we can handle the error and return an appropriate message 
	});
```

* Example: Using custom orFail() method
```js
Card.find({ title: "nonexistant card" }) 
	.orFail(() => { 
		const error = new Error("No card found with that id"); 
		error.statusCode = 404; 
		throw error; 
		// Remember to throw an error s.catch handles it instead of .then 
	})
```

## Global Error Handlers and Custom Errors
* Node.js has a mechanism to handle global errors
##### Global error handlers
* Module: process
	* A module that allows for global error handler
* Event: uncaughtException
	* Catches both synchronous and asynchronous promises
	* An event that allows for global error handling
		* Takes two arguments
			1) error object
			2) origin
	* Determine where error occurred --> look at 'origin' value
		* value of origin = unhandledRejection (error occurred in Promise)
		* value of origin = something else (error occurred by using throw)

* Example
```js
const process = require('process'); // import process module

process.on('uncaughtException', (err, origin) => { // use uncaughtException event
	console.log(`${origin} ${err.name} with the message ${err.message} was not 
	handled. Pay attention to it!`); 
}); 
throw new Error(`The missed error`);// Throw a synchronous error 
```

---
## Approaches to Determine Error Type

##### Rules for Error Handling
* Add conditional statement for checking the error type in the error handling block
	* Use **if** statements & describe the handling in the body of the statement
* Describe logic for unknown errors (also 'default error handling') at the end of the **.catch()**
	* Does not allow any errors to go unnoticed
* Add return statements at each execution
	* Prevents  repeated checks
	* Doesn't allow execution to reach the 'default branch'
* Syntax: handling errors
```js
} catch (err) {
	if (check_condition_for_error_1) {
		// Logic for handling error 1
		return;
	}
	if (check_condition_for_error_2) {
		// Logic for handling error 2
		return;
	}
	// Logic for handling unknown errors
	console.log(`An unknown error ${err.name} has occured: ${err.message}`);
}
```

##### Two primary approaches to determine error type

Option 1: Using the name of an error (stored in the **name** field)
* Unique error names (in "name" field) allow for easy identification
	* Will throw "Error" as name of error in Error class (See #CustomError)
	* Drawbacks
		* Must cross-reference error names w/ code itself & third party libraries
		* Easy to create typos in conditional statement
		* No easy way to describe group of handlers
* Example: 
```js
} catch (err) {
	if (err.name === 'ErrorName') {
		// Logic for handling error 1
		return;
	}
	...// additional if blocks
	}
```

Option 2: Using the error class w/ the **instanceof** operator
* Using **instanceof** operator allows for whether the specified object (error) is an instance of a certain class
	* Takes inheritance into account
* Commonly used for API Errors
	* Describe a general class HttpError & one handler to return error
	* Describe the errors themselves
		* DocumentNotFoundError (error 404)
		* ForbiddenError (403)
* Example
```js
// Creating Custom class errors
class SomeError extends Error {}; 
class AnotherError extends Error {}; 
class ChildOfAnotherError extends AnotherError; 

// creating instance of class errors
let someError = new SomeError("SomeError") 
let anotherError = new AnotherError("AnotherError") 
let childOfAnotherError = new ChildOfAnotherError("Child error of AnotherError")

// This will return true because someError is an instance of SomeError 
console.log(someError instanceof SomeError)

// This will return false because anotherError is an instance of AnotherError, not SomeError
console.log(anotherError instanceof someError)

// This will return true, childOfAnotherError is an instance of ChildOfAnotherError and ChildOfAnotherError is inherited from AnotherError
console.log(childOfAnotherError instanceof AnotherError)

// This will return true, childOfAnotherError is an instance of ChildOfAnotherError
console.log(childOfAnotherError instanceof ChildOfAnotherError) 
```

* Example
```js
class ErrorGroup extends Error {}; 
class FirstChildOfErrorGroup extends ErrorGroup; 
class SecondChildOfErrorGroup extends ErrorGroup; 
try { 
	.... 
} catch(err) { 
	// Separate handler for FirstChildOfAnotherError 
	if (err instanceof FirstChildOfErrorGroup) { 
		// Logic for handling error
	} 
	// Handler for a group of errors 
	if (err instanceof ErrorGroup) { 
		// Logic for handling error
	} 
}
```