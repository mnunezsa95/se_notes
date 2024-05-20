See [[JS - Centralized Error Handling]]
#### Rules for Centralized Error Handling
1) Always terminate promise chains with a catch block
	* Pass the `next()` function to the `catch()` block
	* Add the error handler at end of app.js
	* Unterminated promise chains will result in unhandled promise rejections; app can crash
2) Don't use `throw` in terminating `catch()` blocks
	* `throw` redirects the code handling to the next `catch()` block. 
	* If `throw` is used in the last `catch() `block, it will have no where to go and lead to unhandled promise rejection
3) If the handler receives an error without a status, return a server error.
```js
app.use((err, req, res, next) => {
	// if an error has no status, display 500
	const { statusCode = 500, message } = err;
	res.status(statusCode).send({
		// check the status and display a message based on it
	    message: statusCode === 500 ? 'An error occurred on the server': message
	});
}); 
```