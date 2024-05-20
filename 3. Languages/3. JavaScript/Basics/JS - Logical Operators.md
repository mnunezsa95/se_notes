# Using Logical Operators
* Logical Operators can be used with conditionals to create complex conditional statements (see [[Conditional Statements in JavaScript]])
 
# The 3 Logical Operators (and, or, not)
### The logical NOT ( ! ) operator
* ! --> turns true into false; turns false into true
```js
let isSunny = true;
console.log(!isSunny); // false b/c ! gives the opposite 

let isRaining = false;
console.log(!isRaining); // true b/c ! gives the opposite
```

### The logical AND (&&) operator
* && --> will return **true** ONLY when all operands are true
```js
let isSunny = true;
let isRaining = false;

console.log(isSunny && isRaining); // false b/c only one of the two conditions were true
```

### The logical OR ( | | ) operator
* || --> will return **true** when at least one of the operands is **true**
```js
let isSunny = true;
let isRaining = false;

console.log(isSunny || isRaining); // true b/c at least one of the two conditions are true
```

## Examples: Using Logical Operators with Conditionals
* Example 1
```js
let temperature = 97.9;

if (temperature > 97.6 && temperature <= 99.5) {
    console.log("Everything looks normal.");
} else {
    console.log("Fever alert! Go see a doctor as soon as possible!");
}
```

* Example 2
```js
let year = 2019;

if ((year % 400 === 0) || ((year % 4 === 0) && !(year % 100 === 0))) {
    console.log(year + ' is a leap year.');
} else {
    console.log(year + ' is a non-leap year.');
}
```

* Example 3
```js
const haveXBox = true;
const compatibleWithXBox = false;
const havePlayStation = true;
const compatibleWithPlayStation = true;

if ((haveXBox && !compatibleWithXBox) || ((havePlayStation && compatibleWithPlayStation))) {
	console.log("I should buy it");
} else {
	console.log("I should wait for the port :c");
}
```