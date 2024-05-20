What are numbers in JavaScript? (see [[Numbers in JavaScript]])

### Number.isNaN()
* Description
	* Determines if a value is NaN (converts a value to a number if necessary)
* Arguments
	1) value --> the value to be tested
* Syntax
```js
Number.isNaN(value)
```
* Example
```js
// checking if the following values are NaN
console.log(Number.isNaN(20)); // false
console.log(Number.isNaN('20')); // false 
console.log(Number.isNaN(+'20x')); // true
console.log(Number.isNaN(23 / 0)); // false
```

### Number.isFinite()
* Description
	* Determines if a value is a finite number (converts value to a number if necessary)
		* A finite number --> a number that is not `NaN` or `+-Infinity`
* Arguments
	1) value --> the value to be tested	
 * Syntax
```js
Number.isFinite(value)
```
* Example
```js
// Checking if the following values are Numbers
console.log(Number.isFinite(20));  // true
console.log(Number.isFinite('20')); // false
console.log(Number.isNaN(+'20x')); // false
console.log(Number.isNaN(23 / 0)); // false
```

### Number.isInteger()
* Description
	* Determines if a value is an Integer 
* Arguments
	1) value --> the value to be tested	
* Syntax
```js
Number.isInteger(value)
```
* Example
```js
// Checking if the following numbers are integers
Number.isInteger(99999999999999999999999); // true
Number.isInteger(0.1); // false
Number.isInteger(Math.PI); // false
Number.isInteger(-Infinity); // false
```

### Number.parseInt()
* Description
	* Parses a string argument and returns an integer of the specified radix (the base in mathematical numeral systems)
		* The string MUST begin with a number (stops when it encounters a non-integer value)
		* DOES NOT need to be called on the Number object (but strongly encouraged)
* Arguments
	1) string --> the number (in str form). Whitespace is ignored
	2) radix (optional) --> an integer between 2 and 36 that represents the radix (the base in mathematical numeral systems) of the string.
* Syntax
```js
// can be called without adding the Number object
parseInt(string)
parseInt(string, radix) // radix is optional
```
* Example
```js
// parsing a string to get an integer
console.log(Number.parseInt(' 30px')); // returns 30
```
### Number.parseFloat()
* Description
	* Parses a string argument and returns a floating point number.
		* The string MUST begin with a number (stops when it encounters a non-integer value)
		* DOES NOT need to be called on the Number object (but strongly encouraged)
* Arguments
	1) The value to parse (in str form). Whitespace is ignored
* Syntax
```js
// can be called without adding the Number object
Number.parseFloat(string)
```
* Example
```js
// parsing a string to get a floating-point number
console.log(Number.parseInt(' 2.5rem')); // returns 2.5
```


### Number.BigInt() 
* Description
	* Returns primitive values of type BigInt
* Arguments
	* value --> The numeric value of the object being created (can be string, an integer, a boolean, or another BigInt)
* Syntax:
```js
// Creating a BigInt
BigInt(value)
```

### Math.sqrt()
* Description
	* Returns the square root of a number
* Arguments
	1) x --> a number greater than or equal to 0
* Syntax
```js
Math.sqrt(x)
```
* Example
```js
// Getting the squar root of 25
console.log(Math.sqrt(25)) 
```

### Math.max()
* Description
	* Returns the largest of the numbers from the input parameters
		* Return -Infinity if there are no parameters.
* Arguments
	1) value1, value2, … , valueN --> Zero or more numbers (among which the largest value will be selected and returned)
* Syntax
```js
Math.max()
Math.max(value0, value1, /* …, */ valueN) // can include as many numbers 
```
* Example
```js
console.log(Math.max(1, 3, 2)); // returns 3 (largest number)
```

### Math.min()
* Description
	* Returns the smallest of the numbers from the input parameters
		* Return Infinity if there are no parameters.
* Arguments
	1) value1, … , valueN --> Zero or more numbers (among which the lowest value will be selected and returned)
* Syntax
```js
Math.min()
Math.min(value0, value1, /* …, */ valueN) // can include as many numbers 
```
* Example
```js
console.log(Math.min(1, 3, 2)); // returns 1 (smalledt number)
```

### Math.random()
* Description
	* Returns a floating-point (pseudo-random) number that is between 0 and 1 (with approximately uniform distribution over that range)
* Arguments
	* None
* Syntax
```js
Math.random()
```
* Example
```js
Math.random() * 6 // gets a random number between 0 and 6
```

### Math.trunc()
* Description
	* Returns the integer part of a number by removing any fractional digits.
* Arguments
	* x --> a number
* Syntax
```js
Math.trunc(x)
```
* Example
```js
console.log(Math.trunc(Math.random() * 6) + 1 // gets a random number between 1 and 6; cuts off all fractional components of the number
```

### Math.round()
* Description
	* Returns the value of a number rounded to the nearest integer.
	* Performs type coercion
* Arguments
	* x --> a number
* Syntax
```js
Math.round(x)
```
* Example
```js
// rounding different numbers to the nearest integer
console.log(Math.round(23.3)); // returns 23
console.log(Math.round(23.9)); // returns 24
```

### Math.ciel()
* Description
	* Rounds up and returns the smallest integer greater than or equal to a given number. 
	* Performs type coercion
* Arguments
	* x --> a number
* Syntax
```js
Math.ciel(x)
```
* Example
```js
// rounding different numbers to the cieling
console.log(Math.ciel(23.3)); // returns 24 
console.log(Math.ciel(23.9)); // returns 24
```

### Math.floor()
* Description
	* Rounds down and returns the largest integer less than or equal to a given number.
	* Performs type coercion
* Arguments
	* x --> a number
* Syntax
```js
Math.floor(x)
```
* Example
```js
// rounding different numbers to the nearest integer
console.log(Math.floor(23.3)); // returns 23 
console.log(Math.floor(23.9)); // returns 23
```

### Math.floor()
* Description
	* Rounds down and returns the largest integer less than or equal to a given number.
	* Performs type coercion
* Arguments
	* x --> a number
* Syntax
```js
Math.floor(x)
```
* Example
```js
// rounding different numbers to the nearest integer
console.log(Math.floor(23.3)); // returns 23 
console.log(Math.floor(23.9)); // returns 23
```

### Number.toFixed()
* Description
	* Formats a number using fixed-point notation (returns a string, NOT a number)
* Arguments
	1) digits (optional) --> the number of digits to appear after the decimal point (should be between 0 and 100, inclusive); if omitted, defaults to 0
* Syntax
```js
value.toFixed()
value.toFixed(digits)
```
* Example
```js
// rounding different numbers using toFixed()
console.log((2.7).toFixed(0)); // rounding a number to 0 decimal places (3)
console.log((2.7).toFixed(3)); // rounding a number to 3 decimal places (2.700)
console.log((2.345).toFixed(2)); // rounding a number to 2 decimal places (2.35)
```
