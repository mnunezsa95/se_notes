#### Lexical Environment (Global Scope)
* Global Scope --> Variables & functions have a 'global scope' when declared Globally (outside any function)
	* Variables declared in the **global scope** can be accessed on the **`global` object**
```js
const message = 'Hello, world, one more time!'; console.log(message);
```

### Creating Additional Lexical Environments
* Anytime a new function is created, it creates a new **Lexical Environment** to variables declared inside of it
	* When the function is called, the engine will look for variables inside its own Lexical Environment, then move outwards towards other Lexical Environments until it finds all variables needed for execution

```js
const message = 'Hello, world, one more time!'; // Global variables (Lexical Enviroment)

// function is created
function viewAlert(statement) {
  const someVariable = 'Some value';

  alert(someVariable); // someVariable is found in LEVA
  alert(statement); // statement is found in LEVA
  alert(message); // hmm, there is no message in LEVA
}

// function is called; a new lexical environment is created to store the statement parameter & someVariable variable. Engine will look outwards to global scope for the message variable
viewAlert('Hello, world!'); 
```

### How does Lexical Environment creation work behind scenes?
* When a function is declared, the engine assigns the name of the function to a hidden property called `[[Environment]]`.
	* Allows the function to remember the scope it was created in
	* The Lexical Environment and `[[Environment]]` property CANT be accessed
```js
/* the engine did the following when we declared viewAlert() */
viewAlert.[[Environment]] = global 
```