### What is a for loop
* for loop (see [[JS - Loops]])
	* useful when something needs to be done a specific number of times
	* allow for more control over execution and number of iterations compared to while loops (see [[JS - while loop]])
### Syntax
* initialization --> where the loop variable (counter) is set
	* has an initial value used for 1st iteration
* condition --> statement checked 
	* loop runs as long as the condition is true
* increment --> describes how the counter variable will change
```js
for (initialization; condition; increment) {
	// body
}
```

### Examples
* Example 1:
```js
for (let i = 0; i <= 100; i++) { // loop will run as long as i is less than 100
  console.log(i);
} 
```

* Example 2:
```js
for (let i = 1; i <= 100; i++) {
	if (i % 2 === 0) {
	    console.log(`${ i } is even`);
	} else {
	    console.log(`${ i } is odd`);
    }
}
```

* Example 3:
```js
// logging the instances where “o” occurs, the indices 
for (let i = 0; i < greeting.length; i++) {
	if (greeting[i] === "o") {
    console.log(i);
    }
}
```

* Example 4:
```js
let example = "exampleString";
let kebab = "";

for (let i = 0; i < example.length; i++) {
	if (example[i] === example[i].toUpperCase()) {
		kebab += `-${example[i].toLowerCase()}`;
	} else {
		kebab += example[i];
	}
} 
```