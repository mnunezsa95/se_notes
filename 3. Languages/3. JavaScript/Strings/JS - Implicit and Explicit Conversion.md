# Implicit Conversion
* Implicit Conversion --> implicitly (accidentally) changing the data type when using the + sign (see [[JS - Working with Strings]])
* The addition operator ( + ) has implicit conversion effect
	* Adding values to a string --> all values in the expressions will be implicitly converted into strings
```js
console.log(100 + "500"); // "100500"
console.log("Today you've done " + 30 + 10 + " push-ups"); // "Today you've done 3010 push-ups" 

console.log("10" * 2); // 20 because only the + operator will implicitly convert
console.log("15" - 5); // 10 because only the + operator will implicitly convert
console.log("10" * "2"); // 20 because only the + operator will implicitly convert

alert(2 + 2 + '1' ); // will result in "41" and not "221" bc the two numbers are added first, then the '1' is tacked on
```

# Explicit Conversion
* Explicit Conversion --> Explicitly changing the data type from one to another String(), Number(), Boolean()
- The `String( )` method converts any value passed through it to a string
- The `Number( ) `method converts an argument to a number type (see [[Number & Math Methods]])
	- If null --> 0
- The `Boolean( )` method converts an argument to the Boolean type
	- If Number > 0 --> true
	- if Number = 0 --> false
	- Empty strings --> false
	- Non-empty --> true
	- NaN, null, and undefined --> false
```js
String(2); // "2"
String(undefined); // "undefined"
String(null); // "null"
String(true); // "true" 
Number("2"); // 2
Number(null); // 0 
Boolean(2) // true
Boolean(0) // false
Boolean("") // false
Boolean("any string that isn't empty"); // true 
```