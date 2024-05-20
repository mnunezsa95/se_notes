What is JEST? 
* An automated testing framework (see [[Automated Testing - What is it?]])

### Installing the Framework
1) JEST should be installed as a dev dependency 
```bash
npm install --save-dev jest
```

2) Add the package name in the "`scripts`" section of the `package.json` file as follows:
```json
...
"scripts": {
  "test": "jest"
},
... 
```

### Working with JEST
* Has a variety of methods to write tests (see [[JEST - Installing JEST]], [[JEST - Testing Frameworks]], [[JEST - Methods]])
	* Example
```js
test('Creates a greeting', () => {
	expect(sayHello('Lera', 'Jackson')).toBe('Hello, Lera Jackson!');
}); 
```

