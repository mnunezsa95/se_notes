See [[JS - Introduction to JavaScript]], [[JS - What are Functions?]]

---
# Function Declarations
* Declared by the 
	* **function** keyword --> states a function
	* function name --> name of function
	* parentheses --> used to pass in parameters (see [[JS - Function Parameters & Arguments]])
	* curly braces  --> contains the function body
* Rules for naming function declarations
	* Use camelCase
	* Name should explain what function does
```js
function fnName(param1, param2) {
	// statement1
	// statement2
	// statementN
}
```

**![](https://lh5.googleusercontent.com/Nxx9gfWUVV6UQ8FmV0AQa047ZWZSzbU7GzuBmjrxiPRnQX87cMy1mXSkLTOqA2BMAaYaLzWLX4smmg-7Zp1LYx_Cqh7pqTydIrW7_E3AYo4przwnkERwZGVNy3le0lhDSWGiQcEDgiKKpb5MxExzrjs)**


### Examples
* Example 1
	* Uses the return statement (see [[JS - the return keyword]])
```js
function adder(x, y) {
   return x + y
}

let dinnerCost = adder(10, 11)
console.log(`Our dinner cost ` + dinnerCost + ` dollars.`);
```

* Example 2
```js
function isLeapYear(year) {
	if ((year % 400 === 0) || ((year % 4 === 0) && !(year % 100 === 0))) {
		console.log(year + ' is a leap year.');
	} else {
	    console.log(year + ' is a non-leap year.');
	}
}
```
