What are Regular Expressions (see [[RegExps - JS (Regular Expressions)]])
### stringPrototype.match()
* Description
	* Returns an array containing the specified string, including its location in the string. 
		* If special characters cannot be found --> method returns null
* Arguments
	1) The regex --> A regular expression object, or any object that has a Symbol.match method.
* Syntax
```js
stringPrototype.match(regex);
```
* Example
```js
const userList = 'Emma, Sean, Kate, Owen, Jane, Bartholomew, Luke';
const regex = /Bartholomew/;

userList.match(regex);  // [ 'Bartholomew' ] 
```

### regExpPrototype.test()
* Description
	* Executes a search with this regular expression for a match between a regular expression and a specified string and **returns a boolean value**
	* If global flag is set --> the regular expression receives the `lastIndex` property storing the potion of the matching character
	* If called multiple times, the search will begin from the `lastIndex` character
* Arguments
	1) str --> the string against which the regular expression will be matched
* Syntax
```js
regExpPrototype.test(str)
```
* Example
```js
const comments = [ 'I have an iPhone 6s — it\'s incredibly fast.', 'I have the latest Samsung, everything is fine.', 'Why pay more if I can get a Xiaomi cheap?', 'The Nokia 3310 is the best phone ever. Once I dropped it into the Grand Canyon and it still works.', 'The new iPhones are the best because they have improved water resistance.' ];

const regex = /iPhone/;
const iPhoneComments = comments.filter((item) => regex.test(item)); // search for "iPhone" in the strings

console.log(iPhoneComments);

/* [
  'I have an iPhone 6s — it\'s incredibly fast.',
  'The new iPhones are the best because they have improved water resistance.'
] */ 
```

```js
const regex = /\w+@\w+\.\w+/; // pattern for searching an email
const str = 'Elise Bouer: elisebouer@gmail.com';

regex.test(str); // true 
```

### stringPrototype.search()
* Descriptions
	* Returns the index of the matching character
		* Cannot be used with the global flag (see [[RegExps - JS (Methods and Flags)]])
		* If no match is found --> returns null
* Arguments
	1) regexp --> a regular expression object
* Syntax
```js
stringPrototype.search(regex);
```
* Example
```js
const regex = /\d{3,}/i; // will for for digits starting at 3 or more
const string = '12! equals 479001600'; 
string.search(regex); // 11
```

### stringPrototype.split()
* Descriptions
	* Returns an array of elements separated by whatever you defined with your regular expression.
* Arguments
	1) regexp --> the regular expression that defines where the split should happen
* Syntax
```js
stringPrototype.split(regex);
```
* Example
```js
const regex = /\n/im; // splitting the match pattern at each new line
const text = `I made myself a snowball
As perfect as could be.
I thought I'd keep it as a pet
And let it sleep with me.
I made it some pajamas
And a pillow for its head.
Then last night it ran away,
But first it wet the bed.`

const newText = text.split(regex);
console.log(newText); 
```

### regExpPrototype.exec()
* Descriptions
	* Executes a search with this regular expression for a match in a specified string and returns a result array, or null.
	* If no global flag is set --> Returns the same result as `stringPrototype.match()`
	* If global flag is set --> Returns the first match and adds the matching character's index to the `lastIndex` property of the regular expression.
	* if run multiple times, the search will start after the last matching string.
* Arguments
	1) str --> the string that will be matched against the regular expression
* Syntax
```js
regExpPrototype.exec(str)
```
* Example
```js
let regex = /\w+/;
let str = 'Someone must have been telling lies about Josef K.';

str.match(regex); // ['Someone']
regex.exec(str); // ['Someone'] 
```

### stringPrototype.replace()
* Descriptions
	* Replaces anything in a text by returning a new string
		* Searches the text against the regular expression, creates and returns a new string based on specified replacements
* Arguments
	1) regexp --> the regular expression to be to be used
	2) str / fn --> will be used to replace the old string
* Syntax
```js
stringPrototype.replace(regex, str/fn);
```

![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Frame_268_1588611030.png)

* Example
```js
const strObj = 'The space goes after the comma ,not before the comma.';
const regex = /\s,/g;

strObj.replace(regex, ', '); // 'The space goes after the comma, not before the comma.' 
```