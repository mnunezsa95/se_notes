See: [[Node - Introduction to Node.js]]

--- 

What is the Response Object in Node.js?
* The response object is a parameter added to the callback function within the **createServer()** method. 
* Stores all information about the response
* Has methods and properties for working with the response

# Properties Used in the Response Object
* res.statusCode
	* Used to store the response status code
* res.StatusMessage
	* Use to store the response message
##### Methods Used in the Response Object
* res.setHeader()
	* Sets the header of the response
* res.write()
	* Send the response in parts
* res.writeHead()
	*  Two arguments
		1) statusCode
		2) header object
			* Always specify encoding format (charset = utf8)
				* Other encoding formats --> cause character issues
	* Sets the statusCode and header at the same time
		* Reduces the need for **res.statusCode** & **res.setHeader()**

* res.end()
	* Two arguments
		1) the outgoing data
		2) the encoding format of the outgoing data
	* Ends the response
		* No further response info can be sent after the end() method
		* All service requests MUST end with end() method call

Example: 
```js
const http = require('http'); 
const server = http.createServer((req, res) => { 
	res.statusCode = 200; // the response's status code 
	res.statusMessage = 'OK'; // the content of the message 
	res.setHeader('Content-Type', 'text/plain'); // add a header to the response
	res.write('Hello, '); // send the 1st part of the message - the "Hello,""
	res.write('world!'); // send the 2nd part of the message - the "world!" 
	res.end(); // end the response 
}); 	
server.listen(3000);
```