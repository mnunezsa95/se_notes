See: [[Node - Introduction to Node.js?]]

--- 

What is the Request Object in Node.js?
* The request object is a parameter added to the callback function within the **createServer()** method. 
* Stores all information about the request

Forms in Node.js
* Forms requests are handled differently (see [[Node.js - The <Form> Elements]])

## Properties Used in the Request Object
--Complete list of [http.IncomingMessage class](https://nodejs.org/api/http.html#http_class_http_incomingmessage)--
* req.url
	* Stores the request URL (the path and query/hash parameters)
* req.method
	* Stores the request Method
* req.headers
	* Stores information about the request headers
* req.body
	* Stores information about the request body
* req.cookies
	* Stores information about the cookies (see [[Cookies]], [[Express.js - Module - cookie-parser]])

Example:
```js
const http = require('http'); const server = http.createServer((req, res) => { 
	console.log(req.url); // /hello 
	console.log(req.method); // GET 
	console.log(req.headers); // the request headers will be here 
	console.log(req.body); // the request body will be here
}); 
server.listen(3000);
```

Example: Checking values of incoming request
```js
const server = htttp.createServer((req, res) => {
	if (req.url === '/songs' && req.method === 'GET') {
		console.log('GET the list of songs!')
	}
})
```

----
## Methods Used in the Request Object
#### req.on()
* What is the req.on() method
	* Listens for an event
* Arguments
	1) the event (types of events, see below
		* 'data' --> triggered whenever data package is received
		* 'end' --> triggered when the last package arrives [[Node.js - Processing Request Data]]
			* used to process the request into an JSON object 
		* 'error' --> triggered when an error happens
			* used to handle the error*
	2) the callback function
		* Buffer object
			* Used with the 'data' event handler to read binary code
Example
```js
const http = require('http'); 
const server = http.createServer((req, res) => { 
	req.on('data', (chunk) => { // chunk = the buffer object
		console.log(chunk); // <Buffer 66 69 65 6c 64 3d 76 61 6c 75 65> 
	}); 
	req.on('end', () => { 
		console.log(JSON.parse(data)); 
	});
}); 
server.listen(3000);
```

#### req.pipe()
* What is the req.pipe() method?
	* "pipes" streams together 
	* contains built-in logic for closing streams and handling errors
	* can only be called on readable streams
* Arguments
	* A writable stream
```js
const http = require('http');
const fs = require('fs');

const server = http.createServer(function (req, res) => {
	req.pipe(fs.createWriteStream(`./out-${Math.random()}.txt`)`;
});

server.listen(3000)
```

