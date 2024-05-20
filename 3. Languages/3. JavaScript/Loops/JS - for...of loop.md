### What is a for...of loop?
* Loops through the values of an iterable object (such as an array or map) and do something (see[[JS - Arrays in JavaScript]])
* Does not require additional variables for storing an index

### Syntax
```js
for (let item of iterableName) {
	// body
}
```

### Example
* Example 1
```js
let students = ["Yasmin", "Elise", "Terry"]; // iterable
// add a for loop to print a personalized message for each student

for (let student of students) {
	console.log("Welcome to Practicum, " + student + "!");
} 

// Output
	// "Welcome to Practicum, Yasmin!"
	// "Welcome to Practicum, Elise!"
	// "Welcome to Practicum, Terry!" 
```

* Example 2:
```js
const songLengths = [4, 7, 5, 6, 3, 8, 5, 4, 6, 3];
const maxRecordLength = 40;

let recordLength = 0;
let songsOnRecord = 0;

for (let songLength of songLengths) {
	if (songLength + recordLength > maxRecordLength) {
	    continue;
	}
	
	recordLength += songLength;
	songsOnRecord += 1;
}

console.log(songsOnRecord);
console.log(recordLength);
```