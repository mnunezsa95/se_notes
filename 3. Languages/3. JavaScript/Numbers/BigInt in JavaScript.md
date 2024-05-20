ES2020
* Introduced BigInt Data Type
### How are numbers represented internally?
* Numbers --> stored internally in 64-bits (see [[Numbers in JavaScript]])
	* Only 53 are used to store digits
	* The remaining bits are used for storing decimals

### Why is BigInt needed?
* The “number” type can store large integers (up to 1.7976931348623157 * 10308), but outside of the safe integer range ±(253-1) there’ll be a precision error, because not all digits fit into the fixed 64-bit storage. 

### Max safe integer in JavaScript
* JavaScript has a limit to how big a number can be
	* This is the maximum number that JavaScript can **safely** store
* The Max_SAFE_INTEGER property stores the largest possible number (see [[Number & Math Properties]])
	* Operations beyond this number might not work properly
```js
// largest number in JavaScript
console.log(2 ** 53 - 1); // 9007199254740991

console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
```

---
## What is BigInt 
* BigInt -- a data type used to store extremely large numbers (see [[JS - Data Types in JavaScript]])
	* Helpful when getting data from API

### How to create a BigInt
1) Add `'n'` to the end of a very large number
```js
// using the 'n' to create a large number
console.log(384638921091293938297329381982183n);
```

2) Use the `BigInt()` function (see [[Number & Math Methods]])
```js
// using BigInt() function to create a large number
console.log(BigInt(384638921091293938297329381982183));
```

### Operations with BigInt
* All operations work with BigInt
* Limitations
	* Math object functions do not work with BigInts
	* Cannot combine BigInt with Normal Numbers
```js
// trying to use Math object function on BigInt
Math.sqrt(16n); // Error: Cannot use Math.sqrt on BigInt
```

```js
const huge = 202982929473829482938294n;
const num = 23;
console.log(huge + bigInt(num)); // Error: cannot combined BigInt & normal #s

//Exceptions
console.log(20n > 15);  // true
console.log(20n === 15); // false
console.log(typeof 20n); // bigint
console.log(20n == '20'); // true

console.log(huge + " is REALLY big!!!"); // number is converted to a string
```