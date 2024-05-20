Resources:
* [TripleTen: Conditionals Cheatsheet](https://practicum-content.s3.us-west-1.amazonaws.com/web-developer/cheat-sheet/conditionals-and-loops.pdf)

**![](https://lh6.googleusercontent.com/Dc7jrSbXTblubtO_Fg_I-oD2aLY4YzeWmTecINaLXYCi2dGh3M6chRUckPyjFt4rqIfHvtcqJWq9LCXZK2BAxfJJfumPaVBm3iNbyQV5tfdJjkaI71m1fyp48jHt4wn_mLaz_1lIf-Zm8Q9-VSHSbJI)**

# The 'if' statement
* if statement --> will execute a piece of code only if the specified condition is true
	* The body will be executed (in order) if the statement is true
* Syntax: if statement
	* Condition should be wrapped in parentheses
	* The body of statement should be placed inside the curly braces
	* Semicolons are not needed after curly braces
```js
if (condition) {    
  // the body of the if statement will run if the condition is true
}
```

* Example
```js
let merry = true;  // here the variable merry is set equal to true

if (merry) {       // writing a condition statement
  console.log("😃");  // this line of code will run if the statement is true
}

// Output: 😃          // since the statement is true the output passed
```

# The if...else statement
* If...else --> will execute a different code depending on if the condition is true or false
* Syntax: if...else
```js
if (condition) {    
  // the body of the if statement will run if the condition is true
} else {
  // the body of the else statement to run if the condition is false
}
```

* Example
```js
let merry = false;   // here the variable merry is set equal to false

if (merry) {         // writing a conditional if statement
  console.log("😃");   // will be executed if statement is true
} else {            // writing a conditional else statement
  console.log("😐");   // will be executed if the statement is false
}

// Output: 😐         // executes this because that statement was false
```

# The if...else if...else statement
* else if --> allow for multiple possible conditions
	* go between the original if statement and the final else statement
	* once it finds a condition that is met, it executes the code in the body and exits the statement
* Syntax: else...if 
	* else if condition wrapped in parentheses
```js
if (condition) {    
  // the body of the if statement will run if the condition is true

} else if (condition) {
	// the body of the else if statement will run if condition above is not true

} else {
  // the body of the else statement to run if the conditions are checked and all      are false
}
```

* Example
```js
let stockPrice = 644; // the price of stock

if (stockPrice > 800) {
  console.log("Time to sell");
} else if (stockPrice > 650) {
  console.log("Hold and wait for the price to go up");
} else if (stockPrice > 500) {
  console.log("So cheap, must buy more stocks");
} else {
  console.log("All in");
}

// "So cheap, must buy more stocks"
```

# Summary: Conditional Statements
* The conditions for each branch of a conditional statement are checked sequentially, '
* The first branch with a condition that evaluates to true will be executed. 
	* The remaining branches will not be executed.
```js
if (condition) {
  // only run when condition is true
} else if (otherCondition) {
  // only run when condition is false and otherCondition is true
} else {
  // run when both condition and otherCondition are false
}
```