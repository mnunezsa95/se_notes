Methods to be used with AJAX (see [[JS - AJAX Calls]])
# XMLHttpRequest() Methods

### XMLHttpRequest()
* Description
	* a constructor used to initialize an XMLHttpRequest
* Arguments
	1) paramsDictionary --> an object
		* mozAnon --> when set to true, the browser will not expose origin and user credentials when fetching resources
* Syntax
```js
const request = new XMLHttpRequest(paramsDictionary);
```
* Example
```js
const request = new XMLHttpRequest();
```

### open()
* Description
	* initializes a newly-created request, or re-initializes an existing one
* Arguments
	1) method --> the HTTP request method to use 
		* can be: "GET", "POST", "PUT", "DELETE", "PATCH"
	2) url --> a string containing the url that contains the resource
	3) async (optional) --> boolean indicating whether or not to perform the operation asynchronously
		* true (default) --> will return method while waiting for response
		* false --> will not return until the response is received (acts synchronously)
	4) user (optional) --> the username for authentication purposes 
	5) pass (optional) --> the password for authentication purposes
* Syntax
```js
request.open(method, url, async, user, password)
```
* Example
```js
const request = new XMLHttpRequest();
request.open('GET', 'https://restcountries.com/v3.1/name/deutschland');
```

### send()
* Description
	* sends the request to the server
* Arguments
	1) [body](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send) (optional) --> a body of data to be sent in the XHR request 
* Syntax
```js
request.send(body)
```
* Example
```js
const request = new XMLHttpRequest();
request.open('GET', 'https://restcountries.com/v3.1/name/deutschland');
request.send();
```



---
# XMLHttpRequest() Properties

### responseText
* Description
	* Contains the response received from an XMLHttpRequest
* Syntax/Example
```js
const request = new XMLHttpRequest();
request.open('GET', 'https://restcountries.com/v3.1/name/deutschland');
request.send();

request.addEventListener('load', function () {
  const data = JSON.parse(this.responseText);
  console.log(data);
});
```