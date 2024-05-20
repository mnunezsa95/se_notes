Resource: 
* [Express Rate Limit: Documentation](https://www.npmjs.com/package/express-rate-limit)

# What does the express-rate-limit module do?
* Limits the number of requests from one IP address at one time 
	* Helps prevent DDoS attacks (see [[Distributed Denial of Service (DDoS)]])

#### Installing the express-rate-limit module
* Install the `express-rate-limit` module 
```bash
* Installing the express-rate-limit module
npm install express-rate-limit
```

#### Importing the express-rate-limit module
* Import the `'express-rate-limit'` module into the project
```js
const rateLimit = require('express-rate-limit');
```

#### Using the express-rate-limit module
* The limiter serves as a middleware function that can be executed using the `use()` method (see [[Express.js - Methods & Properties]])
```js
const express = require('express'); 
const rateLimit = require('express-rate-limit'); 
const app = express(); 

const limiter = rateLimit({ 
	windowMs: 15 * 60 * 1000, // in 15 minutes 
	max: 100 // you can make a maximum of 100 requests from one IP 
}); 

// applying the rate-limiter 
app.use(limiter);
```