Strings (see [[JS - Strings in JavaScript]], [[JS - String Methods]])

### Accessing chars in a string
* Chars in a string are accessed by their index
	* Returns `undefined` letter at specified index --> DNE
```js
// using the index to access a string stored in a variable
const wrongWord = "expresso";
console.log(wrongWord[1]); // "x"
console.log(wrongWord[20]); // undefined 
```

### Concatenation
* **Concatenation** --> joining two or more strings by using addition sign `( + )`
	* If a string and number are concatenated --> the number will be converted to a string (see [[JS - Implicit and Explicit Conversion]])
	* Example: 
```js
console.log("Java" + "Script"); // "JavaScript"
console.log(100 + 500); // here we're adding two numbers, so the result is a number: 600

console.log(100 + "500"); // we're concatenating a number and a string, which results in a string: '100500' 
```

### The Escape Character ( \\ )
* The **escape character ( \\ )** --> allows for 
	* single quotes to be used with the apostrophe in a string
	* double quotes to be used with the the double quotes in a string
```js
console.log('The Republic of Côte d\'Ivoire');
console.log("Never Say \"Never\" Again");
```

### The Newline Character (\\n)
* The **newline character ( \\n )** --> invisible character that represents the ending of one line of text and the beginning of the next

### The Newtab character ( \\t )
* The newtab character ( \\t ) is an invisible character that represents the end of a one line and the indent of new line

```js
console.log("The first line of a paragraph is often indented. Like this:\n\n\tLorem Ipsum...")

//The first line of a paragraph is often indented. Like this:
    Lorem Ipsum... 
```

### Template Literals (Template Strings)
* Template Strings --> are strings enclosed in backticks ( ` `` `)
* Why are Template Strings powerful?
	* Strings inside of backticks can take up multiple lines
	* Allow for expressions to be embedded into strings by using a dollar sign ($) followed by a pair of curly braces --> the result of the expression ends up in the final string

```js
console.log(`I am a template literal,
I am pretty cool.
Look at me
taking 
up
all
these
lines!`); 

console.log(`A stitch in time saves ${10 - 1}.`); // "A stitch in time saves 9." 
```

```js
const greeting = "Hi, my name is";
let name = "Kevin";
let punctuation = "!"; 

// can be written like this: 
`${greeting} ${name}${punctuation}`;
```

