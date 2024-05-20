Comparison Operators can be used with conditionals to create complex conditional statements (see [[Conditional Statements in JavaScript]])
### What are Comparison Operators
* Comparison Operators --> determine the equality or difference between two values
* Comparison operators --> take two values and return a boolean (true or false) (see [[JS - Boolean Data Type]])

| Operator | Description              |
| -------- | ------------------------ |
| >        | greater than             |
| <        | less than                |
| >=       | greater than or equal to |
| <=       | less than or equal to    |
| ==       | equality                 |
| !=       | inequality               |
| ===      | strict equality          |
| !==      | strict inequality        |

```js
console.log(7 > 6); // true
console.log(7 < 6); // false
console.log(7 >= 6); // true
console.log(7 <= 6); // false
console.log(7 == 6); // false
console.log(7 != 6); // true
console.log(7 === 6); // false
console.log(7 !== 6); // true
```

# Understanding the Equality & Inequality Operators

### Equality Operators ( ==  and === )
* Used to check if two values are equal or identical
* Equality operator ( == ) --> does not check for underlying data type
* Strict Equality operator ( === ) --> does check for underlying data type

```js
console.log("42" == 42); // string "42" and number 42 return true
console.log("42" === 42); // string "42" and number 42 return false
```

### Inequality Operators ( != and !== )
* Used to check if two values are not equal or identical
* Inequality operator ( != ) --> does not check for underlying data type
* Strict inequality operator ( !== ) --> does check for underlying data type
```js
console.log(7 != 6); // true — inequality
console.log("42" !== 42); // true — strict inequality
console.log("23" != 23); // returns false (reads as '23' == 23) excluding strictness
console.log("23" !=== 23) // returns true (reads as '23' === 23) including strictness
```

# String Comparisons
* Algorithm for comparing strings
	1) Compare the first character of both strings
	2) If the first char from the first string is greater (or less) than the first char on the second string (end here)
	3) If both strings are the same, compare second char of each string
	4) Repeat until the end of the string
	5) If both strings end at the same length, then they are equal. 
		* Otherwise, the longer string is greater.
```js
console.log('Glow' > 'Glee'); // true
// G and G are the same! l and l are the same! o is grater than e! 'Glow' is greater
```

# null and undefined Comparions
* Comparing null and undefined to other values
	* Using strict equality or inequality --> null and undefined returns false (because they are of different data type)
	* Using equality or inequality --> null and undefined return true because they are considered identical