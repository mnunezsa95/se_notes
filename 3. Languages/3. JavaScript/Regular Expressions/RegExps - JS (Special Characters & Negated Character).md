Resources
* [Full list of special characters for Regular Expressions](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)

### Using dots in Regular Expressions
* Dots can be matched to any character in a regexp
	* Can use many in a row
* Dots cannot detect line breaks
```js
const str = `
  I can't remember what his name is:
  it's either Sortini or Sordini.
  Maybe even Surdini spelled with "u".
`;

const regex = /S.r.ini/g; // a dot in a regular expression stands for any character.

str.match(regex); // [ 'Sortini', 'Sordini', 'Surdini' ] 
```

```js
const str = `Abrupt
line break`;

const regex = /Abrupt.line break/; // using dots does not recognize line breaks

str.match(regex); // null 
```


### Escaping Characters
* Escaping dots --> place a backslash ( `\` ) before the dot (`.`), to escape the period (treat it as dot not as 'any letter')
* Escaping other parts of a string --> place a ( `\` ) before the section of the text you want to escape
* Which characters to escape?
	* dot `.`
	* hypen `-`
	* plus `+`
	* parentheses `()`
	* caret (or hat) `^`
	* opening square bracket `[`

```js
const str1 = 'yandex.com/maps/';
const regex1 = /\.com/; // escaping a dot, it's a period now
const regex2 = /\/maps/; // escaping a slash before the word maps

str1.match(regex1); // [ '.com' ]
str1.match(regex2); // [ '/maps' ]

// you need to escape a backslash in order to find it
const str2 = 'C:\\';
const regex3 = /\\/; // escaping a backslash

str2.match(regex3); // [ '\' ] 
```

# Special Characters
* Can be used inside of regular expressions that search for groups of characters, rather than a single specific one (see [[RegExps - JS (Methods and Flags)]])

### Negated Classes 
* Does the opposite of a special character

### \\w   and   \\W
* Special Char: \\w --> searches for any digit, latin letter, or underscore
* Negated Class: \\W --> searches for anything EXCEPT for digits, latin letters and underscores
```js
const str = `
  IT companies' founding dates:
  Yandex: 09.23.1997
  Apple: 04/01/1976
  IBM: 06-16-1911
`;

const regex = /\w\w\W\w\w\W\w\w\w\w/g;

/* the digits are denoted by lowercase \w and the delimiters are uppercase \W. a delimiter is NOT a number, NOT a letter, and NOT an underscore. */

str.match(regex); // [ "09.23.1997", "01/04/1976", "16-06-1911" ] 
```

### \\d   and   \\D
* Special Char: \\d --> searches for any digit
* Negated Class: \\|D --> searches for anything EXCEPT a digit
```js
// will find anything but the digit
const someSymbol = /\D/g;
const string = 'I was born in 1987';

string.match(someSymbol); // ['I', ' ', 'w', 'a', 's', ' ', 'b', 'o', 'r', 'n', ' ', 'i', 'n', ' ']
```

### \\s   and   \\S
* Special Char: \\s --> searches for 'voids' in text (spaces, line breaks and tabs)
* Negated Class: \\S --> searches for anything except for spaces, line breaks and tabs
```js
const str = 'The smell\n' +
                    '            of vegetables' +
                    '                        on a cold day' +
          'performs faithfully an act of reality';

const regex = /\s/g;

str.match(regex).length; // 47 — Brautigan loved spaces 
```

```js
const str = 'The smell\n' +
                    '            of vegetables' +
                    '                        on a cold day' +
          'performs faithfully an act of reality';

const regex = /\S/g;

str.match(regex).length; // 62 — the margin between the number of letters and spaces is not so huge
```

### \\b   and   \\B
* Special Char: \\b --> searches for word boundaries
	* BEFORE the first character in a word string (if first character is a word character)
	* AFTER the first character in a word string (if LAST character is a word character)
	* BETWEEN two characters in a string (where one is a word character and other is NOT)
![image](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_13.05.4_1652110106.png)
* Negated Class: \\B --> searches for numbers, latin letters and underscores (equivalent to \\w)

```js
const string = "sadness";

string.match(/\bs/).index; // 0 — i.e. the first letter s
// the special character points at the border to its left, i.e. the beginning

string.match(/s\b/).index; // 6 - i.e. the last letter s
// the special character points at the border to its right, i.e. the end 
```

### The ^
* The caret (or hat) ` ( ^ ) ` denotes the start of a string. 
	* Used to denote that the following character should only be matched if found at the start of a string.
```js
const regex = /^\d+/g;
const newReg = /\d+/g;
const    str = '2001: A Space Odyssey premiered in 1968';

str.match(regex); // [ '2001' ];
str.match(newReg); // [ '2001', '1968' ]; 
```

### The $
* The dollar sign ` ( $ ) ` denotes the end of a string.
	* Used to denote that the following character should only be matched if found at end of string.
```js
const regex = /\d+$/;
const str = 'https://tripleten.com/learn/web/courses/37/sprints/17/topics/20/lessons/12';

console.log(str.match(regex)); // ( [ '12' ] ) 
```

# Summary

**![](https://lh4.googleusercontent.com/TUOYYrnrzL7rPjJukhqkcXL44LUKT1o07zVFaLBW1-zshztwfulzyQof1319zxNNLcOi3vWgMkzjLEAnFvTgjmwuMBpO9Na7byCl5SbLhoPt_kcnUxv-symcUPU9kjbA4Og_TAQyDQYo7RysYbQA3rg)**