# The Intl Object

### Intl.DateTimeFormat()
* Description:
	* Enables language-sensitive date and time formatting
* Arguments
	1) [local](http://www.lingoes.net/en/translator/langcode.htm) --> a code that can be used to specify the language (see [[Internationalization API (Intl)]])
	2) [options](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat) --> an object with the customization of the format
		* localeMatcher
		* calendar
		* numberingSystem
		* hour12
		* hourCycle
		* timeZone
		* weekday --> possible values ('`long', 'short', 'narrow'` )
		* era --> possible values ('`long', 'short', 'narrow'` )
		* year --> possible values (`'numeric', '2-digit`)
		* month --> possible values (`'numeric', '2-digit', long', 'short', 'narrow'`)
		* day --> possible values (`'numeric', '2-digit`)
		* dayPeriod --> possible values ('`long', 'short', 'narrow'` )
* Syntax
```js
new Intl.DateTimeFormat()
new Intl.DateTimeFormat(locales, options)
```
* Example 
```js
labelDate.textContent = new Intl.DateTimeFormat("en-Us")
```

### Intl.DateTimeFormat().Format()
* Description
	* Formats a date according to the locale and formatting options of this Intl.DateTimeFormat object.
* Arguments
	1) date --> The date to format.
* Syntax
```js
Intl.DateTimeFormat().format(date)
```
* Example
```js
// formatting the date (inside the currentDate variable) to the en-Us
labelDate.textContent = new Intl.DateTimeFormat("en-US").format(currentDate);
```

### Intl.DateTimeFormat().formatRange()
* Description
	* Formats a date range in the most concise way based on the locales and options provided when instantiating this Intl.DateTimeFormat object.
* Arguments
	1) startDate --> A Date object representing the start of the date range.
	2) endDate --> A Date object representing the end of the date range.
* Syntax
```js
formatRange(startDate, endDate)
```
* Example
```
```

### Intl.NumberFormat().
* Description
	* Creates Intl.NumberFormat objects.
	* Enables language-sensitive number formatting
* Arguments
	1) [local](http://www.lingoes.net/en/translator/langcode.htm) --> a code that can be used to specify the language (see [[Internationalization API (Intl)]])
	2) [options](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat) --> An object with some or all of the following properties
		* compactDisplay
		* currency
		* currencyDisplay
		* currencySign
		* localeMatcher
		* notation
		* numberingSystem
		* signDisplay
		* style
		* unit
		* unitDisplay
		* useGrouping
		* roundingMode
		* roundingPriority
		* roundingIncrement
* Syntax
```js
new Intl.NumberFormat(locales, options)
```
* Example
```js

// formatting numbers in different ways
console.log("US: ", new Intl.NumberFormat("en-US".format(num)));
console.log("Germany: ", new Intl.NumberFormat("de-DE".format(num)));
console.log("Syria: ", new Intl.NumberFormat("ar-SY".format(num)));
```

### Intl.NumberFormat().Format()
* Description
	* Formats a number according to the locale and formatting options of this Intl.NumberFormat object. 
* Arguments
	1) number --> A Number, BigInt, or string, to format.
* Syntax
```js
Intl.NumberFormat().format(number)
```
* Example
```js
const amount = 654321.987; // amount that will be formatted
const options1 = { style: 'currency', currency: 'RUB' }; // options object
const numberFormat1 = new Intl.NumberFormat('ru-RU', options1); // creating a new instance of the NumberFormat object
console.log(numberFormat1.format(amount)); // formatting and logging
```