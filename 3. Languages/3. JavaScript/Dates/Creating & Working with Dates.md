### Creating Dates
* There are four ways to create dates in JavaScript (all use the Date () constructor)
	1) Without any parameters
	2) Parsing a date from a string
	3) Using  (year, month, day, hour, minute, second) into the constructor
		* Months are zero-based 
	4) Using number of milliseconds since the beginning of the UTC (Jan 01, 1970)
```js
// Without using parameters
const now = new Date(); // creating a date with current time

// Parsing from a string
const stringDate = new Date('Aug 02 2020 18:05:41');
const christmas = new Date('December 24, 2015');

// Using several parameters (year, month, day, hour, minute, second)
const parameterDates = new Date(2037, 10, 19, 15, 23, 5); 

// Using the number of milliseconds since the beginning of the UTC
const utcDate = new Date(0)
const utcDate2 = new Date(3 * 24 * 60 * 60 * 1000); // a timestamp
```

### Working with Dates

* There are several methods for working with dates (see [[Date and Intl Methods]])