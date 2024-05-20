Resources:
* Youtube Video: [JEST Crash-Course](https://www.youtube.com/watch?v=ajiAl5UNzBU)
* [JEST Modifier Functions](https://jestjs.io/docs/expect#tobeundefined)

#### What is a unit?
* The smallest part of code that can be tested in isolation (see [[Automated Testing - What is it?]])
* Units can be grouped together to form a Test Suite (see [[JEST - Test Suites]])

#### What functions should be tested?
* Ideally, ALL function should be tested
* Avoid ONLY writing code for top-level function
	* Harder to identify what went wrong when an error occurs
* Example:
	* Each function is a UNIT --> Can write a test for each one
```js
// check that the password contains a number
function checkNumber(pass) {
	if (typeof pass === 'string') {
	let regex = /\d/;
		return regex.test(pass); // the regex.test() method will return true if 
    }                           // the passed string matches the regexp
}

// check that the password contains a special character
function checkSymbol(pass) {
	if (typeof pass === 'string') {
		let regex = /[!@#$%^&*(),.?":{}|<>_]/;
	    return regex.test(pass);
	}
}

// run both checks
function checkPass(pass) {
	return checkNumber(pass) && checkSymbol(pass);
} 
```

```js
test('Check that the password contains a number', () => {
	expect(checkNumber('some_not_so_strong_pass')).toBe(false);
    expect(checkNumber('stronger_pass_123')).toBe(true);
});

test('Check that the password contains a special character', () => {
    expect(checkSymbol('somePass')).toBe(false);
    expect(checkSymbol('another_pass')).toBe(true);
});

test('Check password', () => {
    expect(checkPass('somePas$')).toBe(false);
	expect(checkPass('another_pass_123')).toBe(true);
}); 
```