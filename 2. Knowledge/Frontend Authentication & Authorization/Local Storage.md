### What is local storage? 

* Allows for content to be saved to the browser such as:
	* JWTs (see [[JWTs (JSON Web Tokens)]])
* Functions as a "hard-drive" for the browser
	* Unsaved items are lost

### Cons of localStorage 
* A low level of security for large projects (see [[Cookies]])
	* Accessible from JavaScript so, it can be hacked

---
# Browser Storage
#### the localStorage object
* localStorage --> a global JavaScript object used to keep some persistent data in the browser
	* Has a variety of methods (see [[localStorage Methods]])

# Using the localStorage Object
#### Example
* Uses key-value pairs to store information 
	* the `JSON.stringify()` and `JSON.parse()` are used to store and retrieve complex information
* Example
```js
// creating a username
localStorage.setItem('user', JSON.stringify({
  firstName: 'Marvin',
  lastName: 'Quack'
}));

// getting the username
JSON.parse(localStorage.getItem('user'));
```

# Working with Tokens
#### Saving a Token
* Tokens can be saved to localStorage when received in a response (using the then() method)

#### Sending a Token
* Tokens can be sent inside a request (inside the `authorization` header)
	* MUST have an authorization scheme called (`Bearer `) followed by the token (a space in between)
		* authorization scheme --> tells the sever to check the user's rights by using the token

#### Example
```js
// sending a request to the authorization route
fetch('https://api.mywebsite.com/posts', {
	method: 'GET',
	headers: {
	    authorization: `Bearer ${localStorage.getItem('token')}`
	}
}); 
```