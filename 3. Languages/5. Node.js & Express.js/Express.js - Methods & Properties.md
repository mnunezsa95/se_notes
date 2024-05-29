See: [[Node - Introduction to Node.js]], [[Express - Introduction to Express.js]]
Documentation: 
* [Official Documentation: Express.js Methods: Express](https://expressjs.com/en/api.html)

---

#### express()
* What is the express() method?
	* Creates an express project and connects it to an app
* Arguments
	* none
```js
const express = require('express') // import express
const app = express(); // connect express to the app
```

#### express.urlencoded()
* What is the express.urlencoded() method?
	* Parses the incoming request with urlencoded payloads and is based upon the body-parser. 
	* Returns the middleware that parses all the urlencoded bodies.
* Arguments
	1)  an options object (see possible options below)
		* extended 
			* true --> allows for property values received in body to be of any type
			* false --> allows for property values received to only be strings and arrays
* Example
```js
app.use(express.json()); // for parsing application/json
app.use(express.urlencoded({ extended: true })); // for parsing application/x-www-form-urlencoded, the traditional GET form data format 
```

#### express.static()
* What is the express.static() Method?
	* Allows users to access files on the server from the outside
* Arguments
	1) a folder path
* Example
```js
const path = require('path'); //import path module

app.use(express.static(path.join((__dirname, "public"))); // use the join() method of the path module to give users access to a specific "public" folder
```

---
# App Methods
---[Official Documentation: Express.js Methods: Application](https://expressjs.com/en/api.html#app)---

#### app.listen() 
* What is the app.listen() Method
	* Binds and listens for connections on the specified host and port (identical to Node's http.Server.listen() Method)
* Arguments
	1) PORT
* Example
```js
app.listen(PORT, () => {
	// code below used to show which port the application is using
	console.log(`App is listening at port ${port}`)
});
```

#### **app.get()** 
* What is the app.get() method? (see [[HTTP Methods]])
	* handles GET requests (retrieve data from server)
* Arguments
	1) a string w/ the request (represents server path)
	2) a callback handler function --> fires when the server receives a request and route matches.
		* Parameters
			1) the request object 
			2) the response object --> has a variety of method
* Example
```js
app.get('./', (req, res) => {
	// logic for processing request
})
```

#### app.post() 
* What is the app.post() Method? (see [[HTTP Methods]])
	* handles POST requests (create a resource on server)
* Arguments
	1) a string w/ the request (represents server path)
	2) a callback handler function --> fires when the server receives a request and route matches.
```js
app.post('/books', createBook); 
```

#### app.put() 
* What is the app.put() Method? (see [[HTTP Methods]])
	* handles PUT requests (updates a resource on server)
* Arguments
	1) a string w/ the request (represents server path)
	2) a callback handler function --> fires when the server receives a request and route matches.
```js
app.put('/books/:id', replaceBook); 
```

#### app.patch()
* What is the app.patch() Method? (see [[HTTP Methods]])
	* handles patch requests (applies partial modifications to an existing resource)
* Arguments
	1) a string w/ the request (represents server path)
	2) a callback handler function --> fires when the server receives a request and route matches.
```js
app.patch('/books/:id', updateBookInfo); 
```

#### app.delete() 
* What is the app.delete() Method? (see [[HTTP Methods]])
	* handles delete requests (deletes a resource from server)
* Arguments
	1) a string w/ the request (represents server path)
	2) a callback handler function --> fires when the server receives a request and route matches.
```js
app.delete('/books/:id', deleteBook);
```

#### app.use() 
* What is the use() method?
	* Executes the router (once imported)
* Arguments
	1) first part of the file path (router will only start if it matches)
	2) the router itself
* Example
```js
const express = require('express'); 

// import routers
const router = require('./routes.js'); 
const api = require('./api.js'); 
const backoffice = require('./backoffice.js');

const { PORT = 3000 } = process.env; // set port
const app = express(); // import express & create express project

app.use('/', router); 
app.use('/api', api); 
app.use('/admin', backoffice);

app.listen(PORT, () => { 
	console.log(`App listening on port ${PORT}`); 
});
```

--- 
# Router Module Methods
---[Official Documentation: Express.js Methods: Router](https://expressjs.com/en/api.html#router)---

#### router()
* What is the router() method?
	* Creates a new router object
* Arguments
	* none
* Example
```js
const router = require('express').router(); // import and create the router
const { users } = require('./db.js'); // import other files needed for routing

router.get('/users/:id', (req, res) => {
	if (!users[req.params.id]) {
		res.send(`This user does not exist`)
		return;
	}
	const { name, age } = users[req.params.id];
	res.send(`User ${name}, ${age} years old`);
});
module.exports = router; // export the router
```

--- 
# Response Object Methods
#### res.send() 
* What is the res.send() method?
	* Sends a response to the user
	* Automatically sets the header (as needed)
	* Automatically sets status code of 200
		* Can be changed using the res.status() method
	* Accepts different types of data as an argument
		* string (text/plain)
		* string (text/html)
		* object (application/json)
```js
app.get('/', (req, res) => { 
	res.send('some text'); // Content-Type: text/plain 
	res.send('<p>some html</p>'); // Content-Type: text/html 
	res.send({ some: 'json' }); // Content-Type: application/json
});
```

#### res.status() 
* What is the res.status() method?
	* Sets the status code of a response that will be sent to the user (see [[HTTP Methods]])
	* Can be chained with the send() method
```js
app.get('/', (req, res) => { 
	res.status(404); // setting status code to 404
	res.send('some text'); // sending response to user
});
```

#### res.header() 
* What is the res.header() Method?
	* Sets the headers for a response to the user
* Alias: **res.set()**
* Example
```js
const setNoCacheHeaders = (req, res, next) => {
  res.header('Cache-Control', 'no-store');
  next()
};
```

### res.cookie()
* What is the res.cookie() Method?
	* Sets a cookie manually (see [[Cookies]])
* Arguments
	1) key --> the name of the cookie
	2) value --> the value of the cookie
	3) options --> an object with cookie behavior
		* maxAge --> sets the max age of the cookie
		* httpOnly --> takes a boolean value that will determine if the cookie is accessible ONLY via http (false will allow JavaScript to control the cookie --> risky)
		* sameSite --> takes a boolean value that will control whether or not a cookie is sent with cross-site requests, providing some protection against CSRF attacks (see [[Cross-Site Request Forgery (CSRF)]])
* Resources 
	* [Express.js - res.cookie() Documentation]([https://expressjs.com/en/api.html#res.cookie](https://expressjs.com/ru/api.html#res.cookie))
* Example
```js
res.cookie('name', 'Elise', {
  maxAge: 3600000,
  httpOnly: true
  sameSite: true 
}); 
```

---
# Request Object Properties

#### req.query
* What is the req.query property? 
	* A property on the request object that contains the request
	* Queries come in the from of string query (see [[Express.js - Client & Server Communication]])
		* Can be used to filter filter info on server
* Example
```js
const pokemon = [
	{type: 'fire', stage: 1, name: 'Charmander'},
	{type: 'fire', stage: 2, name: 'Charmeleon'},
	{type: 'water', stage: 3, name: 'Charizard'}
]

//--------------
// request coming in
GET `${BASE_PATH}/pokemon?type=fire&stage=3`; // "Charizard"**

//--------------
app.get('./pokemon', (req, res) -> {
	// make a copy of the object
	let result = pokemon
	// filter out pokemon that are not of desired type
	if (req.query.type) {
		result = result.filter(item => item.type === req.query.type)
	}
	// filter out pokemon that are not of desired stafe
	if (req.query.stage) {
		result = result.filter (item => item.stage === req.query.stage)
	}
	res.send(result)
})
```

#### **req.params** 
* All request parameters are properties of the **req.params** (JSON object)
* This object can be destructured to create variables with their values
```js
app.get('/users/:id/albums/:album/:photo', (req, res) => {
	const {id, album, photo} = req.params
	// requesting" "http://localhost:3000/users/123/albums/333/2"
	// request parameters are: {"id":"123","album":"333","photo":"2"}
	res.send(`We're on a user's page with the id of ${id}, looking through album #${album}, photo#${photo}`)
});
```

#### req.headers 
* Contains information about the headers sent in the request
* Can be used to destructure the **Origins** object (contains the URL used to send the request) (see [[CORS]])
	* Used to allow cross-domain requests
```js
app.use(function(req, res, next) { 
	const { origin } = req.headers; // assign the corresponding header to the o      origin variable
});
```

#### req.cookies
* Stores information about the cookies (see [[Cookies]], [[Express.js - Module - cookie-parser]])
* Example
```js
app.get('/posts', (req, res) => { 
	console.log(req.cookies.jwt); // getting the token 
});
```

---
# The cookie-parser Module Methods
#### cookieParser()
* Description
	* Extracts data from the Cookie header and then parse the resulting string into an object (see [[Express.js - Module - cookie-parser]], [[Cookies]])
	* Makes the cookies available in the `req.cookies` object (see [[Node.js - The Request Object]])
* Arguments
	* none
* Resources:
	* [The cookie-parser: Official Documentation](https://github.com/expressjs/cookie-parser)
* Example
```js
const express = require('express');
const cookieParser = require('cookie-parser');

const app = express();

app.use(cookieParser()); // connect the cookie parser as middleware

// Cookies are now available in the `req.cookies` object:
app.get('/posts', (req, res) => {
	console.log(req.cookies.jwt); // getting the token
}); 
```
