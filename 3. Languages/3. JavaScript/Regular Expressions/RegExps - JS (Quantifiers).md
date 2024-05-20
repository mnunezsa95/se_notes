What are quantifiers? see [[RegExps - JS (Regular Expressions)]]

### Quantifier Summary
**![[quantifer-summary.png]]

# Basic Quantifiers

### The + Quantifier
* Placing the ` + ` quantifier **after** a character will look for all words in which that character occurs more than once. 
* Can be made to have **lazy matching behavior** by adding a ` ? `
```js
const str = 'The correct spelling of the word "millennium" is with two Ls';
const regex = /mil+ennium/;

// this regular expression will find both variants: with one "L" and with two "L"s\
str.match(regex); // [ 'millennium' ] 
```

```js
const someSymbols = /e.+?n/gi;
const    str = 'Ed\'s son can swim like a fish';

console.log(str.match(someSymbols));// [ "Ed's son" ] 
```

### The * Quantifier
* Placing the ` * ` quantifier **after** a character will look for matches with zero or more occurrences. 
	* The ` * ` quantifier tells the engine that the preceding character may or may not be included in the word.
	* Can be used to look for different spellings
```js
const exc = 'artist';
const esc = 'artiste';
const regex = /artiste*/; // the letter "e" may or may not occur
exc.match(regex); // [ 'artist' ]
esc.match(regex); // [ 'artiste' ] 
```

### The ? Quantifier 
* Placing the ` ? ` quantifier after a character will ONLY match either zero occurrences or one occurrence of the chosen character
```js
/* makes the letter u optional and matches both spelling variants: favourite and favorite. */

const regex = /favou?rite/g;
const    str = 'favourite or favorite';

str.match(regex); // ['favourite', 'favorite'] 
```

### The | Quantifier 
* Placing the ` | ` quantifier after a character will create 'forks' of the characters and search for alternatives in the regular expression
	* Useful when searching for either English or British English spelling
```js
const someSymbol = /cent(er|re)/g
const    str = 'center or centre';

console.log(str.match(someSymbol)); // ['center', 'centre'] 
```

### The { } Quantifier 
* Place a number inside the ` { } ` will specify the number of matches that it should search for
* Has **greedy matching behavior** (chooses a longer return over a short one)
* Can be made to have **lazy matching behavior** using ` { }? `

```js
const regionCode = /\d{3}/;
const    phoneNumber = 'My phone number: +1(555)324-41-5';

phoneNumber.match(regionCode); // [ '555' ] 
```

* Can be used to find a range of number of matches
```js
const str = 'this much, thiiis much, thiiiiiiis much';
const regex = /thi{2,5}s/; // will search for 2-5 ouccrences of the 'i'

str.match(regex); // [ 'thiiis' ]

// in the word "this" the letter "i" occurs only once and in the word "thiiiiiiis" the letter "i" occurs more than 5 times 
```

* Can also be used to find a range from 1 to infinity 
```js
const someSymbol = /a{1,}/g; // searches from 1 to infinity number of a's
const    str = 'alohaa';

console.log(str.match(someSymbol)); // ['a', 'aa'] 
```

```js
const someSymbols = /e.{2,11}?e/gi; // declaring lazy behavior
const    str = 'Everyone else knows that book, you know';

console.log(str.match(someSymbols)); // ['Everyone', 'else']

/* the lazy quantifier has found the shortest matches this time */  
```

# Lazy vs Greedy Behavior
* Sometimes the quantifier can choose between a shorter return or longer return
	* A lazy quantifier will go for the shorter match
	* A greedy one ends up returning the longer string
```js
const str = 'free from worries'; 
const regexLazy = /fr.+?[es]/; // lazy quantifier 
const regexGreedy = /fr.+[es]/; // greedy quantifier 

console.log(str.match(regexLazy)); // [ 'free' ]
console.log(str.match(regexGreedy)); // [ 'free from worries' ] 
```

# Quiz
**![](https://lh4.googleusercontent.com/963Hd0stqZlnMFh6crblUWwEM9mBk1_8VOGc0Z9HpSMdEG-xqy-3qwGzi5gU2QuVdxWjTvlooeJrYH4BHTtn2jo9VSz2GPcbtsfCJIclZ_WObFa_I--WwQa3hVNIw9xR6Qa7DE5PUQBcXh6Qmefz7kA)**