See [[Creating & Working with Dates]]

# Date Methods

## The get Methods
### datePrototype.getFullYear()
* Description
	* Returns the year for this date according to local time
* Arguments
	* none
* Syntax
```js
datePrototype.getFullYear();
```
* Example
```js
// Getting full year
const future = new Date(2037, 10, 19, 15, 23);
future.getFullYear(); // returns 2037
```

### datePrototype.getMonth()
* Description
	* Returns the month for this date according to local time (month is zero-based)
* Arguments
	* none
* Syntax
```js
datePrototype.getMonth();
```
* Example
```js
// Getting month of the year
const future = new Date(2037, 10, 19, 15, 23);
future.getMonth(); // returns 10
```

### datePrototype.getDate()
* Description
	* Returns the day of the month for this date according to local time.
* Arguments
	* none
* Syntax
```js
datePrototype.getDate();
```
* Example
```js
// Getting day of the month
const future = new Date(2037, 10, 19, 15, 23);
future.getDate(); // returns 19
```

### datePrototype.getDay()
* Description
	* Returns the day of the week for this date according to local time (0 represents Sunday).
* Arguments
	* none
* Syntax
```js
datePrototype.getDay();
```
* Example
```js
// Getting day of the week
const future = new Date(2037, 10, 19, 15, 23);
future.getDay(); // returns 4 (thursday)
```

### datePrototype.getHours()
* Description
	* Returns the hours for this date according to local time. Hours are zero-based.
* Arguments
	* none
* Syntax
```js
datePrototype.getHours();
```
* Example
```js
// Getting hours of current time
const future = new Date(2037, 10, 19, 15, 23);
future.getHours(); // returns 15
```

### datePrototype.getMinute()
* Description
	* Returns the minutes for this date according to local time. Minutes are zero-based.
* Arguments
	* none
* Syntax
```js
datePrototype.getMinutes();
```
* Example
```js
// Getting minutes of current time
const future = new Date(2037, 10, 19, 15, 23);
future.getMinutes(); // returns 23
```

### datePrototype.getSeconds()
* Description
	* Returns the seconds for this date according to local time.
* Arguments
	* none
* Syntax
```js
datePrototype.getSeconds();
```
* Example
```js
// Getting seconds of the specified date
const moonLanding = new Date('July 20, 69 00:20:18');
console.log(moonLanding.getSeconds());
```

### datePrototype.toISOString()
* Description
	* Returns a string representing this date in the date time string format (YYYY-MM-DDTHH:mm:ss.sssZ); the timezone is always UTC (denoted by the suffix Z)
* Arguments
	* none
* Syntax
```js
datePrototype.toISOString();
```
* Example
```js
// Getting a nicely formatted string
const event = new Date('05 October 2011 14:48 UTC');
console.log(event.toISOString()); // "2011-10-05T14:48:00.000Z"
```

### datePrototype.getTime()
* Description
	* Returns the number of milliseconds for this date, since January 1, 1970, UTC.
* Arguments
	* none
* Syntax
```js
datePrototype.getTime()
```
* Example
```js
// Getting the timestampe
const future = new Date(2037, 10, 19, 15, 23);
future.getTime(); // 2142274980000
```

### Date.now()
* Description
	* Returns the number of milliseconds elapsed since January 1, 1970, UTC.
* Arguments
	* none
* Syntax
```js
Date.now()
```
* Example
```js
console.log(Date.now()); // get the current time stamp
```

--- 
## The set Methods



--- 
