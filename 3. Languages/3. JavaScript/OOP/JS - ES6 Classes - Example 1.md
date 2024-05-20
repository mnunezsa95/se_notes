What are ES6 Classes? (see [[JS - ES6 Classes]], [[JS - ES6 Classes - Summary]])

```js
class Account {
  constructor(owner, currency, pin) {
    this.owner = owner;
    this.currency = currency;
    this.pin = pin;
    // can properties that are NOT based on any inputs can be added to                  constructor
    this.movements = [];
    this.locale = global.language;
    console.log(`Thanks for opening an account, ${owner}`);
  }
  
  deposit(val) {
    this.movements.push(val);
    return this;
  }
  
  withdraw(val) {
    this.deposit(-val);
    return this;
  }

  _approveLoan(val) {
    return true;
    return this;
  }

  requestLoan(val) {
    if (this._approveLoan(val)) {
      this.deposit(val);
      console.log(`Loan approved!`);
      return this;
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

# Chaining Methods
* ES6 Class Methods can be **chained**
```js
acc1.deposit(300).deposit(500).deposit(35).withdraw(50).requestLoan(25000); 
// all of these movements will be added to the array
```