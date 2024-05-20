What is automated testing? (see [[Automated Testing - What is it?]])
Working with JEST (see [[JEST - Testing Frameworks]])

## Example 1: 
See [[JEST - Testing Units]]
```js
// isDivisibleByThree.js
const isDivisibleByThree = (number) => {
	return number % 3 === 0;
};

module.exports = isDivisibleByThree;
```

```js
// isDivisibleByThree.test.js
const isDivisibleByThree = require("./isDivisibleByThree");

it("Returns true for numbers divisible by 3", () => {
  expect(isDivisibleByThree(0)).toEqual(true);
  expect(isDivisibleByThree(3)).toEqual(true);
  expect(isDivisibleByThree(-3)).toEqual(true);
  expect(isDivisibleByThree(303)).toEqual(true);
  expect(isDivisibleByThree(999)).toEqual(true);
});

it("Returns false for numbers not divisible by 3", () => {
  expect(isDivisibleByThree(1)).toEqual(false);
  expect(isDivisibleByThree(2)).toEqual(false);
  expect(isDivisibleByThree(4)).toEqual(false);
  expect(isDivisibleByThree(-1)).toEqual(false);
  expect(isDivisibleByThree(-2)).toEqual(false);
  expect(isDivisibleByThree(301)).toEqual(false);
  expect(isDivisibleByThree(1000)).toEqual(false);
});
```

## Example 2: Using Test Suites
* See [[JEST - Test Suites]]
```js
// index.js

const isValidPassword = (password) => {
	const passwordRegex = /^(?=.*[A-Za-z])(?=.*\d)(?=.*[@$!%*#?&])[A-Za-z\d@$!%*#?&]{8,}$/;
	return passwordRegex.test(password);
};

const isValidEmail = (email) => {
	const emailRegex = /(?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])/;
	return emailRegex.test(email);
};

const validateUserInput = ({ email, password }) => {
	const result = {
		isValidated: isValidPassword(password) && isValidEmail(email),
		message: null,
	    error: null
	};
	
	if (isValidPassword(password) && isValidEmail(email)) {
	    result.message = 'User created successfully';
	} else if (isValidEmail(email) && !isValidPassword(password)) {
		result.error = 'Wrong password';
	} else if (!isValidEmail(email) && isValidPassword(password)) {
		result.error = 'Wrong email';
	} else {
		result.error = 'Incorrect data';
	}
	return result
};

module.exports = {
	validateUserInput,
	isValidEmail,
	isValidPassword
};
```

```js
// index.test.js

const { isValidEmail, isValidPassword, validateUserInput } = require("../index.js");

// We've already added some test data for your convenience, but you can use your own
const dataValid = { email: "bob@yandex.com", password: "1amAp0k3m0n%" };
const dataInvalidPassword = { email: "bob@yandex.com", password: "123456" };
const dataInvalidEmail = { email: "bob", password: "1amAp0k3m0n%" };
const dataInvalidCredentials = { email: "bob", password: "12345" };

// Write tests here
describe("name here", () => {
	test("#isValidEmail should check that the email is valid", () => {
	    expect(isValidEmail(dataValid.email)).toBeTruthy();
	    expect(isValidEmail(dataInvalidEmail.email)).toBeFalsy();
	});
	test("#isValidPassword should check the password is valid", () => {
	    expect(isValidPassword(dataValid.password)).toBeTruthy();
	    expect(isValidPassword(dataInvalidPassword.password)).toBeFalsy();
	});
	test("#validateUserInput should return 'message if the data is correct           without returning an error", () => {
		expect(validateUserInput(dataValid).isValidated).toBeTruthy();
		expect(validateUserInput(dataValid).error).toBeNull();
		expect(validateUserInput(dataValid).message).toBe("User created                  successfully");
	});
	test("#validateUserInput should return an email error if the email is            incorrect", () => {
		expect(validateUserInput(dataInvalidEmail).isValidated).toBeFalsy();
	    expect(validateUserInput(dataInvalidEmail).error).toBe("Wrong email");
		expect(validateUserInput(dataInvalidEmail).message).toBeNull();
	});
	test("#validateUserInput should return a password error if the password is       incorrect", () => {
		expect(validateUserInput(dataInvalidPassword).isValidated).toBeFalsy();
		expect(validateUserInput(dataInvalidPassword).error).toBe("Wrong                 password");
	    expect(validateUserInput(dataInvalidPassword).message).toBeNull();
	});
		test("#validateUserInput should return an incorrect data error if all            data is incorrect", () => {
		expect(validateUserInput(dataInvalidCredentials).isValidated).                   toBeFalsy();
		expect(validateUserInput(dataInvalidCredentials).error).toBe("Incorrect          data");
		expect(validateUserInput(dataInvalidCredentials).message).toBeNull();
	});
});
```

## Example 3: Testing HTTP requests
* See [[SuperTest - Testing HTTP Requests]]*
```js
// app.js
const express = require('express');
const app = express();

const successMessage = 'success';
const userData = {
	name: 'Sam',
	email: 'developer@yandex.com',
	isDeveloper: true,
	followersOnGithub: 12
};

app.get('/', (req, res) => {
	res.status(200).send('Hello, world!')
});

app.post('/users', (req, res) => {
	res.status(201).send({
		message: successMessage,
	    data: userData,
	});
});

module.exports = app;
```

```js
const supertest = require("supertest");
const app = require("../app.js");
const request = supertest(app);

// Testing the '/' endpoint with get(), and '/users' endpoint with post()
describe("Testing the app endpoints", () => {
	test('GET "/" must return "Hello, world!" and a correct status', () => {
		return request.get("/").then((res) => {
			expect(res.status).toBe(200);
		    expect(res.text).toBe("Hello, world!");
	    });
	});
	
	test("Returns a 200 response at the /users endpoint and returns JSON object      with user data", () => {
		request.post("/users").then((res) => {
			expect(res.status).toBe(201);
		    expect(res.headers["content-type"]).toMatch("application/json");
		    expect(res.body.data.isDeveloper).toBeTruthy();
		    expect(res.body.data.followersOnGitHub).toBeGreaterThan(10);
	    });
	});
});
```

## Example 4: Testing Databases
* See [[JEST - Database Testing]]

```js
// users.js -- the model document

const mongoose = require('mongoose');
const isEmail = require('validator/lib/isEmail');
const isURL = require('validator/lib/isURL');
const { Schema } = mongoose;

const userSchema = new Schema({
	email: {
		type: String,
	    required: 'email is required',
	    unique: true,
	    validate: {
		    validator: (v) => isEmail(v),
		      message: 'invalid email format',
	    },
	},
	password: {
	    type: String,
	    required: 'password is required',
	    select: false,
	},
	name: {
	    type: String,
	    required: 'name is required',
	    minlength: 2,
	    maxlength: 30,
	},
	about: {
		type: String,
		required: 'about is required',
	    minlength: 2,
	    maxlength: 30,
	},
	avatar: {
		type: String,
		validate: {
	    validator: (v) => isURL(v),
		    message: 'avatar must be a URL',
	    },
	},
}, { versionKey: false });

module.exports = mongoose.model('user', userSchema);
```

```js
// fixtures.index.js
module.exports = {
	user: {
	    name: 'Wendy Webberton',
	    about: 'Super Web Development',
	    password: '1234QWer$',
	    email: 'superwebdev@yandex.com',
	    avatar: 'https://images.unsplash.com/photo-1599701834133-9ae09fcfa601?            ixli1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=700&q=80',
	}
};
```

```js
const mongoose = require("mongoose");
const User = require("../models/user");
const fixtures = require("../fixtures");
const MONGO_URL = "mongodb://localhost:27017/aroundtheus";

// Connects to the database for all tests
beforeAll(() => {
	return mongoose.connect(MONGO_URL, { 
		useNewUrlParser: true, 
		useCreateIndex: true, 
		useFindAndModify: false, 
		useUnifiedTopology: true
	});
});

// Disconnects from the databse after all tests
afterAll(() => {
	return mongoose.disconnect();
});

describe("DataBase Tests", () => {
	// Creates sample data before each test
	beforeEach(() => {
		const { name, about, avatar, email, password } = fixtures.user;
		return User.create({ name, about, avatar, email, password });
	});
	
	// Deletes sample data after each test
	afterEach(() => {
	    User.deleteOne({ email: fixtures.user.email });
	});
	
	test("The user must be complete", () => {
		return User.findOne({ email: fixtures.user.email }).then((user) => {
			expect(user).toBeDefined();
		    expect(user.email).toBe(fixtures.user.email);
		    expect(user.name).toBe(fixtures.user.name);
	    });
	});
});
```