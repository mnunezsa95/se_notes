* What are objects? (see [[JS - Objects in JavaScript]])
# Accessing Object Values
* Values can be accessed 2 ways
	1) Using dot notation
		* Uses a dot ( `.` ), follow by name of the `key`
	2) Using bracket notation
		* Uses square brackets `[ ]`, and the name of the `key` surrounded by `“ “`

```js
const firstOffer = {
	salary: 4000,
	bonus: 5000,
	signingBonus: 8000,
};

const secondOffer = {
	salary: 3000,
	bonus: 10000,
	signingBonus: 6000,
};

const thirdOffer = {}
thirdOffer.salary = Math.max(firstOffer["salary"], secondOffer["salary"]);
thirdOffer.bonus = Math.max(firstOffer["bonus"], secondOffer["bonus"]);
thirdOffer.signingBonus = Math.max(firstOffer["signingBonus"], 
```