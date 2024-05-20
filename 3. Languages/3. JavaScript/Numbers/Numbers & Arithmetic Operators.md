Resources
* [TripleTen: JavaScript Basics Cheatsheet](https://practicum-content.s3.us-west-1.amazonaws.com/web-developer/cheat-sheet/js-basics.pdf)

### What are Arithmetic Operators?
* Arithmetic Operators are used to manipulate operands (see [[Numbers in JavaScript]], [[The Remainder Operator]])
	* Operands --> the input values of an operation 
*![image](https://lh5.googleusercontent.com/LReqxeqZgwDHuvoKhA0rDUOioC4jDKdeqXj8Z-ug9Uc_Rzdm3v8nOylNTWtQ6mps16LjxB2ooyIWX36eLL2--ykwHGQJU44PhdV2YU3LPRl4JrbnvIcT6ympgf9u_udhHPD6ZIwMAQ8c9xnle0UEyOs)
**![](https://lh5.googleusercontent.com/F1jOgUNeHOwH1glpoOpCiCu4q7oJ9hJ_XeTqQi23HKje7p8ifMJpAOy2NkKbUnkELlaHspWiiH1cQm1LR4gTHLQni9qqhTawIFX72x1_-Nl4WqXE7tgfmMt1PBBMw_LCZ9VLxi8f2GFmJs4HtGIIfXU)**

* Examples
```js
12 + 12 // addition operator — returns 24
44 - 4 // subtraction operator — returns 40
5 * 3 // multiplication operator — returns 15
18 / 3 // division operator — returns 6 
4 ** (1/2) ); // 2 (power of 1/2 is the same as a square root)
8 ** (1/3) ); // 2 (power of 1/3 is the same as a cubic root)
```

### Operation Rules (PEMDAS)
* Operations in JS follow the PEMDAS rules
* **Order**: parentheses → exponent → multiplication → division → addition → subtraction
	* For nested parentheses: JS runs from inside --> out
* Semicolons --> not required after numbers, but common practice
* Commas --> are used to evaluate multiple expressions (but only last one is returned)
* Increment (++) --> used to increase a variable by 1
* Decrement (--) --> used to decreased a variable by 1

```js
let a = (1 + 2, 3 + 4);
alert(a); // 7 (the result of 3 + 4) bc only last expression is returned

// using the prefix form
let counter = 2;
++counter; // works the same as counter = counter + 1, but is shorter
console.log(counter); // will return 3

// using the postfix form
let counter = 2;
counter--;      // works the same as counter = counter - 1, but is shorter
console.log(counter); // will return 1
```