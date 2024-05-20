

### Example
```js
// PersoProto is a class
const PersonProto = {
	calcAge() {
		console.log(2037 - this.birthYear)
	},
	init(firstName, birthYear) {
		this.firstName = firstName,
		this.birthYear = birthYear,
	}
};

// steven's prototype will be PersonProto
const steven = Object.create(PersonProto);

const StudentProto = Object.create(PersonProto);

// inheriting the init function & polymorphing it
StudentProto.init = function(firstName, birthYear, course) {
	PersonProto.init.call(this);
	this.course = course;
}

// adding a new function to StudentProto
StudentProto.introduce = function() {
	console.log(`My name is ${this.fullName} and I study ${this.course}`)
}

// Creating a new instance of the StudentProto, called jay
const jay = Object.create(StudentProto);

// Calling the init() function
jay.init('Jay', 2010, 'Computer Science')

// Calling the introduce() method
jay.introduce();

// Calling the calcAge() method (from the PersonProto)
jay.calcAge();
```

**![](https://lh6.googleusercontent.com/dEBGgq2ZMVHoPdv5_bT8KgZ_ERpvCBAhyvzM3KsY7R7lY4_tZT-fbb82B3gjkRbb5UR2vn8jKNItLz76KxWWPWmNNx0SPiCt-IPxBnLxYDvn1NTjePZ96HZZcEMhFfoSd6qcev4eAsd_jsDMuVLcsXE)**