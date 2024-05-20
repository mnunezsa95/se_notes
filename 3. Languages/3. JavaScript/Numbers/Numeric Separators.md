* In JavaScript, large numeric literals are difficult for the human eye to parse quickly, especially when there are lots of repeating digits: `1000000000000`

### What are Numeric Separators
* Numeric separators are underscores `( _ )` that can be used in large numbers to make it easier to read them
	* The JS Engine ignores the underscores so they can be placed anywhere
* Example
```js
// Without using numeric separators
const diameter = 287460000000

// Using Numeric Separators in JavaScript
const diameter = 287_460_000_000 // the engine ignores the underscores
```

### Limitations for Numeric Separators
1) Numeric Separators CANNOT be placed:
	* Before decimals ( . )
	* After decimals ( . )
	* At the start of a number
	* At the end of a number
2) Two Numeric Separators cannot be placed back in a row

### Converting strings that have underscores to a number
* Strings that have underscores cannot be parsed correctly into a number by JavaScript engine
* Example
```js
// converting a string with an underscore into a number
console.log(Number('230_000')); // will produce an error
console.log(parseInt('230_000')); // will produce an error
```