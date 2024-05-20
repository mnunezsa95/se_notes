What is automated testing? (see [[Automated Testing - What is it?]])

#### Testing HTTP Requests
* Can be done by using the SuperTest Library (see [[SuperTest - Library]])

#### Preparing the project for testing
* Ensure that the `process.env.NODE_ENV` is set to `'test'` by JEST runner. 
* Write code to ONLY start listening to port 3001 when not running in test mode
```js
if (process.env.NODE_ENV !== 'test') {
	app.listen(PORT, () => { console.log(`App listening on port ${PORT}`) });
}
```

#### Connecting SuperTest to the project
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
* There are a variety of methods for testing HTTP requests (see [[SuperTest - Methods]])
* Example
```js
describe('Endpoints respond to requests', () => {
	it('Returns data and status 200 on request to "/"', () => {
		return request.get('/').then((response) => {
	        expect(response.status).toBe(200);
            expect(response.text).toBe('Hello, world!');
        });
	});
}); 
```