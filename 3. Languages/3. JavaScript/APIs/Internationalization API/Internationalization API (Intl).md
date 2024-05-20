The JavaScript Internationalization API allows dates to be internationalized for different countries / areas of the world

### How to the Intl API works
* The Intl API does not require data fetching
	* Built-into the engine
* The **Intl** namespace object contains several constructors as well as functionality common to the internationalization constructors and other language sensitive functions. 

### How to use the Intl API
1) Use the `new Intl` keyword (will call a new instance of the Intl object)
2) Use the `.DateTimeFormat()` method (see [[Date and Intl Methods]])
	* Pass in the [ISO Language Code](http://www.lingoes.net/en/translator/langcode.htm) as an argument 
3) Call the format() method

### Retrieving a language from the browser
* The [ISO Language Code](http://www.lingoes.net/en/translator/langcode.htm) can be obtained from the user's browser's language 
* How to retrieve?
	* Use the `navigator.language` (can be set equal to a variable) (see [[Navigator Object: DOM]])

# Formatting Dates
* Dates can be formatted using the `new Intl.DateTimeFormat()` constructor (see [[Date and Intl Methods]])
* There's a variety of different methods and options that can be used with the [Intl.DateTimeFormat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat) constructor
```js
const currentDate = new Date();
const dateOptions = {
	hour: "numeric",
	minute: "numeric",
	day: "numeric",
	month: "long",
	year: "numeric",
	weekday: "long",
};

labelDate.textContent = new Intl.DateTimeFormat(currentAccount.locale, dateOptions).format(currentDate);
```

# Formatting Numbers
* Numbers can be formatted using the `new Intl.NumberFormat()` constructor (see [[Date and Intl Methods]])
* There's a variety of different methods and options that can be used with the [Intl.NumberFormat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat) constructor
```js
const num = 3884764.23;
const options = {
	style: "unit",
	unit: "mile-per-hours",
};

console.log("US: ", new Intl.NumberFormat("en-US", options).format(num));
console.log("Germany: ", new Intl.NumberFormat("de-DE", options).format(num));
console.log("Syria: ", new Intl.NumberFormat("ar-SY", options).format(num));
```

```js
const num = 3884764.23;
const options = {
	style: "unit", 
	unit: "EUR", // sets the currency to Euro
	useGrouping: false // removes the separators (commas)
};

console.log("US: ", new Intl.NumberFormat("en-US", options).format(num));
console.log("Germany: ", new Intl.NumberFormat("de-DE", options).format(num));
console.log("Syria: ", new Intl.NumberFormat("ar-SY", options).format(num));
```

