
Regular expressions allow for complex search algorithms (see [[RegExps - JS (Regular Expressions)]])
### Entities that influence searches
1) Special Characters --> are contained in the regular expression itself and allows for the search to be refined
2) Flags --> customizes the way the methods work 
3) Methods --> defines what should be done when the string is found 

*** Summary --> Special characters define what to search for, flags define how to perform that search, and methods determine what to do with the search result ***

### Regular Expression Methods
* The `stringPrototype.match()` and `regExpPrototype.test()` are easily confused
	* match() --> match() is called on the variable that stores the string; the regexp is passed as an arg
	* test() --> test() is called on the RegExp itself; the string is passed as am arg
```js
const regex = /d/;
const word = 'knowledge';

word.match(regex); // [ 'd' ] — the method found the character in the string
/* match() is a string method. we are calling it as a string method, and the regular expression is passed as an argument. */
```

```js
const regex = /c/;
const word = 'schedule';

regex.test(word); // true — the method confirmed that there is a match in the string

/* test() is a method of the RegExp object. we are calling it as a method of the regExp variable and passing the string as an argument. */
```

# Flags
* Are characters place at the end of regular expressions to customize search settings
	* More than one can be used at a time (order does not matter)
* Example
```js
// using flags in a regular expression
const regex1 = /magic bullet/g; // g flag is set
const regex2 = /cure/gi; // g and i flags are set 
```

### The `g` flag
* The 'global' flag
	* Searches the specified text for every match (not just first one)
```js
const regex = /s/;
const regexGlobal = /s/g;
const word = 'espresso';

word.match(regex); // [ 's' ]
word.match(regexGlobal); // [ 's', 's', 's' ]; 
```

* Using the g flag with match()
	* When g flag is not used --> match() will return an array with additional properties (such as index & input properties)
	*  When g flag is used --> match() will NOT these additional properties (just an array of the strings)
```js

// When g flag is NOT used
const str = 'tro-lo-lo';
const result = str.match(/lo/);

result[0]; // 'lo'
result.index; // 4
result.input; // 'tro-lo-lo' 

// When g flag is used
const str = 'tro-lo-lo';
const result = str.match(/lo/g);
result; // ['lo', 'lo'] 

```

### The `i` flag
* The 'ignore' flag --> used to ignore case sensitivity 
	* When used, the search will ignore uppercase and lowercase
```js
const str = 'Wilhelm Conrad Roentgen was awarded the Nobel Prize in 1901.'

const regex = /roentgen/;
const regexIgnore = /roentgen/i;

str.match(regex); // null
str.match(regexIgnore); // [ 'Roentgen' ] 
```

### The `m` flag
* The 'multiple' flag --> used for multiple line searches (see [[RegExps - JS (Regular Expressions)]], [[RegExps - JS (Special Characters & Negated Character)]])
	* When used, the engine will consider each line break as the "end of one line and beginning of another line"
* The ` m ` flag works for template literals and when the ` \n ` is used
* The ` m ` flag works poorly with the dot ` ( . ) ` b/c it ignores the end of a string
	* A dot mail fail because it will detect any character except for the end of the string
	* Use this combination instead of a dot for searching some character ` [\s\S] `
```js
const str = `Nature’s first green is gold,
  Her hardest hue to hold.
  Her early leaf’s a flower;
  But only so an hour.
  Then leaf subsides to leaf.
  So Eden sank to grief,
  So dawn goes down to day.
  Nothing gold can stay.`;
const regex = /[A-Z]+.?$/gim;

str.match(regex); // ['gold,', 'hold.', 'flower;', 'hour.', 'leaf.', 'grief,', 'day.', 'stay.']
```

### The `u` flag
* The 'unicode' flag --> used for unicode searches. Requires two u flags (one at the beginning \u and on at the end u)
	* When used, allows for characters to be searched by their unicode number
```js
const str = '& is an ampersand. Its Unicode value is 26';
const regex = /\u{26}/; // u flag is not set here
const regexUnicode = /\u{26}/u; // but here it is set

str.match(regex); // null
str.match(regexUnicode); // ['&'] 
```

### The `y` flag
* The 'sticky' flag --> add the sticky property (searches for the string at a particular place in the text)
	* Requires the addition of the `lastIndex` property to the regular expression. This indicates where the search should start
```js
const fuelUp = 'fuel up and go';
const regex = /go/y;

regex.lastIndex = 0; 
fuelUp.match(regex); 
// null. The first word is 'fuel', not 'go'

regex.lastIndex = 12;
fuelUp.match(regex); // [ 'go' ]

/* interestingly enough, different browsers display the info returned by string methods differently: some show the index only, while others show the original string and capturing groups */ 
```

### The `s` flag
* The 'dotall' flag --> enables 'dotall' mode which allows the dot ( . ) to match newline characters ( \n )