### What is a while loop
* while loop (see [[JS - Loops]])
	* continues to execute the code in the body AS LONG AS the condition remains true
	* once condition is false, the loop is exited

### An infinite loop
* Should be written in a way in which the condition eventually becomes false
	* Otherwise loop runs forever, eventually crashes 

### Syntax
```js
while (condition) {
	// body
}
```

### Examples
* Example 1:
```js
let number = 10;    // the variable number has a value of 10

while (number <= 20) {      // while “number" is less than or equal to 20
  console.log(number);      // log “number” into the console   
  number += 2;           // add 2 every time it iterates
} 
```

* Example 2:
```js
let counter = 3;

while (counter > 0) {      // while counter is greater than 0
  console.log(counter);   // log counter to console and
  counter--;             // subtract 1 from counter
}

console.log("Blast off!");
```

* Example 3
```js
let moneyLeft = 15;
let candyPrice = 2;
let candiesBought = 0;

while (moneyLeft >= candyPrice) {
	console.log(`Jenny bought ${++candiesBought} candies`);
	moneyLeft -= candyPrice;
}

console.log(moneyLeft);
```