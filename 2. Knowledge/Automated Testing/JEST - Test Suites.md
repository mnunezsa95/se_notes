What is automated testing? (see [[Automated Testing - What is it?]])

#### What are Test Suites?
* Test Suite --> the grouping of tests for units related to one big task (see [[JEST - Testing Units]])
* Helps organize tests properly 
* Makes it easier for changing, modifying and reading tests

#### Creating a Test Suite
* The `describe()` function is used to define a test suite (see [[JEST - Methods]])
* Example: Using the `describe()` method to define a test suite
```js
describe('Request handler tests', () => {
	test('should validate the data', () => {/* test code */});
	test('should calculate the password hash', () => {/* test code */});
	test('should write the data to the database', () => {/* test code */});
}); 
```

#### Reading a Test Suite Result
* Output
```bash
  PASS  ./api.test.js
  User registration endpoint # the new line
  ✓ should validate the data (3ms)
  ✓ should calculate the password hash (5ms)
  ✓ should write the data to the database (7ms)

Test Suites: 1 passed, 1 total
Tests:       3 passed, 3 total
Snapshots:   0 total
Time:        1.747s
Ran all test suites. 
```