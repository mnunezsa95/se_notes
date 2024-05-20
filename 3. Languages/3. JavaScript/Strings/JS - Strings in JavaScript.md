Resources
* [TripleTen: JavaScript Basics Cheatsheet](https://practicum-content.s3.us-west-1.amazonaws.com/web-developer/cheat-sheet/js-basics.pdf)

Other Notes
* [[JS - String Properties]]
* [[JS - String Methods]]

---
### What are Strings in JavaScript?
* Strings --> a data type that contains letters, characters and other symbols that belong to **unicode standard** (see [[Unicode Standard]])

### Creating Strings
* Strings --> can be created using 3 strategies
	1) single quotes `( '' )`
	2) double quotes `( " " )`
	3) backticks `(``)`
* Example
```js
console.log("word");
console.log('Not just a word, but a whole sentence.');
console.log(`1984`); // even a number can be made to be a string
```

### Rules for Strings
* Must start and end with the same type of quotation marks
* If one type of string is already in use, then use a different type of quotations to surround the string
* Example
```js
console.log("everything is coming up roses"); // will work accurately
console.log('this will not end well"); '// will result in an error 
console.log("The Republic of Côte d'Ivoire"); // using " " for the string in order to be able to use ' ' for the 
console.log('Never Say "Never" Again');
```

