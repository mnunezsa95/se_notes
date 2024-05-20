See: [[Node - Introduction to Node.js?]], [[Express - Introduction to Express.js]]

---
# Requirements for Express.js
* Requirements
	* Project MUST have a **package.json** file
	* If **package.json** does not exist, install one using the following command
		* -y flag --> answers 'yes' to all question when setting up package.json
```bash
npm init -y
```

# Installing Express.js
1) Run the following command
```bash
npm install express
```

2) Set up 'Hot Reloading'
	* Install hot reloading as a devDependency only (only needed for development) using one of the following command
```bash
npm nodemon --save-dev
```

```bash
npm install nodemon -D
```

3) Configure **nodemon** to run when program starts
	* If there is no "start" script (read [NPM Documentation: npm-start](https://docs.npmjs.com/cli/v8/commands/npm-start#description]))
```json
{
	...
	'scripts': {
		"start": nodemon entryPointFile.js
	}
}
```

4) Set **entry point** (in package.json) to file with primary application logic in the package.json file (see [[package.json and package-lock.json]])
	* In the 'main' property of the package.json file

6) Import the Express Module and connect it to the app by using the express() method
	* Example
```js
const express = require('express') // import express
const app = express(); // connect express to the app
```

7) Set the **environmental variable** 
	* Environmental variables are set using the **process.env** (see [[Node.js - Creating a Server]])
	* Example
```js
const express = require('express') // import express
const { Port = 3000 } = process.env;
const app = express();

app.listen(PORT, () => {
	// code below used to show which port the application is using
	console.log(`App is listening at port ${port}`)
});
```
