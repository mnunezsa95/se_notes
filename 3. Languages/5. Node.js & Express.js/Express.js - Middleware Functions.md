See: [[Node - Introduction to Node.js?]], [[Express - Introduction to Express.js]]

---

#### What are Middleware Functions?
* Middleware functions
	* are functions that are executed as part of the server request's life cycle
	* allow us to write processing code inside a separate module
	* allows us to write code that is reusable

#### Middleware Function Syntax
* Arguments 
	1) the request object (see [[Express.js - Methods & Properties]])
	2) the response object (see [[Express.js - Methods & Properties]])
	3) the next callback
		* Represents the 'next' function in the chain of middleware
		* Must be called inside the body of the middleware --> passes execution to the next function
* Syntax
```js
const middlewareFunctionName = (req, res, next) => {
	// logic to deal with req and res
	next(); // call the next function in the chain
}
```

#### Creating a Middleware Function
* Middleware functions can be chained together to call one after the other
	* The order of middleware functions is important
* Example: 3 Middleware functions chained 
	* Usually called after the routes (see [[Express.js - Routing]])
```js
// Middleware function
const doesUserExist = (req, res, next) => { 
	if (!users[req.params.id]) { // checking if user exists
		res.send(`This user doesn't exist`); 
		return; // if no, function will exit and nothing will happen
	} 
	next(); // engine will begin to execute the next function of the same request
};

const doesUserHavePermission = (req, res, next) => {
	// logic for checking if user has permission
	next();
}

// This function will ONLY be called if the next() is called in prev function
const sendUser = (req, res) => { 
	const { name, age } = users[req.params.id]; 
	res.send(`User ${name}, ${age} years old`); 
};

//
router.get('/users/:id', doesUserExist, doesUserHavePermission, sendUser); 
```

#### Connecting Middleware
* Implementing Middleware Functions globally
	* Call the app.use() method and pass the middleware as an argument (see [[Express.js - Methods & Properties]])
	* Syntax
```js
app.use(middleware); 
```
* Example
```js
// Inside of index.js
const express = require('express'); 
const routes = require('./routes.js'); 
const { PORT = 3000 } = process.env; 
const app = express();

const logger = (req, res, next) => { 
	console.log('The request has been logged!'); 
	next(); // calling next()
}; 

app.use(logger); // calling the middleware function globally
app.use('/', routes); 

app.listen(PORT, () => { 
	console.log(`App listening on port ${PORT}`); 
});
```

#### Express's Built-in "Body Parser"
* Two ways to parse the body
	* Using body-parser package (see [[Express.js - The body-parser]])
	* Using middleware (see [[Express.js - Methods & Properties]])
		* Express has a body parser behavior built into express as a middleware function
		* The body parser function is used for express to know how to parse data it receives 
* Example
```js
app.use(express.urlencoded({extended: true})); // for parsing application/x-www-form-urlencoded, the traditional GET form data format
```
