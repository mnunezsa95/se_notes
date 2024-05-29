See: [[Node - Introduction to Node.js]], [[Express - Introduction to Express.js]]

--- 

#### Resources
* [How to Create Complex Routing Logic](https://expressjs.com/en/guide/routing.html) --> The official guide to routing in Express for large project

--- 
# Dynamic Routes
* Dynamic routes are used to handle URLs that match a certain rule
* Creating a dynamic route
	* Add a colon and the name of the property
	* Inside the server request
		* MUST have a value passed in place of the URL parameter
```js
app.get('/users/:id', (req, res) => {
	// code for handling requests
})
```

# Route Parameters
* All request parameters are properties of the **req.params** (JSON object) (see [[Express.js - Methods & Properties]])
* This object can be destructured to create variables with their values
```js
app.get('/users/:id/albums/:album/:photo', (req, res) => {
	const {id, album, photo} = req.params
	// requesting" "http://localhost:3000/users/123/albums/333/2"
	// request parameters are: {"id":"123","album":"333","photo":"2"}
	res.send(`We're on a user's page with the id of ${id}, looking through album #${album}, photo#${photo}`)
});
```
