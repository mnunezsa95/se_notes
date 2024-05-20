* [TripleTen: Conditionals Cheatsheet](https://practicum-content.s3.us-west-1.amazonaws.com/web-developer/cheat-sheet/conditionals-and-loops.pdf)

**![](https://lh6.googleusercontent.com/UsfEDbYmp26cP0asPyyKyAee_nIsMHEagRhfjR6NHs82HJS2QOUulrqJSDYj8cU5EtZp6BD8ykthqCKNLMVx_CQD0gqHn3CzncmSYbKV6lYvwrqKHaFFMHkXfpszqFKyFKYdhOQW6pSrvZMOAML8J1Y)**

### What are Loops used for?
* Loops --> allow piece of code to run multiple times depending on whether or not a condition remains true
	* Each execution of the code is known as an iterable

### Parts of a loop
* condition --> a piece of code that will be checked for true or false
* body --> the part of the code to be repeatedly executed as long as the condition is true

### Types of Loops

| type       | description                                             |
| ---------- | ------------------------------------------------------- |
| for        | loops through a block of a code a number of time        |
| for / in   | loops through the properties of an object               |
| for / of   | loops through the values of an iterable object          |
| while      | loops through a block of code while a condition is true |
| do / while | loops through a block of code while a condition is true |
See:
* [[JS - for loop]]
* [[JS - for...of loop]]
* [[JS - while loop]]

# Changing loop behavior
* The **break** and continue **statement** can change loop behavior 

### break keyword
* break --> immediately 'breaks out' from a loop
```js
for (let i = 0; i <= 10; i++) { // loop will run as long as i is less than 10
  if (i === 5) { // however, if i is equal to 5, it will exit the loop
    break;
  }
  console.log(i);
}
```

### continue keyword
* continue --> immediately 'breaks out' from a current iteration, but NOT the entire loop
	* hops over the iteration
```js
for (let i = 0; i <= 10; i++) { // loop will run as long as i is less than 10
  if (i === 5) {  // however, if i is equal to 5, it will exit the iteration
    continue;    // the loop will continue
  }
  console.log(i);
}

// result: 0, 1, 2, 3, 4, 6, 7, 8, 9, 10
```