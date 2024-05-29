See: [[Node - Introduction to Node.js]], [[Express - Introduction to Express.js]]

--- 

* The client can be given access to static data (HTML files, styles, scripts and images) using the **static()** method. (see [[Express.js - Methods & Properties]])
	* This method makes folders accessible from "the outside"

### Giving Users Access to Static Files
* Store all files that a user would ideally need in a "public" folder
* DO NOT give users access to the root directory
	* Dangerous!
```js
// DO NOT do this!
app.use(express.static(__dirname)); // here we made all files on the server now available to the user
```

* Give users only access to a specific folder (usually "public")
```js
app.use(express.static(path.join(__dirname, 'public'))); // now the client only has access to public files
```

