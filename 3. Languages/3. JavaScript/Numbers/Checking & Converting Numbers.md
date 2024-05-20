### How are numbers interpreted in JavaScript
(see [[Numbers in JavaScript]])

### Checking if a Number is a Number
* The `Number.isNaN()` function can be used to determine if a value is NaN (see [[Number & Math Methods]])
```js
// checking if the following values are NaN
console.log(Number.isNaN(20)); // false
console.log(Number.isNaN('20')); // false 
console.log(Number.isNaN(+'20x')); // true
console.log(Number.isNaN(23 / 0)); // false
```

* The `Number.isInteger()` function can be used to determine if a value is an Integer (see [[Number & Math Methods]])
```js
// checking if the following values are integers
console.log(Number.isFinite(23));  // true
console.log(Number.isFinite(23.0));  // true
console.log(Number.isNaN(23 / 0)); // false
```

* The `Number.isFinite()` function can be used to determine if a value is a Number (see [[Number & Math Methods]])
```js
// Checking if the following values are Numbers
console.log(Number.isFinite(20));  // true
console.log(Number.isFinite('20')); // false
console.log(Number.isNaN(+'20x')); // false
console.log(Number.isNaN(23 / 0)); // false
```

### Converting a String to a Number
* Three ways:
	1) Using the `Number()` function (technically an object)
	2) Using type coercion 
	3) Parsing via the `parseInt()` method (see [[Number & Math Methods]])

* Example: 
```js
console.log(Number('23')); // coverts the string to a number
console.log(+'23'); // converting string to number using type coercion
console.log(Number.parseInt('30px')); // parsing the string to create a number
```