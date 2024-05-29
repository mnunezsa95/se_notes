See: [[Node - Introduction to Node.js]]

--- 

## Connecting the HTTP API
* HTTP API --> built-in Node.js API
	* Handles incoming requests from an NIC  (see: [[Node - Introduction to Node.js]])
* Connecting the HTTP API
	1) Import the http module using the require() method (see [[Node.js - Methods]])
```js
const http = require('http');
```
## Building a Server
* Use the createServer() Method to create a new server (see [[Node.js - Methods]])
* Accepts a callback function (two parameters) to handle server responses and execute code when receiving a request
	* Callback takes 2 parameters
		1) The **request** object (req)
			* Stores information about the request (see [[Node.js - The Request Object]])
		2)  The **response** object (res) 
			* Contains properties and methods for working with the response (see [[Node.js - The Response Object]])
* Example
```js
const server = http.createServer(function (req, res) { // setting up a server
	// to be executed by callback
}); 
```

## Setting up a Port
* Computer has several programs running that need to receive incoming requests from the NIC
	* NICs have multiple entry points (also "ports")
		* There are 65,535 ports (0-65,535)
* Setting up a port
	* Use the listen() method on the server to set up a port (see [[Node.js - Methods]])
* Example:
```js
server.listen(3000)
```

#### Environmental Variables
* Environmental Variables
	* Allow applications to be more flexible 
	* Used to pass data needed to configure the app
	* Should be defined before executing the start command
* Environmental variables in Script Files
	* Stored in the **process.env** object
	* Rules for writing Environmental Variables
		* Use ALL Capitals
		* Separate each word using underscore ( _ )
```js
// Example 1
const {PORT = 3000} = process.env; // pass default parameter
server.listen(PORT)

// Example 2
if (process.env.NODE_ENV !== 'production') { // if node env does != production 
	console.log('Code executed in development mode')
}
```

