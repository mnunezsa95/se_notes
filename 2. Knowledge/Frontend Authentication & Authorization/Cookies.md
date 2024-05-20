* JWT can be stored 
	* In local storage (can be risky for large project) (see [[Local Storage]])
	* In cookies

# What are cookies?
* Local data files that store data (related to a specific domain) in the browser

#### How Cookies work
1) Browser uses a `Set-Cookie` header in the response (see [[Node.js - The Response Object]])
	* Writes data to a browser cookie
2) Browser saves the `name=value` in the browser's cookies

#### Setting & Sending Cookies (on the backend)
* Express.js has a useful method: `res.cookie()`  for setting cookies manually (see [[Express.js - Methods & Properties]])
	* Allow for cookie behavior to be controlled
	* Cookies can be made to only be accessible via HTTP (making them safer)
* Example
```js
// let's send a token, the browser will save it in cookies
res.cookie('jwt', token, { maxAge: 3600000, httpOnly: true }).end(); 
// if the response has no body, you can use the end() method 
```

#### Sending Cookies with fetch() (on the frontend)
* If cookies have the `httpOnly` set to true they cannot be accessed via JavaScript
	* If frontend & backend on same domain --> browser automatically sends cookies
	* If frontend & backend on same domain --> must enable the `credentials` option to '`include`' in the object of the fetch method (see [[JS - Fetch API & Methods]])

#### Parsing Cookies (on the backend)
* The `cookie-parser` module is a middleware that extracts data from the Cookie header and then parse the resulting string into an object (see [[Express.js - Module - cookie-parser]])

#### Drawbacks of Using Cookies
* Can cause alot of bugs in the code once turned on