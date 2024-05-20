### Can operations with dates be performed?
* Operations with dates can be performed
	* For example, two dates can be subtracted in order to determine the difference between the two dates
### Important Conversion
* `1000 * 60 * 60 * 24` 
	* Converts milliseconds to days

### Typical Steps for Operations with Dates
* How to do this:
	1) Convert a date to a number (the result is a timestamp) (see [[Creating & Working with Dates]])
	2) Perform calculations with the timestamps
	3) Convert back to dates
* Example
```js
// Operations with Dates

// function that takes in two dates and find the difference between the two timestampes, converts the difference to days and returns it
const calcDaysPassed = (date1, date2) => {
	return Math.abs((date2 - date1) / (1000 * 60 * 60 * 24));
};

const days1 = calcDaysPassed(new Date(2037, 3, 14), new Date(2037, 3, 4));
```

### Working with complex date operations
* For precise calculations use a **Moment.js** library (see [[Moment.js]])
	* Time changes due to daylight saving difference 

