**Inheritance** --> a class' ability to inherit methods and properties from a parent class
* Inheritance requires the following to work:
	1) the **extends** keyword --> extending of the child from a parent
	2) the **super()** --> inheriting the parent properties
		* "calls" the parent constructor
	3) Additional properties can be added to the child class
	4) Additional methods can be added to the child class 
		* Inherited methods can undergo [polymorphism](https://www.geeksforgeeks.org/polymorphism-in-javascript/) (see [[JS - ES6 Classes - Polymorphism]])


```js
// the parent class

class PersonCl { 
	constructor(fullName, birthYear) { // construcotr takes two arguments
		this.fullName = fullName;
		this.birthYear = birthYear;
	}
	// Instance Methods
	calcAge() {
		console.log(2037 - this.birthYear);
	}
	greet() {
		console.log(`Hey ${this.fullName}`)
	}
}

```

```js
// the child class

// the 'entends' keyword connects the two prototypes
class StudentCl extends PersonCl { 
	constructor(fullName, birthYear, course) { 
		// super() should always be called first!
		super(fullName, birthyear); // super = constructor fn of parent class
		this.course = course;
	}
	introduce() {
		console.log(`My name is ${this.fullName} and I study ${this.course}`)
	}
	// overwriting the calcAge() function from the parent
	calcAge() {
		console.log(`I'm ${2037 - this.birthYear} years old, but as a student I          feel more like ${2037-this.birthYear + 10}`);
	}
}

// Creating a new instance of the student class
const marta = new studentCl('Marta Jones', 2012, 'Computer Science');

marta.introduce(); // My name is Marta Jones and I study Computer Science
mart.calcAge(); // I'm 25 years old, but as a student I feel more like 35
```