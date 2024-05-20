### Real Private Fields & Methods
* Not yet part of the language, but proposal to EMCA has reached stage 3

# Fields
* Fields --> properties that will be ALL instances of a class

### Public Fields
* Defined by declaring inside the class (outside the constructor) with a semicolon at the end
```js
class Account {
	// public fields (instances)
	locale = navigator.language;
	_movenments = [];
}
```

### Private Fields
* Fields will become truly private by adding a hash ` ( # ) ` before a field
	* These will be truly private and unaccessible
```js
class Account {
	// public fields (instances)
	locale = navigator.language;
	#movenments = [];
}
```

### Public Methods
* Nothing will be changing

### Private Methods
* Methods will become truly private by adding a hash prior to the method
```js
#method(param1, param2) {
	// method logic
}
```

# Example: Full

```js

class Account {
    locale = global.language;
    #movements = []; // private field
    #pin; // private field
  constructor(owner, currency, pin) {
    this.owner = owner;
    this.currency = currency;
    this.#pin = pin;
  }
  deposit(val) {
    this.movements.push(val);
  }
  withdraw(val) {
    this.deposit(-val);
  }
  // private method
  #approveLoan(val) {
    return true;
  }
  requestLoan(val) {
    if (this.#approveLoan(val)) {
      this.deposit(val);
      console.log(`Loan approved!`);
    }
  }
}

// declaring a new instance of the account class
const acc1 = new Account("Jonas", "Eur", 1111, []);

// calling methods on the class
acc1.deposit(250); 
acc1.withdraw(140);
acc1.requestLoan(1000);
```