What is a Regular Expression (see [[RegExps - JS (Regular Expressions)]])
# Sets
* Define a group of characters to search for
* How to create a set
	* Wrap the group of characters inside a set of square brackets
```js
// Looking for all characters 'a' and 'b':
'baseball'.match(/[ab]/g); // [ 'b', 'a', 'b', 'a'] 
```

```js
const str = '03/14/2018'; 
const regex = /0[345]\W\d\d\W2018/g; // this pattern searches spring months in 2018

str.match(regex); 
```

# Ranges
* Matches characters within a selected range of values
* Ranges can be combined (letters and numbers, and chars outside the range)
* How to create a range
	* Divide two characters by a hyphen
```js
const regex = /[m-t]/gi; // search from letters m to t
'Martian'.match(regex); // [ 'M', 'r', 't', 'n' ] 
```

```js
const str = '04/20/2019';
const regex = /0[1-6]\W\d\d\W2019/g; // this pattern searches for months in the first half of 2019
str.match(regex); // [ '04/20/2019' ] 
```

```js
const regex = /[A-Z0-9\-]/g; // all uppercase letters, numbers, and hyphens
const str = 'she flew on a BOEING 737-800'; 

str.match(regex).join(""); // 'BOEING737-800' 
```

# Negated Sets and Ranges
* Does the opposite of what is placed in the brackets ` [ ] `
* How to create a negated set or range
	* Add a carrot ^ character at the beginning of the range (to do the opposite)
```js
const str = 'Midterm grades: D C C A D B B C A';
const regex = /[^C-F]/g;

str.match(regex).join(''); // 'Midterm grades:      A  B B  A'

// it looks better now, but it will look suspicious if you leave blank spots on your report card like this!
```