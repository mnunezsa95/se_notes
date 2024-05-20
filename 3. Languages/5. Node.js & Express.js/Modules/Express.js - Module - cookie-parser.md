# What is the cookie-parser module used for?
* A middleware that extracts data from the Cookie header and then parse the resulting string into an object (see [[Cookies]])

#### Installing the cookie-parser module
* Use NPM to install the cookie-parser module
```bash
npm install cookie-parser
```

#### Importing the cookie-parser module
* Import the cookie-parser into the required module
```js
// importing cookieParser
const cookieParser = require('cookie-parser');
```

#### Using the cookieParser() method
* cookieParser is a method that can be executed using the `use()` (see [[Express.js - Methods & Properties]])
	*  makes the cookies available in the `req.cookies` object (see [[Node.js - The Request Object]], [[Express.js - Methods & Properties]])
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