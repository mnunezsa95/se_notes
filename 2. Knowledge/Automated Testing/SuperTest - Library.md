* What is automated testing? (see [[Automated Testing - What is it?]])
* Resources
	* [SuperTest Library Documentation](https://github.com/ladjs/supertest#readme)

#### What is SuperTest Library?
* Provides convenient tools for testing servers

#### How does the SuperTest Library work? 
* Starts testing --> connects to the server --> runs tests --> disconnects from the server --> finishes tests
	* Takes charge of connecting to and from the server

#### Installing SuperTest
1) Install SuperTest as a dev dependency
```bash
npm install --save-dev supertest
```

#### Connecting the SuperTest Library to a project
1) Create an `endpoint.test.js` file in the tests
2) Connect the library to this file
```js
// endpoint.test.js
const supertest = require('supertest');
const app = require('./app.js')
```
3) The `supertest` variable contains a function; pass it to your app as follows:
```js
// endpoint.test.js
const request = supertest(app);
```

#### Working with SuperTest
* The SuperTest library has a variety of methods for testing HTTP requests (see [[SuperTest - Methods]], [[SuperTest - Testing HTTP Requests]])