Numbers are a type of data in JavaScript (see [[JS - Data Types in JavaScript]])
# How are numbers presented in JavaScript
* In JavaScript
	* All numbers are presented as floating-point numbers
	* Numbers are represented internally in a 64-base 2 format (stored in a binary format)
		* Base 10 --> numbers 0 - 9
		* Binary Base 2 --> numbers 0 - 1
* Numbers in JavaScript include:
	* Integers 
	* Floating-point numbers
	* Infinity 
	* -Infinity
	* NaN (Not a Number) --> represents computational error (result of incorrect or undefined mathematical operation)
* Example
```js
// Determing how numbers are presented as floating-point numbers
console.log(23 === 23.0) // true because the two numbers are identical
```

```js
// Binary Base 2 will result in weird calculations

console.log(0.1 + 0.2) // 0.30000000000000004
console.log(0.1 + 0.2 === 0.3) // false due to the way JavaScript deals with numbers
```

# Operations with Numbers in JavaScript

* Operations with Numbers & Mathematics (see [[Number & Math Methods]], [[Numbers & Arithmetic Operators]])
* There are static Math properties built-into JavaScript (see [[Number & Math Properties]])

# Representing Large Numbers
* By Default, large numbers are not represented by commas, making it hard for the human eye to parse these numbers
* ES2021 introduced Numeric Separators for support with visualizing large numbers (see [[Numeric Separators]])