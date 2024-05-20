#### What are Logs?
* Logs contain information about events that occur on the server. 
	* Contains info about requests to the server and the server's response to those requests
* Logs help better understand what is going on in the server including errors (see [[JS - Error Handling]], [[JS - Validating Inbound Server Data]], [[JS - Centralized Error Handling]])

#### Winston Library
* The most popular and flexible solution for logging errors (see [[Node.js - Module - winston]])

#### Setting up winston
1) Install winston
2) Import winston

# Using winston
* express-winston has a function called `logger()` that can be used to create a request logger
	* Can be used to log requests to the server & errors that occur on it

#### Using the `logger()` function
* `logger()` --> takes in an object of options
	* `transports` option --> an array that is responsible for identifying where the log should be written
	* `format` option --> responsible for the output format of the log
		* `json()` is common --> easy to parse
* Example: using `logger()` function
```js
// middlewares/logger.js

const winston = require('winston');
const expressWinston = require('express-winston');

// create a request logger
const requestLogger = expressWinston.logger({
	transports: [
		new winston.transports.File({ filename: 'request.log' }),
	],
	format: winston.format.json(),
}); 
```

#### Using the `errorLogger()` function
* `errorLogger()` --> responsible for writing the log (i.e. error name, error message, stack trace)
* Example
```js
// middlewares/logger.js

// error logger
const errorLogger = expressWinston.errorLogger({
	transports: [
		new winston.transports.File({ filename: 'error.log' }),
	],
	format: winston.format.json(),
}); 
```

#### How `logger()` and `errorLogger()` work together
* Request made to server --> `request.log` file is created (via the `logger()` function) --> info about request will be logged in JSON format
* If an error occurs --> `error.log` file is created (via the `errorLogger` function) --> info about the error is logged in JSON format. 
	* Will ONLY include part of the data, since the request body is NOT written to the log (by default) because it can contain sensitive info
		* Behavior can be manually changed. 
