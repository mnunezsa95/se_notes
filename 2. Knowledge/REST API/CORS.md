Resources
* [Understanding Cross-Origin-Resource-Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
* [Exploiting CORS Misconfigurations for Bitcoins and Bounties](https://portswigger.net/research/exploiting-cors-misconfigurations-for-bitcoins-and-bounties)

# Preventing the Attack: CORS

* In modern browsers, it is not possible to send a request from the front-end site. This will return an error (CORS Browser Restriction)
	* Example: If on https://one-site.com, cannot request anything using fetch() method from https://another-site.com.
![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Screen_Shot_2019-09-17_at_17.28.47_1600087243.png)

* Browsers send the request + additional data (in the form of cookies) to the server.
	* Without restrictions, scammers could use cookies for malicious purposes
* CORS browser restriction was introduced for security reasons (by default cross-domain requests are restricted)
	* This behavior can be changed (needed for open-source APIs)

--- 
# Allowing Cross-Domain Requests
* Browsers can't decide if cross-domain requests should be allowed
	* Needs permission from server
* Permission from server obtained using **pre-flight** mechanism
	1) Browser sends preliminary **OPTIONS** request to server
	2) Browser received the permission
	3) Browser sends the main request to the domain
* If cross-domain requests are needed
	* Set special response headers 
	* Handle the OPTIONS request on all endpoints

# Headers for Allowing Requests
### Access-Control-Allow-Origin
* Used to specify from which URL requests can be processed
	* The **asterisk ( * )** is used to allow requests from any URL
* Example
```bash
# This will allow the website to send requests to our server:
Access-Control-Allow-Origin: https://my-site.com
# This will allow requests from any website
Access-Control-Allow-Origin: *
```

### Access-Control-Allow-Methods
* Used to specify which request methods are permitted
* Example
```bash
# This will allow access to specific methods
Access-Control-Allow-Methods: GET,HEAD,PUT,PATCH,POST,DELETE 
```

### Access-Control-Allow-Headers
* Used to specify which request headers are permitted
* Example
```bash
Access-Control-Allow-Headers: Origin, X-Requested-With, Content-Type, Accept
```

# Setting Headers in Express.js
* Express uses middleware functions to allow cross-domain requests using the res.header() method (see [[Express.js - Methods & Properties]])
* Handle the **OPTIONS** using a conditional
```js
app.use(function(req, res, next) { 
	res.header('Access-Control-Allow-Origin', 'https://around.nomoreparties.co');
	res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With',               'Content-Type', 'Accept');
	res.header('Access-Control-Allow-Methods',                                          'GET,HEAD,PUT,PATCH,POST,DELETE'); 
	res.header("Access-Control-Allow-Credentials", true); 
	
	if (req.method === 'OPTIONS') { 
		res.send() 
	} else {
		next(); 
});
```

# Allowing Requests from Multiple Resources
* The **Access-Control-Allow-Origin** header can container either 
	* a single URL 
	* all URLs (using the asterisk)
* All requests have an Origin header.
* How to allow requests from multiple URLS, but not all of them
	* Create an array of allowed origins
	* Access the request's Origin header (contains the address from which this request is being sent)
	* Set up a conditional to check for the Origin header in the allowed origins array
```js
// an array of allowed domains 
const allowedOrigins = [ 
	'https://around.nomoreparties.co', 
	'http://around.nomoreparties.co', 
	'http://localhost:3000' 
];

app.use(function(req, res, next) { 
	const { origin } = req.headers; // assign the corresponding header to the           origin variable (accessing the origin object)
	res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With,               Content-Type, Accept'); 
	res.header('Access-Control-Allow-Methods', 'GET,HEAD,PUT,PATCH,POST,DELETE');
	if (allowedOrigins.includes(origin)) { // check that the origin value is                                                          among the allowed domains 
		res.header('Access-Control-Allow-Origin', origin); 
	} 
		// Respond to preflight OPTIONS requests 
		if (req.method === 'OPTIONS') { 
			res.send() 
		} else { 
			next(); 
		}
});
```

# The cors package
* NPM has a built-in package that can be used to set headers and handle the preflight OPTIONS at endpoints automatically
	* cors package must be imported
```js
// Imports the cors package
const cors = require("cors");
```


* Once installed:
	* The app.use() method can be used to set and handle the endpoints (see [[Express.js - Methods & Properties]])
```js
const cors = require("cors"); // Place this before any routes const 
allowedOrigins = [ 
	"https://around.nomoreparties.co", 
	"http://around.nomoreparties.co", 
	"http://localhost:3000", // Use the port your frontend is served on 
]; 

app.use(cors({ origin: allowedOrigins }));
```
