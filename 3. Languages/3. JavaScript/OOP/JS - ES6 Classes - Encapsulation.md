### What is Encapsulation?
* [Encapsulation](https://www.geeksforgeeks.org/encapsulation-in-javascript/) --> the practice of hiding the internal details of an object and exposing only the necessary information to the outside world.
* Advantage of Encapsulation--> hides away the complexity of the device, leaving the user with a convenient and intuitive way of interacting with it.

### Why is Encapsulation needed? 
1) Prevent from code outside of a class, accidentally manipulating data inside a class
2) When a small interface is introduced, internal methods can be changed with confidence (external code will not rely on external methods)

### Convention for Encapsulation
* Adding an underscore `( _ )` in front **property name** or **method**
	* Does NOT actually make it private, but informs other engineers that this should not be touched or altered
```js
class className {
	constructor(property1, property2) {
		this._property1 = property1; // protected property
		this._property2 = property2;
	}
}
```

### Using Encapsulation
```js
class BankAccount {
    constructor(accountNumber, accountHolderName, balance) {
        this._accountNumber = accountNumber;
        this._accountHolderName = accountHolderName;
        this._balance = balance;
    }
    showAccountDetails() {
        console.log(`Account Number: ${this._accountNumber}`);
        console.log(`Account Holder Name: ${this._accountHolderName}`);
        console.log(`Balance: ${this._balance}`);
    }
    deposit(amount) {
        this._balance += amount;
        this.showAccountDetails();
    }
}

let myBankAccount = new BankAccount("123456", "John Doe", 1000);
myBankAccount.deposit(500); 
// Output: Account Number: 123456 Account Holder Name: 
// John Doe Balance: 150

```