What are numbers in JavaScript? (see [[Numbers in JavaScript]])

### Number.MAX_SAFE_INTEGER
* Description
	* Represents the maximum safe integer in JavaScript (2^53 – 1). (see [[BigInt in JavaScript]])
* Syntax
```js
Number.MAX_SAFE_INTEGER; // 9007199254740991
```
* Example
```js
// Numbers will not represent properly after the MAX_SAFE_INTEGER
console.log(Number.MAX_SAFE_INTEGER);
// Expected output: 9007199254740991

console.log(x);
// Expected output: 9007199254740992
console.log(x === y);
// Expected output: true
```
### Math.PI
* Description
	* Represents the ratio of the circumference of a circle to its diameter, approximately 3.14159.
* Syntax
```js
Math.PI // value is 3.14159
```
* Example
```js
console.log(Math.PI * Number.parseFloat('10px') ** 2); // logs the value of PI * 10 to the power of 2 (value is 314.159)
```

