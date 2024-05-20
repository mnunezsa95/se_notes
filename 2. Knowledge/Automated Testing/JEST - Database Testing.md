* What is automated testing? (see [[Automated Testing - What is it?]])

#### Limitations to DataBase Testing
* Cannot use real data bc it can damage user data
* Add random meaningless data to the database to perform tests
	* Random data should be deleted after use
#### How Database Testing works
* 1) Add test data --> 2) test --> delete test data

#### Methods for Database Testing
* There are several methods for database testing (see [[JEST - Methods]])

#### Testing Databases
* Example
```js
beforeAll(() => {
	// connecting to the database
}); 

afterAll(() => {
	// disconnecting from the database
});

describe('Database tests', () => {
	beforeEach(() => {
		// before each test, add the needed test data to the database
	});
	
	afterEach(() => {
		// after each test, remove the data from the database
	});
	
	test('should test...', () => {
		/* code to check if the tests function properly */
	});
}); 
```

* Example: Calling the `beforeAll()` and `afterAll()` methods inside the `describe()` block.  Then, the `beforeAll()` and `afterAll()` callbacks will be called at the beginning and end of the test suite, respectively.
```js
beforeAll(() => {
	// connecting to the database
}); 

afterAll(() => {
	// disconnecting from the database
});

describe('Database tests', () => {
	beforeAll(() => { // will run before all tests inside this describe() block          code that adds the necessary test data before the tests run
	});
	
	afterAll(() => { // will run after all tests inside this describe() block            code that removes the test data from the database after all the the              tests have run
	});
	
	test('db...', () => {/*  code to check db tests */});
	test('performs other tests...', () => {/* code to check other tests */});
});

describe('Endpoint tests', () => {
	// beforeAll() and afterAll() from the previous describe() block won't be          run here, but the global beforeAll() and afterAll() will be run
	
	test('the endpoints', () => {/* code to check tests */});
}) 
```