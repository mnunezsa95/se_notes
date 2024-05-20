Switch statements are a type of conditional statement in JavaScript (see [[Conditional Statements in JavaScript]])
### Switch-Case Statements
* Used when there can ONLY be on right answer
* Syntax
	* `switch` --> declares a switch-case statement
	* `case` --> used to identify a case of the condition
	* `break` --> needed at end of each case to break out of the code if case is met
		* If omitted --> returns the last case whether a match or not
	* `default` --> used to handle a situation where the condition does not match any case
```js
switch (condition) {
    case First_possible_value:
        // Code to be executed 
        break; 
    case Second_possible_value:
        // Code to be executed
        break;
    ...
    case nth_possible_value:
        // Code to be executed
        break;
    default:
	    // code to be executed if cases don't match
} 
```

* Example
```js
const yourNumber = "D135";
let windowNumber;

switch (yourNumber) {
    case "D133":
        windowNumber = 1;
        break;
    case "D134":
        windowNumber = 2;
        break;
    case "D135":
        windowNumber = 3;
        break;
    case "D136":
        windowNumber = 4;
        break;
    case "D137":
        windowNumber = 5;
}
```

```js
// evaluating multiple cases

let catName;
const cartoon = "Shrek";
switch (cartoon) { 
    case "Shrek":
    case "Shrek 2":
    case "Shrek the Third":
        catName = "Puss in Boots"; // will be executed if cartoon matches any of 
        break;                                        // the cases above
    case "Garfield and Friends":
        catName = "Garfield";
}

console.log(catName); // "Puss in Boots" 
```