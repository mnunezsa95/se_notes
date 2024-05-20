### What are tokens?
* See [[JWTs (JSON Web Tokens)]]

### Getting Token from Header
* Authorization looks like a middleware
	* If token is valid --> request will continue for further processing
	* If token is not valid --> request will go to a controller to return an error to client
* How to get authorization from header?
	1) Create a middleware function for handling authorization
	2) Retrieve the authorization from the request header
	3) Check for a non-existent token first
	4) If the token does exist, get it from the authorization constant that was destructured and call the `replace()` method
	5) Verify that the token is the same one sent to the user before using the `jwt.verify()` method and set its return equal to the payload (see [[Node.js - Module -  jsonwebtoken]], [[Node.js - Methods]])
		* `jwt.verify()` returns the decoded payload
		* Should be placed in a try...catch() statement since it returns an error if something goes wrong 
	6) Add the payload to the req object (see [[Node.js - The Request Object]])
	7) Send the request to other middleware as needed
	8) Apply the middleware to necessary routes
* Example
```js
// middleware/auth.js 
const jwt = require("jsonwebtoken");

module.exports = (req, res, next) => { 
	// getting authorization from the header 
	const { authorization } = req.headers; 
	// let's check the header exists and starts with 'Bearer ' 
	if (!authorization || !authorization.startsWith('Bearer ')) { 
		return res.status(401).send({ message: 'Authorization required' }); 
	} 
	// getting the token 
	const token = authorization.replace('Bearer ', '');
	
	// verifying the token 
	let payload; 
	
	try { 
		// trying to verify the token 
		payload = jwt.verify(token, 'some-secret-key'); 
	} catch (err) { // we return an error if something goes wrong 
		return res.status(401).send({ message: 'Authorization required' }); 
	}
	req.user = payload; // assigning the payload to the request object
	next(); // sending the request to the next middleware
};
```

```js
// app.js 
// applying authorization to necessary routes
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');

const { createUser, login } = require('./controllers/auth');
const auth = require('./middleware/auth'); // import authorization middleware

const app = express();

// some routes will NOT need authorization (like register and login)
app.post('/signup', createUser);
app.post('/signin', login);

// authorization
app.use(auth); // all routes below this line will secured

// these routes need auth
app.use('/cards', require('./routes/cards')); 
```

```js
// cam also be done like this:
const auth = require('./middleware/auth'); // import authorization middleware
app.use('/cards', auth, require('./routes/cards')); 
```

### Getting the user object
* Since the payload was saved to the user property of the request object it can be tied to it and can be used upon authorization
```js
// controllers/cards.js

module.exports.createCard = (req, res) => Card.create({
  name: req.body.name,
  link: req.body.link,
  owner: req.user._id // employing req.user in a handler
}); 
```