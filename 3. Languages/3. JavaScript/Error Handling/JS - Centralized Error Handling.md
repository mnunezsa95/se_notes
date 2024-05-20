* See [[JS - Error Handling]]

#### What is centralized error handling?
* Providing a central location (such as a middleware for error handling)
	* Leads to less repetitive code
* Rules for centralized error handling (see [[JS - Centralized Error Handling Rules]])

#### Centralized Error Handling Middleware
* Accepts 4 paramaters
	1) error
	2) requestObject
	3) responseObject
	4) nextFunction
		* Accepts an argument (requests will go to the error handler) such as an Error instance (see [[JS - Error Constructor()]])
* Goes after all other `app.use()` statements
* Example
```js 
// app.js

// all the app.js code
// other app.use() statements

// we handle all errors here
app.use((err, req, res, next) => {
	res.send({ message: err.message });
	next(new Error('Authorization error')); // adding an Error instance
});

app.listen(PORT); 
```

#### Setting an error status
* Two ways of setting an error status
	1) Assign an additional property to the `Error` instance, then call `next()`
	2) Creating Custom Errors

```js
// 1) Assigning the statusCode property
try {
	payload = jwt.verify(token, 'some-secret-key');
} catch (e) {
	const err = new Error('Authorization required'); 
	err.statusCode = 401;
	next(err);
} 
```

```js
// 2) Creating a custom error
// errors/not-found-err.js

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


#### Working with Custom Errors
* New error classes can be created by extending the error class as shown above (see [[JS - Error Classes]])
```js
class NotFoundError extends Error {
	constructor(message) {
	    super(message);
	    this.statusCode = 404;
	}
}
module.exports = NotFoundError; 
```

* Created error classes can be used in other parts of the code 
	* Using `catch(next)` is the same as `.catch(err => next(err));`
```js
// in controller.js

const NotFoundError = require('./errors/not-found-err');

module.exports.getProfile = (req, res, next) => 
	User.findOne({ _id: req.params.userId }).then((user) => {
	    if (!user) {
			// if there is no such user, throw an exception
	    throw new NotFoundError('No user with matching ID found');
    }
    res.send(user);
}).catch(next); 
```

* In app.js
```js
// apps.js
app.use((err, req, res, next) => {
	res.status(err.statusCode).send({ message: err.message });
}); 
```

