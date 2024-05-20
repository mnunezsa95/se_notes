Resources
* [JEST Modifier Functions](https://jestjs.io/docs/expect#tobeundefined)

---
#### test() / it()
* Used to start creating a test in JEST (see [[JEST - Installing JEST]])
* Arguments
	1) name --> the name of the test
	2) fn --> the function the test should run
* Example
```js
test('Creates a greeting', () => {
	expect(sayHello('Lera', 'Jackson')).toBe('Hello, Lera Jackson!');
}); 
```

#### expect()
* Returns an object with methods for testing (matcher functions)
* Arguments
	1) expectedValue 
* Example
```js
expect(1).toBe(1); // true
expect(1).toBe(2); // false
expect(1 + 2).toBe(3); // true 
```

#### toBe() 
* A matcher function that compares its own argument to the one passed to the `expect()` function
* Used to compare primitive values and object references
* Arguments
	* expectedValue --> the value that it should expect
* Example
```js
// Example using primitive values
expect(1).toBe(1); // true
expect(1).toBe(2); // false
expect(1 + 2).toBe(3); // true 
expect('Expectation').toBe('Expectation');  // true
expect('Expectation').toBe('Reality'); // false

// Object references
const a = {}; 
const b = a;
expect(a).toBe(b); // true

const a = {};
const b = {};
expect(a).toBe(b); // false
```

#### toEqual() 
* Used to compare objects and arrays (useful for checking if the two objects are the same)
	* For objects: checks that the resulting object contains ALL the same keys and values
		* Any properties that are NOT specified in the expected object are ignored
	* For arrays: checks that ALL the items in the real output are exactly the same as in the expected output
		* Missing elements & `undefined` are considered equal
* Example
```js
// tests will pass
expect({ a: undefined, b: 10, c: 'text' }).toEqual({ b: 10, c: 'text' });
expect([1, 2, 3]).toEqual([1, 2, 3]); 
expect([[undefined, 1]]).toEqual([[, 1]]) // the first element is missing in the second array

// tests won't pass
expect({ a: undefined, b: 10, c: 'text' }).toEqual({ a: 12, b: 10, c: 'text' });
expect([1, 2, 3, undefined]).toEqual([1, 2, 3]); // arrays do not match in length
```

#### toStrictEqual() 
* Used to compare objects and arrays MORE STRICTLY
	* Output object or array MUST match the the expected one EXACTLY (have all the same properties or items)
* Example
```js
// tests will pass
expect({ b: 10, c: 'text' }).toStrictEqual({ b: 10, c: 'text' });
expect([3, 4, undefined]).toStrictEqual([3, 4, undefined]);

// tests won't pass
expect({ a: undefined, b: 10, c: 'text' }).toStrictEqual({ b: 10, c: 'text' });
expect([[undefined,  1]]).toStrictEqual([[, 1]])
```

#### toBeTruthy() 
* Checks that the output is `true`
* Example
```js
// tests will pass
expect(1).toBeTruthy();
expect(true).toBeTruthy();

// tests won't pass
expect(null).toBeTruthy();
expect(0).toBeTruthy();
```

#### toBeFalsy() 
* Checks that the output is `false`
* Example
```js
// tests will pass
expect(undefined).toBeFalsy(); 
expect(1/'string').toBeFalsy();

// tests won't pass
expect(true).toBeFalsy();
```

#### toBeUndefined() 
* Checks if the output is `undefined`.
* Example
```js

const x; // undefined
expect(x).toBeUndefined(); // true
expect(undefined).toBeUndefined(); // true 
```

#### toBeDefined() 
* Checks that the result is not `undefined`. 
	* Passes even with the value of `null`
* Example
```js
expect(1).toBeDefined(); // true
expect(null).toBeDefined(); // true
expect('string').toBeDefined(); // true

const x;
expect(x).toBeDefined(); // false
expect(undefined).toBeDefined(); // false
```

#### toBeNull()
* Checks that the output is `null`
* Example
```js
const x = null;

expect(null).toBeNull(); // true
expect(x).toBeNull();  // true

expect(0).toBeNull(); // false
expect(undefined).toBeNull(); // false
expect('string').toBeNull(); // false
```

#### toMatch()
* Checks whether a string matches a regular expression
* Example
```js
expect('1').toMatch(/^\d+$/); // true
expect('1337').toMatch(/^\d+$/); // true
expect('4242').toMatch(/^\d+$/); // true

expect('21as1').toMatch(/^\d+$/); // false
expect('string').toMatch(/^\d+$/); // false
```

#### toContain()
* Checks whether the resulting array or string contains the value specified 
* Example
```js
expect('Oh, hi Mark!').toContain('Mark'); // true
expect(['Mary', 'Louisa', 'Stuart']).toContain('Stuart'); // true

expect('Oh, hi Mark!').toContain('Lisa'); // false
expect(['Mary', 'Louisa', 'Stuart']).toContain('Louise'); // false
```

#### toBeGreaterThan()
* Compares the output with the number passed in the method
	* Checks if it is greater than
* Example
```js
expect(2).toBeGreaterThan(1); // True: 2 is greater than 1
expect(2).toBeGreaterThan(2); // False: 2 is not greater than 2
```

#### toBeGreaterThanOrEqual()
* Compares the output with the number passed in the method
	* Checks if it is greater than or equal to
* Example
```js
expect(2).toBeGreaterThanOrEqual(2); // True: 2 is equal to 2
expect(2).toBeGreaterThanOrEqual(3); //False: 2 is not greater than or equal to 3

```

#### toBeLessThan()
* Compares the output with the number passed in the method
	* Checks if it is less than
* Example
```js
expect(2).toBeLessThan(3); // True: 2 is less than 3
expect(2).toBeLessThan(2); // False: 2 is not less than 2
```

#### toBeLessThanOrEqual()
* Compares the output with the number passed in the method
	* Checks if it is less than or equal to
* Example
```js
expect(2).toBeLessThanOrEqual(2); // True: 2 is equal to 2
expect(2).toBeLessThanOrEqual(1); // False: 2 is not less than or equal to 1
```

#### describe()
* Defines a test suite
* Arguments
	1) the suite name (the description of what is being tested)
	2) callback function with tests
* Example
```js
describe('Request handler tests', () => {
	test('should validate the data', () => {/* test code */});
	test('should calculate the password hash', () => {/* test code */});
	test('should write the data to the database', () => {/* test code */});
}); 
```

---
# Database Testing
* The `beforeAll()` and `afterAll()` can be used to add and delete sample data to the database before running tests
* The `beforeEach()` and `afterEach()` can be used to add and delete data before each test

#### beforeAll()
* Will run before running all tests in a file
* Example
```js

```

#### afterAll()
* Will run after running all tests in a file
* Example
```js

```

#### beforeEach()
* Will run before each test
	* Takes longer and is more diligent (runs twice for every test) than `beforeAll()`
* Example
```js

```

#### afterEach()
* Will run after each test
	* Takes longer and is more diligent (runs twice for every test) than `afterAll()`
* Example
```js

```