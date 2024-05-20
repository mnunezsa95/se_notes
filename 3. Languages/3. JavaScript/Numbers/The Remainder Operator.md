### What is the Remainder Operator (%)? 
* Returns the remainder (what is left over) from a division. It always takes the sign of the dividend

* Example
```js
// Determining the remainder of the following:
console.log(5 % 2); // 5 = 2 + 2 + 1 --> the remainder is 1
console.log(8 % 3); // 8 = 2* 3 + 2 --> the remainder is 2 
```

### Use cases for the Remainder (%)
1) Checking whether a number is even or odd.
	* Can check whether the remainder is equal to 0 or not
```js
// function for checking if a number is even or odd
const isEven = (n) => {
	if (n % 2 === 0) {
		return true
	} else {
		return false
}

}
// checking numbers to determine if they are even or odd
console.log(isEven(8)); // result is true
console.log(isEven(23)); // result is false
console.log(isEven(514)); // result is true
```

