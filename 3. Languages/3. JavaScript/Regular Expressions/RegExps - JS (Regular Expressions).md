See:
* [[RegExps - Introduction to Regular Expressions]]

Resources
* [Regular Expression Visualizer](https://jex.im/regulex/#!flags=&re=%5E(a%7Cb)*%3F%24) 
* [Testing Regular Expressions: RegExp 101](https://regex101.com/)
* [Form Validation using Regular Expression](https://css-tricks.com/form-validation-part-1-constraint-validation-html/)

### How to Create a RegEx
* Regexes are enclosed in forward slashes `/.../`
* Example
```js
const regex = /expressing regularly/;
console.log(regex); // result: /expressing regularly/
```

### Using RegExps
* There are several methods for working with regexps
	1) match() --> will return an array containing the specified string, including its location in the string (see [[Regexps - JS (Methods)]])
		* If the string does not exist --> returns null
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

### Multilines
* ` \n ` is used to define a new line (line-break) in a string. 
```js
const str1 = `Good night, good night. Parting is such sweet sorrow
  That I shall say good night till it be morrow.`;
const str2 = 'I do not like green eggs and ham\nI do not like them Sam I am.' 
```