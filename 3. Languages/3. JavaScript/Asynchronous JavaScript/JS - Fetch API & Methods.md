# Using the Fetch API
* An interface for accessing and manipulating parts of the protocol, such as requests and responses using the global **fetch()** method

# Fetch API Method

#### fetch()
* Description
	* Starts process of fetching a resource from the network, and returns a promise which is fulfilled once the response is available (see [[JS - Promises]])
* Arguments
	1) resource --> the resource to be fetched (can be a string with a stringifier or request object)
	2) [options](https://developer.mozilla.org/en-US/docs/Web/API/fetch) (optional) --> an object containing custom settings to be applied to the request (possible options are)
		* method --> the request method
		* headers --> headers to be added to the request
		* body --> body to be added to the request
		* mode --> the mode to be used for the request (cors, no-cors, same-origin)
		* credentials --> controls what browsers do with credentials (see [[Cookies]])
			* omit --> browsers exclude credentials from the request and ignore credentials sent back in the response
			* same-origin --> browser to include credentials to same-origin URLs and use any credentials returned in response
		* cache --> A string indicating how the request will interact with the browser's HTTP cache. 
		* redirect --> how to handle re-direct response
		* referrer --> a string specifying the referrer of the request
		* referrerPolicy --> specifies the referrer policy to use for the request.
		* integrity --> contains the subresource integrity value of the request 
		* keepalive --> the keepalive option can be used to allow the request to outlive the page
		* signal --> communicates with a fetch request and abort it if desired via an AbortController.
		* priority --> specifies the priority of the fetch request relative to other requests of the same type
* Syntax
```js
fetch(resource, options)
```
* Example
```js
const request = fetch('https://restcountries.com/v3.1/name/portugal');
console.log(request);
```