#### A Testing Framework
* Set of libraries for testing code 
* Helpful to test code after redesigning/updating features or adding new features

### Where to Write Tests
* Tests should be written in a separate file (named after file containing the main code it will test, with `.test.` at the end of the file name)
* Example
	* `function.js` --> main code
	* `function.test.js` --> test code
```js
// function.js
const sayHello = (firstName, lastName) => {
	return `Hello, ${firstName} ${lastName}!`;
};
module.exports = sayHello; 
```

### How to Write Tests
* Can use a variety of methods to write test functions (see [[JEST - Methods]])

### What Should Be Tested?
* Ideally, ALL Functions

### Reading Test Results
* Example Output: PASS Result
	* "PASS" appears next to the test files that have passed the tests
```bash
# result from the console
  PASS  ./function.test.js
  ✓ Creates a greeting (3ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.747s
Ran all test suites. 
```

* Example Output: Failed Result
```bash
> jest

 FAIL  ./function.test.js # Indicates the file with the failed test
  ✕ Creates a greeting (12ms)

  ● Creates a greeting

    expect(received).toBe(expected) // Object.is equality
        
    Expected: "Hello, Ms. Lera Jackson"
    Received: "Hello, Mr. Lera Jackson"
      3 | 
      4 | test('Creates a greeting', () => {
    > 5 |   expect(sayHello("Lera", "Jackson")).toBe("Hello, Ms. Lera Jackson");              # indicates the specific location of the error
	    |                                       ^
      6 | });
      7 | 
      at Object.toBe (function.test.js:5:39)

Test Suites: 1 failed, 1 total 
Tests:       1 failed, 1 total # reports failed tests out of total
Snapshots:   0 total
Time:        1.963s
Ran all test suites.
```