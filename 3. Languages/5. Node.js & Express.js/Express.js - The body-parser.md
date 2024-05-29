See: [[Node - Introduction to Node.js]], [[Express - Introduction to Express.js]]

--- 

* Data is broken down into segments during transmission from the client and the server
* Once received the data is re-assembled on the receiving side in chunks
	* Express has a "body-parser" package that makes the parsing of the body easier 
```js
const postForm = (req, res) => {
	const { body } = req; // simply refer to the body object
};
```
