Resources
* [TripleTen: JavaScript Basics Cheatsheet](https://practicum-content.s3.us-west-1.amazonaws.com/web-developer/cheat-sheet/js-basics.pdf)

### Data Types
* null and undefined are data types in JavaScript (see [[JS - Data Types in JavaScript]])
* NaN is of the "Number" data type (even though it represents Not a Number)

# What are null, undefined and NaN?
- **null**, **undefined** and **NaN** signify absence of a value
	- **undefined** --> When a value is not assigned
	- **null** --> Intentional absence of a value
	- **NaN** --> Error with number operation
### null
* A primitive data type
* Can be assigned to a variable (will represent a non-existent value)
* null = absence or non-existence of a value
* null  is of the 'object' type
```js
let meaningofLife = null;

console.log(meaningofLife); // null
typeof meaningOfLife; // "object" (surprisingly!)
```

### undefined
* A primitive data type
* undefined = 'value not assigned'
* undefined is of the 'undefined' type
* Represents with variables that have not been assigned values
```js
/* let's declare a variable called meaningOfLife note - it hasn't been assigned a value yet */ 

let meaningOfLife;

console.log(meaningOfLife); // "undefined" 
typeof meaningOfLife; // "undefined" 
```

### NaN (not a number)
* NaN = an error in number operations has occurred
* NaN is of the 'Number' type
```js
console.log("string" * 2); // NaN
// In this example, there is an attempt to multiply a string by 2. The operation fails and outputs NaN as the result.
```

### Summary: null, undefined, NaN

| Description                                                                   | Value     | Type      |
| ----------------------------------------------------------------------------- | --------- | --------- |
| undefined = is the value of a variable that has not been assigned a value yet | undefined | undefined |
| null = represents the intentional absence or non-existence of a value         | null      | object    |
| NaN = used to represent an uncomputable numerical calculation                 | NaN       | number    |
