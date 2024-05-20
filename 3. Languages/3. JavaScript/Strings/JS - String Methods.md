What are strings? (see [[JS - Strings in JavaScript]])
String Properties (see [[JS - String Properties]])

---
# Methods of Searching Strings for Characters

#### indexOf()
* Description:
	* Returns the index of the character within the string on which it's called
		* case sensitive
		* returns -1 if the searchString is not found
* Arguments
	1) searchString --> the substring to search for
	2) position (optional) --> 
* Syntax
```js
stringPrototype.indexOf(searchString, position)
```
* Example
```js
"Practicum".indexOf("P"); // 0
"espresso".indexOf("s"); // 1
"espresso".indexOf("x"); // -1 because no instance of this char

const elements = "Earth, Air, Fire, Water";
elements.indexOf("Fire");

"salt and pepper".indexOf("salt") !== -1; // true
```

#### includes()
* Description:
	* Returns a boolean after checking wether a character or combination of characters exists within a string
* Arguments
	1) searchString -->  the substring to search for
	2) position (optional) --> The position within the string at which to begin searching for. (Defaults to 0.)
* Syntax
```js
stringPrototype.includes(searchString, position)
```
* Example
```js
"Harry Potter and the Prisoner of Azkaban".includes("Harry Potter"); // true
"Teamwork".includes("I"); // false 
```

#### startsWith()
* Description:
	* Returns a boolean after checking wether a string BEGINS with the characters or combination of characters 
* Arguments
	1) searchString -->  The characters to be searched for at the start of this string
	2) position (optional) --> The position within the string at which to begin searching for. (Defaults to 0.)
* Syntax
```js
stringPrototype.startsWith(searchString, position)
```
* Example
```js
"Vendetta".startsWith("V"); // true
"The perfect date".startsWith("Dinner and a movie"); // false
```

#### startsWith()
* Description:
	* Returns a boolean after checking wether a string ENDS with the characters or combination of characters 
* Arguments
	1) searchString -->  The characters to be searched for at the start of this string
	2) endPosition (optional) --> The end position within the string at which to begin searching for. (Defaults to 0.)
* Syntax
```js
stringPrototype.endsWith(searchString, endPosition)
```
* Example
```js
const theRealEnd = "This is not the end";
theRealEnd.endsWith("end"); // true bc the string that the endsWith() method was called on, ends with "end"
```


---

# Methods of Converting Strings

#### toUpperCase()
* Description
	* Converts all of the characters of a string to uppercase
* Arguments
	* none
* Syntax
```js
stringPrototype.toUpperCase()
```
* Example
```js
"Turn Caps Lock off".toUpperCase(); // "TURN CAPS LOCK OFF" 
```

#### toLowerCase()
* Description
	* Converts all of the characters of a string to lowercase
* Arguments
	* none
* Syntax
```js
stringPrototype.toLowerCase()
```
* Example
```js
"Turn Caps Lock on".toLowerCase(); // "turn caps lock on" 
```


#### split()
* Description
	* Breaks up the string up into an array based on the separator
* Arguments
	1) separator --> The pattern describing where each split should occur (" " is commonly used)
	2) limit --> A non-negative integer specifying a limit on the number of substrings to be included in the array
* Syntax
```js
stringPrototype.split(separator, limit)
```
* Example
```js
"I came. I saw. I conquered.".split(". "); // [ 'I came', 'I saw', 'I conquered.' ]
```

#### slice()
* Description
	* Extracts a section of this string and returns it as a new string, without modifying the original string.
* Arguments
	1) indexStart --> index where the slicing should begin (included)
	2) indexEnd (optional) --> index where the slicing should begin (excluded)
* Syntax
```js
stringPrototype.split(indexStart, indexEnd)
```
* Example
```js
"Believe".slice(2, 5); // "lie" bc slicing starts at index 2 & stops at index 5

"Google Maps".slice(7); // "Maps" bc indexEnd omitted, so goes till end
"Google Translate".slice(7); // "Translate" bc indexEnd omitted, so goes till end
```